---
title: Como estender o Designer de Linguagem Específica do Domínio
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 6a2388619dea31696fe4416032cc12cd1fe5b372
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860362"
---
# <a name="how-to-extend-the-domain-specific-language-designer"></a>Como estender o Designer de Linguagem Específica do Domínio

Você pode tornar as extensões para o designer que você pode usar para editar as definições de DSL. Tipos de extensão que você pode fazer incluem a adição de comandos de menu, adicionando manipuladores para arrastar e clique duas vezes em gestos e regras que são disparadas quando determinados tipos de valores ou relacionamentos são alterados. As extensões podem ser empacotadas como o Visual Studio Integration extensão (VSIX) e distribuídas para outros usuários.

Para código de exemplo e obter mais informações sobre esse recurso, consulte o Visual Studio [SDK de visualização e modelagem](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db).

## <a name="set-up-the-solution"></a>Configurar a solução

Configure um projeto que contém o código de sua extensão e um projeto VSIX que exporta o projeto. A solução pode conter outros projetos que são incorporados ao mesmo VSIX.

### <a name="to-create-a-dsl-designer-extension-solution"></a>Para criar uma solução de extensão do Designer de DSL

1.  Crie um novo projeto usando o modelo de projeto de biblioteca de classes. No **novo projeto** caixa de diálogo, clique em **Visual c#** e, na janela do meio, clique em **biblioteca de classes**.

     Esse projeto conterá o código de suas extensões.

2.  Crie um novo projeto usando o modelo de projeto do VSIX. No **novo projeto** diálogo caixa, expanda **Visual c#**, clique em **extensibilidade**e, em seguida, na janela Central selecione **projeto VSIX**.

     Selecione **adicionar a solução**.

     Vsixmanifest é aberto no editor de manifesto do VSIX.

3.  Acima do campo de conteúdo, clique em **adicionar conteúdo**.

4.  No **adicionar conteúdo** caixa de diálogo, defina **selecionar um tipo de conteúdo** para **componente MEF**e defina **projeto** ao seu projeto de biblioteca de classe.

5.  Clique em **selecionar edições** e certifique-se de que **Visual Studio Enterprise** é verificada.

6.  Certifique-se de que o projeto VSIX é o projeto de inicialização da solução.

7.  No projeto de biblioteca de classes, adicione referências aos assemblies a seguir:

     Microsoft.VisualStudio.CoreUtility

     Microsoft.VisualStudio.Modeling.Sdk.11.0

     Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0

     Microsoft.VisualStudio.Modeling.Sdk.DslDefinition.11.0

     Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0

     System.ComponentModel.Composition

     System.Drawing

     System.Drawing.Design

     System.Windows.Forms

## <a name="test-and-deployment"></a>Teste e implantação

Para testar qualquer uma das extensões neste tópico, compile e execute a solução. Uma instância experimental do Visual Studio é aberto. Nesse caso, abra uma solução DSL. Edite o diagrama de DslDefinition. O comportamento de extensão pode ser visto.

Para implantar as extensões do Visual Studio principal e a outros computadores, siga estas etapas:

1.  Localize o arquivo de instalação de VSIX, no seu projeto do VSIX na gaveta\\*\*\\\*.vsix

2.  Copie esse arquivo para o computador de destino e, em seguida, no Windows Explorer (ou Explorador de arquivos), clique duas vezes nele.

     O Gerenciador de extensões do Visual Studio é aberto para confirmar se a extensão foi instalada.

Para desinstalar a extensão, siga estas etapas:

1.  No Visual Studio, sobre o **ferramentas** menu, clique em **Gerenciador de extensões**.

2.  Selecione a extensão e excluí-lo.

## <a name="add-a-shortcut-menu-command"></a>Adicionar um comando de Menu de atalho

Para fazer com que um comando de menu de atalho aparecem na superfície de Designer de DSL ou na janela do Gerenciador de DSL, escreva uma classe que se assemelha a seguir.

A classe deve implementar `ICommandExtension` e deve ter o atributo `DslDefinitionModelCommandExtension`.

```csharp
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.DslDefinition;
using Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.DslDesigner;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace Fabrikam.SimpleDslDesignerExtension
{
  /// <summary>
  /// Command extending the DslDesigner.
  /// </summary>
  [DslDefinitionModelCommandExtension]
  public class MyDslDesignerCommand : ICommandExtension
  {
    /// <summary>
    /// Selection Context for this command
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Is the command visible and active?
    /// This is called when the user right-clicks.
    /// </summary>
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible = true;
      // Is there any selected DomainClasses in the Dsl explorer?
      command.Enabled =
        SelectionContext.AtLeastOneSelected<DomainClass>();

      // Is there any selected ClassShape on the design surface?
      command.Enabled |=
        (SelectionContext.GetCurrentSelection<ClassShape>()
                .Count() > 0);
    }
    /// <summary>
    /// Executes the command
    /// </summary>
    /// <param name="command">Command initiating this action</param>
    public void Execute(IMenuCommand command)
    {
      ...
    }
    /// <summary>
    /// Label for the command
    /// </summary>
    public string Text
    {
      get { return "My Command"; }
    }
  }
}
```

## <a name="handle-mouse-gestures"></a>Lidar com gestos do Mouse

O código é semelhante ao código do comando de menu.

```csharp
[DslDefinitionModelGestureExtension]
 class MouseGesturesExtensions : IGestureExtension
 {
  /// <summary>
  /// Double-clicking on a shape representing a Domain model element displays this model element in a dialog box
  /// </summary>
  /// <param name="targetElement">Shape element on which the user has clicked</param>
  /// <param name="diagramPointEventArgs">event args for this double-click</param>
  public void OnDoubleClick(ShapeElement targetElement,
       DiagramPointEventArgs diagramPointEventArgs)
  {
   ModelElement modelElement = PresentationElementHelper.
        GetDslDefinitionModelElement(targetElement);
   if (modelElement != null)
   {
    MessageBox.Show(string.Format(
      "Double clicked on {0}", modelElement.ToString()),
      "Model element double-clicked");
   }
  }

  /// <summary>
  /// Tells if the DslDesigner can consume the to-be-dropped information
  /// </summary>
  /// <param name="targetMergeElement">Shape on which we try to drop</param>
  /// <param name="diagramDragEventArgs">Drop event</param>
  /// <returns><c>true</c> if we can consume the to be dropped data, and <c>false</c> otherwise</returns>
  public bool CanDragDrop(ShapeElement targetMergeElement,
        DiagramDragEventArgs diagramDragEventArgs)
  {
   if (diagramDragEventArgs.Data.GetDataPresent(DataFormats.FileDrop))
   {
    diagramDragEventArgs.Effect = DragDropEffects.Copy;
    return true;
   }
   return false;
  }

  /// <summary>
  /// Processes the drop by displaying the dropped text
  /// </summary>
  /// <param name="targetMergeElement">Shape on which we dropped</param>
  /// <param name="diagramDragEventArgs">Drop event</param>
  public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
  {
   if (diagramDragEventArgs.Data.GetDataPresent(DataFormats.FileDrop))
   {
    string[] droppedFiles =
      diagramDragEventArgs.Data.
               GetData(DataFormats.FileDrop) as string[];
    MessageBox.Show(string.Format("Dropped text {0}",
        string.Join("\r\n", droppedFiles)), "Dropped Text");
   }
  }
 }
```

## <a name="respond-to-value-changes"></a>Responder a alterações de valor

Esse manipulador precisa de um modelo de domínio para funcionar corretamente. Nós fornecemos um modelo de domínio simples.

```csharp
using System.Diagnostics;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.DslDefinition;
namespace Fabrikam.SimpleDslDesignerExtension
{
  /// <summary>
  /// Rule firing when the type of a domain model property is changed. The change is displayed
  /// in the debugger (Output window of the Visual Studio instance debugging this extension)
  /// </summary>
  [RuleOn(typeof(PropertyHasType))]
  public class DomainPropertyTypeChangedRule : RolePlayerChangeRule
  {
    /// <summary>
    /// Method called when the Type of a Domain Property
    /// is changed by the user in a DslDefinition
    /// </summary>
    /// <param name="e"></param>
    public override void RolePlayerChanged(RolePlayerChangedEventArgs e)
    {
      // We are only interested in the type
      if (e.DomainRole.Id == PropertyHasType.TypeDomainRoleId)
      {
        PropertyHasType relationship =
           e.ElementLink as PropertyHasType;
        DomainType newType = e.NewRolePlayer as DomainType;
        DomainType oldType = e.OldRolePlayer as DomainType;
        DomainProperty property = relationship.Property;

         // We write about the Type change in the debugguer
        Debug.WriteLine(string.Format("The type of the Domain property '{0}' of domain class '{1}' changed from '{2}' to '{3}'",
          property.Name,
          property.Class.Name,
          oldType.GetFullName(false),
          newType.GetFullName(false))
} }  }  );
```

O código a seguir implementa um modelo simples. Crie um novo GUID para substituir o espaço reservado.

```csharp
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.DslDefinition;
namespace Fabrikam.SimpleDslDesignerExtension
{
    /// <summary>
    /// Simplest possible domain model
    /// needed only for extension rules.
    /// </summary>
    [DomainObjectId(SimpleDomainModelExtension.DomainModelId)]
    public class SimpleDomainModelExtension : DomainModel
    {
        // Id of this domain model extension
        // Please replace this with a new GUID:
        public const string DomainModelId =
                  "00000000-0000-0000-0000-000000000000";

        /// <summary>
        /// Constructor for the domain model extension
        /// </summary>
        /// <param name="store">Store in which the domain model will be loaded</param>
        public SimpleDomainModelExtension(Store store)
            : base(store, new Guid(SimpleDomainModelExtension.DomainModelId))
        {

        }

        /// <summary>
        /// Rules brought by this domain model extension
        /// </summary>
        /// <returns></returns>
        protected override System.Type[] GetCustomDomainModelTypes()
        {
            return new Type[] {
                     typeof(DomainPropertyTypeChangedRule)
                              };
        }
    }

    /// <summary>
    /// Provider for the DomainModelExtension
    /// </summary>
    [Export(typeof(DomainModelExtensionProvider))]    [ProvidesExtensionToDomainModel(typeof(DslDefinitionModelDomainModel))]
    public class SimpleDomainModelExtensionProvider
          : DomainModelExtensionProvider
    {
        /// <summary>
        /// Extension model type
        /// </summary>
        public override Type DomainModelType
        {
            get
            {
                return typeof(SimpleDomainModelExtension);
            }
        }

    }
}
```