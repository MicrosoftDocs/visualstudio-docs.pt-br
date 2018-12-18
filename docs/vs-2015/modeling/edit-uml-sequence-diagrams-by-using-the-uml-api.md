---
title: Editar diagramas de sequência UML usando a API UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML activity diagrams, programming
ms.assetid: 8cdd0203-85ef-4c62-9abc-da4cb26fa504
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: f68cf87a7f45b906c6de43e0a837d49132b7a3e0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725554"
---
# <a name="edit-uml-sequence-diagrams-by-using-the-uml-api"></a>Editar diagramas de sequência UML usando a API UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma interação é uma sequência de mensagens entre um conjunto de linhas da vida. Uma interação é exibida em um diagrama de sequência UML.  
  
 Para obter detalhes completos da API, consulte <xref:Microsoft.VisualStudio.Uml.Interactions?displayProperty=fullName>.  
  
 Para obter uma introdução mais geral para escrever comandos e manipuladores de gesto para diagramas de UML, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
## <a name="basic-code"></a>Código básico  
  
### <a name="namespace-imports"></a>Importações de Namespace  
 Você deve incluir o seguinte `using` instruções:  
  
```  
using Microsoft.VisualStudio.Uml.Classes;  
   // for basic UML types such as IPackage  
using Microsoft.VisualStudio.Uml.Interactions;  
   // for interaction types  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
   // to create elements and use additional functions  
```  
  
 Se você estiver criando comandos de menu e manipuladores de gesto, também será necessário:  
  
```  
using System.ComponentModel.Composition;   
   // for Import and Export  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
   // for ICommandExtension  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
   // for diagrams and context  
```  
  
 Para obter mais informações, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
### <a name="getting-the-context"></a>Obtendo o contexto  
 Se você estiver editando uma interação como parte de um manipulador de gesto ou comando em um diagrama de sequência, você pode obter uma referência ao contexto. Por exemplo:  
  
```  
[SequenceDesignerExtension]  
[Export(typeof(ICommandExtension))]    
public class MySequenceDiagramCommand : ICommandExtension  
{  
    [Import]  
    public IDiagramContext Context { get; set; }  
    public void QueryStatus (IMenuCommand command)  
    {  
      ISequenceDiagram sequenceDiagram =   
          Context.CurrentDiagram as ISequenceDiagram;  
         ...  
```  
  
### <a name="generated-and-uml-sequence-diagrams"></a>Gerado e os diagramas de sequência UML  
 Há dois tipos de diagramas de sequência: aqueles que são criados manualmente em um projeto de modelagem UML e aqueles que foram gerados por código do programa. Use o `UmlMode` ter propriedade para descobrir qual sequência de diagrama.  
  
> [!NOTE]
>  Essa propriedade retorna false somente para diagramas de sequência gerado por meio do código usando o Visual Studio 2013 e versões anteriores. Isso inclui a sequência de código gerado diagramas migrados do 2013 e anteriores. Esta versão do Visual Studio não dá suporte a gerar novos diagramas de sequência.  
  
 Por exemplo, se você quiser fazer um comando de menu que só é visível em diagramas de sequência UML, então o `QueryStatus()` método poderia incluir a instrução a seguir:  
  
```  
command.Enabled = command.Visible =   
      sequenceDiagram != null && sequenceDiagram.UmlMode;  
```  
  
 Em uma sequência gerada diagrama, as linhas de vida, mensagens e outros elementos são basicamente as mesmas que em um diagrama de sequência UML. Em um modelo UML, o modelo Store tem uma raiz, que é o modelo que possui todos os outros elementos. Mas uma interação gerada existe na Store seu próprio modelo, que tem uma raiz nula:  
  
```  
IModel rootModel = sequenceDiagram.ModelStore.Root;  
    // !sequenceDiagram.UmlMode == (rootModel == null)  
```  
  
## <a name="to-create-and-display-an-interaction"></a>Para criar e exibir uma interação  
 Crie a interação como um filho de um pacote ou modelo.  
  
 Por exemplo, se você estiver desenvolvendo um comando que pode ser executado em um diagrama de sequência em branco, você sempre deve começar verificando se a interação existe.  
  
```  
public void Execute (IMenuCommand command)  
{  
    ISequenceDiagram sequenceDiagram =   
         Context.CurrentDiagram as ISequenceDiagram;  
    if (sequenceDiagram == null) return;  
    // Get the diagram's interaction:  
    IInteraction interaction = sequenceDiagram.Interaction;  
    // A new sequence diagram might have no interaction:  
    if (interaction == null)  
    {  
       // Get the home package or model of the diagram:  
       IPackage parentPackage = sequenceDiagram.GetObject<IPackage>();  
       interaction = parentPackage.CreateInteraction();  
       // Display the interaction on the sequence diagram:  
       sequenceDiagram.Bind(interaction);  
    }   
```  
  
## <a name="updating-an-interaction-and-its-layout"></a>Atualização de uma interação e seu Layout  
 Quando você atualiza uma interação, sempre terminar sua operação atualizando seu layout usando um dos seguintes métodos:  
  
- `ISequenceDiagram.UpdateShapePositions()` Ajusta as posições das formas que recentemente foram inseridas ou movidas e seus vizinhos.  
  
- `ISequenceDiagram.Layout([SequenceDiagramLayoutKinds])` redesenha o diagrama inteiro. Você pode usar o parâmetro para especificar o reposicionamento das linhas da vida, mensagens ou ambos.  
  
  Isso é particularmente importante quando você insere novos elementos ou move elementos existentes. Eles não estarão nas posições corretas no diagrama até que você executou uma dessas operações. Você só precisa chamar uma dessas operações uma vez no final de uma série de alterações.  
  
  Para evitar bemusing o usuário que executa um comando Desfazer após seu comando, use uma `ILinkedUndoTransaction` para incluir as alterações e o último `Layout()` ou `UpdateShapePositions()` operações. Por exemplo:  
  
```  
using (ILinkedUndoTransaction transaction = LinkedUndoContext.BeginTransaction("create loop"))  
{  
  Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop, messages);  
  Diagram.UpdateShapePositions();  
  transaction.Commit();  
}  
```  
  
 Para usar um `ILinkedUndoTransaction`, você deve fazer essa declaração em sua classe:  
  
```  
[Import] ILinkedUndoContext LinkedUndoContext { get; set; }  
```  
  
 Para obter mais informações, consulte [atualizações de modelo UML de Link usando transações](../modeling/link-uml-model-updates-by-using-transactions.md).  
  
## <a name="building-an-interaction"></a>Criação de uma interação  
  
### <a name="to-create-lifelines"></a>Criar linhas de vida  
  
```  
ILifeline lifeline = interaction.CreateLifeline();  
```  
  
 Uma linha da vida representa um elemento conectável, ou seja, uma instância de um tipo. Por exemplo, se a interação é usada para mostrar como um componente delega a mensagens de entrada para suas partes internas, as linhas da vida podem representar as portas e as partes do componente:  
  
```  
foreach (IConnectableElement part in   
            component.Parts  
           .Concat<IConnectableElement>(component.OwnedPorts))  
{  
   ILifeline lifeline = interaction.CreateLifeline();  
   lifeline.Represents = part;  
}  
```  
  
 Como alternativa, se a interação mostra um conjunto arbitrário de objetos, você pode criar uma propriedade ou outro `IConnectableElement` na interação em si:  
  
```  
ILifeline lifeline = interaction.CreateLifeline();  
IProperty property1 = interaction.CreateProperty();  
property1.Type = model.CreateInterface();  
property1.Type.Name = "Type 1";  
lifeline.Represents = property1;  
```  
  
 Como uma alternativa adicional, você pode definir o nome e tipo de uma linha da vida sem vinculá-lo a um elemento conectável:  
  
```  
ILifeline lifeline = interaction.CreateLifeline();  
lifeline.Name = "c1";  
lifeline.SetInstanceType("Customer");  
System.Diagnostics.Debug.Assert(  
           lifeline.GetDisplayName() == "c1:Customer"  );  
```  
  
### <a name="to-create-messages"></a>Para criar as mensagens  
 Para criar uma mensagem, você deve identificar pontos de inserção em que as linhas de vida de origem e destino. Por exemplo:  
  
```  
interaction.CreateMessage( sourceInsertionPoint,   
                           targetInsertionPoint,   
                           MessageKind.Complete,   
                           MessageSort.ASynchCall)  
```  
  
 Para criar uma mensagem que tem um indefinido de origem ou destino indefinido:  
  
```  
interaction.CreateLostFoundMessage(MessageKind.Found, insertionPoint);  
```  
  
 Há várias mensagens que você pode usar para identificar os pontos de inserção em todos os principais pontos em uma linha da vida:  
  
|Método em ILifeline|Usá-lo para inserir no momento|  
|-------------------------|------------------------------------|  
|`FindInsertionPointAtTop()`|Na parte superior da linha de vida.|  
|`FindInsertionPointAtBottom()`|A parte inferior da linha de vida.|  
|`FindInsertionPointAfterMessage`<br /><br /> `(IMessage previous)`|Um ponto imediatamente após a mensagem especificada.|  
|`FindInsertionPointAfterExecutionSpecification`<br /><br /> `(IExecutionSpecification previous)`|O ponto pode ser na linha de vida, ou em um bloco de especificação de execução pai.|  
|`FindInsertionPointAfterInteractionUse`<br /><br /> `(IInteractionUse previous)`|Um ponto de um uso de interação a seguir.|  
|`FindInsertionPointAfterCombinedFragment`<br /><br /> `(ICombinedFragment previous)`|Um ponto de um fragmento combinado a seguir.|  
|`FindInsertionPoint(IExecutionSpecification block)`|Na parte superior de um bloco de execução.|  
|`FindInsertionPoint(IInteractionOperand fragment)`|Na parte superior de um operando de um fragmento combinado.|  
  
 Quando você cria mensagens, tome cuidado para evitar definindo uma mensagem que passa pela outra mensagem.  
  
### <a name="to-create-combined-fragments-and-interaction-uses"></a>Para criar fragmentos combinados e usos de interação  
 Você pode criar fragmentos combinados e interação usa, especificando um ponto de inserção em cada linha da vida que deve ser coberta pelo elemento. Tome cuidado para evitar especificando um conjunto de pontos que passa por uma mensagem ou fragmento existente.  
  
```  
Interaction.CreateCombinedFragment(InteractionOperatorKind.Loop,   
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));  
Interaction.CreateInteractionUse(  
  Interaction.Lifelines.Select(lifeline => lifeline.FindInsertionPointAtTop()));  
```  
  
 Você também pode criar um fragmento combinado que aborda um conjunto existente de mensagens. Todas as mensagens devem se originar na mesma linha da vida ou bloco de execução.  
  
```  
ICombinedFragment cf = Interaction.CreateCombinedFragment(  
  InteractionOperatorKind.Loop,  
  Interaction.Lifelines.First().GetAllOutgoingMessages());  
```  
  
 Um fragmento combinado sempre é criado com um operando único. Para criar um novo operando, você deve especificar o operando existente que você deseja inserir antes ou depois, e se você deseja inserir depois dela, ou antes dela:  
  
```  
// Create an additional operand before the first  
cf.CreateInteractionOperand(cf.Operands.First(), false);  
// Create an additional operand after the last:  
cf.CreateInteractionOperand(cf.Operands.Last(), true);  
```  
  
## <a name="troubleshooting"></a>Solução de problemas  
 As formas aparecerão em posições incorretas se as alterações não forem concluídas com um `UpdateShapePositions()` ou `Layout()` operação.  
  
 A maioria dos outros problemas são causados por pontos de inserção que está sendo desalinhados, para que novas mensagens ou fragmentos precisam ultrapassar a outras pessoas. Os sintomas podem ser que nenhuma alteração é realizada ou uma exceção será lançada. A exceção não pode ser lançada até que o `UpdateShapePositions()` ou `Layout()` operação é executada.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Uml.Interactions?displayProperty=fullName>   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md)   
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)



