---
title: Definir um comando de menu em um diagrama de modelagem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending, menu commands
ms.assetid: 79c277de-5871-4fc7-9701-55eec5c3cd46
caps.latest.revision: 63
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: c211c37817ba996105d7496dc49e91db9fa9298e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809097"
---
# <a name="define-a-menu-command-on-a-modeling-diagram"></a>Definir um comando de menu em um diagrama de modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode definir itens de menu adicionais nos menus de atalho de um diagrama UML. Você pode controlar se o comando de menu aparece e é habilitado no menu de atalho de qualquer elemento no diagrama, e você pode escrever código que é executado quando o usuário escolhe o item de menu. Você pode empacotar essas extensões em uma extensão de integração do Visual Studio ([VSIX](http://go.microsoft.com/fwlink/?LinkId=160780)) e distribuí-lo para outros usuários do Visual Studio.  

## <a name="requirements"></a>Requisitos  
 Ver [requisitos de](../modeling/extend-uml-models-and-diagrams.md#Requirements).  

 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  

## <a name="defining-the-menu-command"></a>Definindo o comando de menu  
 Para criar um comando de menu para um designer UML, você deve criar uma classe que define o comportamento do comando e inserir a classe em um Visual Studio Integration VSIX (extensão). O VSIX atua como um contêiner que pode instalar o comando. Há dois métodos alternativos de definição de um comando de menu:  

-   **Crie um comando de menu em seu próprio VSIX usando um modelo de projeto.** Esse é o método mais rápido. Usá-lo se você não deseja combinar seus comandos de menu com outros tipos de extensão, como extensões de validação, itens de caixa de ferramentas personalizada ou manipuladores de gestos.  

-   **Crie comando de menu separado e projetos VSIX.** Use este método se você desejar combinar vários tipos de extensão no mesmo VSIX. Por exemplo, se seu comando de menu esperar que o modelo observe as restrições específicas, você poderá inseri-lo no mesmo VSIX que um método de validação.  

#### <a name="to-create-a-menu-command-in-its-own-vsix"></a>Para criar um comando de menu em seu próprio VSIX  

1. No **novo projeto** caixa de diálogo **projetos de modelagem**, selecione **extensão de comando**.  

2. Abra o **. CS** de arquivos no novo projeto e modificar o `CommandExtension` classe para implementar o comando.  

    Para obter mais informações, consulte [Implementando o comando de Menu](#Implementing).  

3. Você pode adicionar comandos adicionais para esse projeto definindo novas classes.  

4. Teste o comando de menu pressionando F5. Para obter mais informações, consulte [executando o comando de Menu](#Executing).  

5. Instalar o comando de menu em outro computador copiando o arquivo **bin\\\*\\\*. VSIX** que é compilado pelo seu projeto. Para obter mais informações, consulte [instalando e desinstalando uma extensão](#Installing).  

   Aqui está o procedimento alternativo:  

#### <a name="to-create-a-menu-command-in-a-separate-class-library-dll-project"></a>Para criar um comando de menu em um projeto de biblioteca (DLL) de classe separada  

1. Crie um projeto de biblioteca de classes, em uma nova solução do Visual Studio ou em uma solução existente.  

   1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  

   2.  Sob **modelos instalados**, selecione **Visual c#** ou **Visual Basic**. Na coluna do meio, escolha **biblioteca de classes**.  

   3.  Definir **solução** para indicar se você deseja criar uma nova solução ou adicionar um componente a uma solução VSIX que você já abriu.  

   4.  Defina o projeto de nome e o local e clique em Okey.  

2. Adicione as seguintes referências ao seu projeto.  


   |                                                                                                    Referência                                                                                                    |                                                                                                  O que isso permite que você faça                                                                                                  |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                                        System.ComponentModel.Composition                                                                                        |                                         Define componentes usando [Managed Extensibility Framework (MEF)](http://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde).                                          |
   |                                                                                      Microsoft.VisualStudio.Uml.Interfaces                                                                                      |                                                                                        Ler e alterar as propriedades de elementos de modelo.                                                                                         |
   |                                                                             Microsoft.VisualStudio.ArchitectureTools.Extensibility                                                                              |                                                                                      Criar elementos de modelo, modifique as formas em diagramas.                                                                                       |
   |                                                                                  Microsoft.VisualStudio.Modeling.Sdk.[version]                                                                                  | Defina manipuladores de eventos do modelo.<br /><br /> Encapsule a série de alterações ao seu modelo. Para obter mais informações, consulte [atualizações de modelo UML de Link usando transações](../modeling/link-uml-model-updates-by-using-transactions.md). |
   |                                                            Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]<br /><br /> (nem sempre necessário)                                                             |                                                                                   Elementos de diagrama adicional de acesso para manipuladores de gestos.                                                                                   |
   | Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer<br /><br /> Necessário somente para os comandos em diagramas de camada. Para obter mais informações, consulte [estender diagramas de camada](../modeling/extend-layer-diagrams.md). |                                                                                             Defina comandos em um diagrama de camada.                                                                                              |


3. Adicionar um arquivo de classe ao projeto e defina seu conteúdo para o código a seguir.  

   > [!NOTE]
   >  Alterar o namespace, nome de classe e o valor retornado por `Text` com sua preferência.  
   >   
   >  Se você definir vários comandos, eles aparecem no menu em ordem alfabética dos nomes de classe.  

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

    Para obter mais informações sobre o que colocar nos métodos, consulte [Implementando o comando de Menu](#Implementing).  

   Você deve adicionar seu comando de menu a um projeto VSIX, que atua como um contêiner para o comando de instalação. Se você quiser, você pode incluir outros componentes no mesmo VSIX.  

#### <a name="to-add-a-menu-command-to-a-vsix-project"></a>Para adicionar um comando de menu a um projeto VSIX  

1.  Você não precisará deste procedimento se você tiver criado o comando de menu com seu próprio VSIX.  

2.  Crie um projeto VSIX, a menos que sua solução já tenha um.  

    1.  Na **Gerenciador de soluções**, no menu de atalho da solução, escolha **Add**, **novo projeto**.  

    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, escolha **extensibilidade**. Na coluna do meio, escolha **VSIX Project**.  

3.  No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.  

4.  Abra **vsixmanifest**.  

    1.  Sobre o **metadados** guia, defina um nome para o VSIX.  

    2.  Sobre o **instalar destinos** guia, defina as versões do Visual Studio como os destinos.  

    3.  Sobre o **ativos** guia, escolha um **New**e, na caixa de diálogo, defina:  

         **Tipo de** = **componente MEF**  

         **Código-fonte** = **um projeto na solução atual**  

         **Projeto** = *seu projeto de biblioteca de classes*  

##  <a name="Implementing"></a> Implementando o comando de Menu  
 A classe de comando de menu implementa os métodos necessários para <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension>.  

|||  
|-|-|  
|`string Text { get; }`|Retorne o rótulo do seu item de menu.|  
|`void QueryStatus(IMenuCommand command);`|Chamado quando o usuário clica com o botão direito no diagrama.<br /><br /> Esse método não deve alterar o modelo.<br /><br /> Use `DiagramContext.CurrentDiagram.SelectedShapes` para determinar se você deseja que o comando apareça e seja habilitado.<br /><br /> Defina:<br /><br /> -   `command.Visible` para `true` se o comando deve aparecer no menu quando o usuário clica com o botão direito no diagrama<br />-   `command.Enabled` para `true` se o usuário pode clicar no comando no menu<br />-   `command.Text` Para definir o rótulo de menu dinamicamente|  
|`void Execute (IMenuCommand command);`|Chamado quando o usuário clica o item de menu, se estiver visível e habilitado.|  

### <a name="accessing-the-model-in-code"></a>Acessando o modelo no código  
 Incluindo a declaração a seguir em sua classe de comando de menu:  

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
 Os elementos de modelo UML estão disponíveis por meio da API. Da seleção atual ou da raiz do modelo, você pode acessar todos os outros elementos. Para obter mais informações, consulte [navegar no modelo UML](../modeling/navigate-the-uml-model.md) e [programação com a API UML](../modeling/programming-with-the-uml-api.md).  

 Se você estiver lidando com um diagrama de sequência, consulte também [diagramas de sequência UML Editar usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).  

 A API também permite que você altere as propriedades de elementos, excluir elementos e relações e criar novos elementos.  

 Por padrão, cada alteração feita no seu método de execução será executada em uma transação separada. O usuário poderá desfazer separadamente cada alteração. Se você quiser agrupar as alterações em uma única transação, use uma <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ILinkedUndoTransaction> conforme descrito em [atualizações de modelo UML de Link usando transações](../modeling/link-uml-model-updates-by-using-transactions.md).  

### <a name="use-the-ui-thread-for-updates"></a>Usar o Thread de interface do usuário para atualizações  
 Em alguns casos, ele pode ser útil fazer atualizações para o modelo de um thread em segundo plano. Por exemplo, se o comando carregar dados de um recurso lento, você pode executar o carregamento em um thread de plano de fundo para que o usuário possa ver as alterações enquanto elas estão em andamento e cancelar a operação se for necessário.  

 No entanto, você deve estar ciente de que o armazenamento de modelo não é thread-safe. Você sempre deve usar o thread de interface do usuário do usuário para fazer atualizações e se for possível, impedir que o usuário faça edições quando a operação em segundo plano está em andamento. Por exemplo, consulte [atualizar um modelo UML de um thread em segundo plano](../modeling/update-a-uml-model-from-a-background-thread.md).  

##  <a name="Executing"></a> Executando o comando de Menu  
 Para fins de teste, execute o comando no modo de depuração.  

#### <a name="to-test-the-menu-command"></a>Para testar o comando de menu  

1.  Pressione **F5**, ou o **depurar** menu, escolha **iniciar depuração**.  

     Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciado.  

     **Solução de problemas**: se um novo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não for iniciado:  

    -   Se você tiver mais de um projeto, certifique-se de que o projeto do VSIX está definido como o projeto de inicialização da solução.  

    -   No Gerenciador de soluções, no menu de atalho da inicialização ou somente projeto, escolha **propriedades**. No editor de propriedades de projeto, selecione a **depurar** guia. Certifique-se de que a cadeia de caracteres na **Iniciar programa externo** campo é o nome do caminho completo do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], normalmente:  

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`  

2.  Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem. Use um diagrama que pertence a um dos tipos listados nos atributos de sua classe de comando de menu.  

3.  Abra o menu de atalho em qualquer lugar no diagrama. O comando deve aparecer no menu.  

     **Solução de problemas**: se o comando não aparecer no menu, verifique se:  

    -   O projeto de comando de menu está listado como um componente MEF na **ativos** guia **source.extensions.manifest** no projeto VSIX.  

    -   Os parâmetros do `Import` e `Export` atributos são válidos.  

    -   O `QueryStatus` método não está definindo o `command`.`Enabled` ou `Visible` campos `false`.  

    -   O tipo de diagrama de modelo que você está usando (classe UML, sequência e assim por diante) é listado como um dos atributos de classe de comando de menu `[ClassDesignerExtension]`, `[SequenceDesignerExtension]` e assim por diante.  

##  <a name="Installing"></a> Instalando e desinstalando uma extensão  
 Você pode instalar um [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão em seu próprio computador e em outros computadores.  

#### <a name="to-install-an-extension"></a>Para instalar uma extensão  

1.  No seu computador, localize o **VSIX** arquivo que foi criado pelo seu projeto VSIX.  

    1.  Na **Gerenciador de soluções**, no menu de atalho do projeto VSIX, escolha **Abrir pasta no Windows Explorer**.  

    2.  Localize o arquivo **bin\\\*\\**_Seuprojeto_**. VSIX**  

2.  Cópia de **. VSIX** arquivo ao computador de destino no qual você deseja instalar a extensão. Isso pode ser seu próprio computador ou outro.  

     O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] que você especificou no **vsixmanifest**.  

3.  No computador de destino, abra o **VSIX** arquivo, por exemplo, clicando duas vezes nele.  

     **Instalador de extensão do Visual Studio** abre e instala a extensão.  

4.  Iniciar ou reiniciar [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)].  

#### <a name="to-uninstall-an-extension"></a>Para desinstalar uma extensão  

1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.  

2. Expandir **extensões instaladas**.  

3. Selecione a extensão e, em seguida, escolha **desinstalação**.  

   Raramente, uma extensão defeituosa Falha ao carregar e cria um relatório na janela de erros, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:  

   *% LocalAppData %* **\Local\Microsoft\VisualStudio\\\Extensions [versão]**  

##  <a name="MenuExample"></a> Exemplo  
 O exemplo a seguir mostra o código para um comando de menu que fará intercâmbio entre os nomes dos dois elementos em um diagrama de classe. Esse código deve ser criado um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projeto de extensão e instalado conforme descrito nas seções anteriores.  

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

## <a name="see-also"></a>Consulte também  
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Definir um manipulador de gesto em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)   
 [Definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md)   
 [Definir restrições de validação para modelos UML](../modeling/define-validation-constraints-for-uml-models.md)   
 [Editar diagramas de sequência UML usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)   
 [Exemplo: Comando para alinhar formas em um diagrama UML](http://go.microsoft.com/fwlink/?LinkID=213809)



