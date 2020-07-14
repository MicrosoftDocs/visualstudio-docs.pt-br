---
title: Criando uma extensão com um comando de menu | Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f9e9963e05b0991beaea7da4027f4db3df4e4eb
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903917"
---
# <a name="create-an-extension-with-a-menu-command"></a>Criar uma extensão com um comando de menu

Este tutorial mostra como criar uma extensão com um comando de menu que inicia o bloco de notas.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-menu-command"></a>Criar um comando de menu

1. Crie um projeto VSIX chamado **FirstMenuCommand**. Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** pesquisando por "VSIX".

2. Quando o projeto for aberto, adicione um modelo de item de comando personalizado chamado **FirstCommand**. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , vá para extensibilidade do **Visual C#**  >  **Extensibility** e selecione **comando personalizado**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para *FirstCommand.cs*.

3. Compile o projeto e comece a depuração.

    A instância experimental do Visual Studio é exibida. Para obter mais informações sobre a instância experimental, consulte [a instância experimental](../extensibility/the-experimental-instance.md).

::: moniker range="vs-2017"

4. Na instância experimental, abra a janela **ferramentas**  >  **extensões e atualizações** . Você deve ver a extensão **FirstMenuCommand** aqui. (Se você abrir **extensões e atualizações** em sua instância de trabalho do Visual Studio, não verá **FirstMenuCommand**).

::: moniker-end

::: moniker range=">=vs-2019"

4. Na instância experimental, abra a janela **extensões**  >  **gerenciar extensões** . Você deve ver a extensão **FirstMenuCommand** aqui. (Se você abrir **gerenciar extensões** em sua instância de trabalho do Visual Studio, não verá **FirstMenuCommand**).

::: moniker-end

Agora, vá para o menu **ferramentas** na instância experimental. Você deverá ver o comando **Invoke FirstCommand** . Neste ponto, o comando abre uma caixa de mensagem que diz **FirstCommandPackage dentro de FirstMenuCommand. FirstCommand. MenuItemCallback ()**. Veremos como iniciar o bloco de notas a partir desse comando na próxima seção.

## <a name="change-the-menu-command-handler"></a>Alterar o manipulador de comandos de menu

Agora, vamos atualizar o manipulador de comandos para iniciar o bloco de notas.

1. Pare a depuração e volte para sua instância de trabalho do Visual Studio. Abra o arquivo *FirstCommand.cs* e adicione a seguinte instrução Using:

    ```csharp
    using System.Diagnostics;
    ```

2. Localize o Construtor FirstCommand privado. É aí que o comando é conectado ao serviço de comando e o manipulador de comandos é especificado. Altere o nome do manipulador de comandos para StartNotepad, da seguinte maneira:

    ```csharp
    private FirstCommand(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        CommandID menuCommandID = new CommandID(CommandSet, CommandId);
        // Change to StartNotepad handler.
        MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

3. Remova o `MenuItemCallback` método e adicione um `StartNotepad` método, que apenas iniciará o bloco de notas:

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. Agora experimente. Ao iniciar a depuração do projeto e clicar em **ferramentas**  >  **invocar FirstCommand**, você deverá ver uma instância do bloco de notas aparecer.

    Você pode usar uma instância da <xref:System.Diagnostics.Process> classe para executar qualquer executável, não apenas o bloco de notas. Experimente `calc.exe` , por exemplo,.

## <a name="clean-up-the-experimental-environment"></a>Limpar o ambiente experimental

Se você estiver desenvolvendo várias extensões ou apenas explorando resultados com versões diferentes do seu código de extensão, seu ambiente experimental pode parar de funcionar da maneira que deveria. Nesse caso, você deve executar o script de redefinição. Ele é chamado **redefinir a instância experimental do Visual Studio**e é fornecido como parte do SDK do Visual Studio. Esse script remove todas as referências às suas extensões do ambiente experimental, para que você possa começar do zero.

Você pode acessar esse script de uma das duas maneiras:

1. Na área de trabalho, localize **redefinir a instância experimental do Visual Studio**.

2. Na linha de comando, execute o seguinte:

    ```xml
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>Implantar sua extensão

Agora que você tem sua extensão de ferramenta em execução da maneira desejada, é hora de pensar em compartilhá-la com seus amigos e colegas. Isso é fácil, desde que tenha o Visual Studio 2015 instalado. Tudo o que você precisa fazer é enviar a eles o arquivo *. vsix* que você criou. (Não se esqueça de compilá-lo no modo de liberação.)

Você pode encontrar o arquivo *. vsix* para essa extensão no diretório bin do *FirstMenuCommand* . Especificamente, supondo que você criou a configuração de versão, ela estará em:

*\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\ FirstMenuCommand. vsix*

Para instalar a extensão, seu amigo precisa fechar todas as instâncias abertas do Visual Studio e clicar duas vezes no arquivo *. vsix* , que abre o instalador do **VSIX**. Os arquivos são copiados para o diretório *%LocalAppData%\Microsoft\VisualStudio \<version> \Extensions* .

Quando o seu amigo abre o Visual Studio novamente, ele encontrará a extensão FirstMenuCommand em **ferramentas**  >  **extensões e atualizações**. Eles podem acessar **extensões e atualizações** para desinstalar ou desabilitar a extensão também.

## <a name="next-steps"></a>Próximas etapas

Este tutorial mostrou apenas uma pequena parte do que você pode fazer com uma extensão do Visual Studio. Aqui está uma lista curta de outras coisas (razoavelmente simples) que você pode fazer com as extensões do Visual Studio:

1. Você pode fazer muitas coisas com um comando de menu simples:

   1. Adicione seu próprio ícone: [Adicionar ícones a comandos de menu](../extensibility/adding-icons-to-menu-commands.md)

   2. Alterar o texto do comando de menu: [alterar o texto de um comando de menu](../extensibility/changing-the-text-of-a-menu-command.md)

   3. Adicionar um atalho de menu a um comando: [associar atalhos de teclado a itens de menu](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. Adicionar diferentes tipos de comandos, menus e barras de ferramentas: [estender menus e comandos](../extensibility/extending-menus-and-commands.md)

3. Adicionar janelas de ferramentas e estender as janelas de ferramentas internas do Visual Studio: [estender e personalizar o Windows](../extensibility/extending-and-customizing-tool-windows.md)

4. Adicionar IntelliSense, sugestões de código e outros recursos a editores de código existentes: [estenda o editor e os serviços de linguagem](../extensibility/extending-the-editor-and-language-services.md)

5. Adicionar opções e páginas de propriedades e configurações de usuário à sua extensão: [estender Propriedades e janela de propriedades](../extensibility/extending-properties-and-the-property-window.md) e [estender as configurações e opções de usuário](../extensibility/extending-user-settings-and-options.md)

   Outros tipos de extensões exigem um pouco mais de trabalho, como criar um novo tipo de projeto ([estender projetos](../extensibility/extending-projects.md)), criar um novo tipo de editor ([criar editores e designers personalizados](../extensibility/creating-custom-editors-and-designers.md)) ou implementar sua extensão em um shell isolado: [shell isolado do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
