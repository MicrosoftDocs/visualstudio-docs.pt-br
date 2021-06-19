---
title: Manipuladores de alterações nos valores de propriedades de domínio
description: Saiba mais sobre manipuladores de alteração de valor de propriedade de domínio que podem ser usados em uma linguagem Visual Studio específica do domínio.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, overriding event handlers
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1c6cdb027bafdf4d1fe7689d7dd30d697b539370
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388991"
---
# <a name="domain-property-value-change-handlers"></a>Manipuladores de alteração de valor da propriedade de domínio

Em um Visual Studio específico do domínio, quando o valor de uma propriedade de domínio é alteração, os métodos e são invocados no `OnValueChanging()` manipulador de propriedades de `OnValueChanged()` domínio. Para responder à mudança, você pode substituir esses métodos.

## <a name="override-the-property-handler-methods"></a>Substituir os métodos do Manipulador de Propriedades

Cada propriedade de domínio de sua linguagem específica do domínio é manipulada por uma classe que está aninhada em sua classe de domínio pai. Seu nome segue o formato *PropertyName* PropertyHandler. Você pode inspecionar essa classe de manipulador de propriedades no arquivo **Dsl\Generated Code\DomainClasses.cs**. Na classe, `OnValueChanging()` é chamado imediatamente antes de o valor ser alterado, e `OnValueChanged()` é chamado imediatamente após o valor ser alterado.

Por exemplo, suponha que você tenha uma classe de domínio chamada que tem uma propriedade de domínio de cadeia de `Comment` caracteres chamada `Text` e uma propriedade de inteiro chamada `TextLengthCount` . Para fazer com que sempre contenha o comprimento da cadeia de caracteres, você pode escrever o seguinte código em um `TextLengthCount` arquivo separado no projeto `Text` Dsl:

```csharp
// Domain Class "Comment":
public partial class Comment
{
  // Domain Property "Text":
  partial class TextPropertyHandler
  {
    protected override void OnValueChanging(CommentBase element, string oldValue, string newValue)
    {
      base.OnValueChanging(element, oldValue, newValue);

      // To update values outside the Store, write code here.

      // Let the transaction manager handle undo:
      Store store = element.Store;
      if (store.InUndoRedoOrRollback || store.InSerializationTransaction) return;

      // Update values in the Store:
      this.TextLengthCount = newValue.Length;
    }
  }
}
```

Observe os seguintes pontos sobre os manipuladores de propriedades:

- Os métodos do manipulador de propriedades são chamados, quando o usuário faz alterações em uma propriedade de domínio e quando o código do programa atribui um valor diferente para a propriedade.

- Os métodos são chamados apenas quando o valor muda. O manipulador não é invocado se o código do programa atribui um valor que é igual ao valor atual.

- As propriedades de domínio de armazenamento calculadas e personalizadas não têm métodos OnValueChanged e OnValueChanging.

- Você não pode usar um manipulador de alterações para modificar o novo valor. Se você quiser fazer isso, por exemplo, para restringir o valor de um determinado intervalo, defina uma `ChangeRule`.

- Você não pode adicionar um manipulador de alterações para uma propriedade que representa a função de um relacionamento. Em vez disso, defina uma `AddRule` e uma `DeleteRule` na classe de relação. Essas regras são disparadas quando você cria ou altera links. Para obter mais informações, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

### <a name="changes-in-and-out-of-the-store"></a>Alterações dentro e fora do repositório

Os métodos do manipulador de propriedades são chamados dentro da transação que iniciou a alteração. Portanto, você pode fazer mais alterações no repositório sem abrir uma nova transação. As alterações podem resultar em outras chamadas do manipulador.

Quando uma transação está sendo desfeita, refeita ou revertida, você não deve fazer mudanças no repositório, ou seja, alterações para modelar elementos, relações, formas, conectores, diagramas ou propriedades dele.

Além disso, em geral, você não deve atualizar os valores quando o modelo estiver sendo carregado do arquivo.

As alterações no modelo devem ser protegidas por um teste como este:

```csharp
if (!store.InUndoRedoOrRollback && !store. InSerializationTransaction)
{
   this.TextLength = ...; // in-store changes
}
```

Por outro lado, se o manipulador de propriedades propagar alterações fora do repositório, por exemplo, para um arquivo, banco de dados ou variáveis que não são de repositório, você deve sempre fazer essas alterações para que os valores externos sejam atualizados quando o usuário invocar desfazer ou refazer.

### <a name="cancel-a-change"></a>Cancelar uma alteração

Se você quiser evitar uma alteração, você pode reverter a transação atual. Por exemplo, você pode garantir que a propriedade permaneça dentro de um intervalo específico.

```csharp
if (newValue > 10)
{
   store.TransactionManager.CurrentTransaction.Rollback();
   System.Windows.Forms.MessageBox.Show("Value must be less than 10");
}
```

### <a name="alternative-technique-calculated-properties"></a>Técnica alternativa: propriedades calculadas

O exemplo anterior mostra como OnValueChanged() pode ser usado para propagar os valores de uma propriedade de domínio para outra. Cada propriedade tem seu próprio valor armazenado.

Em vez disso, você poderia considerar a definição da propriedade derivada como uma propriedade calculada. Nesse caso, a propriedade não tem armazenamento próprio e está definindo a função que é avaliada sempre que o seu valor é necessário. Para obter mais informações, consulte [Propriedades de armazenamento calculadas e personalizadas.](../modeling/calculated-and-custom-storage-properties.md)

Em vez do exemplo anterior, você pode definir **o campo Tipo** de para ser Calculado `TextLengthCount` **na** Definição de DSL. Você forneceria seu próprio **método Get** para essa propriedade de domínio. O **método Get** retornaria o comprimento atual da cadeia de `Text` caracteres.

No entanto, há uma possível desvantagem referente às propriedades calculadas, pois a expressão é avaliada toda vez que o valor é usado, o que pode representar um problema de desempenho. Além disso, não há nenhum OnValueChanging() e OnValueChanged() em uma propriedade calculada.

### <a name="alternative-technique-change-rules"></a>Técnica alternativa: alterar as regras

Se você definir um ChangeRule, ele será executado no final de uma transação na qual o valor de uma propriedade é alterado.  Para obter mais informações, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

Se várias alterações são feitas em uma transação, a ChangeRule executa quando todas estão concluídas. Por outro lado, o OnValue... os métodos são executados quando algumas das alterações não foram executadas. Dependendo do que você deseja fazer, essa pode fazer uma ChangeRule mais adequada.

Você também pode usar um ChangeRule para ajustar o novo valor da propriedade para mantê-lo dentro de um intervalo específico.

> [!WARNING]
> Se uma regra fizer alterações no conteúdo do repositório, outras regras e manipuladores de propriedades podem ser disparados. Se uma regra alterar a propriedade que disparou essas regras e manipuladores, ela será chamada novamente. Verifique se suas definições de regras não resultam em disparos infinitos.

```csharp
using Microsoft.VisualStudio.Modeling;
...
// Change rule on the domain class Comment:
[RuleOn(typeof(Comment), FireTime = TimeToFire.TopLevelCommit)]
class MyCommentTrimRule : ChangeRule
{
  public override void
    ElementPropertyChanged(ElementPropertyChangedEventArgs e)
  {
    base.ElementPropertyChanged(e);
    Comment comment = e.ModelElement as Comment;

    if (comment.Text.StartsWith(" ") || comment.Text.EndsWith(" "))
      comment.Text = comment.Text.Trim();
    // If changed, rule will trigger again.
  }
}

// Register the rule:
public partial class MyDomainModel
{
 protected override Type[] GetCustomDomainModelTypes()
 { return new Type[] { typeof(MyCommentTrimRule) };
 }
}
```

## <a name="example"></a>Exemplo

### <a name="description"></a>Descrição

O exemplo a seguir substitui o manipulador de propriedades de uma propriedade de domínio e notifica o usuário quando uma propriedade da classe de domínio `ExampleElement` foi alterada.

### <a name="code"></a>Código

```csharp
using DslModeling = global::Microsoft.VisualStudio.Modeling;
using DslDesign = global::Microsoft.VisualStudio.Modeling.Design;

namespace msft.FieldChangeSample
{
  public partial class ExampleElement
  {
    internal sealed partial class NamePropertyHandler
    {
      protected override void OnValueChanged(ExampleElement element,
         string oldValue, string newValue)
      {
        if (!this.Store.InUndoRedoOrRollback)
        {
           // make in-store changes here...
        }
        // This part is called even in undo:
        System.Windows.Forms.MessageBox.Show("Value Has Changed");
        base.OnValueChanged(element, oldValue, newValue);
      }
    }
  }
}
```
