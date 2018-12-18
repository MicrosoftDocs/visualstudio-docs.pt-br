---
title: Criar uma extensão com um comando de Menu | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
caps.latest.revision: 57
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fb99149a7b617d8e48e036d9e706e5e1c0a6169b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779301"
---
# <a name="creating-an-extension-with-a-menu-command"></a>Criando uma extensão com um comando de menu
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como criar uma extensão com um comando de menu que inicia o bloco de notas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-menu-command"></a>Criação de um comando de Menu  
  
1.  Crie um projeto do VSIX chamado **FirstMenuCommand**. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c# / extensibilidade**.  
  
2.  Quando o projeto aberto, adicione um modelo de item de comando personalizado chamado **FirstCommand**. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c# / extensibilidade** e selecione **comando personalizado**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para **FirstCommand.cs**.  
  
3.  Compile o projeto e comece a depuração.  
  
     A instância experimental do Visual Studio é exibida. Para obter mais informações sobre a instância experimental, consulte [a instância Experimental](../extensibility/the-experimental-instance.md).  
  
4.  Na instância experimental, abra o **ferramentas / extensões e atualizações** janela. Você deve ver a **FirstMenuCommand** extensão aqui. (Se você abrir **extensões e atualizações** em sua instância de trabalho do Visual Studio, você não verá **FirstMenuCommand**).  
  
     Agora vá para o **ferramentas** menu na instância experimental. Você deve ver **FirstCommand invocar** comando. Neste ponto ele apenas traz uma caixa de mensagem que diz "FirstCommandPackage dentro FirstMenuCommand.FirstCommand.MenuItemCallback()". Veremos como realmente começar o bloco de notas desse comando na próxima seção.  
  
## <a name="changing-the-menu-command-handler"></a>Alterando o manipulador de comandos de Menu  
 Agora vamos atualizar o manipulador de comandos para iniciar o bloco de notas.  
  
1.  Parar a depuração e voltar para sua instância de trabalho do Visual Studio. Abra o arquivo FirstCommand.cs e adicione a seguinte instrução using:  
  
    ```csharp  
    using System.Diagnostics;  
    ```  
  
2.  Localize o construtor FirstCommand particular. Isso é onde o comando é conectado ao serviço de comando e o manipulador de comando é especificado. Altere o nome do manipulador de comando para o StartNotepad, da seguinte maneira:  
  
    ```csharp  
    private FirstCommand(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
         OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(CommandSet, CommandId);  
            // Change to StartNotepad handler.  
            MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
3.  Remova o método MenuItemCallback e adicione um método StartNotepad que apenas iniciará o bloco de notas:  
  
    ```csharp  
    private void StartNotepad(object sender, EventArgs e)  
    {  
        Process proc = new Process();  
        proc.StartInfo.FileName = "notepad.exe";  
        proc.Start();  
    }  
    ```  
  
4.  Agora tente. Quando você iniciar a depuração do projeto e clique em **ferramentas / invocar FirstCommand**, você deve ver uma instância do bloco de notas.  
  
     Você pode usar uma instância da <xref:System.Diagnostics.Process> classe para executar qualquer executável, não apenas o bloco de notas. Tente com calc.exe, por exemplo.  
  
## <a name="cleaning-up-the-experimental-environment"></a>Limpando ambiente Experimental  
 Se você estiver desenvolvendo várias extensões, ou apenas explorando os resultados com diferentes versões do seu código de extensão, o seu ambiente experimental pode parar de funcionar como deveria. Nesse caso, você deve executar o script de reinicialização. Ele é chamado **redefinir a instância Experimental do Visual Studio 2015**, e ele é fornecido como parte do SDK do Visual Studio. Esse script remove todas as referências a suas extensões do ambiente experimental, para que você possa começar do zero.  
  
 Você pode chegar a este script em uma das duas maneiras:  
  
1.  Na área de trabalho, localize **redefinir a instância Experimental do Visual Studio 2015**.  
  
2.  Na linha de comando, execute o seguinte:  
  
    ```  
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp && PAUSE  
  
    ```  
  
## <a name="deploying-your-extension"></a>Implantar sua extensão  
 Agora que você tem a sua extensão da ferramenta em execução da maneira desejada, é hora de pensar em compartilhá-lo com seus amigos e colegas. Isso é fácil, desde que eles têm instalado o Visual Studio 2015. Tudo o que você precisa fazer é enviá-los o arquivo. VSIX que você criou. (Certifique-se de criá-lo no modo de versão.)  
  
 Você pode encontrar o arquivo. VSIX para esta extensão no diretório bin FirstMenuCommand. Especificamente, supondo que você criou a configuração de versão, ele estará em:  
  
 **\<diretório de código > \FirstMenuCommand\FirstMenuCommand\bin\Release\ FirstMenuCommand.vsix**  
  
 Para instalar a extensão, seu amigo precisa fechar todas as instâncias abertas do Visual Studio e, em seguida, duas vezes no arquivo. VSIX, que abre o **instalador do VSIX**. Os arquivos são copiados para o **%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions** directory.  
  
 Quando seu amigo traz o Visual Studio novamente, ele encontrará a extensão FirstMenuCommand na **ferramentas / extensões e atualizações**. Ele pode ir para **extensões e atualizações** para desinstalar ou desabilitar a extensão, muito.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostrou apenas uma pequena parte do que você pode fazer com uma extensão do Visual Studio. Aqui está uma lista curta de outras coisas (razoavelmente fácil), que você pode fazer com as extensões do Visual Studio:  
  
1. Você pode fazer muito mais coisas com um comando de menu simples:  
  
   1.  Adicionar seu próprio ícone: [adicionando ícones a comandos de Menu](../extensibility/adding-icons-to-menu-commands.md)  
  
   2.  Alterar o texto do comando de menu: [alterar o texto de um comando de Menu](../extensibility/changing-the-text-of-a-menu-command.md)  
  
   3.  Adicionar um atalho de menu a um comando: [atalhos de teclado associando a itens de Menu](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
  
2. Adicionar tipos diferentes de comandos, menus e barras de ferramentas: [estendendo Menus e comandos](../extensibility/extending-menus-and-commands.md)  
  
3. Adicionar janelas de ferramenta e estender as janelas de ferramentas internas do Visual Studio: [estendendo e personalizando o Windows de ferramenta](../extensibility/extending-and-customizing-tool-windows.md)  
  
4. Adicionar o IntelliSense, sugestões de código e outros recursos existentes de editores de código: [estender o Editor e os serviços de linguagem](../extensibility/extending-the-editor-and-language-services.md)  
  
5. Adicionar páginas de propriedade e as opções e configurações do usuário para sua extensão: [estendendo propriedades e a janela de propriedade](../extensibility/extending-properties-and-the-property-window.md) e [estendendo as configurações do usuário e opções](../extensibility/extending-user-settings-and-options.md)  
  
   Outros tipos de extensões exigem um pouco mais de trabalho, como a criação de um novo tipo de projeto ([estendendo projetos](../extensibility/extending-projects.md)), criando um novo tipo de editor ([criação personalizada editores e Designers](../extensibility/creating-custom-editors-and-designers.md)), ou Implementando a sua extensão em um shell isolado: [Shell isolado do Visual Studio](../extensibility/visual-studio-isolated-shell.md)

