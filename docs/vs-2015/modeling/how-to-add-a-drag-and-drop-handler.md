---
title: 'Como: adicionar um manipulador de arrastar e soltar | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39ee88a0-85c3-485e-8c0a-d9644c6b25d9
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: f89ea35c9113ddff67a9d1322b1c83c41e05709a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49848965"
---
# <a name="how-to-add-a-drag-and-drop-handler"></a>Como adicionar um manipulador de evento de arrastar e soltar
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível adicionar manipuladores para eventos arrastar e soltar à DSL, para os usuários poderem arrastar itens para o diagrama de outros diagramas ou de outras partes do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Também é possível adicionar manipuladores de eventos como cliques duplos. Juntos, os manipuladores de arrastar-e-soltar e clique duas vezes são conhecidos como *manipuladores de gesto*.  
  
 Este tópico discute gestos de arrastar e soltar originados em outros diagramas. Para mover e copiar eventos dentro de um único diagrama, considere a alternativa de definir uma subclasse de `ElementOperations`. Para obter mais informações, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md). Também poderá ser possível personalizar a definição da DSL.  
  
## <a name="in-this-topic"></a>Neste tópico  
  
-   As duas primeiras seções descrevem métodos alternativos para definir um manipulador de gestos:  
  
    -   [Definindo manipuladores de gestos substituindo métodos ShapeElement&lt;1](#overrideShapeElement). Os métodos `OnDragDrop`, `OnDoubleClick`, `OnDragOver` e outros podem ser substituídos.  
  
    -   [Definindo manipuladores de gestos usando MEF](#MEF). Use esse método se desejar permitir a desenvolvedores terceiros definir seus próprios manipuladores à DSL. Usuários podem escolher instalar as extensões de terceiros após instalar a DSL.  
  
-   [Como decodificar o Item arrastado](#extracting). Elementos podem ser arrastados de qualquer janela ou da área de trabalho, bem como de uma DSL.  
  
-   [Como obter o Original arrastada Item](#getOriginal). Se o item arrastado for um elemento DSL, é possível abrir o modelo de origem e acessar o elemento.  
  
-   [Usando ações do Mouse: Arrastando itens de compartimento](#mouseActions). Este exemplo demonstra um manipulador de nível inferior que intercepta ações do mouse nos campos de uma forma. O exemplo permite ao usuário reordenar os itens em um compartimento arrastando com o mouse.  
  
##  <a name="overrideShapeElement"></a> Definindo manipuladores de gestos substituindo métodos ShapeElement  
 Adicione um novo arquivo de código ao projeto DSL. Para um manipulador de gestos, geralmente é necessário ter ao menos as seguintes instruções `using`:  
  
```csharp  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using System.Linq;  
```  
  
 No novo arquivo, defina uma classe parcial da classe da forma ou do diagrama que deve responder à operação de arrastar. Substitua os seguintes métodos:  
  
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragOver%2A>- Esse método é chamado quando o ponteiro do mouse entra na forma durante uma operação de arrastar. O método deve inspecionar o item que o usuário está arrastando e definir a propriedade Efeito para indicar se o usuário pode soltar o item nessa forma. A propriedade Efeito determina a aparência do cursor enquanto estiver sobre a forma e também determina se `OnDragDrop()` será chamado quando o usuário soltar o botão do mouse.  
  
  ```csharp  
  partial class MyShape // MyShape generated from DSL Definition.  
  {  
      public override void OnDragOver(DiagramDragEventArgs e)  
      {  
        base.OnDragOver(e);  
        if (e.Effect == System.Windows.Forms.DragDropEffects.None   
             && IsAcceptableDropItem(e)) // To be defined  
        {  
          e.Effect = System.Windows.Forms.DragDropEffects.Copy;  
        }  
      }  
  
  ```  
  
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragDrop%2A> – Esse método é chamado se o usuário soltar o botão do mouse enquanto o ponteiro do mouse estiver sobre essa forma ou diagrama, se `OnDragOver(DiagramDragEventArgs e)` anteriormente definir `e.Effect` para outro valor além de `None`.  
  
  ```csharp  
  public override void OnDragDrop(DiagramDragEventArgs e)  
      {  
        if (!IsAcceptableDropItem(e))  
        {  
          base.OnDragDrop(e);  
        }  
        else   
        { // Process the dragged item, for example merging a copy into the diagram  
          ProcessDragDropItem(e); // To be defined  
        }    
      }  
  
  ```  
  
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDoubleClick%2A> – Esse método é chamado quando o usuário clica duas vezes na forma ou diagrama.  
  
   Para obter mais informações, consulte [como: interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md).  
  
  Defina `IsAcceptableDropItem(e)` para determinar se o item arrastado é aceitável e ProcessDragDropItem(e) para atualizar o modelo quando o item for solto. Esses métodos devem primeiro extrair o item dos argumentos do evento. Para obter informações sobre como fazer isso, consulte [como obter uma referência para o item arrastado](#extracting).  
  
##  <a name="MEF"></a> Definindo manipuladores de gestos usando MEF  
 MEF (Managed Extensibility Framework) permite definir componentes que podem ser instalados com configuração mínima. Para saber mais, confira [Managed Extensibility Framework (MEF)](http://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde).  
  
#### <a name="to-define-a-mef-gesture-handler"></a>Para definir um manipulador de gestos de MEF  
  
1.  Adicionar ao seu **Dsl** e **DslPackage** projetos a **MefExtension** arquivos que são descritos na [estender a DSL usando MEF](../modeling/extend-your-dsl-by-using-mef.md).  
  
2.  Agora é possível definir um manipulador de gestos como um componente MEF:  
  
    ```  
  
    // This attribute is defined in the generated file  
    // DslPackage\MefExtension\DesignerExtensionMetaDataAttribute.cs:  
    [MyDslGestureExtension]  
    public class MyGestureHandlerClassName : IGestureExtension  
    {  
      /// <summary>  
      /// Called to determine whether a drag onto the diagram can be accepted.  
      /// </summary>  
      /// <param name="diagramDragEventArgs">Contains a link to the item that is being dragged</param>  
      /// <param name="targetMergeElement">The shape or connector that the mouse is over</param>  
      /// <returns>True if the item can be accepted on the targetMergeElement.</returns>  
      public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)  
      {  
        MyShape target = targetMergeElement as MyShape;  
        if (target == null) return false;  
        if (target.IsAcceptableDropItem(diagramDragEventArgs)) return true;   
        return false;  
      }  
      public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)  
      {  
        MyShape target = targetMergeElement as MyShape;  
        if (target == null || ! target.IsAcceptableDropItem(diagramDragEventArgs)) return;  
        // Process the dragged item, for example merging a copy into the diagram:  
        target.ProcessDragDropItem(diagramDragEventArgs);  
     }  
  
    ```  
  
     É possível criar mais de um componente de manipulador de gestos, como quando existem diversos tipos de objetos arrastados.  
  
3.  Adicione definições de classe parcial para as classes de forma, conector ou diagrama de destino e defina os métodos `IsAcceptableDropItem()` e `ProcessDragDropItem()`. Esses métodos devem começar extraindo o item arrastado dos argumentos do evento. Para obter mais informações, consulte [como obter uma referência para o item arrastado](#extracting).  
  
##  <a name="extracting"></a> Como decodificar o item arrastado  
 Quando o usuário arrasta um item para o diagrama ou de uma parte do diagrama para outra, as informações sobre o item que está sendo arrastado estão disponíveis em `DiagramDragEventArgs`. Como a operação de arrastar pode ter começado em qualquer objeto na tela, os dados podem estar disponíveis em qualquer um entre uma variedade de formatos. O código deve reconhecer os formatos com os quais é capaz de lidar.  
  
 Para saber os formatos nos quais as informações de origem do arrasto estão disponíveis, execute o código em modo de depuração, definindo um ponto de interrupção na entrada para `OnDragOver()` ou `CanDragDrop()`. Inspecione os valores do parâmetro `DiagramDragEventArgs`. As informações são fornecidas em dois formulários:  
  
- <xref:System.Windows.Forms.IDataObject>  `Data` – Essa propriedade contém versões serializadas dos objetos de origem, geralmente em mais de um formato. Suas funções mais úteis são:  
  
  -   diagramEventArgs.Data.GetDataFormats() – Lista os formatos nos quais é possível decodificar o objeto arrastado. Por exemplo, se o usuário arrastar um arquivo da área de trabalho, os formatos disponíveis incluem o nome de arquivo ("`FileNameW`").  
  
  -   `diagramEventArgs.Data.GetData(format)` – Decodifica o objeto arrastado no formato especificado. Converte o objeto para o tipo adequado. Por exemplo:  
  
       `string fileName = diagramEventArgs.Data.GetData("FileNameW") as string;`  
  
       Também é possível transmitir objetos como referências do Model Bus da origem em seu próprio formato personalizado. Para obter mais informações, consulte [como enviar referências do Model Bus em arrastar e soltar](#mbr).  
  
- <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> `Prototype` – Use essa propriedade se desejar que os usuários arrastar itens de uma DSL ou um modelo UML. Um protótipo de grupo de elementos contém um ou mais objetos, links e os valores de suas propriedades. Também é usado em operações colar e ao adicionar um elemento da caixa de ferramentas. Em um protótipo, objetos e seus tipos são identificados por Guid. Por exemplo, esse código permite ao usuário arrastar elementos de classe de um diagrama UML ou do Gerenciador de Modelos UML:  
  
  ```csharp  
  private bool IsAcceptableDropItem(DiagramDragEventArgs e)  
  {  
    return e.Prototype != null && e.Prototype.RootProtoElements.Any(element =>   
          element.DomainClassId.ToString()   
          == "3866d10c-cc4e-438b-b46f-bb24380e1678"); // Accept UML class shapes.  
   // Or, from another DSL: SourceNamespace.SourceShapeClass.DomainClassId  
  }  
  
  ```  
  
   Para aceitar formas UML, determine as Guids das classes de forma UML por experimento. Lembre-se de que geralmente há mais de um tipo de elemento em qualquer diagrama. Lembre-se também de que um objeto arrastado de uma DSL ou diagrama UML é a forma, não o elemento do modelo.  
  
  `DiagramDragEventArgs` também têm propriedades que indicam a posição atual do ponteiro do mouse e se o usuário está pressionando as teclas CTRL, ALT ou SHIFT.  
  
##  <a name="getOriginal"></a> Como obter o original de um elemento arrastado  
 As propriedades `Data` e `Prototype` dos argumentos do evento contêm apenas uma referência à forma arrastada. Geralmente, se desejar criar um objeto na DSL de destino que é derivada do protótipo de alguma maneira, será necessário obter acesso ao original, por exemplo, lendo o conteúdo do arquivo ou navegando até o elemento do modelo representado por uma forma.  É possível usar o Visual Studio Model Bus para ajudar com isso.  
  
### <a name="to-prepare-a-dsl-project-for-model-bus"></a>Preparar um projeto DSL para Model Bus  
  
1.  Torne a DSL de origem acessível pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Model Bus:  
  
    1.  Faça o download e instale a extensão Visual Studio Model Bus, se ainda não estiver instalada. Para obter mais informações, consulte [SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=185579).  
  
    2.  Abra o arquivo de definição da DSL da DSL de origem no Designer de DSL. Clique duas vezes na superfície de design e, em seguida, clique em **habilitar Modelbus**. Na caixa de diálogo, escolha uma ou as duas opções.  Clique em **OK**. Um novo projeto "ModelBus" é adicionado à solução de DSL.  
  
    3.  Clique em **transformar todos os modelos** e recompile a solução.  
  
###  <a name="mbr"></a> Enviar um objeto de uma DSL de origem  
  
1.  Na subclasse ElementOperations, substitua `Copy()` para codificar uma Referência do Model Bus (MBR) no IDataObject. Esse método será chamado quando o usuário começar a arrastar do diagrama de origem. A MBR codificada estará disponível no IDataObject quando o usuário soltar no diagrama de destino.  
  
    ```  
  
    using Microsoft.VisualStudio.Modeling;  
    using Microsoft.VisualStudio.Modeling.Shell;  
    using Microsoft.VisualStudio.Modeling.Diagrams;  
    using Microsoft.VisualStudio.Modeling.Integration;  
    using Microsoft.VisualStudio.Modeling.Integration.Shell;  
    using System.Drawing; // PointF  
    using  System.Collections.Generic; // ICollection  
    using System.Windows.Forms; // for IDataObject  
    ...  
    public class MyElementOperations : DesignSurfaceElementOperations  
    {  
        public override void Copy(System.Windows.Forms.IDataObject data, System.Collections.Generic.ICollection<ModelElement> elements, ClosureType closureType, System.Drawing.PointF sourcePosition)  
        {  
          base.Copy(data, elements, closureType, sourcePosition);  
  
          // Get the ModelBus service:  
          IModelBus modelBus =  
              this.Store.GetService(typeof(SModelBus)) as IModelBus;  
          DocData docData = ((VSDiagramView)this.Diagram.ActiveDiagramView).DocData;  
          string modelFile = docData.FileName;  
          // Get an adapterManager for the target DSL:  
          ModelBusAdapterManager manager =  
              (modelBus.FindAdapterManagers(modelFile).First());  
          ModelBusReference modelReference = manager.CreateReference(modelFile);  
          ModelBusReference elementReference = null;  
          using (ModelBusAdapter adapter = modelBus.CreateAdapter(modelReference))  
          {  
            elementReference = adapter.GetElementReference(elements.First());  
          }  
  
          data.SetData("ModelBusReference", elementReference);  
        }  
    ...}  
  
    ```  
  
### <a name="to-receive-a-model-bus-reference-from-a-dsl-in-a-target-dsl-or-uml-project"></a>Para receber uma Referência do Model Bus de uma DSL na DSL de destino ou no projeto UML  
  
1.  No projeto DSL de destino, adicione referências do projeto a:  
  
    -   O projeto Dsl de origem.  
  
    -   O projeto ModelBus de origem.  
  
2.  No arquivo de código do manipulador de gestos, adicione as seguintes referências de namespace:  
  
    ```csharp  
    using Microsoft.VisualStudio.Modeling;  
    using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
    using Microsoft.VisualStudio.Modeling.Diagrams;  
    using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
    using Microsoft.VisualStudio.Modeling.Integration;  
    using SourceDslNamespace;  
    using SourceDslNamespace.ModelBusAdapters;  
  
    ```  
  
3.  O exemplo a seguir ilustra como obter acesso ao elemento do modelo de origem:  
  
    ```  
    partial class MyTargetShape // or diagram or connector   
    {  
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)  
      {  
        // Verify that we're being passed an Object Shape.  
        ElementGroupPrototype prototype = diagramDragEventArgs.Prototype;  
        if (prototype == null) return;  
        if (Company.InstanceDiagrams.ObjectShape.DomainClassId  
          != prototype.RootProtoElements.First().DomainClassId)  
          return;  
        // - This is an ObjectShape.  
        // - We need to access the originating Store, find the shape, and get its object.  
  
        IModelBus modelBus = targetDropElement.Store.GetService(typeof(SModelBus)) as IModelBus;  
  
        // Unpack the MBR that was packed in Copy:  
        ModelBusReference reference = diagramDragEventArgs.Data.GetData("ModelBusReference") as ModelBusReference;  
        using (SourceDslAdapter adapter = modelBus.CreateAdapter(reference) as SourceDslAdapter)  
        {  
          using (ILinkedUndoTransaction t = LinkedUndoContext.BeginTransaction("doing things"))  
          {  
            // Quickest way to get the shape from the MBR:  
            ObjectShape firstShape = adapter.ResolveElementReference<ObjectShape>(reference);  
  
            // But actually there might be several shapes - so get them from the prototype instead:  
            IElementDirectory remoteDirectory = adapter.Store.ElementDirectory;  
            foreach (Guid shapeGuid in prototype.SourceRootElementIds)  
            {  
              PresentationElement pe = remoteDirectory.FindElement(shapeGuid) as PresentationElement;  
              if (pe == null) continue;  
              SourceElement instance = pe.ModelElement as SourceElement;  
              if (instance == null) continue;  
  
              // Do something with the object:  
          instance...  
            }  
            t.Commit();  
          }  
        }  
    }  
  
    ```  
  
### <a name="to-accept-an-element-sourced-from-a-uml-model"></a>Aceitar um elemento originado em um modelo UML  
  
-   O código a seguir aceita um objeto arrastado de um diagrama UML.  
  
    ```csharp  
  
      using Microsoft.VisualStudio.ArchitectureTools.Extensibility;  
      using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
      using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
      using Microsoft.VisualStudio.Modeling;  
      using Microsoft.VisualStudio.Modeling.Diagrams;  
      using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
      using Microsoft.VisualStudio.Uml.Classes;  
      using System;  
      using System.ComponentModel.Composition;  
      using System.Linq;  
    ...  
    partial class TargetShape  
    {  
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)  
      {  
            EnvDTE.DTE dte = this.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE;  
            // Find the UML project  
            foreach (EnvDTE.Project project in dte.Solution.Projects)  
            {  
              IModelingProject modelingProject = project as IModelingProject;  
              if (modelingProject == null) continue; // not a modeling project  
              IModelStore store = modelingProject.Store;  
              if (store == null) return;  
  
              foreach (IDiagram dd in store.Diagrams())  
              {  
                  // Get Modeling.Diagram that implements UML.IDiagram:  
                  Diagram diagram = dd.GetObject<Diagram>();   
  
                  foreach (Guid elementId in e.Prototype.SourceRootElementIds)  
                  {  
                    ShapeElement shape = diagram.Partition.ElementDirectory.FindElement(elementId) as ShapeElement;  
                    if (shape == null) continue;  
                    // This example assumes the shape is a UML class:  
                    IClass classElement = shape.ModelElement as IClass;  
                    if (classElement == null) continue;  
  
                    // Now do something with the UML class element ...  
                  }  
            }  
          break; // don't try any more projects   
    }  }  }  
  
    ```  
  
##  <a name="mouseActions"></a> Usando ações do Mouse: Arrastando itens de compartimento  
 É possível compilar um manipulador que intercepta ações do mouse nos campos de uma forma. O exemplo a seguir permite ao usuário reordenar os itens em um compartimento arrastando com o mouse.  
  
 Para compilar este exemplo, crie uma solução usando o **diagramas de classe** modelo de solução. Adicione um arquivo de código e adicione o código a seguir. Ajuste o namespace para o mesmo que o seu próprio.  
  
```csharp  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Design;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using System.Collections.Generic;  
using System.Linq;  
  
// This sample allows users to re-order items in a compartment shape by dragging.  
  
// This example is built on the "Class Diagrams" solution template of VMSDK (DSL Tools).  
// You will need to change the following domain class names to your own:  
// ClassShape = a compartment shape  
// ClassModelElement = the domain class displayed using a ClassShape  
// This code assumes that the embedding relationships displayed in the compartments  
// don't use inheritance (don't have base or derived domain relationships).  
  
namespace Company.CompartmentDrag  // EDIT.  
{  
 /// <summary>  
 /// Manage the mouse while dragging a compartment item.  
 /// </summary>  
 public class CompartmentDragMouseAction : MouseAction  
 {  
  private ModelElement sourceChild;  
  private ClassShape sourceShape;  
  private RectangleD sourceCompartmentBounds;  
  
  public CompartmentDragMouseAction(ModelElement sourceChildElement, ClassShape sourceParentShape, RectangleD bounds)  
   : base (sourceParentShape.Diagram)  
  {  
   sourceChild = sourceChildElement;  
   sourceShape = sourceParentShape;  
   sourceCompartmentBounds = bounds; // For cursor.  
  }  
  
  /// <summary>  
  /// Call back to the source shape to drop the dragged item.  
  /// </summary>  
  /// <param name="e"></param>  
  protected override void OnMouseUp(DiagramMouseEventArgs e)  
  {  
   base.OnMouseUp(e);  
   sourceShape.DoMouseUp(sourceChild, e);  
   this.Cancel(e.DiagramClientView);  
   e.Handled = true;  
  }  
  
  /// <summary>  
  /// Ideally, this shouldn't happen. This action should only be active  
  /// while the mouse is still pressed. However, it can happen if you  
  /// move the mouse rapidly out of the source shape, let go, and then   
  /// click somewhere else in the source shape. Yuk.  
  /// </summary>  
  /// <param name="e"></param>  
  protected override void OnMouseDown(DiagramMouseEventArgs e)  
  {  
   base.OnMouseDown(e);  
   this.Cancel(e.DiagramClientView);  
   e.Handled = false;  
  }  
  
  /// <summary>  
  /// Display an appropriate cursor while the drag is in progress:  
  /// Up-down arrow if we are inside the original compartment.  
  /// No entry if we are elsewhere.  
  /// </summary>  
  /// <param name="currentCursor"></param>  
  /// <param name="diagramClientView"></param>  
  /// <param name="mousePosition"></param>  
  /// <returns></returns>  
  public override System.Windows.Forms.Cursor GetCursor(System.Windows.Forms.Cursor currentCursor, DiagramClientView diagramClientView, PointD mousePosition)  
  {  
   // If the cursor is inside the original compartment, show up-down cursor.  
   return sourceCompartmentBounds.Contains(mousePosition)   
    ? System.Windows.Forms.Cursors.SizeNS // Up-down arrow.  
    : System.Windows.Forms.Cursors.No;  
  }  
 }  
  
 /// <summary>  
 /// Override some methods of the compartment shape.  
 /// *** GenerateDoubleDerived must be set for this shape in DslDefinition.dsl. ****  
 /// </summary>  
 public partial class ClassShape  
 {  
  /// <summary>  
  /// Model element that is being dragged.  
  /// </summary>  
  private static ClassModelElement dragStartElement = null;  
  /// <summary>  
  /// Absolute bounds of the compartment, used to set the cursor.  
  /// </summary>  
  private static RectangleD compartmentBounds;  
  
  /// <summary>  
  /// Attach mouse listeners to the compartments for the shape.  
  /// This is called once per compartment shape.  
  /// The base method creates the compartments for this shape.  
  /// </summary>  
  public override void EnsureCompartments()  
  {  
   base.EnsureCompartments();  
   foreach (Compartment compartment in this.NestedChildShapes.OfType<Compartment>())  
   {  
    compartment.MouseDown += new DiagramMouseEventHandler(compartment_MouseDown);  
    compartment.MouseUp += new DiagramMouseEventHandler(compartment_MouseUp);  
    compartment.MouseMove += new DiagramMouseEventHandler(compartment_MouseMove);  
   }  
  }  
  
  /// <summary>  
  /// Remember which item the mouse was dragged from.  
  /// We don't create an Action immediately, as this would inhibit the  
  /// inline text editing feature. Instead, we just remember the details  
  /// and will create an Action when/if the mouse moves off this list item.  
  /// </summary>  
  /// <param name="sender"></param>  
  /// <param name="e"></param>  
  void compartment_MouseDown(object sender, DiagramMouseEventArgs e)  
  {  
   dragStartElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();  
   compartmentBounds = e.HitDiagramItem.Shape.AbsoluteBoundingBox;  
  }  
  
  /// <summary>  
  /// When the mouse moves away from the initial list item, but still inside the compartment,  
  /// create an Action to supervise the cursor and handle subsequent mouse events.  
  /// Transfer the details of the initial mouse position to the Action.  
  /// </summary>  
  /// <param name="sender"></param>  
  /// <param name="e"></param>  
  void compartment_MouseMove(object sender, DiagramMouseEventArgs e)  
  {  
   if (dragStartElement != null)  
   {  
    if (dragStartElement != e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault())  
    {  
     e.DiagramClientView.ActiveMouseAction = new CompartmentDragMouseAction(dragStartElement, this, compartmentBounds);  
     dragStartElement = null;  
    }  
   }  
  }  
  
  /// <summary>  
  /// User has released the mouse button.   
  /// </summary>  
  /// <param name="sender"></param>  
  /// <param name="e"></param>  
  void compartment_MouseUp(object sender, DiagramMouseEventArgs e)  
  {  
    dragStartElement = null;  
  }  
  
  /// <summary>  
  /// Forget the source item if mouse up occurs outside the  
  /// compartment.  
  /// </summary>  
  /// <param name="e"></param>  
  public override void OnMouseUp(DiagramMouseEventArgs e)  
  {  
   base.OnMouseUp(e);  
   dragStartElement = null;  
  }  
  
  /// <summary>  
  /// Called by the Action when the user releases the mouse.  
  /// If we are still on the same compartment but in a different list item,  
  /// move the starting item to the position of the current one.  
  /// </summary>  
  /// <param name="dragFrom"></param>  
  /// <param name="e"></param>  
  public void DoMouseUp(ModelElement dragFrom, DiagramMouseEventArgs e)  
  {  
   // Original or "from" item:  
   ClassModelElement dragFromElement = dragFrom as ClassModelElement;  
   // Current or "to" item:  
   ClassModelElement dragToElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();  
   if (dragFromElement != null && dragToElement != null)  
   {  
    // Find the common parent model element, and the relationship links:  
    ElementLink parentToLink = GetEmbeddingLink(dragToElement);  
    ElementLink parentFromLink = GetEmbeddingLink(dragFromElement);  
    if (parentToLink != parentFromLink && parentFromLink != null && parentToLink != null)  
    {  
     // Get the static relationship and role (= end of relationship):  
     DomainRelationshipInfo relationshipFrom = parentFromLink.GetDomainRelationship();  
     DomainRoleInfo parentFromRole = relationshipFrom.DomainRoles[0];  
     // Get the node in which the element is embedded, usually the element displayed in the shape:  
     ModelElement parentFrom = parentFromLink.LinkedElements[0];  
  
     // Same again for the target:  
     DomainRelationshipInfo relationshipTo = parentToLink.GetDomainRelationship();  
     DomainRoleInfo parentToRole = relationshipTo.DomainRoles[0];  
     ModelElement parentTo = parentToLink.LinkedElements[0];  
  
     // Mouse went down and up in same parent and same compartment:  
     if (parentTo == parentFrom && relationshipTo == relationshipFrom)  
     {  
      // Find index of target position:  
      int newIndex = 0;  
      var elementLinks = parentToRole.GetElementLinks(parentTo);  
      foreach (ElementLink link in elementLinks)  
      {  
       if (link == parentToLink) { break; }  
       newIndex++;  
      }  
  
      if (newIndex < elementLinks.Count)  
      {  
       using (Transaction t = parentFrom.Store.TransactionManager.BeginTransaction("Move list item"))  
       {  
        parentFromLink.MoveToIndex(parentFromRole, newIndex);  
        t.Commit();  
       }  
      }  
     }  
    }  
   }  
  }  
  
  /// <summary>  
  /// Get the embedding link to this element.  
  /// Assumes there is no inheritance between embedding relationships.  
  /// (If there is, you need to make sure you've got the relationship  
  /// that is represented in the shape compartment.)  
  /// </summary>  
  /// <param name="child"></param>  
  /// <returns></returns>  
  ElementLink GetEmbeddingLink(ClassModelElement child)  
  {  
   foreach (DomainRoleInfo role in child.GetDomainClass().AllEmbeddedByDomainRoles)  
   {  
    foreach (ElementLink link in role.OppositeDomainRole.GetElementLinks(child))  
    {  
     // Just the assume the first embedding link is the only one.  
     // Not a valid assumption if one relationship is derived from another.  
     return link;  
    }  
   }  
   return null;  
  }  
 }  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)   
 [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md)



