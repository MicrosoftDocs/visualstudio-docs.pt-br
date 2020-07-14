---
title: Regras propagam alterações dentro do modelo
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2050fe0ea2d1a9bb0bf278c13c2beb587412c643
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542552"
---
# <a name="rules-propagate-changes-within-the-model"></a>Regras propagam alterações dentro do modelo
Você pode criar uma regra de repositório para propagar uma alteração de um elemento para outro no SDK de modelagem e visualização (VMSDK). Quando ocorre uma alteração em qualquer elemento da loja, as regras são agendadas para serem executadas, geralmente quando a transação mais externa é confirmada. Há diferentes tipos de regras para diferentes tipos de eventos, como adicionar um elemento ou excluí-lo. Você pode anexar regras a tipos específicos de elementos, formas ou diagramas. Muitos recursos internos são definidos por regras: por exemplo, as regras garantem que um diagrama seja atualizado quando o modelo for alterado. Você pode personalizar sua linguagem específica de domínio adicionando suas próprias regras.

 As regras de armazenamento são particularmente úteis para a propagação de alterações dentro da loja, ou seja, alterações em elementos de modelo, relações, formas ou conectores e suas propriedades de domínio. As regras não são executadas quando o usuário invoca os comandos desfazer ou refazer. Em vez disso, o Gerenciador de transações garante que o conteúdo da loja seja restaurado para o estado correto. Se você quiser propagar alterações para recursos fora da loja, use armazenar eventos. Para obter mais informações, consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

 Por exemplo, suponha que você queira especificar que sempre que o usuário (ou seu código) criar um novo elemento do tipo ExampleDomainClass, um elemento adicional de outro tipo será criado em outra parte do modelo. Você poderia escrever uma addrule e associá-la a ExampleDomainClass. Você escreveria o código na regra para criar o elemento adicional.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;

namespace ExampleNamespace
{
 // Attribute associates the rule with a domain class:
 [RuleOn(typeof(ExampleDomainClass), FireTime=TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class MyAddRule : AddRule
 {
  // Override the abstract method:
  public override void ElementAdded(ElementAddedEventArgs e)
  {
    base.ElementAdded(e);
    ExampleDomainClass element = e.ModelElement;
    Store store = element.Store;
    // Ignore this call if we're currently loading a model:
    if (store.TransactionManager.CurrentTransaction.IsSerializing)
       return;

    // Code here propagates change as required - for example:
      AnotherDomainClass echo = new AnotherDomainClass(element.Partition);
      echo.Name = element.Name;
      echo.Parent = element.Parent;
    }
  }
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
   protected override Type[] GetCustomDomainModelTypes()
   {
     List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
     types.Add(typeof(MyAddRule));
     // If you add more rules, list them here.
     return types.ToArray();
   }
 }
}
```

> [!NOTE]
> O código de uma regra deve alterar o estado apenas dos elementos dentro da loja; ou seja, a regra deve alterar apenas elementos de modelo, relações, formas, conectores, diagramas ou suas propriedades. Se você quiser propagar alterações para recursos fora da loja, defina armazenar eventos. Para obter mais informações, consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

### <a name="to-define-a-rule"></a>Para definir uma regra

1. Defina a regra como uma classe prefixada com o `RuleOn` atributo. O atributo associa a regra a uma de suas classes de domínio, relações ou elementos de diagrama. A regra será aplicada a todas as instâncias dessa classe, que podem ser abstratas.

2. Registre a regra adicionando-a ao conjunto retornado por `GetCustomDomainModelTypes()` em sua classe de modelo de domínio.

3. Derive a classe de regra de uma das classes de regra abstrata e escreva o código do método de execução.

   As seções a seguir descrevem essas etapas mais detalhadamente.

### <a name="to-define-a-rule-on-a-domain-class"></a>Para definir uma regra em uma classe de domínio

- Em um arquivo de código personalizado, defina uma classe e Prefixe-a com o <xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> atributo:

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

- O tipo de entidade no primeiro parâmetro pode ser uma classe de domínio, relação de domínio, forma, conector ou diagrama. Normalmente, você aplica regras a relações e classes de domínio.

     Normalmente, o `FireTime` é `TopLevelCommit` . Isso garante que a regra seja executada somente depois que todas as alterações principais da transação tiverem sido feitas. As alternativas são embutidas, o que executa a regra logo após a alteração; e LocalCommit, que executa a regra no final da transação atual (que pode não ser a mais externa). Você também pode definir a prioridade de uma regra para afetar sua ordenação na fila, mas esse é um método não confiável de obter o resultado necessário.

- Você pode especificar uma classe abstrata como o tipo de entidade.

- A regra se aplica a todas as instâncias da classe Subject.

- O valor padrão para `FireTime` é TimeToFire. TopLevelCommit. Isso faz com que a regra seja executada quando a transação mais externa é confirmada. Uma alternativa é TimeToFire. Inline. Isso faz com que a regra seja executada logo após o evento de disparo.

### <a name="to-register-the-rule"></a>Para registrar a regra

- Adicione sua classe de regra à lista de tipos retornados pelo `GetCustomDomainModelTypes` em seu modelo de domínio:

    ```csharp
    public partial class ExampleDomainModel
     {
       protected override Type[] GetCustomDomainModelTypes()
       {
         List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
         types.Add(typeof(MyAddRule));
         // If you add more rules, list them here.
         return types.ToArray();
       }
     }

    ```

- Se você não tiver certeza do nome da sua classe de modelo de domínio, procure dentro do arquivo **Dsl\GeneratedCode\DomainModel.cs**

- Escreva este código em um arquivo de código personalizado em seu projeto DSL.

### <a name="to-write-the-code-of-the-rule"></a>Para gravar o código da regra

- Derive a classe de regra de uma das seguintes classes base:

  | Classe base | Gatilho |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | Um elemento, link ou forma é adicionado.<br /><br /> Use isso para detectar novas relações, além de novos elementos. |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | Um valor de propriedade de domínio é alterado. O argumento do método fornece os valores novos e antigos.<br /><br /> Para formas, essa regra é disparada quando a `AbsoluteBounds` propriedade interna é alterada, se a forma for movida.<br /><br /> Em muitos casos, é mais conveniente substituir `OnValueChanged` ou `OnValueChanging` no manipulador de propriedades. Esses métodos são chamados imediatamente antes e depois da alteração. Por outro lado, a regra geralmente é executada no final da transação. Para obter mais informações, consulte [manipuladores de alteração de valor de propriedade de domínio](../modeling/domain-property-value-change-handlers.md). **Observação:**  Essa regra não é disparada quando um link é criado ou excluído. Em vez disso, grave um `AddRule` e um `DeleteRule` para o relacionamento de domínio. |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | Disparado quando um elemento ou link está prestes a ser excluído. A Propriedade ModelElement. isdeleble é true até o final da transação. |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | Executado quando um elemento ou link foi excluído. A regra é executada Depois que todas as outras regras forem executadas, incluindo DeletingRules. ModelElement. isexcluindo é false e ModelElement. IsDeleted é true. Para permitir um desfazer subsequente, o elemento não é realmente removido da memória, mas é removido de Store. ElementDirectory. |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | Um elemento é movido de uma partição de armazenamento para outra.<br /><br /> (Observe que isso não está relacionado à posição gráfica de uma forma.) |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | Essa regra se aplica somente a relações de domínio. Ele será disparado se você atribuir explicitamente um elemento de modelo para o final de um link. |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | Disparado quando a ordenação de links para ou de um elemento é alterada usando os métodos MoveBefore ou MoveToIndex em um link. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | Executado quando uma transação é criada. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | Executado quando a transação está prestes a ser confirmada. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | Executado quando a transação está prestes a ser revertida. |

- Cada classe tem um método que você substitui. Digite `override` sua classe para descobri-la. O parâmetro desse método identifica o elemento que está sendo alterado.

  Observe os seguintes pontos sobre as regras:

1. O conjunto de alterações em uma transação pode disparar muitas regras. Normalmente, as regras são executadas quando a transação mais externa é confirmada. Eles são executados em uma ordem não especificada.

2. Uma regra é sempre executada dentro de uma transação. Portanto, você não precisa criar uma nova transação para fazer alterações.

3. As regras não são executadas quando uma transação é revertida ou quando as operações de desfazer ou refazer são executadas. Essas operações redefinem todo o conteúdo da loja para seu estado anterior. Portanto, se a regra alterar o estado de qualquer coisa fora da loja, ela poderá não manter em sincronização com o conteúdo da loja. Para atualizar o estado fora da loja, é melhor usar eventos. Para obter mais informações, consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

4. Algumas regras são executadas quando um modelo é carregado do arquivo. Para determinar se o carregamento ou salvamento está em andamento, use `store.TransactionManager.CurrentTransaction.IsSerializing` .

5. Se o código da regra criar mais gatilhos de regra, eles serão adicionados ao final da lista de acionamento e serão executados antes da conclusão da transação. DeletedRules são executadas após todas as outras regras. Uma regra pode ser executada muitas vezes em uma transação, uma vez para cada alteração.

6. Para passar informações de e para regras, você pode armazenar informações no `TransactionContext` . Esse é apenas um dicionário que é mantido durante a transação. Ela é descartada quando a transação termina. Os argumentos de evento em cada regra fornecem acesso a ele. Lembre-se de que as regras não são executadas em uma ordem previsível.

7. Use regras depois de considerar outras alternativas. Por exemplo, se você quiser atualizar uma propriedade quando um valor for alterado, considere usar uma propriedade calculada. Se você quiser restringir o tamanho ou o local de uma forma, use um `BoundsRule` . Se você quiser responder a uma alteração em um valor de propriedade, adicione um `OnValueChanged` manipulador à propriedade. Para obter mais informações, consulte [respondendo e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

## <a name="example"></a>Exemplo
 O exemplo a seguir atualiza uma propriedade quando uma relação de domínio é instanciada para vincular dois elementos. A regra será disparada não apenas quando o usuário criar um link em um diagrama, mas também se o código do programa criar um link.

 Para testar este exemplo, crie uma DSL usando o modelo de solução de fluxo de tarefas e insira o código a seguir em um arquivo no projeto DSL. Compile e execute a solução e abra o arquivo de exemplo no projeto de depuração. Desenhe um link de comentário entre uma forma de comentário e um elemento de fluxo. O texto no comentário muda para o relatório no elemento mais recente ao qual você o conectou.

 Na prática, você normalmente escreveria um DeleteRule para cada addrule.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.TaskRuleExample
{

  [RuleOn(typeof(CommentReferencesSubjects))]
  public class RoleRule : AddRule
  {

    public override void ElementAdded(ElementAddedEventArgs e)
    {
      base.ElementAdded(e);
      CommentReferencesSubjects link = e.ModelElement as CommentReferencesSubjects;
      Comment comment = link.Comment;
      FlowElement subject = link.Subject;
      Transaction current = link.Store.TransactionManager.CurrentTransaction;
      // Don't want to run when we're just loading from file:
      if (current.IsSerializing) return;
      comment.Text = "Flow has " + subject.FlowTo.Count + " outgoing connections";
    }

  }

  public partial class TaskRuleExampleDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(RoleRule));
      return types.ToArray();
    }
  }

}
```

## <a name="see-also"></a>Confira também

- [Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md)