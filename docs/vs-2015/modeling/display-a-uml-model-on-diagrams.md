---
title: Exibir um modelo UML em diagramas | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: adf1f1f2-2ad9-4ade-82de-c6a5194ab471
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 06a22161068dd7604fe7bb4153e322c0954b89d2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533012"
---
# <a name="display-a-uml-model-on-diagrams"></a>Exibir um modelo UML em diagramas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No código do programa para uma extensão do Visual Studio, você pode controlar como os elementos do modelo são exibidos em diagramas. Para ver quais versões do Visual Studio oferecem suporte a modelos UML, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

Neste tópico:
- [Para exibir um elemento em um diagrama](#Display)

- [Acessando as formas que representam um elemento](#GetShapes)

- [Movendo e redimensionando formas](#Moving)

- [Para remover uma forma de um diagrama](#Removing)

- [Abrindo e Criando diagramas](#Opening)

- [Exemplo: comando para alinhar formas](#AlignCommand)

## <a name="to-display-an-element-on-a-diagram"></a><a name="Display"></a>Para exibir um elemento em um diagrama
 Quando você cria um elemento, como um caso de uso ou uma ação, o usuário pode vê-lo no Gerenciador de modelos UML, mas ele nem sempre aparece automaticamente em um diagrama. Em alguns casos, você deve escrever o código para exibi-lo. A tabela a seguir resume as alternativas.

|Tipo de elemento|Por exemplo,|Para exibir isso, seu código deve|
|---------------------|-----------------|-------------------------------------|
|Classificador|`Class`<br /><br /> `Component`<br /><br /> `Actor`<br /><br /> `Use Case`|Crie formas associadas em diagramas especificados. Você pode criar qualquer número de formas para cada classificador.<br /><br /> `diagram.Display<modelElementType>`<br /><br /> `(modelElement, parentShape,`<br /><br /> `xPosition , yPosition);`<br /><br /> Defina `parentShape` como `null` para uma forma no nível superior do diagrama.<br /><br /> Para exibir uma forma dentro de outra:<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `useCaseDiagram.Display`<br /><br /> `(useCase,`<br /><br /> `subsystemShape,`<br /><br /> `subsystemShape.XPosition + 5,`<br /><br /> `subsystemShape.YPosition + 5);`**Observação:**  Se você executar a exibição dentro de uma transação **ILinkedUndo** , o método às vezes retornará não `IShape` . Mas a forma foi criada corretamente e pode ser acessada usando`IElement.Shapes().`|
|Filho do classificador|Atributo, operação,<br /><br /> Parte, porta|Automático-nenhum código é necessário.<br /><br /> Ele é exibido como parte do pai.|
|Comportamento|Interação (sequência),<br /><br /> Atividade|Associe o comportamento a um diagrama apropriado.<br /><br /> Cada comportamento pode ser associado a no máximo um diagrama por vez.<br /><br /> Por exemplo:<br /><br /> `sequenceDiagram.Bind(interaction);`<br /><br /> `activityDiagram.Bind(activity);`|
|Filho do comportamento|Linhas de vida, mensagens, ações, nós de objeto|Automático-nenhum código é necessário.<br /><br /> Ele será exibido se o pai estiver associado a um diagrama.|
|Relação|Associação, generalização, fluxo, dependência|Automático-nenhum código é necessário.<br /><br /> Ele é exibido em todos os diagramas nos quais ambas as extremidades são exibidas.|

## <a name="accessing-the-shapes-that-represent-an-element"></a><a name="GetShapes"></a>Acessando as formas que representam um elemento
 A forma que representa um elemento pertence aos tipos:

 `IShape`

 `IShape<` *ElementType* `>`

 em que *ElementType* é um tipo de elemento de modelo, como `IClass` ou `IUseCase` .

|Sintaxe|Descrição|
|-|-|
|`anElement.Shapes ()`|Todos os `IShapes` que representam esse elemento em diagramas abertos.|
|`anElement.Shapes(aDiagram)`|Todos os `IShapes` que representam esse elemento em um diagrama específico.|
|`anIShape.GetElement()`|O `IElement` que a forma representa. Normalmente, você o converteria em uma subclasse de ielemento.|
|`anIShape.Diagram`|O `IDiagram` que contém a forma.|
|`anIShape.ParentShape`|A forma que contém `anIShape` . Por exemplo, uma forma de porta está contida em uma forma de componente.|
|`anIShape.ChildShapes`|Formas contidas em um `IShape` ou `IDiagram` .|
|`anIShape.GetChildShapes<IUseCase>()`|As formas contidas em um `IShape` ou `IDiagram` que representam elementos do tipo especificado, como `IUseCase` .|
|`IShape iShape = ...;`<br /><br /> `IShape<IClass> classShape = iShape.ToIShape<IClass>();`<br /><br /> `IClass aClass = classShape.Element;`|Converta um genérico `IShape` em um tipo fortemente tipado `IShape<IElement>` .|
|`IShape<IClassifier> classifierShape;`<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `classifierShape.ToIShape<IUseCase>();`|Converta uma forma de um tipo de forma com parâmetros para outro.|

## <a name="moving-and-resizing-shapes"></a><a name="Moving"></a>Movendo e redimensionando formas

|Sintaxe|Descrição|
|-|-|
|`anIShape.Move(x, y, [width], [height])`|Mova ou redimensione uma forma.|
|`IDiagram.EnsureVisible( IEnumerable<IShape> shapes, bool zoomToFit = false)`|Ative a janela e role o diagrama para que todas as formas determinadas fiquem visíveis. Todas as formas devem estar no diagrama. Se `zoomToFit` for true, o diagrama será dimensionado, se necessário, para que todas as formas fiquem visíveis.|

 Para obter um exemplo, consulte [definindo um comando de alinhamento](#AlignCommand).

## <a name="to-remove-a-shape-from-a-diagram"></a><a name="Removing"></a>Para remover uma forma de um diagrama
 Você pode excluir formas de alguns tipos de elemento sem excluir o elemento.

|Elemento de modelo|Para remover a forma|
|-------------------|-------------------------|
|Um classificador: uma classe, interface, enumeração, ator, caso de uso ou componente|`shape.Delete();`|
|Um comportamento: interação ou atividade|Você pode excluir o diagrama do projeto. Use `IDiagram.FileName` para obter o caminho.<br /><br /> Isso não exclui o comportamento do modelo.|
|Qualquer outra forma|Não é possível excluir explicitamente outras formas de um diagrama. A forma será desapareceda automaticamente se o elemento for excluído do modelo ou se a forma pai for removida do diagrama.|

## <a name="opening-and-creating-diagrams"></a><a name="Opening"></a>Abrindo e Criando diagramas

### <a name="to-access-the-users-current-diagram-from-a-command-or-gesture-extension"></a>Para acessar o diagrama atual do usuário de uma extensão de comando ou gesto
 Declare esta propriedade importada em sua classe:

 `[Import]`

 `IDiagramContext Context { get; set; }`

 Em um método, acesse o diagrama:

 `IClassDiagram classDiagram =`

 `Context.CurrentDiagram as IClassDiagram;`

> [!NOTE]
> Uma instância de `IDiagram` (e seus subtipos, como `IClassDiagram` ) é válida somente dentro do comando que você está processando. Não é recomendável manter um `IDiagram` objeto em uma variável que persiste enquanto o controle é retornado ao usuário.

 Para obter mais informações, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).

### <a name="to-obtain-a-list-of-open-diagrams"></a>Para obter uma lista de diagramas abertos
 Uma lista de diagramas que estão abertos no momento no projeto:

```
Context.CurrentDiagram.ModelStore.Diagrams()
```

## <a name="to-access-the-diagrams-in-a-project"></a>Para acessar os diagramas em um projeto
 A [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API pode ser usada para abrir e criar diagramas e projetos de modelagem.

 Observe a conversão de `EnvDTE.ProjectItem` para `IDiagramContext` .

```

      using EnvDTE; // Visual Studio API
...
[Import]
public IServiceProvider ServiceProvider { get; set; }
...
// Get Visual Studio API
DTE dte = ServiceProvider.GetService(typeof(DTE)) as DTE;
// Get current Visual Studio project
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;
// Open and process every diagram in the project.
foreach (ProjectItem item in project.ProjectItems)
{
  // Cast ProjectItem to IDiagramContext
  IDiagramContext context = item as IDiagramContext;
  if (context == null)
  {
     // This is not a diagram file.
     continue;
  }
  // Open the file and give the window the focus.
  if (!item.IsOpen)
  {
      item.Open().Activate();
  }
  // Get the diagram.
  IDiagram diagram = context.CurrentDiagram;
  // Deal with specific diagram types.
  ISequenceDiagram seqDiagram = diagram as ISequenceDiagram;
  if (seqDiagram != null)
  { ... } } }
```

 Instâncias de `IDiagram` e seus subtipos não são válidos depois que você retorna o controle para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

 Você também pode obter o repositório de modelos de um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto do:

```

      Project project = ...;
IModelStore modelStore = (project as IModelingProject).Store;
```

## <a name="example-command-for-aligning-shapes"></a><a name="AlignCommand"></a>Exemplo: comando para alinhar formas
 O código a seguir implementa um comando de menu que alinha as formas de forma organizada. O usuário deve primeiro posicionar duas ou mais formas no alinhamento aproximado vertical ou horizontalmente. Em seguida, o comando align pode ser usado para alinhar seus centros.

 Para disponibilizar o comando, adicione este código a um projeto de comando de menu e, em seguida, implante a extensão resultante para os usuários. Para obter mais informações, consulte [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace AlignCommand
{
  // Implements a command to align shapes in a UML class diagram.
  // The user first selects shapes that are roughly aligned either vertically or horizontally.
  // This command will straighten them up.

  // Place this file in a menu command extension project.
  // See https://msdn.microsoft.com/library/ee329481.aspx

  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension] // TODO: Add other diagram types if needed
  class CommandExtension : ICommandExtension
  {
    /// <summary>
    /// See https://msdn.microsoft.com/library/ee329481.aspx
    /// </summary>
    [Import]
    IDiagramContext context { get; set; }

    /// <summary>
    /// Transaction context.
    /// See https://msdn.microsoft.com/library/ee330926.aspx
    /// </summary>
    [Import]
    ILinkedUndoContext linkedUndo { get; set; }

    /// <summary>
    /// Called when the user selects the command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      Align(context.CurrentDiagram.SelectedShapes);
    }

    /// <summary>
    /// Called when the user right-clicks on the diagram.
    /// Determines whether the command is enabled.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      IEnumerable<IShape> currentSelection = context.CurrentDiagram.SelectedShapes;
      // Make it visible if there are shapes selected:
      command.Visible = currentSelection.Count() > 0 && !(currentSelection.FirstOrDefault() is IDiagram);

      // Make it enabled if there are two or more shapes that are roughly in line:
      command.Enabled = currentSelection.Count() > 1
        && (HorizontalAlignCenter(currentSelection) > 0.0
        || VerticalAlignCenter(currentSelection) > 0.0);

    }

    /// <summary>
    /// Title of the menu command.
    /// </summary>
    public string Text
    {
      get { return "Align Shapes"; }
    }

    /// <summary>
    /// Find a horizontal line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double HorizontalAlignCenter(IEnumerable<IShape> shapes)
    {
      double Y = -1.0;
      double top = 0.0, bottom = shapes.First().Bottom();
      foreach (IShape shape in shapes)
      {
        top = Math.Max(top, shape.Top());
        bottom = Math.Min(bottom, shape.Bottom());
      }
      if (bottom > top) Y = (bottom + top) / 2.0;
      return Y;
    }

    /// <summary>
    /// Find a vertical line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double VerticalAlignCenter(IEnumerable<IShape> shapes)
    {
      double X = -1.0;
      double left = 0.0, right = shapes.First().Right();
      foreach (IShape shape in shapes)
      {
        left = Math.Max(left, shape.Left());
        right = Math.Min(right, shape.Right());
      }
      if (right > left) X = (right + left) / 2.0;
      return X;
    }

    /// <summary>
    /// Line up those shapes that are roughly aligned.
    /// </summary>
    /// <param name="shapes"></param>
    private void Align(IEnumerable<IShape> shapes)
    {
      if (shapes.Count() > 1)
      {
        // The shapes must all overlap either horizontally or vertically.
        // Find a horizontal line that is covered by all the shapes:
        double Y = HorizontalAlignCenter(shapes);
        if (Y > 0.0) // Negative if they don't overlap.
        {
          // Adjust all the shape positions in one transaction:
          using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
          {
            foreach (IShape shape in shapes)
            {
              shape.AlignYCenter(Y);
            }
            t.Commit();
          }
        }
        else
        {
          // Find a vertical line that is covered by all the shapes:
          double X = VerticalAlignCenter(shapes);
          if (X > 0.0) // Negative if they don't overlap.
          {
            // Adjust all the shape positions in one transaction:
            using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
            {
              foreach (IShape shape in shapes)
              {
                shape.AlignXCenter(X);
              }
              t.Commit();
            }
          }
        }
      }
    }
  }

  /// <summary>
  /// Convenience extensions for IShape.
  /// </summary>
  public static class IShapeExtension
  {
    public static double Bottom(this IShape shape)
    {
      return shape.YPosition + shape.Height;
    }

    public static double Top(this IShape shape)
    {
      return shape.YPosition;
    }

    public static double Left(this IShape shape)
    {
      return shape.XPosition;
    }

    public static double Right(this IShape shape)
    {
      return shape.XPosition + shape.Width;
    }

    public static void AlignYCenter(this IShape shape, double Y)
    {
      shape.Move(shape.XPosition, Y - shape.YCenter());
    }

    public static void AlignXCenter(this IShape shape, double X)
    {
      shape.Move(X - shape.XCenter(), shape.YPosition);
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double YCenter(this IShape shape)
    {
        return shape.Height / 2.0;
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double XCenter(this IShape shape)
    {
        return shape.Width / 2.0;
    }
  }
}

```

## <a name="see-also"></a>Consulte Também
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md) [navegar pelo modelo UML](../modeling/navigate-the-uml-model.md)
 