---
title: Definir um manipulador de gesto em um diagrama de modelagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending, double-click
- UML - extending, drag and drop
ms.assetid: e5e1d70a-3539-4321-a3b1-89e86e4d6430
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 3e448b14a2a24994b9f03a569b0bb568d538bc69
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722181"
---
# <a name="define-a-gesture-handler-on-a-modeling-diagram"></a>Definir um manipulador de gestos em um diagrama de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir comandos que são executados quando o usuário clica duas vezes ou arrasta itens em um diagrama UML. Você pode empacotar essas extensões em uma extensão de integração do Visual Studio ([VSIX](http://go.microsoft.com/fwlink/?LinkId=160780)) e distribuí-lo para outros usuários do Visual Studio.  
  
 Se já houver um comportamento interno para o tipo de diagrama e o tipo de elemento que você deseja arrastar, pode não ser capaz de adicionar ou substituir esse comportamento.  
  
## <a name="requirements"></a>Requisitos  
 Ver [requisitos de](../modeling/extend-uml-models-and-diagrams.md#Requirements).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="creating-a-gesture-handler"></a>Criando um manipulador de gesto  
 Para definir um manipulador de gesto para um designer UML, você deve criar uma classe que define o comportamento do manipulador de gesto e inserir essa classe em um Visual Studio Integration VSIX (extensão). O VSIX atua como um contêiner que pode instalar o manipulador. Há dois métodos alternativos de definição de um manipulador de gesto:  
  
-   **Crie um manipulador de gesto em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Usá-lo se você não deseja combinar seu manipulador com outros tipos de extensão, como extensões de validação, itens de caixa de ferramentas personalizada ou comandos de menu.  
  
-   **Crie manipulador separado de gesto e projetos VSIX.** Use este método se você desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se seu manipulador de gesto esperar que o modelo observe as restrições específicas, você poderá inseri-lo no mesmo VSIX que um método de validação.  
  
#### <a name="to-create-a-gesture-handler-in-its-own-vsix"></a>Para criar um manipulador de gesto em seu próprio VSIX  
  
1. No **novo projeto** caixa de diálogo **projetos de modelagem**, selecione **extensão de gesto**.  
  
2. Abra o **. CS** de arquivos no novo projeto e modificar o `GestureExtension` classe para implementar seu manipulador de gesto.  
  
    Para obter mais informações, consulte [Implementando o manipulador de gesto](#Implementing).  
  
3. Teste o manipulador de gesto pressionando F5. Para obter mais informações, consulte [executando o manipulador de gesto](#Executing).  
  
4. Instalar o manipulador de gesto em outro computador copiando o arquivo **bin\\\*\\\*. VSIX** que é compilado pelo seu projeto. Para obter mais informações, consulte [instalando e desinstalando uma extensão](#Installing).  
  
   Aqui está o procedimento alternativo:  
  
#### <a name="to-create-a-separate-class-library-dll-project-for-the-gesture-handler"></a>Para criar um projeto de biblioteca (DLL) de classe separada para o manipulador de gesto  
  
1. Criar um projeto de biblioteca de classes, nova [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução, ou em uma solução existente.  
  
   1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
   2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, na coluna do meio, escolha **biblioteca de classes**.  
  
2. Adicione as seguintes referências ao seu projeto.  
  
    `Microsoft.VisualStudio.Modeling.Sdk.[version]`  
  
    `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]`  
  
    `Microsoft.VisualStudio.ArchitectureTools.Extensibility`  
  
    `Microsoft.VisualStudio.Uml.Interfaces`  
  
    `System.ComponentModel.Composition`  
  
    `System.Windows.Forms`  
  
    `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer` – Você precisa apenas se você estiver estendendo diagramas de camada. Para obter mais informações, consulte [estender diagramas de camada](../modeling/extend-layer-diagrams.md).  
  
3. Adicionar um arquivo de classe ao projeto e defina seu conteúdo para o código a seguir.  
  
   > [!NOTE]
   >  Altere o nome de namespace e classe de acordo com sua preferência.  
  
   ```  
   using System.ComponentModel.Composition;  
   using System.Linq;  
   using System.Collections.Generic;  
   using Microsoft.VisualStudio.Modeling.Diagrams;  
   using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
   using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
   using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;  
   using Microsoft.VisualStudio.Modeling;  
   using Microsoft.VisualStudio.Uml.Classes;  
   // ADD other UML namespaces if required  
  
   namespace MyGestureHandler // CHANGE  
   {  
     // DELETE any of these attributes if the handler  
     // should not work with some types of diagram.  
     [ClassDesignerExtension]  
     [ActivityDesignerExtension]  
     [ComponentDesignerExtension]  
     [SequenceDesignerExtension]  
     [UseCaseDesignerExtension]  
     // [LayerDesignerExtension]  
  
     // Gesture handlers must export IGestureExtension:  
     [Export(typeof(IGestureExtension))]  
     // CHANGE class name  
     public class MyGesture1 : IGestureExtension  
     {  
       [Import]  
       public IDiagramContext DiagramContext { get; set; }  
  
       /// <summary>  
       /// Called when the user double-clicks on the diagram  
       /// </summary>  
       /// <param name="targetElement"></param>  
       /// <param name="diagramPointEventArgs"></param>  
       public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
  
         // Get the target shape, if any. Null if the target is the diagram.  
         IShape targetIShape = targetElement.CreateIShape();  
  
         // Do something...  
       }  
  
       /// <summary>  
       /// Called repeatedly when the user drags from anywhere on the screen.  
       /// Return value should indicate whether a drop here is allowed.  
       /// </summary>  
       /// <param name="targetMergeElement">References the element to be dropped on.</param>  
       /// <param name="diagramDragEventArgs">References the element to be dropped.</param>  
       /// <returns></returns>  
       public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
  
         // Get the target element, if any. Null if the target is the diagram.  
         IShape targetIShape = targetMergeElement.CreateIShape();  
  
         // This example allows drag of any UML elements.  
         return GetModelElementsFromDragEvent(diagramDragEventArgs).Count() > 0;  
       }  
  
       /// <summary>  
       /// Execute the action to be performed on the drop.  
       /// </summary>  
       /// <param name="targetDropElement"></param>  
       /// <param name="diagramDragEventArgs"></param>  
       public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
       }  
  
       /// <summary>  
       /// Retrieves UML IElements from drag arguments.  
       /// Works for drags from UML diagrams.  
       /// </summary>  
       private IEnumerable<IElement> GetModelElementsFromDragEvent  
               (DiagramDragEventArgs dragEvent)  
       {  
         //ElementGroupPrototype is the container for  
         //dragged and copied elements and toolbox items.  
         ElementGroupPrototype prototype =  
            dragEvent.Data.  
            GetData(typeof(ElementGroupPrototype))  
                 as ElementGroupPrototype;  
         // Locate the originals in the implementation store.  
         IElementDirectory implementationDirectory =  
            dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;  
  
         return prototype.ProtoElements.Select(  
           prototypeElement =>  
           {  
             ModelElement element = implementationDirectory  
               .FindElement(prototypeElement.ElementId);  
             ShapeElement shapeElement = element as ShapeElement;  
             if (shapeElement != null)  
             {  
               // Dragged from a diagram.  
               return shapeElement.ModelElement as IElement;  
             }  
             else  
             {  
               // Dragged from UML Model Explorer.  
               return element as IElement;  
             }  
           });  
       }  
  
     }  
   }  
  
   ```  
  
    Para obter mais informações sobre o que colocar nos métodos, consulte [Implementando o manipulador de gesto](#Implementing).  
  
   Você deve adicionar seu comando de menu a um projeto VSIX, que atua como um contêiner para o comando de instalação. Se você quiser, você pode incluir outros componentes no mesmo VSIX.  
  
#### <a name="to-add-a-separate-gesture-handler-to-a-vsix-project"></a>Para adicionar um manipulador separado de gesto a um projeto VSIX  
  
1.  Você não precisará deste procedimento se você tiver criado o manipulador de gesto com seu próprio VSIX.  
  
2.  Crie um projeto VSIX, a menos que sua solução já tenha um.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho da solução, escolha **Add**, **novo projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, selecione **extensibilidade**. Na coluna do meio, escolha **VSIX Project**.  
  
3.  Defina o projeto VSIX como o projeto de inicialização da solução.  
  
    -   No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.  
  
4.  Na **vsixmanifest**, adicione o projeto de biblioteca de classes de manipulador de gesto como um componente de MEF:  
  
    1.  Sobre o **metadados** guia, defina um nome para o VSIX.  
  
    2.  Sobre o **instalar destinos** guia, defina as versões do Visual Studio como os destinos.  
  
    3.  Sobre o **ativos** guia, escolha um **New**e, na caixa de diálogo, defina:  
  
         **Tipo de** = **componente MEF**  
  
         **Código-fonte** = **um projeto na solução atual**  
  
         **Projeto** = *seu projeto de biblioteca de classes*  
  
##  <a name="Executing"></a> Executar o manipulador de gesto  
 Para fins de teste, execute o manipulador de gesto em modo de depuração.  
  
#### <a name="to-test-the-gesture-handler"></a>Para testar o manipulador de gesto  
  
1. Pressione **F5**, ou o **depurar** menu, clique em **iniciar depuração**.  
  
    Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciado.  
  
    **Solução de problemas**: se um novo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não for iniciado:  
  
   -   Se você tiver mais de um projeto, certifique-se de que o projeto do VSIX está definido como o projeto de inicialização da solução.  
  
   -   No Solution Explorer, no menu de atalho da inicialização ou somente projeto, escolha Propriedades. No editor de propriedades de projeto, escolha o **depurar** guia. Certifique-se de que a cadeia de caracteres na **Iniciar programa externo** campo é o nome do caminho completo do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], normalmente:  
  
        `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`  
  
2. Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem. Use um diagrama que pertence a um dos tipos listados nos atributos de classe de manipulador de gesto.  
  
3. Clique duas vezes em qualquer lugar no diagrama. Seu manipulador de clique duplo deve ser chamado.  
  
4. Arraste um elemento do UML Explorer para o diagrama. Seu manipulador arrastar deve ser chamado.  
  
   **Solução de problemas**: se o manipulador de gesto não funcionar, verifique se:  
  
-   O projeto do manipulador de gesto está listado como um componente MEF na **ativos** guia **source.extensions.manifest** no projeto VSIX.  
  
-   Os parâmetros de todos os `Import` e `Export` atributos são válidos.  
  
-   O `CanDragDrop` método não está retornando `false`.  
  
-   O tipo de modelo de diagrama que você está usando (classe UML, sequência e assim por diante) está listado como um dos atributos de classe de manipulador [ClassDesignerExtension], gesto [SequenceDesignerExtension] e assim por diante.  
  
-   Não há nenhuma funcionalidade interna já definida para esse tipo de destino e elemento solto.  
  
##  <a name="Implementing"></a> Implementando o manipulador de gesto  
  
### <a name="the-gesture-handler-methods"></a>Os métodos do manipulador de gesto  
 A classe de manipulador de gesto implementa e exporta <xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement.IGestureExtension>. Os métodos que você precisa definir são da seguinte maneira:  
  
|||  
|-|-|  
|`bool CanDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|Retornar `true` para permitir que o elemento de origem referenciado em `dragEvent` para ser solto nesse destino.<br /><br /> Esse método não deve fazer alterações no modelo. Ele deve funcionar rapidamente, porque ele é usado para determinar o estado da seta quando o usuário move o mouse.|  
|`void OnDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|Atualizar o modelo com base no objeto de origem referenciado em `dragEvent`e o destino.<br /><br /> Chamado quando o usuário libera o mouse após arrastar.|  
|`void OnDoubleClick (ShapeElement target, DiagramPointEventArgs pointEvent)`|`target` é a forma que o usuário clicou duas vezes.|  
  
 Você pode escrever manipuladores que podem aceitar não apenas UML, mas também uma ampla variedade de outros itens, como arquivos, nós em uma exibição de classe do .NET e assim por diante. O usuário pode arrastar qualquer um desses itens para um diagrama UML, desde que você escreva um `OnDragDrop` método que possa decodificar o formulário serializado dos itens. Os métodos de decodificação variam de um tipo de item para outro.  
  
 Os parâmetros desses métodos são:  
  
-   `ShapeElement target`. A forma ou diagrama no qual o usuário arrastou algo.  
  
     `ShapeElement` é uma classe na implementação subjacente ao UML ferramentas de modelagem. Para reduzir o risco de colocar o modelo UML e diagramas em um estado inconsistente, é recomendável que você não use os métodos dessa classe diretamente. Em vez disso, coloque o elemento em um `IShape`e, em seguida, use os métodos descritos [exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md).  
  
    -   Para obter um `IShape`:  
  
        ```  
        IShape targetIShape = target.CreateIShape(target);  
        ```  
  
    -   Para obter o elemento de modelo que é o destino de arrastar ou clique duas vezes em operação:  
  
        ```  
        IElement target = targetIShape.Element;  
        ```  
  
         Você pode converter isso em um tipo de elemento mais específico.  
  
    -   Para obter o armazenamento de modelo UML que contém o modelo UML:  
  
        ```  
        IModelStore modelStore =   
          targetIShape.Element.GetModelStore();   
        ```  
  
    -   Para obter acesso ao provedor de host e o serviço:  
  
        ```  
        target.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE  
        ```  
  
-   `DiagramDragEventArgs eventArgs`. Esse parâmetro carrega o formulário serializado do objeto de fonte de uma operação de arrastar:  
  
    ```  
    System.Windows.Forms.IDataObject data = eventArgs.Data;    
    ```  
  
     Você pode arrastar elementos de vários tipos diferentes para um diagrama, de diferentes partes do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], ou na área de trabalho do Windows. Diferentes tipos de elemento são codificados de diferentes maneiras na `IDataObject`. Para extrair os elementos dele, consulte a documentação para o tipo de objeto apropriado.  
  
     Se seu objeto de origem é um elemento UML arrastado do Gerenciador de modelos UML ou de outro diagrama UML, consulte [elementos de modelo de obter UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).  
  
### <a name="writing-the-code-of-the-methods"></a>Gravando o código dos métodos  
 Para obter mais informações sobre como escrever o código para ler e atualizar o modelo, consulte [Programando com a API UML](../modeling/programming-with-the-uml-api.md).  
  
 Para obter informações sobre como acessar informações de modelo em uma operação de arrastar, consulte [elementos de modelo de obter UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).  
  
 Se você estiver lidando com um diagrama de sequência, consulte também [diagramas de sequência UML Editar usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).  
  
 Além dos parâmetros dos métodos, você também pode declarar uma propriedade importada em sua classe que fornece acesso para o diagrama atual e o modelo.  
  
```  
[Import] public IDiagramContext DiagramContext { get; set; }  
```  
  
 A declaração de `IDiagramContext` permite que você escreva código em seus métodos que acessam o diagrama, a seleção atual e o modelo:  
  
```  
IDiagram diagram = this.DiagramContext.CurrentDiagram;  
foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>)  
{ IElement element = shape.Element; ... }  
IModelStore modelStore = diagram.ModelStore;  
IModel model = modelStore.Root;  
foreach (IDiagram diagram in modelStore.Diagrams) {...}  
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}  
```  
  
 Para obter mais informações, consulte [navegar no modelo UML](../modeling/navigate-the-uml-model.md).  
  
##  <a name="Installing"></a> Instalando e desinstalando uma extensão  
 Você pode instalar um [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão em seu próprio computador e em outros computadores.  
  
#### <a name="to-install-an-extension"></a>Para instalar uma extensão  
  
1.  No seu computador, localize o **VSIX** arquivo que foi criado pelo seu projeto VSIX.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **Abrir pasta no Windows Explorer**.  
  
    2.  Localize o arquivo **bin\\\*\\**_Seuprojeto_**. VSIX**  
  
2.  Cópia de **. VSIX** arquivo ao computador de destino no qual você deseja instalar a extensão. Isso pode ser seu próprio computador ou outro.  
  
     O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou no **vsixmanifest**.  
  
3.  No computador de destino, abra o **VSIX** arquivo.  
  
     **Instalador de extensão do Visual Studio** abre e instala a extensão.  
  
4.  Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  
  
#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão  
  
1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.  
  
2. Expandir **extensões instaladas**.  
  
3. Selecione a extensão e, em seguida, escolha **desinstalação**.  
  
   Raramente, uma extensão defeituosa Falha ao carregar e cria um relatório na janela de erros, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:  
  
   *% LocalAppData %* **\Local\Microsoft\VisualStudio\\\Extensions [versão]**  
  
##  <a name="DragExample"></a> Exemplo  
 O exemplo a seguir mostra como criar linhas de vida em um diagrama de sequência, com base nas partes e portas de um componente arrastadas de um diagrama de componente.  
  
 Para testá-lo, pressione F5. Uma instância experimental do Visual Studio é aberto. Nesse caso, abrir um modelo UML e crie um componente em um diagrama de componente. Adicione a este componente algumas interfaces e partes de componentes internos. Selecione as interfaces e partes. Em seguida, arraste as interfaces e partes para um diagrama de sequência. (Arraste do diagrama de componentes até a guia para o diagrama de sequência e para baixo para o diagrama de sequência). Uma linha da vida será exibida para cada interface e parte.  
  
 Para obter mais informações sobre interações de associação para diagramas de sequência, consulte [diagramas de sequência UML Editar usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).  
  
```  
using System.Collections.Generic;  
using System.ComponentModel.Composition;  
using System.Linq;  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.Uml.Interactions;  
using Microsoft.VisualStudio.Uml.CompositeStructures;  
using Microsoft.VisualStudio.Uml.Components;  
  
/// <summary>  
/// Creates lifelines from component ports and parts.  
/// </summary>  
[Export(typeof(IGestureExtension))]  
[SequenceDesignerExtension]  
public class CreateLifelinesFromComponentParts : IGestureExtension  
{  
  [Import]  
  public IDiagramContext Context { get; set; }  
  
  /// <summary>  
  /// Called by the modeling framework when  
  /// the user drops something on a target.  
  /// </summary>  
  /// <param name="target">The target shape or diagram </param>  
  /// <param name="dragEvent">The item being dragged</param>  
  public void OnDragDrop(ShapeElement target,  
           DiagramDragEventArgs dragEvent)  
  {  
    ISequenceDiagram diagram = Context.CurrentDiagram  
            as ISequenceDiagram;  
    IInteraction interaction = diagram.Interaction;  
    if (interaction == null)  
    {  
      // Sequence diagram is empty: create an interaction.  
      interaction = diagram.ModelStore.Root.CreateInteraction();  
      interaction.Name = Context.CurrentDiagram.Name;  
      diagram.Bind(interaction);  
    }  
    foreach (IConnectableElement connectable in  
       GetConnectablesFromDrag(dragEvent))  
    {  
      ILifeline lifeline = interaction.CreateLifeline();  
      lifeline.Represents = connectable;  
      lifeline.Name = connectable.Name;  
    }  
  }  
  
  /// <summary>  
  /// Called by the modeling framework to determine whether  
  /// the user can drop something on a target.  
  /// Must not change anything.  
  /// </summary>  
  /// <param name="target">The target shape or diagram</param>  
  /// <param name="dragEvent">The item being dragged</param>  
  /// <returns>true if this item can be dropped on this target</returns>  
  public bool CanDragDrop(ShapeElement target,  
           DiagramDragEventArgs dragEvent)  
  {  
    IEnumerable<IConnectableElement> connectables = GetConnectablesFromDrag(dragEvent);  
    return connectables.Count() > 0;  
  }  
  
  ///<summary>  
  /// Get dragged parts and ports of an IComponent.  
  ///</summary>  
  private IEnumerable<IConnectableElement>  
    GetConnectablesFromDrag(DiagramDragEventArgs dragEvent)  
  {  
    foreach (IElement element in  
      GetModelElementsFromDragEvent(dragEvent))  
    {  
      IConnectableElement part = element as IConnectableElement;  
      if (part != null)  
      {  
        yield return part;  
      }  
    }  
  }  
  
  /// <summary>  
  /// Retrieves UML IElements from drag arguments.  
  /// Works for drags from UML diagrams.  
  /// </summary>  
  private IEnumerable<IElement> GetModelElementsFromDragEvent  
          (DiagramDragEventArgs dragEvent)  
  {  
    //ElementGroupPrototype is the container for  
    //dragged and copied elements and toolbox items.  
    ElementGroupPrototype prototype =  
       dragEvent.Data.  
       GetData(typeof(ElementGroupPrototype))  
            as ElementGroupPrototype;  
    // Locate the originals in the implementation store.  
    IElementDirectory implementationDirectory =  
       dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;  
  
    return prototype.ProtoElements.Select(  
      prototypeElement =>  
      {  
        ModelElement element = implementationDirectory  
          .FindElement(prototypeElement.ElementId);  
        ShapeElement shapeElement = element as ShapeElement;  
        if (shapeElement != null)  
        {  
          // Dragged from a diagram.  
          return shapeElement.ModelElement as IElement;  
        }  
        else  
        {  
          // Dragged from UML Model Explorer.  
          return element as IElement;  
        }  
      });  
  }  
  
  public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)  
  {  
  }  
}  
  
```  
  
 O código do `GetModelElementsFromDragEvent()` descrito [elementos de modelo de obter UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).  
  
## <a name="see-also"></a>Consulte também  
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)



