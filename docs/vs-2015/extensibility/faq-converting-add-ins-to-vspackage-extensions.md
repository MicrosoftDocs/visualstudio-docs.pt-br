---
title: 'Perguntas Frequentes: Convertendo suplementos em extensões VSPackage | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a01d333-6e31-423f-ae06-5091a4fcb7a9
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b2318ff719f51660b4cec0eec6b7a051ea54aa67
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817341"
---
# <a name="faq-converting-add-ins-to-vspackage-extensions"></a>Perguntas frequentes: convertendo suplementos em extensões VSPackage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Suplementos agora são preteridos. Para fazer uma nova extensão do Visual Studio, você precisará criar uma extensão do VSIX. Aqui estão as respostas a algumas perguntas frequentes sobre como converter um suplemento do Visual Studio em uma extensão do VSIX.  
  
> [!WARNING]
>  Iniciando no Visual Studio 2015, para projetos c# e Visual Basic, você pode usar o projeto do VSIX e adicionar modelos de item para comandos de menu, janelas de ferramenta e VSPackages. Para obter mais informações, consulte [o que há de novo no SDK do Visual Studio 2015](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md).  
  
> [!IMPORTANT]
>  Em muitos casos, você pode simplesmente transferir o seu código de suplemento a um projeto do VSIX com um item de projeto de VSPackage. Você pode obter o objeto de automação DTE chamando <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> no método <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>.  
>   
>  `DTE2 dte = (DTE2)GetService(typeof(DTE));`  
>   
>  Para obter mais informações, consulte [como posso executar meu código de suplemento em um VSPackage?](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_RunAddin) abaixo.  
  
## <a name="what-software-do-i-need-to-develop-vsix-extensions"></a>Qual software precisa desenvolver extensões VSIX?  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="wheres-the-extension-documentation"></a>Onde está a documentação de extensão?  
 Iniciar com [começando a desenvolver extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md). Outros artigos sobre desenvolvimento de extensão do VSSDK no MSDN estão abaixo que um.  
  
## <a name="can-i-convert-my-add-in-project-to-a-vsix-project"></a>Pode converter o meu projeto de suplemento a um projeto VSIX?  
 Um projeto de suplemento não pode ser convertido diretamente a um projeto VSIX, pois os mecanismos usados em projetos do VSIX não são os mesmos que aqueles em projetos de suplemento. O modelo de projeto do VSIX, além dos modelos de item de projeto à direita tem muito código que o torna relativamente fácil de começar a trabalhar e em execução como uma extensão do VSIX.  
  
##  <a name="BKMK_StartDeveloping"></a> Como para começar a desenvolver extensões VSIX?  
 Aqui está como fazer um VSIX que possui um comando de menu:  
  
#### <a name="to-make-a-vsix-extension-that-has-a-menu-command"></a>Para tornar uma extensão do VSIX que possui um comando de menu  
  
1.  Crie um projeto VSIX. (**Arquivo**, **New**, **projeto**, ou tipo **projeto** no **início rápido** janela). Além de **novo projeto** caixa de diálogo caixa, expanda **Visual c# / extensibilidade** ou **Visual Basic / extensibilidade** e selecione **projeto VSIX**.) Nomeie o projeto **TestExtension** e especifique um local para ele.  
  
2.  Adicionar um **comando personalizado** modelo de item de projeto. (Clique com botão direito no nó do projeto na **Gerenciador de soluções** e selecione **Add / Novo Item**. Além de **novo projeto** caixa de diálogo do Visual c# ou Visual Basic, selecione o **extensibilidade** nó e selecione **comando personalizado**.)  
  
3.  Pressione F5 para compilar e executar o projeto em modo de depuração.  
  
     Uma segunda instância do Visual Studio é exibida. A segunda instância é chamada de instância experimental e não poderá ter as mesmas configurações que a instância do Visual Studio que estiver usando para escrever código. Na primeira vez que executar a instância experimenta, será solicitado para entrar no VS Online e especificar o tema e o perfil.  
  
     Sobre o **ferramentas** menu (na instância experimental), você verá um botão chamado **nome do meu comando**. Quando você escolhe esse botão, uma mensagem deverá aparecer: **dentro de Testvspackagepackage**.  
  
##  <a name="BKMK_RunAddin"></a> Como posso executar meu código de suplemento em um VSPackage?  
 Código de suplemento geralmente é executado de uma entre duas maneiras:  
  
- Acionado por um comando de menu (o código está no método de `IDTCommandTarget.Exec`)  
  
- Automaticamente na inicialização (o código está no manipulador de eventos `OnConnection`.)  
  
  É possível fazer as mesmas coisas em um VSPackage. Aqui está como incluir um código de suplemento no método de retorno de chamada:  
  
#### <a name="to-implement-a-menu-command-in-a-vspackage"></a>Implementar um comando de menu em um VSPackage  
  
1. Criar VSPackage que possui um comando de menu. (Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).)  
  
2. Abra o arquivo que contém a definição do VSPackage. (Em um projeto c#, ele tem  <em>\<o nome do projeto ></em>Package.cs.)  
  
3. Inclua as seguintes instruções `using` no arquivo:  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. Encontre o método `MenuItemCallback`. Inclua uma chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> para obter o objeto <xref:EnvDTE80.DTE2>:  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. Inclua o código que o suplemento continha em seu método `IDTCommandTarget.Exec`. Por exemplo, aqui está um código que adiciona um novo painel para o **saída** janela e exibe "Algum texto" no novo painel.  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));  
       OutputWindow outputWindow = dte.ToolWindows.OutputWindow;  
  
       OutputWindowPane outputWindowPane = outputWindow.OutputWindowPanes.Add("A New Pane");  
       outputWindowPane.OutputString("Some Text");  
   }  
  
   ```  
  
6. Compile e execute esse projeto. Pressione F5 ou selecione **inicie** sobre o **depurar** barra de ferramentas. Na instância experimental do Visual Studio, o **ferramentas** menu deve ter um botão chamado **nome do meu comando**. Quando você escolhe este botão, as palavras **algum texto** deve aparecer em uma **saída** painel da janela. (Talvez você precise abrir o **saída** janela.)  
  
   Também é possível configurar a execução do código na inicialização. No entanto, essa abordagem geralmente é desencorajada para extensões de VSPackage. Se muitas extensões tentarem carregar na inicialização do Visual Studio, o tempo de inicialização poderá tornar-se notavelmente mais longo. Uma prática melhor é carregar o VSPackage automaticamente apenas quando alguma condição for atendida (como a abertura de uma solução).  
  
   Esse procedimento mostra como executar código de suplemento em um VSPackage que é carregado automaticamente quando uma solução for aberta:  
  
#### <a name="to-autoload-a-vspackage"></a>Carregar um VSPackage automaticamente  
  
1. Crie um projeto do VSIX com um item de projeto do Visual Studio Package. (Para as etapas para fazer isso, consulte [como começar a desenvolver extensões VSIX?](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping). Basta adicionar o **Visual Studio Package** de item de projeto em vez disso.) Nomeie o projeto do VSIX **como TestAutoload**.  
  
2. Abra TestAutoloadPackage.cs. Encontre a linha onde a classe do pacote é declarada:  
  
   ```csharp  
   public sealed class <name of your package>Package : Package  
   ```  
  
3. Acima dessa linha há um conjunto de atributos. Inclua este atributo:  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
   ```  
  
4. Defina um ponto de interrupção no método `Initialize()` e inicie a depuração (F5).  
  
5. Na instância experimental, abra um projeto. O VSPackage deverá ser carregado e o ponto de interrupção deverá ser atingido.  
  
   É possível especificar outros contextos nos quais carregará o VSPackage usando os campos de <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>. Para obter mais informações, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).  
  
## <a name="how-can-i-get-the-dte-object"></a>Como obter o objeto DTE?  
 Se o suplemento não exibir a UI—por exemplo, comandos de menu, botões da barra de ferramentas ou janelas de ferramentas—você poderá usar o código no estado em que estiver desde que obtenha o objeto de automação DTE do VSPackage. Veja como:  
  
#### <a name="to-get-the-dte-object-from-a-vspackage"></a>Obter o objeto DTE de um VSPackage  
  
1. Em um projeto do VSIX com um modelo de item de pacote do Visual Studio, procure o  <em>\<nome do projeto ></em>arquivo Package.cs. Essa é a classe derivada de <xref:Microsoft.VisualStudio.Shell.Package>; poderá ajudar a interagir com o Visual Studio. Nesse caso, use o <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> para obter o objeto <xref:EnvDTE80.DTE2>.  
  
2. Inclua estas instruções `using`:  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
3. Encontre o método `Initialize`. Esse método manipula o comando especificado no assistente de pacote. Inclua uma chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> para obter o objeto DTE:  
  
   ```csharp  
   DTE dte = (DTE)GetService(typeof(DTE));  
   ```  
  
   Após ter o objeto de automação <xref:EnvDTE.DTE>, é possível incluir o restante do código de suplemento no projeto. Se o objeto <xref:EnvDTE80.DTE2> for necessário, é possível fazer a mesma coisa.  
  
## <a name="how-do-i-change-menu-commands-and-toolbar-buttons-in-my-add-in-to-the-vspackage-style"></a>Como alterar comandos de menu e botões da barra de ferramentas no suplemento para o estilo do VSPackage?  
 Extensões de VSPackage usam o arquivo .vsct para criar a maioria dos comandos de menu, barras de ferramentas, botões de barras de ferramentas e outras UI. O **comando Custom** modelo de item de projeto oferece a opção para criar um comando na **ferramentas** menu. Para obter mais informações, consulte [criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md).  
  
 Para obter mais informações sobre arquivos. VSCT, consulte [como os VSPackages adicionar elementos Interface do usuário](../extensibility/internals/how-vspackages-add-user-interface-elements.md). Para instruções passo a passo que mostram como usar o arquivo. VSCT para adicionar itens de menu, barras de ferramentas e botões de barra de ferramentas, consulte [estendendo Menus e comandos](../extensibility/extending-menus-and-commands.md).  
  
## <a name="how-do-i-add-custom-tool-windows-in-the-vspackage-way"></a>Como incluir janelas de ferramenta personalizadas da maneira do VSPackage?  
 O modelo de item de projeto da janela de ferramenta personalizada oferece a opção para criar uma janela de ferramentas. Para obter mais informações sobre este modelo de item de projeto, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md). Para obter informações sobre janelas de ferramentas, consulte [estendendo e personalizando o Windows de ferramenta](../extensibility/extending-and-customizing-tool-windows.md) e os artigos contidos, especialmente [adicionando uma janela de ferramentas](../extensibility/adding-a-tool-window.md).  
  
## <a name="how-do-i-manage-visual-studio-windows-in-the-vspackage-way"></a>Como gerenciar janelas do Visual Studio da maneira do VSPackage?  
 Se o suplemento gerencia janelas do Visual Studio, o código do suplemento deverá funcionar em um VSPackage. Por exemplo, este procedimento mostra como adicionar código que gerencia o **lista de tarefas** para o `MenuItemCallback` método do VSPackage.  
  
#### <a name="to-insert-window-management-code-from-an-add-in-into-a-vspackage"></a>Inserir código de gerenciamento de janelas a partir de um suplemento em um VSPackage  
  
1. Crie um VSPackage que tenha um comando de menu, como mostra a [como começar a desenvolver extensões VSIX?](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) seção.  
  
2. Abra o arquivo que contém a definição do VSPackage. (Em um projeto c#, ele tem  <em>\<o nome do projeto ></em>Package.cs.)  
  
3. Inclua estas instruções `using`:  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. Encontre o método `MenuItemCallback`. Inclua uma chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> para obter o objeto <xref:EnvDTE80.DTE2>:  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. Inclua o código do suplemento. Por exemplo, aqui está um código que adiciona novas tarefas para o **lista de tarefas**, lista o número de tarefas e, em seguida, exclui uma tarefa.  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)   
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       TaskList tl = (TaskList)dte.ToolWindows.TaskList;   
       askItem tlItem;   
  
       // Add a couple of tasks to the Task List.   
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 1.",    
           vsTaskPriority.vsTaskPriorityHigh, vsTaskIcon.vsTaskIconUser,   
           true, "", 10, true, true);  
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 2.",   
           vsTaskPriority.vsTaskPriorityLow, vsTaskIcon.vsTaskIconComment, true, "", 20, true,true);  
  
       // List the total number of task list items after adding the new task items.  
       System.Windows.Forms.MessageBox.Show("Task Item 1 description: "+tl.TaskItems.Item(2).Description);  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
  
       // Remove the second task item. The items list in reverse numeric order.   
       System.Windows.Forms.MessageBox.Show("Deleting the second task item");  
       tl.TaskItems.Item(2).Delete();  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
   }  
   ```  
  
## <a name="how-do-i-manage-projects-and-solutions-in-a-vspackage"></a>Como gerenciar projetos e soluções em um VSPackage?  
 Se o suplemento gerencia projetos e soluções, o código do suplemento deverá funcionar em um VSPackage. Por exemplo, esse procedimento mostra como incluir código que obtém o projeto de inicialização.  
  
1. Crie um VSPackage que tenha um comando de menu, como mostra a [como começar a desenvolver extensões VSIX?](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) seção.  
  
2. Abra o arquivo que contém a definição do VSPackage. (Em um projeto c#, ele tem  <em>\<o nome do projeto ></em>Package.cs.)  
  
3. Inclua estas instruções `using`:  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. Encontre o método `MenuItemCallback`. Inclua uma chamada para <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> para obter o objeto <xref:EnvDTE80.DTE2>:  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. Inclua o código do suplemento. Por exemplo, o código a seguir obtém o nome do projeto de inicialização em uma solução. (Um projeto multi-soluções deve estar aberto ao executar esse pacote.)  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       SolutionBuild2 sb = (SolutionBuild2)dte.Solution.SolutionBuild;   
       Project startupProj;   
       string msg = "";  
  
       foreach (String item in (Array)sb.StartupProjects)   
       {  
           msg += item;   
       }  
       System.Windows.Forms.MessageBox.Show("Solution startup Project: "+msg);   
       startupProj = dte.Solution.Item(msg);   
       System.Windows.Forms.MessageBox.Show("Full name of solution's startup project: "+"/n"+startupProj.FullName);   
   }  
   ```  
  
## <a name="how-do-i-set-keyboard-shortcuts-in-a-vspackage"></a>Como definir atalhos de teclado em um VSPackage?  
 Use o elemento `<KeyBindings>` do arquivo .vsct. No exemplo a seguir, o atalho de teclado para o comando `idCommand1` é Alt+A e o atalho de teclado para o comando `idCommand2` é Alt+Ctrl+A. Observe a sintaxe dos nomes das teclas.  
  
```xml  
<KeyBindings>  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand1" editor="guidVSStd97" key1="A" mod1="ALT" />  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand2" editor="guidVSStd97" key1="A" mod1="CONTROL" mod2="ALT" />  
</KeyBindings>  
```  
  
## <a name="how-do-i-handle-automation-events-in-a-vspackage"></a>Como manipular eventos de automação em um VSPackage?  
 Eventos de automação em um VSPackage são manipulados da mesma maneira que no suplemento. O código a seguir mostra como manipular o evento `OnItemRenamed`. (Este exemplo considera que você já obteve o objeto DTE.)  
  
```csharp  
Events2 dteEvents = (Events2)dte.Events;  
dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;   
. . .  
public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)   
{  
    string s = "[Event] Renamed " + oldName + " to " + Path.GetFileName(projItem.get_FileNames(1) + " in project " + projItem.ContainingProject.Name;   
}  
```

