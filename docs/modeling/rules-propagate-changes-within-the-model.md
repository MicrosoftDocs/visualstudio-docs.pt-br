---
title: Regras propagam alterações dentro do modelo
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 8f506b71240024206523821080cdf958660aa963
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49865955"
---
# <a name="rules-propagate-changes-within-the-model"></a>Regras propagam alterações dentro do modelo
Você pode criar uma regra do repositório para propagar uma alteração de um elemento para outro na visualização e o SDK de modelagem (VMSDK). Quando ocorre uma alteração a qualquer elemento na Store, as regras estão agendadas para ser executado, normalmente, quando a transação externa é confirmada. Há diferentes tipos de regras para diferentes tipos de eventos, como adicionar um elemento ou excluí-lo. Você pode anexar as regras para tipos específicos de elementos, formas ou diagramas. Muitos recursos internos são definidos por regras: por exemplo, as regras de garantem que um diagrama é atualizado quando o modelo é alterado. Você pode personalizar sua linguagem específica do domínio, adicionando suas próprias regras.

 Regras de Store são particularmente úteis para propagar alterações dentro do armazenamento – ou seja, alterações para elementos de modelo, relações, formas ou conectores e seu domínio de propriedades. As regras não são executados quando o usuário invoca os comandos de desfazer ou refazer. Em vez disso, o Gerenciador de transações certifica-se de que o repositório de conteúdo é restaurado para o estado correto. Se você deseja propagar alterações aos recursos fora do repositório, use eventos de Store. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).

 Por exemplo, suponha que você deseja especificar que, sempre que o usuário (ou seu código) cria um novo elemento do tipo ExampleDomainClass, um elemento adicional de outro tipo é criado em outra parte do modelo. Você poderia escrever um AddRule e associá-lo a ExampleDomainClass. Você deve escrever o código na regra para criar o elemento adicional.

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
>  O código de uma regra deve alterar o estado somente de elementos dentro do Store; ou seja, a regra deve alterar apenas os elementos de modelo, relações, formas, conectores, diagramas ou suas propriedades. Se você deseja propagar alterações aos recursos fora do repositório, defina eventos de Store. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md)

### <a name="to-define-a-rule"></a>Para definir uma regra

1. Defina a regra como uma classe prefixada com o `RuleOn` atributo. O atributo associa a regra com uma das suas classes de domínio, relações ou elementos de diagrama. A regra será aplicada a cada instância dessa classe, que pode ser abstrato.

2. Registre-se a regra ao adicioná-lo para o conjunto retornado por `GetCustomDomainModelTypes()` em sua classe de modelo de domínio.

3. Derive a classe de regra de uma das classes abstratas de regra e escrever o código do método de execução.

   As seções a seguir descrevem essas etapas mais detalhadamente.

### <a name="to-define-a-rule-on-a-domain-class"></a>Para definir uma regra em uma classe de domínio

-   Em um arquivo de código personalizado, defina uma classe e um prefixo com o <xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> atributo:

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

-   O tipo de entidade no primeiro parâmetro pode ser uma classe de domínio, o relacionamento de domínio, a forma, o conector ou o diagrama. Normalmente, você aplica regras a classes de domínio e relações.

     O `FireTime` costuma ser `TopLevelCommit`. Isso garante que a regra é executada somente depois que todas as principais alterações da transação foram feitas. As alternativas são embutidos, o que a regra é executada logo após a alteração; e LocalCommit, que executa a regra no final da transação atual (que não pode ser mais externo). Você também pode definir a prioridade de uma regra para afetar sua ordenação na fila, mas este é um método confiável de atingir o resultado que necessário.

-   Você pode especificar uma classe abstrata como o tipo de entidade.

-   A regra se aplica a todas as instâncias da classe da entidade.

-   O valor padrão para `FireTime` é TimeToFire.TopLevelCommit. Isso faz com que a regra a ser executado quando a transação externa é confirmada. Uma alternativa é TimeToFire.Inline. Isso faz com que a regra a ser executada logo após o evento de gatilho.

### <a name="to-register-the-rule"></a>Para registrar a regra

-   Adicione sua classe de regra à lista de tipos retornados por `GetCustomDomainModelTypes` em seu modelo de domínio:

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

-   Se você não tiver certeza do nome da sua classe de modelo de domínio, examinar o arquivo **Dsl\GeneratedCode\DomainModel.cs**

-   Escreva esse código em um arquivo de código personalizado em seu projeto DSL.

### <a name="to-write-the-code-of-the-rule"></a>Escrever o código da regra

- Derive a classe de regra de uma das seguintes classes base:


  | Classe base | Disparador |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | Um elemento, um link ou uma forma é adicionada.<br /><br /> Use isso para detectar novas relações, além de novos elementos. |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | Um valor de propriedade de domínio é alterado. O argumento de método fornece os valores novos e antigos.<br /><br /> Para formas, esta regra é disparada quando o interno `AbsoluteBounds` alterações de propriedade, se a forma é movida.<br /><br /> Em muitos casos, é mais conveniente substituir `OnValueChanged` ou `OnValueChanging` no manipulador de propriedade. Esses métodos são chamados imediatamente antes e após a alteração. Por outro lado, a regra é executada normalmente no final da transação. Para obter mais informações, consulte [manipuladores de alteração de valor de propriedade de domínio](../modeling/domain-property-value-change-handlers.md). **Observação:** essa regra não é disparada quando um link é criado ou excluído. Em vez disso, escreva uma `AddRule` e um `DeleteRule` para a relação de domínio. |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | Acionado quando um elemento ou o link está prestes a ser excluído. A propriedade ModelElement.IsDeleting é true até o término da transação. |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | Executado quando um elemento ou um link foi excluído. A regra é executada depois que todas as outras regras foram executadas, incluindo DeletingRules. ModelElement.IsDeleting for false, e ModelElement.IsDeleted for true. Para permitir um Desfazer subsequente, o elemento não é realmente removido da memória, mas ele é removido do Store.ElementDirectory. |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | Um elemento é movido de um repositório de partição para outra.<br /><br /> (Observe que isso não está relacionado à posição de uma forma gráfica). |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | Essa regra se aplica somente a relações de domínio. Se você atribuir explicitamente um elemento de modelo para ambas as extremidades de um link é disparado. |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | Acionado quando a ordenação de links para ou de um elemento é alterada usando os métodos MoveBefore ou MoveToIndex em um link. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | Executado quando uma transação é criada. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | Executado quando a transação está prestes a ser confirmada. |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | Executado quando a transação está prestes a ser revertida. |


- Cada classe tem um método que você substituir. Tipo `override` em sua classe para descobri-lo. O parâmetro deste método identifica o elemento que está sendo alterado.

  Observe os seguintes pontos sobre as regras:

1.  O conjunto de alterações em uma transação pode disparar regras de muitos. Geralmente, as regras são executadas quando a transação externa é confirmada. Elas são executadas em uma ordem não especificada.

2.  Uma regra sempre será executada dentro de uma transação. Portanto, não é preciso criar uma nova transação para fazer alterações.

3.  As regras não são executadas quando uma transação é revertida, ou quando são executadas as operações de desfazer ou refazer. Essas operações de redefinição de todo o conteúdo da Store para seu estado anterior. Portanto, se sua regra altera o estado de qualquer coisa fora a Store, ele pode não manter em synchronism com a Store conteúdo. Para atualizar o estado de fora a Store, é melhor usar eventos. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).

4.  Algumas regras são executadas quando um modelo é carregado do arquivo. Para determinar se o carregamento ou salvamento está em andamento, use `store.TransactionManager.CurrentTransaction.IsSerializing`.

5.  Se o código da sua regra cria mais gatilhos de regra, eles serão adicionados ao final da lista de acionamento e serão executados antes que a transação seja concluída. DeletedRules são executados depois de todas as outras regras. Uma regra pode executar muitas vezes em uma transação, uma vez para cada alteração.

6.  Para passar informações para e de regras, você pode armazenar informações no `TransactionContext`. Isso é apenas um dicionário que é mantido durante a transação. Ele é descartado quando a transação termina. Os argumentos do evento em cada regra fornecem acesso a ele. Lembre-se de que as regras não são executadas em uma ordem previsível.

7.  Usar regras após considerar outras alternativas. Por exemplo, se você quiser atualizar uma propriedade quando um valor for alterado, considere o uso de uma propriedade calculada. Se você quiser restringir o tamanho ou local de uma forma, use um `BoundsRule`. Se você quiser responder a uma alteração em um valor de propriedade, adicione um `OnValueChanged` manipulador para a propriedade. Para obter mais informações, consulte [respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

## <a name="example"></a>Exemplo
 O exemplo a seguir atualiza uma propriedade quando uma relação de domínio é instanciada para vincular dois elementos. A regra será acionada não apenas quando o usuário cria um link em um diagrama, mas também se o código de programa cria um link.

 Para testar este exemplo, criar uma DSL usando o modelo de solução de fluxo de tarefa e insira o código a seguir em um arquivo no projeto Dsl. Compilar e executar a solução e abra o arquivo de exemplo no projeto de depuração. Desenhe um Link de comentário entre uma forma de comentário e um elemento de fluxo. Altera o texto do comentário ao relatório do elemento mais recente que você se conectou a ele para.

 Na prática, você geralmente escreveria um DeleteRule para cada AddRule.

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

## <a name="see-also"></a>Consulte também

- [Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md)
- [BoundsRules restringem o local e o tamanho de uma forma](../modeling/boundsrules-constrain-shape-location-and-size.md)