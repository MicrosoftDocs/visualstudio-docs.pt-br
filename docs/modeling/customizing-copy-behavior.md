---
title: Personalizando o comportamento da operação de copiar
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b189d3dbd5c1872094b0c1be2a64eb2c02bf1e2e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547336"
---
# <a name="customizing-copy-behavior"></a>Personalizando o comportamento da operação de copiar
Em uma DSL (linguagem específica de domínio) criada com o SDK de visualização e modelagem do Visual Studio, você pode alterar o que acontece quando o usuário copia e cola elementos.

## <a name="standard-copy-and-paste-behavior"></a>Comportamento copiar e colar padrão
 Para habilitar a cópia, defina a propriedade **habilitar copiar colar** do nó do **Editor** no Gerenciador de DSL.

 Por padrão, quando o usuário copia elementos para a área de transferência, os seguintes elementos também são copiados:

- Descendentes incorporados dos elementos selecionados. (Ou seja, elementos que são destinos de incorporação de relações que têm origem em elementos copiados.)

- Links de relações entre os elementos copiados.

  Esta regra aplica-se recursivamente aos elementos e links copiados.

  ![Elementos copiados e colados](../modeling/media/dslcopypastedefault.png)

  Os elementos e links copiados são serializados e armazenados em um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> (EGP), que é colocado na área de transferência.

  Uma imagem dos elementos copiados também é colocada na área de transferência. Isso permite que o usuário cole-os em outros aplicativos, como o Word.

  O usuário pode colar os elementos copiados em um destino que pode aceitar os elementos de acordo com a definição de DSL. Por exemplo, em uma DSL gerada a partir do modelo de solução de componentes, o usuário pode colar portas em componentes, mas não no diagrama, também pode colar componentes no diagrama, mas não em outros componentes.

## <a name="customizing-copy-and-paste-behavior"></a>Personalizando o comportamento copiar e colar
 Para obter mais informações sobre como personalizar o modelo usando o código do programa, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

 **{1&amp;gt;Habilite ou desabilite os recursos copiar, recortar e colar.&amp;lt;1}**
No Gerenciador de DSL, defina a propriedade **habilitar copiar colar** do nó do **Editor** .

 **Copie links para o mesmo destino.**  Por exemplo, para copiar uma caixa de comentários vinculada ao mesmo elemento de assunto.
Defina a propriedade de **cópia propagada** da função para **propagar a cópia somente para vincular**. Para obter mais informações, consulte [Personalizando o comportamento de cópia de link](#customizeLinks).

 Copie os elementos vinculados. Por exemplo, quando você copia um novo elemento, cópias de todas as caixas de comentários vinculadas também são feitas.
Defina a propriedade de **cópia propagada** da função para **propagar a cópia para o link e**o representante da função oposto. Para obter mais informações, consulte [Personalizando o comportamento de cópia de link](#customizeLinks).

 **Duplique com rapidez os elementos copiando e colando.**  Normalmente, o item que você acabou de copiar ainda fica selecionado e você não pode colar o mesmo tipo de elemento nele.
Adicione uma Diretiva Element Merge à classe de domínio e configure-a para encaminhar mesclagens para a classe pai. Isso terá o mesmo efeito sobre as operações de arrastar. Para obter mais informações, consulte [Personalizando a criação e movimentação do elemento](../modeling/customizing-element-creation-and-movement.md).

 \- ou –

 Selecione o diagrama antes de colar os elementos, substituindo `ClipboardCommandSet.ProcessOnPasteCommand()`. Adicione este código em um arquivo personalizado no projeto DslPackage:

```csharp
namespace Company.MyDsl {
using System.Linq;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Shell;
partial class MyDslClipboardCommandSet
{
  protected override void ProcessOnMenuPasteCommand()
  {
 // Deselect the current selection after copying:
 Diagram diagram = (this.CurrentModelingDocView as SingleDiagramDocView).Diagram;
    this.CurrentModelingDocView
     .SelectObjects(1, new object[] { diagram }, 0);
  }
} }
```

 **Crie links adicionais quando o usuário colar em um destino selecionado.**  Por exemplo, quando uma caixa de comentários é colada em um elemento, um link é estabelecido entre eles.
Adicione uma Diretiva Element Merge à classe de domínio de destino e configure-a para processar a mesclagem, adicionando links. Isso terá o mesmo efeito sobre as operações de arrastar. Para obter mais informações, consulte [Personalizando a criação e movimentação do elemento](../modeling/customizing-element-creation-and-movement.md).

 \- ou –

 Substitua `ClipboardCommandSet.ProcessOnPasteCommand()` para criar os links adicionais depois de chamar o método base.

 **Personalize os formatos nos quais os elementos podem ser copiados** para aplicativos externos, por exemplo, para adicionar uma borda ao formulário de bitmap.
Substitua *MyDsl* `ClipboardCommandSet.ProcessOnMenuCopyCommand()` no projeto DslPackage.

 **Personalize como os elementos são copiados para a área de transferência pelo comando copiar, mas não em uma operação de arrastar.**
Substitua *MyDsl* `ClipboardCommandSet.CopyModelElementsIntoElementGroupPrototype()` no projeto DslPackage.

 **Preserve o layout da forma com os comandos copiar e colar.**
Quando os usuários copiam várias formas, você pode preservar as posições relativas delas quando são coladas. Essa técnica é demonstrada pelo exemplo em [VMSDK: exemplo de diagramas de circuito](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8).

 Para conseguir esse efeito, adicione as formas e conectores ao ElementGroupPrototype copiado. O método mais conveniente para substituir é o ElementOperations.CreateElementGroupPrototype(). Para fazer isso, adicione o seguinte código ao projeto Dsl:

```csharp

public class MyElementOperations : DesignSurfaceElementOperations
{
  // Create an EGP to add to the clipboard.
  // Called when the elements to be copied have been
  // collected into an ElementGroup.
 protected override ElementGroupPrototype CreateElementGroupPrototype(ElementGroup elementGroup, ICollection<ModelElement> elements, ClosureType closureType)
  {
 // Add the shapes and connectors:
 // Get the elements already in the group:
    ModelElement[] mels = elementGroup.ModelElements
        .Concat(elementGroup.ElementLinks) // Omit if the paste target is not the diagram.
        .ToArray();
 // Get their shapes:
    IEnumerable<PresentationElement> shapes =
       mels.SelectMany(mel =>
            PresentationViewsSubject.GetPresentation(mel));
    elementGroup.AddRange(shapes);

 return base.CreateElementGroupPrototype
           (elementGroup, elements, closureType);
  }

 public MyElementOperations(IServiceProvider serviceProvider, ElementOps1Diagram diagram)
      : base(serviceProvider, diagram)
  { }
}

// Replace the standard ElementOperations
// singleton with your own:
partial class MyDslDiagram // EDIT NAME
{
 /// <summary>
 /// Singleton ElementOperations attached to this diagram.
 /// </summary>
 public override DesignSurfaceElementOperations ElementOperations
  {
 get
    {
 if (singleton == null)
      {
        singleton = new MyElementOperations(this.Store as IServiceProvider, this);
      }
 return singleton;
    }
  }
 private MyElementOperations singleton = null;
}
```

 **Cole formas em um local escolhido, como a posição atual do cursor.**
Quando os usuários copiam várias formas, você pode preservar as posições relativas delas quando são coladas. Essa técnica é demonstrada pelo exemplo em [VMSDK: exemplo de diagramas de circuito](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8).

 Para conseguir esse efeito, substitua `ClipboardCommandSet.ProcessOnMenuPasteCommand()` para usar a versão específica do local do `ElementOperations.Merge()`. Para fazer isso, adicione o seguinte código ao projeto DslPackage:

```csharp

partial class MyDslClipboardCommandSet // EDIT NAME
{
   /// <summary>
    /// This method assumes we only want to paste things onto the diagram
    /// - not onto anything contained in the diagram.
    /// The base method pastes in a free space on the diagram.
    /// But if the menu was used to invoke paste, we want to paste in the cursor position.
    /// </summary>
    protected override void ProcessOnMenuPasteCommand()
    {

  NestedShapesSampleDocView docView = this.CurrentModelingDocView as NestedShapesSampleDocView;

      // Retrieve data from clipboard:
      System.Windows.Forms.IDataObject data = System.Windows.Forms.Clipboard.GetDataObject();

      Diagram diagram = docView.CurrentDiagram;
      if (diagram == null) return;

      if (!docView.IsContextMenuShowing)
      {
        // User hit CTRL+V - just use base method.

        // Deselect anything that's selected, otherwise
        // pasted item will be incompatible:
        if (!this.IsDiagramSelected())
        {
          docView.SelectObjects(1, new object[] { diagram }, 0);
        }

        // Paste into a convenient spare space on diagram:
    base.ProcessOnMenuPasteCommand();
      }
      else
      {
        // User right-clicked - paste at mouse position.

        // Utility class:
        DesignSurfaceElementOperations op = diagram.ElementOperations;

        ShapeElement pasteTarget = diagram;

        // Check whether what's in the paste buffer is acceptable on the target.
        if (pasteTarget != null && op.CanMerge(pasteTarget, data))
        {

        // Although op.Merge would be a no-op if CanMerge failed, we check CanMerge first
          // so that we don't create an empty transaction (after which Undo would be no-op).
          using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("paste"))
          {
            PointD place = docView.ContextMenuMousePosition;
            op.Merge(pasteTarget, data, PointD.ToPointF(place));
            t.Commit();
          }
        }
      }
    }
  }
```

 **Permitir que o usuário arraste e solte elementos.**
Consulte [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).

## <a name="customizing-link-copy-behavior"></a><a name="customizeLinks"></a>Personalizando o comportamento de cópia de link
 Quando o usuário copia um elemento, o comportamento padrão é que todos os elementos incorporados também sejam copiados. Você pode modificar o comportamento de cópia padrão. Na definição de DSL, selecione uma função em um lado de uma relação e, na janela Propriedades defina o valor de **cópia Propagas** .

 ![Propaga a propriedade de cópia da função de domínio](../modeling/media/dslpropagatescopy.png)

 Há três valores:

- Não propagar cópia

- Propagar cópia somente para link - quando o grupo é colado, a nova cópia desse link se referirá ao elemento existente na outra extremidade do link.

- Propagar cópia para link e usuário oposto - o grupo copiado inclui uma cópia do elemento na outra extremidade do link.

  ![Efeito da cópia com PropagateCopyToLinkOnly](../modeling/media/dslpropagatecopy.png)

  As mudanças que você fizer afetarão os elementos e a imagem que é copiada.

## <a name="programming-copy-and-paste-behavior"></a>Comportamento copiar e colar de programação
 Muitos aspectos do comportamento de uma DSL em relação a copiar, colar, criar e excluir objetos são regidos por uma instância do <xref:Microsoft.VisualStudio.Modeling.ElementOperations> que é acoplada ao diagrama. Você pode modificar o comportamento de sua DSL derivando sua própria classe de <xref:Microsoft.VisualStudio.Modeling.ElementOperations> e substituindo a <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.ElementOperations%2A> propriedade de sua classe de diagrama.

> [!TIP]
> Para obter mais informações sobre como personalizar o modelo usando o código do programa, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

 ![Diagrama de sequência para a operação de cópia](../modeling/media/dslcopyseqdiagram.png)

 ![Diagrama de sequência da operação colar](../modeling/media/dslpasteseqdiagram.png)

#### <a name="to-define-your-own-elementoperations"></a>Para definir seus próprios ElementOperations

1. Em um novo arquivo no seu projeto DSL, crie uma classe que derivada de <xref:Microsoft.VisualStudio.Modeling.Diagrams.DesignSurfaceElementOperations>.

2. Adicione uma definição de classe parcial para a sua classe de diagrama. O nome dessa classe pode ser encontrado em **Dsl\GeneratedCode\Diagrams.cs**.

    Na classe de diagrama, substitua <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.ElementOperations%2A> para retornar uma instância de sua subclasse ElementOperations. Você deve retornar a mesma instância em cada chamada.

   Adicione este código em um arquivo personalizado no projeto DslPackage:

```csharp

using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;

  public partial class MyDslDiagram
  {
    public override DesignSurfaceElementOperations ElementOperations
    {
      get
      {
        if (this.elementOperations == null)
        {
          this.elementOperations = new MyElementOperations(this.Store as IServiceProvider, this);
        }
        return this.elementOperations;
      }
    }
    private MyElementOperations elementOperations = null;
  }

  public class MyElementOperations : DesignSurfaceElementOperations
  {
    public MyElementOperations(IServiceProvider serviceProvider, MyDslDiagram diagram)
      : base(serviceProvider, diagram)
    { }
    // Overridden methods follow
  }
```

## <a name="receiving-items-dragged-from-other-models"></a>Recebendo itens arrastados de outros modelos
 O ElementOperations também pode ser usado para definir os comportamentos copiar, mover, apagar e arrastar e soltar. Como uma demonstração do uso do ElementOperations, o exemplo que fornecemos aqui define o comportamento personalizado de arrastar e soltar. No entanto, para essa finalidade, você pode considerar a abordagem alternativa descrita em [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md), que é mais extensível.

 Defina dois métodos em sua classe ElementOperations:

- `CanMerge(ModelElement targetElement, System.Windows.Forms.IDataObject data)`que determina se o elemento de origem pode ser arrastado para a forma de destino, o conector ou o diagrama.

- `MergeElementGroupPrototype(ModelElement targetElement, ElementGroupPrototype sourcePrototype)`que combina o elemento de origem no destino.

### <a name="canmerge"></a>CanMerge()
 `CanMerge()`é chamado para determinar os comentários que devem ser fornecidos ao usuário à medida que o mouse se move pelo diagrama. Os parâmetros para o método são o elemento sobre o qual o mouse está passando, e os dados sobre a origem a partir da qual a operação de arrastar foi realizada. O usuário pode arrastar a partir de qualquer lugar na tela. Portanto, o objeto de origem pode ser de muitos tipos diferentes e pode ser serializado em diferentes formatos. Se a origem for um modelo DSL ou UML, o parâmetro de dados é a serialização de um <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype>. As operações de arrastar, copiar e da caixa de ferramentas usam o ElementGroupPrototypes para representar fragmentos de modelos.

 Um Element Group Prototype pode conter qualquer número de elementos e links. Os tipos de elementos podem ser identificados pelas suas Guids. A GUID é da forma que foi arrastada, e não o elemento do modelo subjacente. No seguinte exemplo, `CanMerge()` retorna true se a forma de uma classe de um diagrama UML for arrastada para esse diagrama.

```csharp
public override bool CanMerge(ModelElement targetShape, System.Windows.Forms.IDataObject data)
 {
  // Extract the element prototype from the data.
  ElementGroupPrototype prototype = ElementOperations.GetElementGroupPrototype(this.ServiceProvider, data);
  if (targetShape is MyTargetShape && prototype != null &&
        prototype.RootProtoElements.Any(rootElement =>
          rootElement.DomainClassId.ToString()
          ==  "3866d10c-cc4e-438b-b46f-bb24380e1678")) // Guid of UML Class shapes
          // or SourceClass.DomainClassId
        return true;
   return base.CanMerge(targetShape, data);
 }
```

## <a name="mergeelementgroupprototype"></a>MergeElementGroupPrototype()
 Esse método é chamado quando o usuário solta um elemento em um diagrama, forma ou conector. Ele deve mesclar o conteúdo arrastado para o elemento de destino. Neste exemplo, o código determina se ele reconhece a combinação de tipos de destino e protótipos; em caso afirmativo, o método converte os elementos arrastados para um protótipo dos elementos que devem ser adicionados ao modelo. O método base é chamado para executar a mesclagem, dos elementos convertidos ou não convertidos.

```csharp
public override void MergeElementGroupPrototype(ModelElement targetShape, ElementGroupPrototype sourcePrototype)
{
  ElementGroupPrototype prototypeToMerge = sourcePrototype;
  MyTargetShape pel = targetShape as MyTargetShape;
  if (pel != null)
  {
    prototypeToMerge = ConvertDraggedTypeToLocal(pel, sourcePrototype);
  }
  if (prototypeToMerge != null)
    base.MergeElementGroupPrototype(targetShape, prototypeToMerge);
}
```

 Este exemplo lida com elementos de classe UML arrastados de um diagrama de classe UML. A DSL não foi criada para armazenar classes UML diretamente, em vez disso, criamos um elemento DSL para cada classe UML arrastada. Isso pode ser útil, por exemplo, se a DSL for um diagrama de instância. O usuário pode arrastar as classes para o diagrama para criar instâncias dessas classes.

```csharp

private ElementGroupPrototype ConvertDraggedTypeToLocal (MyTargetShape snapshot, ElementGroupPrototype prototype)
{
  // Find the UML project:
  EnvDTE.DTE dte = snapshot.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE;
  foreach (EnvDTE.Project project in dte.Solution.Projects)
  {
    IModelingProject modelingProject = project as IModelingProject;
    if (modelingProject == null) continue; // not a modeling project
    IModelStore store = modelingProject.Store;
    if (store == null) continue;
    // Look for the shape that was dragged:
    foreach (IDiagram umlDiagram in store.Diagrams())
    {
      // Get modeling diagram that implements UML diagram:
      Diagram diagram = umlDiagram.GetObject<Diagram>();
      Guid elementId = prototype.SourceRootElementIds.FirstOrDefault();
      ShapeElement shape = diagram.Partition.ElementDirectory.FindElement(elementId) as ShapeElement;
      if (shape == null) continue;
      IClass classElement = shape.ModelElement as IClass;
      if (classElement == null) continue;

      // Create a prototype of elements in my DSL, based on the UML element:
      Instance instance = new Instance(snapshot.Store);
      instance.Type = classElement.Name;
      // Pack them into a prototype:
      ElementGroup group = new ElementGroup(instance);
      return group.CreatePrototype();
    }
  }
  return null;
}
```

## <a name="standard-copy-behavior"></a>Comportamento copiar padrão 
 O código nesta seção mostra métodos que você pode substituir para alterar o comportamento de cópia. Para ajudá-lo a entender como fazer suas próprias personalizações, esta seção mostra o código que substitui os métodos envolvidos na cópia, mas não altera o comportamento padrão.

 Quando o usuário pressiona CTRL+C ou usa o comando Copiar, o método <xref:Microsoft.VisualStudio.Modeling.Shell.ClipboardCommandSet.ProcessOnMenuCopyCommand%2A> é chamado. Você pode ver como isso é configurado em **DslPackage\Generated Code\CommandSet.cs**. Para obter mais informações sobre como os comandos são configurados, consulte [como adicionar um comando ao menu de atalho](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

 Você pode substituir ProcessOnMenuCopyCommand adicionando uma definição de classe parcial de *MyDsl* `ClipboardCommandSet` no projeto DslPackage.

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Windows.Forms;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

partial class MyDslClipboardCommandSet
{
  /// <summary>
  /// Override ProcessOnMenuCopyCommand() to copy elements to the
  /// clipboard in different formats, or to perform additional tasks
  /// before or after copying - for example deselect the copied elements.
  /// </summary>
  protected override void ProcessOnMenuCopyCommand()
  {
    IList<ModelElement> selectedModelElements = this.SelectedElements;
    if (selectedModelElements.Count == 0) return;

    // System container for clipboard data.
    // The IDataObject can contain data in several formats.
    IDataObject dataObject = new DataObject();

    Bitmap bitmap = null; // For export to other programs.
    try
    {
      #region Create EGP for copying to a DSL.
      this.CopyModelElementsIntoElementGroupPrototype
                     (dataObject, selectedModelElements);
      #endregion

      #region Create bitmap for copying to another application.
      // Find all the shapes associated with this selection:
      List<ShapeElement> shapes = new List<ShapeElement>(
        this.ResolveExportedShapesForClipboardImages
              (dataObject, selectedModelElements));

      bitmap = this.CreateBitmapForClipboard(shapes);
      if (bitmap != null)
      {
        dataObject.SetData(DataFormats.Bitmap, bitmap);
      }
      #endregion

      // Add the data to the clipboard:
      Clipboard.SetDataObject(dataObject, true, 5, 100);
    }
    finally
    {
      // Dispose bitmap after SetDataObject:
      if (bitmap != null) bitmap.Dispose();
    }
  }
/// <summary>
/// Override this to customize the element group that is copied to the clipboard.
/// </summary>
protected override void CopyModelElementsIntoElementGroupPrototype(IDataObject dataObject, IList<ModelElement> selectedModelElements)
{
  return this.ElementOperations.Copy(dataObject, selectedModelElements);
}
}
```

 Cada diagrama tem uma instância singleton de ElementOperations. Você pode fornecer seu próprio derivativo. Este arquivo, que pode ser colocado no projeto DSL, iria se comportar da mesma forma que o código que ele substitui:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

namespace Company.MyDsl
{
  partial class MyDslDiagram
  {
    /// <summary>
    /// Singleton ElementOperations attached to this diagram.
    /// </summary>
    public override DesignSurfaceElementOperations ElementOperations
    {
      get
      {
        if (this.elementOperations == null)
        {
          this.elementOperations = new MyElementOperations(this.Store as IServiceProvider, this);
        }
        return this.elementOperations;
      }
    }
    private MyElementOperations elementOperations = null;
  }

  // Our own version of ElementOperations so that we can override:
  public class MyElementOperations : DesignSurfaceElementOperations
  {
    public MyElementOperations(IServiceProvider serviceProvider, ElementOps1Diagram diagram)
      : base(serviceProvider, diagram)
    { }

    /// <summary>
    /// Copy elements to the clipboard data.
    /// Provides a hook for adding custom data.
    /// </summary>
    public override void Copy(System.Windows.Forms.IDataObject data,
      ICollection<ModelElement> elements,
      ClosureType closureType,
      System.Drawing.PointF sourcePosition)
    {
      if (CanAddElementGroupFormat(elements, closureType))
      {
        AddElementGroupFormat(data, elements, closureType);
      }

      // Override these to store additional data:
      if (CanAddCustomFormat(elements, closureType))
      {
        AddCustomFormat(data, elements, closureType, sourcePosition);
      }
    }

    protected override void AddElementGroupFormat(System.Windows.Forms.IDataObject data, ICollection<ModelElement> elements, ClosureType closureType)
    {
      // Add the selected elements and those implied by the propagate copy rules:
      ElementGroup elementGroup = this.CreateElementGroup(elements, closureType);

      // Mark all the elements that are not embedded under other elements:
      this.MarkRootElements(elementGroup, elements, closureType);

      // Store in the clipboard data:
      ElementGroupPrototype elementGroupPrototype = this.CreateElementGroupPrototype(elementGroup, elements, closureType);
      data.SetData(ElementGroupPrototype.DefaultDataFormatName, elementGroupPrototype);
    }

    /// <summary>
    /// Override this to store additional elements in the element group:
    /// </summary>
    protected override ElementGroupPrototype CreateElementGroupPrototype(ElementGroup elementGroup, ICollection<ModelElement> elements, ClosureType closureType)
    {
      ElementGroupPrototype prototype = new ElementGroupPrototype(this.Partition, elementGroup.RootElements, elementGroup);
      return prototype;
    }

    /// <summary>
    /// Create an element group from the given starting elements, using the
    /// copy propagation rules specified in the DSL Definition.
    /// By default, this includes all the embedded descendants of the starting elements,
    /// and also includes reference links where both ends are already included.
    /// </summary>
    /// <param name="startElements">model elements to copy</param>
    /// <param name="closureType"></param>
    /// <returns></returns>
    protected override ElementGroup CreateElementGroup(ICollection<ModelElement> startElements, ClosureType closureType)
    {
      // ElementClosureWalker finds all the connected elements,
      // according to the propagate copy rules specified in the DSL Definition:
      ElementClosureWalker walker = new ElementClosureWalker(this.Partition,
        closureType, // Normally ClosureType.CopyClosure
        startElements,
        true, // Do not load other models.
        null, // Optional list of domain roles not to traverse.
        true); // Include relationship links where both ends are already included.

      walker.Traverse(startElements);
      IList<ModelElement> closureList = walker.ClosureList;
      Dictionary<object, object> closureContext = walker.Context;

      // create a group for this closure
      ElementGroup group = new ElementGroup(this.Partition);
      group.AddRange(closureList, false);

      // create the element group prototype for the group
      foreach (object key in closureContext.Keys)
      {
        group.SourceContext.ContextInfo[key] = closureContext[key];
      }

      return group;
    }
  }
}
```

## <a name="see-also"></a>Confira também

- [Personalizando a criação e o movimento de elementos](../modeling/customizing-element-creation-and-movement.md)
- [Como adicionar um manipulador de evento do tipo "arrastar e soltar"](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [Exemplo: exemplo de diagramas de circuito VMSDK](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
