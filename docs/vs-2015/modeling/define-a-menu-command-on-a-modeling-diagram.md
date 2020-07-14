---
title: Definir um comando de menu em um diagrama de modelagem | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, menu commands
ms.assetid: 79c277de-5871-4fc7-9701-55eec5c3cd46
caps.latest.revision: 63
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b6481a56b4cbc254baaee3ae087201df69c371b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534206"
---
# <a name="define-a-menu-command-on-a-modeling-diagram"></a>Definir um comando de menu em um diagrama de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir itens de menu adicionais nos menus de atalho de um diagrama UML. Você pode controlar se o comando de menu é exibido e está habilitado no menu de atalho de qualquer elemento no diagrama e pode escrever o código que é executado quando o usuário escolhe o item de menu. Você pode empacotar essas extensões em uma extensão de integração do Visual Studio ([VSIX](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)) e distribuí-las a outros usuários do Visual Studio.

## <a name="requirements"></a>Requisitos
 Consulte [requisitos](../modeling/extend-uml-models-and-diagrams.md#Requirements).

 Para ver quais versões do Visual Studio oferecem suporte a esse recurso, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="defining-the-menu-command"></a>Definindo o comando de menu
 Para criar um comando de menu para um designer UML, você deve criar uma classe que define o comportamento do comando e inserir a classe em uma extensão de integração do Visual Studio (VSIX). O VSIX atua como um contêiner que pode instalar o comando. Há dois métodos alternativos de definir um comando de menu:

- **Crie um comando de menu em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Use-o se você não quiser combinar seus comandos de menu com outros tipos de extensão, como extensões de validação, itens de caixa de ferramentas personalizados ou manipuladores de gestos.

- **Crie um comando de menu separado e projetos VSIX.** Use esse método se desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se o comando de menu espera que o modelo Observe restrições específicas, você pode inseri-lo no mesmo VSIX como um método de validação.

#### <a name="to-create-a-menu-command-in-its-own-vsix"></a>Para criar um comando de menu em seu próprio VSIX

1. Na caixa de diálogo **novo projeto** , em **modelagem de projetos**, selecione **extensão de comando**.

2. Abra o arquivo **. cs** no novo projeto e modifique a `CommandExtension` classe para implementar o comando.

    Para obter mais informações, consulte [implementando o comando de menu](#Implementing).

3. Você pode adicionar outros comandos a esse projeto definindo novas classes.

4. Teste o comando de menu pressionando F5. Para obter mais informações, consulte [executando o comando de menu](#Executing).

5. Instale o comando de menu em outro computador copiando o arquivo **bin \\ \* \\ \* . vsix** criado pelo seu projeto. Para obter mais informações, consulte [Instalando e desinstalando uma extensão](#Installing).

   Este é o procedimento alternativo:

#### <a name="to-create-a-menu-command-in-a-separate-class-library-dll-project"></a>Para criar um comando de menu em um projeto de biblioteca de classes separado (DLL)

1. Crie um projeto de biblioteca de classes, seja em uma nova solução do Visual Studio ou em uma solução existente.

   1. No menu **Arquivo**, escolha **Novo**, **Projeto**.

   2. Em **modelos instalados**, selecione **Visual C#** ou **Visual Basic**. Na coluna do meio, escolha **biblioteca de classes**.

   3. Defina a **solução** para indicar se você deseja criar uma nova solução ou adicionar um componente a uma solução VSIX que você já abriu.

   4. Defina o nome do projeto e o local e clique em OK.

2. Adicione as referências a seguir ao seu projeto.

   |                                                                                                    Referência                                                                                                    |                                                                                                  O que isso permite que você faça                                                                                                  |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                                        System. ComponentModel. composição                                                                                        |                                         Defina componentes usando o [Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde).                                          |
   |                                                                                      Microsoft. VisualStudio. Uml. interfaces                                                                                      |                                                                                        Ler e alterar propriedades de elementos de modelo.                                                                                         |
   |                                                                             Microsoft. VisualStudio. ArchitectureTools. Extensibility                                                                              |                                                                                      Criar elementos de modelo, modificar formas em diagramas.                                                                                       |
   |                                                                                  Microsoft. VisualStudio. Modeling. Sdk. versão                                                                                  | Defina manipuladores de eventos de modelo.<br /><br /> Encapsular a série de alterações em seu modelo. Para obter mais informações, consulte [vincular atualizações de modelo UML usando transações](../modeling/link-uml-model-updates-by-using-transactions.md). |
   |                                                            Microsoft. VisualStudio. Modeling. Sdk. Diagrams. versão<br /><br /> (nem sempre é necessário)                                                             |                                                                                   Acesse elementos de diagrama adicionais para manipuladores de gestos.                                                                                   |
   | Microsoft. VisualStudio. ArchitectureTools. Extensibility. Layer<br /><br /> Necessário somente para comandos em diagramas de camadas. Para obter mais informações, consulte [estender diagramas de camada](../modeling/extend-layer-diagrams.md). |                                                                                             Definir comandos em um diagrama de camada.                                                                                              |

3. Adicione um arquivo de classe ao projeto e defina seu conteúdo para o código a seguir.

   > [!NOTE]
   > Altere o namespace, o nome da classe e o valor retornado por `Text` para sua preferência.
   >
   >  Se você definir vários comandos, eles aparecerão no menu em ordem alfabética dos nomes de classe.

   ```
   using System.ComponentModel.Composition;
   using System.Linq;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;
   using Microsoft.VisualStudio.Uml.Classes;
       // ADD other UML namespaces if required

   namespace UMLmenu1 // CHANGE
   {
     // DELETE any of these attributes if the command
     // should not appear in some types of diagram.
     [ClassDesignerExtension]
     [ActivityDesignerExtension]
     [ComponentDesignerExtension]
     [SequenceDesignerExtension]
     [UseCaseDesignerExtension]
     // [LayerDesignerExtension]

     // All menu commands must export ICommandExtension:
     [Export (typeof(ICommandExtension))]
     // CHANGE class name – determines order of appearance on menu:
     public class Menu1 : ICommandExtension
     {
       [Import]
       public IDiagramContext DiagramContext { get; set; }

       public void QueryStatus(IMenuCommand command)
       { // Set command.Visible or command.Enabled to false
         // to disable the menu command.
         command.Visible = command.Enabled = true;
       }

       public string Text
       {
         get { return "MENU COMMAND LABEL"; }
       }

       public void Execute(IMenuCommand command)
       {
         // A selection of starting points:
         IDiagram diagram = this.DiagramContext.CurrentDiagram;
         foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>())
         { IElement element = shape.Element; }
         IModelStore modelStore = diagram.ModelStore;
         IModel model = modelStore.Root;
         foreach (IElement element in modelStore.AllInstances<IClass>())
         { }
       }
     }
   }
   ```

    Para obter mais informações sobre o que colocar nos métodos, consulte [implementando o comando de menu](#Implementing).

   Você deve adicionar o comando de menu a um projeto VSIX, que atua como um contêiner para instalar o comando. Se desejar, você pode incluir outros componentes no mesmo VSIX.

#### <a name="to-add-a-menu-command-to-a-vsix-project"></a>Para adicionar um comando de menu a um projeto VSIX

1. Você não precisará desse procedimento se tiver criado o comando de menu com seu próprio VSIX.

2. Crie um projeto VSIX, a menos que sua solução já tenha um.

    1. No **Gerenciador de soluções**, no menu de atalho da solução, escolha **Adicionar**, **novo projeto**.

    2. Em **modelos instalados**, expanda **Visual C#** ou **Visual Basic**, em seguida, escolha **extensibilidade**. Na coluna do meio, escolha **projeto VSIX**.

3. No Gerenciador de Soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.

4. Open **Source. Extension. vsixmanifest**.

    1. Na guia **metadados** , defina um nome para o VSIX.

    2. Na guia **instalar destinos** , defina as versões do Visual Studio como os destinos.

    3. Na guia **ativos** , escolha um **novo**e, na caixa de diálogo, defina:

         **Tipo**  =  de **Componente MEF**

         **Origem**  =  do **Um projeto na solução atual**

         **Projeto**  =  do *Seu projeto de biblioteca de classes*

## <a name="implementing-the-menu-command"></a><a name="Implementing"></a>Implementando o comando de menu
 A classe de comando de menu implementa os métodos necessários para o <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> .

|Assinatura|Descrição|
|-|-|
|`string Text { get; }`|Retornar o rótulo do item de menu.|
|`void QueryStatus(IMenuCommand command);`|Chamado quando o usuário clica com o botão direito do mouse no diagrama.<br /><br /> Esse método não deve alterar o modelo.<br /><br /> Use `DiagramContext.CurrentDiagram.SelectedShapes` para determinar se você deseja que o comando apareça e esteja habilitado.<br /><br /> Definição<br /><br /> -   `command.Visible`para `true` se o comando precisar aparecer no menu quando o usuário clicar com o botão direito do mouse no diagrama<br />-   `command.Enabled`para `true` se o usuário puder clicar no comando no menu<br />-   `command.Text`para definir o rótulo do menu dinamicamente|
|`void Execute (IMenuCommand command);`|Chamado quando o usuário clica no item de menu, se estiver visível e habilitado.|

### <a name="accessing-the-model-in-code"></a>Acessando o modelo no código
 Incluindo a seguinte declaração em sua classe de comando de menu:

```
[Import] public IDiagramContext DiagramContext { get; set; }
```

 ...

 A declaração de `IDiagramContext` permite que você escreva código em seus métodos que acessam o diagrama, a seleção atual e o modelo:

```
IDiagram diagram = this.DiagramContext.CurrentDiagram;
foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>())
{ IElement element = shape.Element; ... }
IModelStore modelStore = diagram.ModelStore;
IModel model = modelStore.Root;
foreach (IElement element in modelStore.AllInstances<IUseCase>()) {...}
```

### <a name="navigating-and-updating-the-model"></a>Navegando e atualizando o modelo
 Os elementos do modelo UML estão disponíveis por meio da API. Na seleção atual ou na raiz do modelo, você pode acessar todos os outros elementos. Para obter mais informações, consulte [navegar no modelo UML](../modeling/navigate-the-uml-model.md) e [programar com a API UML](../modeling/programming-with-the-uml-api.md).

 Se você estiver lidando com um diagrama de sequência, consulte também [Editar diagramas de sequência UML usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).

 A API também permite que você altere as propriedades de elementos, exclua elementos e relações e crie novos elementos e relações.

 Por padrão, cada alteração feita em seu método execute será executada em uma transação separada. O usuário poderá desfazer cada alteração separadamente. Se você quiser agrupar as alterações em uma única transação, use um <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ILinkedUndoTransaction> conforme descrito em [vincular atualizações de modelo UML usando transações](../modeling/link-uml-model-updates-by-using-transactions.md).

### <a name="use-the-ui-thread-for-updates"></a>Usar o thread de interface do usuário para atualizações
 Em alguns casos, pode ser útil fazer atualizações para o modelo de um thread em segundo plano. Por exemplo, se o comando carregar dados de um recurso lento, você poderá executar o carregamento em um thread brackground para que o usuário possa ver as alterações enquanto elas estiverem em andamento e cancelar a operação se for necessário.

 No entanto, você deve estar ciente de que o repositório de modelos não é thread-safe. Você sempre deve usar o thread da interface do usuário para fazer atualizações e, se possível, impedir que o usuário faça edições enquanto a operação em segundo plano estiver em andamento. Para obter um exemplo, consulte [atualizar um modelo UML de um thread em segundo plano](../modeling/update-a-uml-model-from-a-background-thread.md).

## <a name="executing-the-menu-command"></a><a name="Executing"></a>Executando o comando de menu
 Para fins de teste, execute o comando no modo de depuração.

#### <a name="to-test-the-menu-command"></a>Para testar o comando de menu

1. Pressione **F5**ou, no menu **depurar** , escolha **Iniciar Depuração**.

     Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciada.

     **Solução de problemas**: se um novo não [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Iniciar:

    - Se você tiver mais de um projeto, verifique se o projeto VSIX está definido como o projeto de inicialização da solução.

    - No Gerenciador de Soluções, no menu de atalho do projeto de inicialização ou somente, escolha **Propriedades**. No editor de propriedades do projeto, selecione a guia **depurar** . Verifique se a cadeia de caracteres no campo **Iniciar programa externo** é o nome de caminho completo de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , normalmente:

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem. Use um diagrama que pertença a um dos tipos listados nos atributos de sua classe de comando de menu.

3. Abra o menu de atalho em qualquer lugar do diagrama. O comando deve aparecer no menu.

     **Solução de problemas**: se o comando não aparecer no menu, verifique se:

    - O projeto de comando de menu é listado como um componente MEF na guia **ativos** em **Source. Extensions. manifest** no projeto VSIX.

    - Os parâmetros dos `Import` atributos e `Export` são válidos.

    - O `QueryStatus` método não está definindo o `command` .`Enabled` ou `Visible` campos para `false` .

    - O tipo de diagrama de modelo que você está usando (classe UML, sequência e assim por diante) é listado como um dos atributos de classe de comando de menu `[ClassDesignerExtension]` `[SequenceDesignerExtension]` e assim por diante.

## <a name="installing-and-uninstalling-an-extension"></a><a name="Installing"></a>Instalando e desinstalando uma extensão
 Você pode instalar uma [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão no seu próprio computador e em outros computadores.

#### <a name="to-install-an-extension"></a>Para instalar uma extensão

1. Em seu computador, localize o arquivo **. vsix** criado por seu projeto VSIX.

    1. No **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **abrir pasta no Windows Explorer**.

    2. Localize o arquivo **bin \\ \* \\ **_seuprojeto_**. vsix**

2. Copie o arquivo **. vsix** para o computador de destino no qual você deseja instalar a extensão. Este pode ser seu próprio computador ou outro.

     O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou na **origem. Extension. vsixmanifest**.

3. No computador de destino, abra o arquivo **. vsix** , por exemplo, clicando duas vezes nele.

     O **instalador de extensão do Visual Studio** é aberto e instala a extensão.

4. Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] .

#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão

1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.

2. Expanda **extensões instaladas**.

3. Selecione a extensão e escolha **desinstalar**.

   Raramente, uma extensão defeituosa não carrega e cria um relatório na janela de erro, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:

   *% LocalAppData%* **\Local\Microsoft\VisualStudio \\ [versão] \Extensions**

## <a name="example"></a><a name="MenuExample"></a>Exemplo
 O exemplo a seguir mostra o código de um comando de menu que vai trocar os nomes de dois elementos em um diagrama de classe. Esse código deve ser compilado em um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto de extensão e instalado conforme descrito nas seções anteriores.

```
using System.Collections.Generic; // for IEnumerable
using System.ComponentModel.Composition;
  // for [Import], [Export]
using System.Linq; // for IEnumerable extensions
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
  // for IDiagramContext
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
  // for designer extension attributes
using Microsoft.VisualStudio.Modeling.Diagrams;
  // for ShapeElement
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
  // for IGestureExtension, ICommandExtension, ILinkedUndoContext
using Microsoft.VisualStudio.Uml.Classes;
  // for class diagrams, packages

/// <summary>
/// Extension to swap names of classes in a class diagram.
/// </summary>
namespace SwapClassNames
{
  // Declare the class as an MEF component:
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  // Add more ExportMetadata attributes to make
  // the command appear on diagrams of other types.
  public class NameSwapper : ICommandExtension
  {
  // MEF required interfaces:
  [Import]
  public IDiagramContext Context { get; set; }
  [Import]
  public ILinkedUndoContext LinkedUndoContext { get; set; }

  /// <summary>
  /// Swap the names of the currently selected elements.
  /// </summary>
  /// <param name="command"></param>
  public void Execute(IMenuCommand command)
  {
    // Get selected shapes that are IClassifiers -
    // IClasses, IInterfaces, IEnumerators.
    var selectedShapes = Context.CurrentDiagram
     .GetSelectedShapes<IClassifier>();
    if (selectedShapes.Count() < 2) return;

    // Get model elements displayed by shapes.
    IClassifier firstElement = selectedShapes.First().Element;
    IClassifier lastElement = selectedShapes.Last().Element;

    // Do the swap in a transaction so that user
    // cannot undo one change without the other.
    using (ILinkedUndoTransaction transaction =
    LinkedUndoContext.BeginTransaction("Swap names"))
    {
    string firstName = firstElement.Name;
    firstElement.Name = lastElement.Name;
    lastElement.Name = firstName;
    transaction.Commit();
    }
  }

  /// <summary>
  /// Called by Visual Studio to determine whether
  /// menu item should be visible and enabled.
  /// </summary>
  public void QueryStatus(IMenuCommand command)
  {
    int selectedClassifiers = Context.CurrentDiagram
     .GetSelectedShapes<IClassifier>().Count();
    command.Visible = selectedClassifiers > 0;
    command.Enabled = selectedClassifiers == 2;
  }

  /// <summary>
  /// Name of the menu command.
  /// </summary>
  public string Text
  {
    get { return "Swap Names"; }
  }
  }

}
```

## <a name="see-also"></a>Consulte Também
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md) [estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md) [definir um manipulador de gestos em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) [definir um item da caixa de ferramentas de modelagem personalizado](../modeling/define-a-custom-modeling-toolbox-item.md) [definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md) [Editar diagramas de sequência UML usando a programação de API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md) [com a API UML](../modeling/programming-with-the-uml-api.md)
 