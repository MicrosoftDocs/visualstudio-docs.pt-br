---
title: Tutorial de extensão do Hello World | Microsoft Docs
ms.date: 03/14/2019
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c66f48a4b3c5948393e10f34810f3cb87c78c924
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711656"
---
# <a name="create-your-first-extension-hello-world"></a>Crie sua primeira extensão: Hello World

Este exemplo do Hello World orienta você a criar sua primeira extensão para o Visual Studio. Este tutorial mostra como adicionar um novo comando ao Visual Studio.

No processo, você aprenderá como:

* **[Crie um projeto de extensibilidade](#create-an-extensibility-project)**
* **[Adicione um comando personalizado](#add-a-custom-command)**
* **[Modificar o código-fonte](#modify-the-source-code)**
* **[Execute-o.](#run-it)**

Para este exemplo, você usará o Visual C# para adicionar um botão de menu personalizado chamado "Say Hello World!" que se parece com isso:

![Olá comando mundial](media/hello-world-say-hello-world.png)

> [!NOTE]
> Este artigo se aplica ao Visual Studio no Windows. Para visual studio para Mac, consulte [Extensibility walkthrough no Visual Studio for Mac](/visualstudio/mac/extending-visual-studio-mac-walkthrough).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de ter instalado a carga de trabalho de desenvolvimento de **extensão do Visual Studio,** que inclui o modelo VSIX que você precisará e o código de exemplo.

> [!NOTE]
> Você pode usar qualquer edição do Visual Studio (Community, Professional ou Enterprise) para criar um projeto de extensibilidade do Visual Studio.

## <a name="create-an-extensibility-project"></a>Crie um projeto de extensibilidade

::: moniker range="vs-2017"

Etapa 1. No menu **Arquivo**, selecione **Novo** > **Projeto**.

Etapa 2. Na caixa de pesquisa no canto superior direito, digite "vsix" e selecione o Projeto Visual C# **VSIX**. Digite "HelloWorld" para o **Nome** na parte inferior da caixa de diálogo e selecione **OK**.

![novo projeto](media/hello-world-new-project.png)

Agora você deve ver a página Como começar e alguns recursos de amostra.

Se você precisar deixar este tutorial e voltar para ele, você pode encontrar seu novo projeto HelloWorld na **Página inicial** na seção **Recente.**

::: moniker-end

::: moniker range=">=vs-2019"

Etapa 1. No menu **Arquivo**, selecione **Novo** > **Projeto**. Procure por "vsix" e selecione o Projeto Visual C# **VSIX** e, em **seguida, Next**.

Etapa 2. Digite "HelloWorld" para o nome do **projeto** e selecione **Criar**.

![novo projeto](media/hello-world-new-project-2019.png)

Agora você deve ver o projeto HelloWorld no **Solution Explorer**.

::: moniker-end

## <a name="add-a-custom-command"></a>Adicione um comando personalizado

Etapa 1. Se você selecionar o arquivo *manifesto .vsixmanifest,* poderá ver quais opções podem ser mutáveis, como descrição, autor e versão.

Etapa 2. Clique com o botão direito do mouse no projeto (não na solução). No menu de contexto, **selecione Adicionar** e, em seguida, **Novo Item**.

Etapa 3. Selecione a seção **Extensibility** e escolha **Comando**.

Etapa 4. No **campo Nome** na parte inferior, digite um nome de arquivo como *Command.cs*.

![comando personalizado](media/hello-world-vsix-command.png)

Seu novo arquivo de comando está visível no **Solution Explorer**. Sob o nó **Recursos,** você encontrará outros arquivos relacionados ao seu comando. Por exemplo, se você deseja modificar a imagem, o arquivo PNG está aqui.

## <a name="modify-the-source-code"></a>Modificar o código-fonte

Neste ponto, o comando e o texto button são gerados automaticamente e não são muito interessantes. Você pode modificar o arquivo VSCT e o arquivo CS se quiser fazer alterações.

* O arquivo VSCT é onde você pode renomear seus comandos, bem como definir para onde eles vão no sistema de comandos do Visual Studio. Ao explorar o arquivo VSCT, você notará comentários que explicam o que cada seção dos controles de código VSCT.

* O arquivo CS é onde você pode definir ações, como o manipulador de cliques.

::: moniker range="vs-2017"

Etapa 1. No **Solution Explorer,** encontre o arquivo VSCT para o seu novo comando. Neste caso, ele será chamado *commandPackage.vsct*.

![pacote de comando vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

Etapa 1. No **Solution Explorer,** encontre o arquivo VSCT para o pacote VS de extensão. Neste caso, ele se chamará *HelloWorldPackage.vsct*.

::: moniker-end

Etapa 2. Alterar `ButtonText` o parâmetro `Say Hello World!`para .

```xml
  ...
  <Button guid="guidCommandPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidCommandPackageCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
        <ButtonText>Say Hello World!</ButtonText>
     </Strings>
  </Button>
  ...
```

Etapa 3. Volte para **o Solution Explorer** e encontre o arquivo *Command.cs.* No `Execute` método, mude `message` a `string.Format(..)` `Hello World!`seqüência de para .

```csharp
  ...
  private void Execute(object sender, EventArgs e)
  {
    ThreadHelper.ThrowIfNotOnUIThread();
    string message = "Hello World!";
    string title = "Command";

    // Show a message box to prove we were here
    VsShellUtilities.ShowMessageBox(
        this.ServiceProvider,
        message,
        title,
        OLEMSGICON.OLEMSGICON_INFO,
        OLEMSGBUTTON.OLEMSGBUTTON_OK,
        OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST);
  }
  ...
```

Certifique-se de salvar suas alterações em cada arquivo.

## <a name="run-it"></a>Execute-o.

Agora você pode executar o código fonte na Instância Experimental do Visual Studio.

Etapa 1. Pressione **F5** para executar o comando **Iniciar depuração.** Este comando constrói seu projeto e inicia o depurador, lançando uma nova instância do Visual Studio chamada **De instância experimental**.

::: moniker range="vs-2017"

Você verá as palavras **Exemplo Experimental** na barra de título do Visual Studio.

![barra de título instância experimental](media/hello-world-exp-instance.png)

::: moniker-end

Etapa 2. No menu **Ferramentas** da **Instância Experimental**, clique em **Dizer Olá Mundo!**.

![resultado final](media/hello-world-final-result.png)

Você deve ver a saída do seu novo comando personalizado, neste caso o diálogo no centro da tela que lhe dá o **Hello World!** mensagem.

## <a name="next-steps"></a>Próximas etapas

Agora que você já sabe o básico de trabalhar com o Visual Studio Extensibility, aqui é onde você pode aprender mais:

* [Comece a desenvolver extensões do Visual Studio](starting-to-develop-visual-studio-extensions.md) - Amostras, tutoriais. e publicando sua extensão
* [Novidades no Visual Studio 2017 SDK](what-s-new-in-the-visual-studio-2017-sdk.md) - Novos recursos de extensibilidade no Visual Studio 2017
* [Novidades no Visual Studio 2019 SDK](whats-new-visual-studio-2019-sdk.md) - Novos recursos de extensibilidade no Visual Studio 2019
* [Dentro do Visual Studio SDK](internals/inside-the-visual-studio-sdk.md) - Conheça os detalhes da Extensibilidade visual studio
