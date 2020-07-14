---
title: Adicionar comandos e gestos a diagramas de dependência
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom commands
- dependency diagrams, adding custom gestures
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4ff23e07bd6e81b11d94a8256c33b57b4b0c558c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531385"
---
# <a name="add-commands-and-gestures-to-dependency-diagrams"></a>Adicionar comandos e gestos a diagramas de dependência

Você pode definir comandos de menu de clique com o botão direito do mouse e manipuladores de gestos em diagramas de dependência no Visual Studio. Você pode empacotar essas extensões em uma extensão de integração do Visual Studio (VSIX) que pode ser distribuída para outros usuários do Visual Studio.

Você pode definir vários manipuladores de comando e de gesto no mesmo projeto do Visual Studio, se desejar. Você também pode combinar vários desses projetos em um VSIX. Por exemplo, você pode definir um único VSIX que inclui comandos de camada e uma linguagem específica de domínio.

> [!NOTE]
> Você também pode personalizar a validação de arquitetura, na qual o código-fonte dos usuários é comparado com diagramas de dependência. Você deve definir a validação de arquitetura em um projeto do Visual Studio separado. Você pode adicioná-lo ao mesmo VSIX que outras extensões. Para obter mais informações, consulte [Adicionar validação de arquitetura personalizada a diagramas de dependência](../modeling/add-custom-architecture-validation-to-layer-diagrams.md).

## <a name="requirements"></a>Requisitos

Consulte [requisitos](../modeling/extend-layer-diagrams.md#requirements).

## <a name="define-a-command-or-gesture-in-a-new-vsix"></a>Definir um comando ou gesto em um novo VSIX

O método mais rápido de criar uma extensão é usar o modelo de projeto. Isso coloca o código e o manifesto do VSIX no mesmo projeto.

1. Crie uma nova **extensão de comando de designer de camada** ou projeto de **extensão de gesto de designer de camada** .

   O modelo cria um projeto que contém um pequeno exemplo de trabalho.

2. Para testar a extensão, pressione **Ctrl** + **F5** ou **F5**.

    Uma instância experimental do Visual Studio é iniciada. Nesta instância, crie um diagrama de dependência. O comando ou a extensão do gesto deve funcionar neste diagrama.

3. Feche a instância experimental e modifique o código de exemplo.

4. Você pode adicionar mais manipuladores de comando ou de gesto ao mesmo projeto. Saiba mais em uma das seções a seguir:

    [Definindo um comando de menu](#command)

    [Definindo um manipulador de gestos](#gesture)

::: moniker range="vs-2017"

5. Para instalar a extensão na instância principal do Visual Studio ou em outro computador, localize o arquivo *. vsix* no diretório *bin* . Copie-o para o computador em que você deseja instalá-lo e clique duas vezes nele. Para desinstalá-lo, escolha **extensões e atualizações** no menu **ferramentas** .

::: moniker-end

::: moniker range=">=vs-2019"

5. Para instalar a extensão na instância principal do Visual Studio ou em outro computador, localize o arquivo *. vsix* no diretório *bin* . Copie-o para o computador em que você deseja instalá-lo e clique duas vezes nele. Para desinstalá-lo, escolha **gerenciar extensões** no menu **extensões** .

::: moniker-end

## <a name="add-a-command-or-gesture-to-a-separate-vsix"></a>Adicionar um comando ou gesto para um VSIX separado

Se você quiser criar um VSIX que contém comandos, validadores de camada e outras extensões, recomendamos que você crie um projeto para definir o VSIX e separe projetos para os manipuladores.

1. Crie um projeto de **Biblioteca de Classes**. Este projeto conterá classes de manipulador de comando ou de gesto.

   > [!NOTE]
   > Você pode definir mais de uma classe de manipulador de comando ou de gesto em uma biblioteca de classes, mas deve definir classes de validação de camada em uma biblioteca de classes separada.

2. Adicione ou crie um projeto VSIX em sua solução. Um projeto VSIX contém um arquivo chamado **Source. Extension. vsixmanifest**.

3. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto VSIX e escolha **definir como projeto de inicialização**.

4. Em **Source. Extension. vsixmanifest**, em **ativos**, adicione o comando ou o projeto de manipulador de gestos como um componente MEF.

    1. Na guia **ativos**., escolha **novo**.

    2. Em **tipo**, selecione **Microsoft. VisualStudio. MefComponent**.

    3. Na **origem**, selecione **projeto na solução atual** e selecione o nome do seu projeto de manipulador de comando ou de gesto.

    4. Salve o arquivo.

5. Retorne ao projeto de manipulador de comando ou gesto e adicione as seguintes referências de projeto:

   |**Referência**|**O que isso permite que você faça**|
   |-|-|
   |Arquivos de Programas\microsoft Visual Studio [versão] \Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|Criar e editar camadas|
   |Microsoft. VisualStudio. Uml. interfaces|Criar e editar camadas|
   |Microsoft. VisualStudio. ArchitectureTools. Extensibility|Modificar formas em diagramas|
   |System. ComponentModel. composição|Definir componentes usando Managed Extensibility Framework (MEF)|
   |Microsoft. VisualStudio. Modeling. Sdk. versão|Definir extensões de modelagem|
   |Microsoft. VisualStudio. Modeling. Sdk. Diagrams. versão|Atualizar formas e diagramas|

6. Edite o arquivo de classe no projeto de biblioteca de classes C# para conter o código para sua extensão. Saiba mais em uma das seções a seguir:

     [Definindo um comando de menu](#command)

     [Definindo um manipulador de gestos](#gesture)

7. Para testar o recurso, pressione **Ctrl** + **F5** ou **F5**.

   Uma instância experimental do Visual Studio é aberta. Nesta instância, crie ou abra um diagrama de dependência.

8. Para instalar o VSIX na instância principal do Visual Studio ou em outro computador, localize o arquivo **. vsix** no diretório **bin** do projeto VSIX. Copie-o para o computador em que você deseja instalar o VSIX. Clique duas vezes no arquivo VSIX no explorador de arquivos.

## <a name="defining-a-menu-command"></a><a name="command"></a>Definindo um comando de menu

Você pode adicionar mais definições de comando de menu a um gesto ou projeto de comando existente. Cada comando é definido por uma classe que tem as seguintes características:

- A classe é declarada da seguinte maneira:

   `[LayerDesignerExtension]`

   `[Export(typeof(ICommandExtension))]`

   `public class`  *MyLayerCommand*  `: ICommandExtension { ... }`

- O namespace e o nome da classe não são importantes.

- Os métodos que implementam `ICommandExtension` são os seguintes:

  - `string Text {get;}`-O rótulo que aparece no menu.

  - `void QueryStatus(IMenuCommand command)`-chamado quando o usuário clica com o botão direito do mouse no diagrama e determina se o comando deve ser visível e habilitado para a seleção atual do usuário.

  - `void Execute(IMenuCommand command)`-chamado quando o usuário seleciona o comando.

- Para determinar a seleção atual, você pode importar `IDiagramContext` :

   `[Import]`

   `public IDiagramContext DiagramContext { get; set; }`

   `...`

   `DiagramContext.CurrentDiagram.SelectedShapes.Count()...`

Para adicionar um novo comando, crie um novo arquivo de código que contenha o exemplo a seguir. Em seguida, teste e edite-o.

```csharp
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtension // Change to your preference.
{
  // This is a feature for dependency diagrams:
  [LayerDesignerExtension]
  // This feature is a menu command:
  [Export(typeof(ICommandExtension))]
  // Change the class name to your preference:
  public class MyLayerCommand : ICommandExtension
  {
    [Import]
    public IDiagramContext DiagramContext { get; set; }

    [Import]
    public ILinkedUndoContext LinkedUndoContext { get; set; }

    // Menu command label:
    public string Text
    {
      get { return "Duplicate layers"; }
    }

    // Called when the user right-clicks the diagram.
    // Defines whether the command is visible and enabled.
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible =
      command.Enabled = DiagramContext.CurrentDiagram
        .SelectedShapes.Count() > 0;
    }

    // Called when the user selects the command.
    public void Execute(IMenuCommand command)
    {
      // A selection of starting points:
      IDiagram diagram = this.DiagramContext.CurrentDiagram;
      ILayerModel lmodel = diagram.GetLayerModel();
      foreach (ILayer layer in lmodel.Layers)
      { // All layers in model.
      }
      // Updates should be performed in a transaction:
      using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("copy selection"))
      {
        foreach (ILayer layer in
          diagram.SelectedShapes
            .Select(shape=>shape.GetLayerElement())
            .Where(element => element is ILayer))
        {
          ILayer copy = lmodel.CreateLayer(layer.Name + "+");
          // Position the shapes:
          IShape originalShape = layer.GetShape();
          copy.GetShape().Move(
            originalShape.XPosition + originalShape.Width * 1.2,
            originalShape.YPosition);
        }
        t.Commit();
      }
    }
  }
}
```

## <a name="defining-a-gesture-handler"></a><a name="gesture"></a>Definindo um manipulador de gestos

Um manipulador de gestos responde quando o usuário arrasta itens para o diagrama de dependência e quando o usuário clica duas vezes em qualquer lugar no diagrama.

Para o projeto VSIX do manipulador de gestos ou comando existente, você pode adicionar um arquivo de código que define um manipulador de gestos:

```csharp
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtensions // change to your preference
{
  [LayerDesignerExtension]
  [Export(typeof(IGestureExtension))]
  public class MyLayerGestureHandler : IGestureExtension
  {
  }
}
```

Observe os seguintes pontos sobre manipuladores de gestos:

- Os membros do `IGestureExtension` são os seguintes:

     **OnDoubleClick** – chamado quando o usuário clica duas vezes em qualquer lugar do diagrama.

     **CanDragDrop** -chamado repetidamente à medida que o usuário move o mouse enquanto arrasta um item para o diagrama. Ele deve funcionar rapidamente.

     **OnDragDrop** – chamado quando o usuário remove um item no diagrama.

- O primeiro argumento para cada método é um `IShape` , a partir do qual você pode obter o elemento de camada. Por exemplo:

    ```csharp
    public void OnDragDrop(IShape target, IDataObject data)
    {
        ILayerElement element = target.GetLayerElement();
        if (element is ILayer)
        {
            // ...
        }
    }
    ```

- Os manipuladores para alguns tipos de itens arrastados já estão definidos. Por exemplo, o usuário pode arrastar itens do Gerenciador de Soluções para um diagrama de dependência. Você não pode definir um manipulador de arrastar para esses tipos de item. Nesses casos, seus `DragDrop` métodos não serão invocados.

## <a name="see-also"></a>Confira também

- [Adicionar validação de arquitetura personalizada a diagramas de dependência](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)
