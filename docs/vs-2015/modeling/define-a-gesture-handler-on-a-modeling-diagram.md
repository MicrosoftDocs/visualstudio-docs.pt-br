---
title: Definir um manipulador de gestos em um diagrama de modelagem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, double-click
- UML - extending, drag and drop
ms.assetid: e5e1d70a-3539-4321-a3b1-89e86e4d6430
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: af4123b24ab9286e306a1034de4416a31ae76f2b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533062"
---
# <a name="define-a-gesture-handler-on-a-modeling-diagram"></a>Definir um manipulador de gestos em um diagrama de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir comandos que são executados quando o usuário clica duas vezes ou arrasta itens para um diagrama UML. Você pode empacotar essas extensões em uma extensão de integração do Visual Studio ([VSIX](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)) e distribuí-las a outros usuários do Visual Studio.

 Se já houver um comportamento interno para o tipo de diagrama e o tipo de elemento que você deseja arrastar, talvez você não consiga adicionar ou substituir esse comportamento.

## <a name="requirements"></a>Requisitos
 Consulte [requisitos](../modeling/extend-uml-models-and-diagrams.md#Requirements).

 Para ver quais versões do Visual Studio oferecem suporte a esse recurso, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="creating-a-gesture-handler"></a>Criando um manipulador de gestos
 Para definir um manipulador de gestos para um designer UML, você deve criar uma classe que define o comportamento do manipulador de gestos e inserir essa classe em uma extensão de integração do Visual Studio (VSIX). O VSIX atua como um contêiner que pode instalar o manipulador. Há dois métodos alternativos para definir um manipulador de gestos:

- **Crie um manipulador de gestos em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Use-o se você não quiser combinar seu manipulador com outros tipos de extensão, como extensões de validação, itens de caixa de ferramentas personalizados ou comandos de menu.

- **Crie um manipulador de gestos e projetos VSIX separados.** Use esse método se desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se o manipulador de gestos espera que o modelo Observe restrições específicas, você pode inseri-lo no mesmo VSIX como um método de validação.

#### <a name="to-create-a-gesture-handler-in-its-own-vsix"></a>Para criar um manipulador de gestos em seu próprio VSIX

1. Na caixa de diálogo **novo projeto** , em **modelagem de projetos**, selecione **extensão do gesto**.

2. Abra o arquivo **. cs** no novo projeto e modifique a `GestureExtension` classe para implementar o manipulador de gestos.

    Para obter mais informações, consulte [implementando o manipulador de gestos](#Implementing).

3. Teste o manipulador de gestos pressionando F5. Para obter mais informações, consulte [executando o manipulador de gestos](#Executing).

4. Instale o manipulador de gestos em outro computador copiando o arquivo **bin \\ \* \\ \* . vsix** criado pelo seu projeto. Para obter mais informações, consulte [Instalando e desinstalando uma extensão](#Installing).

   Este é o procedimento alternativo:

#### <a name="to-create-a-separate-class-library-dll-project-for-the-gesture-handler"></a>Para criar um projeto de biblioteca de classes (DLL) separado para o manipulador de gestos

1. Crie um projeto de biblioteca de classes, seja em uma nova [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução ou em uma solução existente.

   1. No menu **Arquivo**, escolha **Novo**, **Projeto**.

   2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**e, em seguida, na coluna do meio, escolha **biblioteca de classes**.

2. Adicione as referências a seguir ao seu projeto.

    `Microsoft.VisualStudio.Modeling.Sdk.[version]`

    `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]`

    `Microsoft.VisualStudio.ArchitectureTools.Extensibility`

    `Microsoft.VisualStudio.Uml.Interfaces`

    `System.ComponentModel.Composition`

    `System.Windows.Forms`

    `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer`– Você só precisará disso se estiver estendendo diagramas de camada. Para obter mais informações, consulte [estender diagramas de camada](../modeling/extend-layer-diagrams.md).

3. Adicione um arquivo de classe ao projeto e defina seu conteúdo para o código a seguir.

   > [!NOTE]
   > Altere o namespace e o nome da classe de acordo com sua preferência.

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

    Para obter mais informações sobre o que colocar nos métodos, consulte [implementando o manipulador de gestos](#Implementing).

   Você deve adicionar o comando de menu a um projeto VSIX, que atua como um contêiner para instalar o comando. Se desejar, você pode incluir outros componentes no mesmo VSIX.

#### <a name="to-add-a-separate-gesture-handler-to-a-vsix-project"></a>Para adicionar um manipulador de gestos separado a um projeto VSIX

1. Você não precisará desse procedimento se tiver criado o manipulador de gestos com seu próprio VSIX.

2. Crie um projeto VSIX, a menos que sua solução já tenha um.

    1. No **Gerenciador de soluções**, no menu de atalho da solução, escolha **Adicionar**, **novo projeto**.

    2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**e, em seguida, selecione **extensibilidade**. Na coluna do meio, escolha **projeto VSIX**.

3. Defina o projeto VSIX como o projeto de inicialização da solução.

    - No Gerenciador de Soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.

4. Na **origem. Extension. vsixmanifest**, adicione o projeto de biblioteca de classes do manipulador de gestos como um componente do MEF:

    1. Na guia **metadados** , defina um nome para o VSIX.

    2. Na guia **instalar destinos** , defina as versões do Visual Studio como os destinos.

    3. Na guia **ativos** , escolha um **novo**e, na caixa de diálogo, defina:

         **Tipo**  =  de **Componente MEF**

         **Origem**  =  do **Um projeto na solução atual**

         **Projeto**  =  do *Seu projeto de biblioteca de classes*

## <a name="executing-the-gesture-handler"></a><a name="Executing"></a>Executando o manipulador de gestos
 Para fins de teste, execute o manipulador de gestos no modo de depuração.

#### <a name="to-test-the-gesture-handler"></a>Para testar o manipulador de gestos

1. Pressione **F5**ou, no menu **depurar** , clique em **Iniciar Depuração**.

    Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciada.

    **Solução de problemas**: se um novo não [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Iniciar:

   - Se você tiver mais de um projeto, verifique se o projeto VSIX está definido como o projeto de inicialização da solução.

   - No Gerenciador de Soluções, no menu de atalho do projeto de inicialização ou somente, escolha Propriedades. No editor de propriedades do projeto, escolha a guia **depurar** . Verifique se a cadeia de caracteres no campo **Iniciar programa externo** é o nome de caminho completo de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , normalmente:

        `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem. Use um diagrama que pertença a um dos tipos listados nos atributos da classe do manipulador de gestos.

3. Clique duas vezes em qualquer lugar do diagrama. O manipulador de clique duplo deve ser chamado.

4. Arraste um elemento do Gerenciador UML para o diagrama. O manipulador de arrastar deve ser chamado.

   **Solução de problemas**: se o manipulador de gestos não funcionar, verifique se:

- O projeto do manipulador de gestos é listado como um componente do MEF na guia **ativos** em **Source. Extensions. manifest** no projeto VSIX.

- Os parâmetros de todos os `Import` `Export` atributos e são válidos.

- O `CanDragDrop` método não está retornando `false` .

- O tipo de diagrama de modelo que você está usando (classe UML, sequência etc.) está listado como um dos atributos de classe do manipulador de gestos [ClassDesignerExtension], [SequenceDesignerExtension] e assim por diante.

- Não há nenhuma funcionalidade interna já definida para esse tipo de destino e elemento Descartado.

## <a name="implementing-the-gesture-handler"></a><a name="Implementing"></a>Implementando o manipulador de gestos

### <a name="the-gesture-handler-methods"></a>Os métodos do manipulador de gestos
 A classe do manipulador de gestos implementa e exporta <xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement.IGestureExtension> . Os métodos que você precisa definir são os seguintes:

|Assinatura|Descrição|
|-|-|
|`bool CanDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|Retorne `true` para permitir que o elemento de origem referenciado no `dragEvent` seja Descartado neste destino.<br /><br /> Esse método não deve fazer alterações no modelo. Ele deve funcionar rapidamente, pois é usado para determinar o estado da seta à medida que o usuário move o mouse.|
|`void OnDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|Atualize o modelo com base no objeto de origem referenciado em `dragEvent` e no destino.<br /><br /> Chamado quando o usuário libera o mouse após arrastar.|
|`void OnDoubleClick (ShapeElement target, DiagramPointEventArgs pointEvent)`|`target`é a forma com que o usuário clicou duas vezes.|

 Você pode escrever manipuladores que podem aceitar não apenas UML também uma ampla variedade de outros itens, como arquivos, nós em uma exibição de classe do .NET e assim por diante. O usuário pode arrastar qualquer um desses itens para um diagrama UML, desde que você escreva um `OnDragDrop` método que possa decodificar a forma serializada dos itens. Os métodos de decodificação variam de um tipo de item para outro.

 Os parâmetros desses métodos são:

- `ShapeElement target`. A forma ou o diagrama no qual o usuário arrastou algo.

    `ShapeElement`é uma classe na implementação que se baseia nas ferramentas de modelagem UML. Para reduzir o risco de colocar o modelo UML e os diagramas em um estado inconsistente, recomendamos que você não use os métodos dessa classe diretamente. Em vez disso, empacote o elemento em um `IShape` e, em seguida, use os métodos descritos em [exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md).

  - Para obter um `IShape` :

      ```
      IShape targetIShape = target.CreateIShape(target);
      ```

  - Para obter o elemento de modelo que é direcionado pela operação de arrastar ou clicar duas vezes:

      ```
      IElement target = targetIShape.Element;
      ```

      Você pode convertê-lo em um tipo mais específico de elemento.

  - Para obter o repositório de modelos UML que contém o modelo UML:

      ```
      IModelStore modelStore =
        targetIShape.Element.GetModelStore(); 
      ```

  - Para obter acesso ao host e ao provedor de serviços:

      ```
      target.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE
      ```

- `DiagramDragEventArgs eventArgs`. Esse parâmetro transporta a forma serializada do objeto de origem de uma operação de arrastar:

    ```
    System.Windows.Forms.IDataObject data = eventArgs.Data;
    ```

     Você pode arrastar elementos de vários tipos diferentes para um diagrama, de partes diferentes do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou da área de trabalho do Windows. Diferentes tipos de elemento são codificados de maneiras diferentes no `IDataObject` . Para extrair os elementos dele, consulte a documentação do tipo apropriado de objeto.

     Se o objeto de origem for um elemento UML arrastado do Gerenciador de modelos UML ou de outro diagrama UML, consulte [obter elementos de modelo UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

### <a name="writing-the-code-of-the-methods"></a>Gravando o código dos métodos
 Para obter mais informações sobre como escrever o código para ler e atualizar o modelo, consulte [programação com a API UML](../modeling/programming-with-the-uml-api.md).

 Para obter informações sobre como acessar informações de modelo em uma operação de arrastar, consulte [obter elementos de modelo UML do IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

 Se você estiver lidando com um diagrama de sequência, consulte também [Editar diagramas de sequência UML usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).

 Além dos parâmetros dos métodos, você também pode declarar uma propriedade importada em sua classe que fornece acesso ao diagrama e ao modelo atuais.

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

## <a name="installing-and-uninstalling-an-extension"></a><a name="Installing"></a>Instalando e desinstalando uma extensão
 Você pode instalar uma [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão no seu próprio computador e em outros computadores.

#### <a name="to-install-an-extension"></a>Para instalar uma extensão

1. Em seu computador, localize o arquivo **. vsix** criado por seu projeto VSIX.

    1. No **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **abrir pasta no Windows Explorer**.

    2. Localize o arquivo **bin \\ \* \\ **_seuprojeto_**. vsix**

2. Copie o arquivo **. vsix** para o computador de destino no qual você deseja instalar a extensão. Este pode ser seu próprio computador ou outro.

     O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou na **origem. Extension. vsixmanifest**.

3. No computador de destino, abra o arquivo **. vsix** .

     O **instalador de extensão do Visual Studio** é aberto e instala a extensão.

4. Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] .

#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão

1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.

2. Expanda **extensões instaladas**.

3. Selecione a extensão e escolha **desinstalar**.

   Raramente, uma extensão defeituosa não carrega e cria um relatório na janela de erro, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:

   *% LocalAppData%* **\Local\Microsoft\VisualStudio \\ [versão] \Extensions**

## <a name="example"></a><a name="DragExample"></a>Exemplo
 O exemplo a seguir mostra como criar linhas de vida em um diagrama de sequência, com base nas partes e portas de um componente, arrastados de um diagrama de componente.

 Para testá-lo, pressione F5. Uma instância experimental do Visual Studio é aberta. Nessa instância, abra um modelo UML e crie um componente em um diagrama de componente. Adicione a esse componente algumas interfaces e partes de componentes internas. Selecione as interfaces e as partes. Em seguida, arraste as interfaces e partes para um diagrama de sequência. (Arraste do diagrama de componente até a guia do diagrama de sequência e, em seguida, para baixo até o diagrama de sequência.) Uma linha de vida será exibida para cada interface e parte.

 Para obter mais informações sobre como associar interações a diagramas de sequência, consulte [Editar diagramas de sequência UML usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).

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

 O código de `GetModelElementsFromDragEvent()` é descrito em [obter elementos de modelo UML de IDataObject](../modeling/get-uml-model-elements-from-idataobject.md).

## <a name="see-also"></a>Consulte Também
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md) [estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md) [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [definir restrições de validação para programação de modelos UML](../modeling/define-validation-constraints-for-uml-models.md) [com a API UML](../modeling/programming-with-the-uml-api.md)
