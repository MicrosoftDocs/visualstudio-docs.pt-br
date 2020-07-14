---
title: Tutorial de extensão de Olá, Mundo | Microsoft Docs
ms.date: 03/14/2019
ms.topic: tutorial
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 796cb53ea5124662c695cce55241794802f042c0
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905931"
---
# <a name="tutorial---create-your-first-extension-hello-world"></a>Tutorial – Crie sua primeira extensão: Olá, Mundo

Este Olá, Mundo exemplo orienta você pela criação da sua primeira extensão para o Visual Studio. Este tutorial mostra como adicionar um novo comando ao Visual Studio.

No processo, você aprenderá a:

* **[Criar um projeto de extensibilidade](#create-an-extensibility-project)**
* **[Adicionar um comando personalizado](#add-a-custom-command)**
* **[Modificar o código-fonte](#modify-the-source-code)**
* **[Execute-o.](#run-it)**

Para este exemplo, você usará o Visual C# para adicionar um botão de menu personalizado chamado "Diga Olá, Mundo!" Isso se parece com este:

![Olá, Mundo comando](media/hello-world-say-hello-world.png)

> [!NOTE]
> Este artigo se aplica ao Visual Studio no Windows. Para Visual Studio para Mac, consulte [passo a passos de extensibilidade no Visual Studio para Mac](/visualstudio/mac/extending-visual-studio-mac-walkthrough).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você instalou a carga de trabalho de **desenvolvimento de extensão do Visual Studio** , que inclui o modelo VSIX que você precisará e o código de exemplo.

> [!NOTE]
> Você pode usar qualquer edição do Visual Studio (Community, Professional ou Enterprise) para criar um projeto de extensibilidade do Visual Studio.

## <a name="create-an-extensibility-project"></a>Criar um projeto de extensibilidade

::: moniker range="vs-2017"

Etapa 1. No menu **Arquivo**, selecione **Novo** > **Projeto**.

Etapa 2. Na caixa de pesquisa no canto superior direito, digite "VSIX" e selecione o **projeto VSIX**do Visual C#. Digite "HelloWorld" para o **nome** na parte inferior da caixa de diálogo e selecione **OK**.

![novo projeto](media/hello-world-new-project.png)

Agora você deve ver a página Introdução e alguns recursos de exemplo.

Se você precisar sair deste tutorial e voltar a ele, poderá encontrar o novo projeto HelloWorld na **página inicial** na seção **recente** .

::: moniker-end

::: moniker range=">=vs-2019"

Etapa 1. No menu **Arquivo**, selecione **Novo** > **Projeto**. Pesquise "VSIX" e selecione o **projeto VSIX** do Visual C# e, em seguida, **Avançar**.

Etapa 2. Digite "HelloWorld" para o **nome do projeto** e selecione **criar**.

![novo projeto](media/hello-world-new-project-2019.png)

Agora você deve ver o projeto HelloWorld no **Gerenciador de soluções**.

::: moniker-end

## <a name="add-a-custom-command"></a>Adicionar um comando personalizado

Etapa 1. Se você selecionar o arquivo de manifesto *. vsixmanifest* , poderá ver quais opções são alteráveis, como descrição, autor e versão.

Etapa 2. Clique com o botão direito do mouse no projeto (não na solução). No menu de contexto, selecione **Adicionar**e **novo item**.

Etapa 3. Selecione a seção **extensibilidade** e, em seguida, escolha **comando**.

Etapa 4. No campo **nome** na parte inferior, insira um nome de arquivo, como *Command.cs*.

![comando personalizado](media/hello-world-vsix-command.png)

O novo arquivo de comando está visível no **Gerenciador de soluções**. No nó **recursos** , você encontrará outros arquivos relacionados ao comando. Por exemplo, se você quiser modificar a imagem, o arquivo PNG estará aqui.

## <a name="modify-the-source-code"></a>Modificar o código-fonte

Neste ponto, o comando e o texto do botão são gerados automaticamente e não são muito interessantes. Você pode modificar o arquivo VSCT e o arquivo CS se quiser fazer alterações.

* O arquivo VSCT é onde você pode renomear seus comandos, bem como definir onde eles vão no sistema de comandos do Visual Studio. Ao explorar o arquivo VSCT, você notará comentários que explicam o que cada seção dos controles de código VSCT.

* O arquivo CS é onde você pode definir ações, como o manipulador de cliques.

::: moniker range="vs-2017"

Etapa 1. Em **Gerenciador de soluções**, localize o arquivo vsct para o novo comando. Nesse caso, ele será chamado de *CommandPackage. vsct*.

![pacote de comando vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

Etapa 1. Em **Gerenciador de soluções**, localize o arquivo vsct para sua extensão vs Package. Nesse caso, ele será chamado de *HelloWorldPackage. vsct*.

::: moniker-end

Etapa 2. Altere o `ButtonText` parâmetro para `Say Hello World!` .

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

Etapa 3. Volte para **Gerenciador de soluções** e localize o arquivo *Command.cs* . No `Execute` método, altere a cadeia `message` de caracteres de `string.Format(..)` para `Hello World!` .

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

Certifique-se de salvar as alterações em cada arquivo.

## <a name="run-it"></a>Execute-o.

Agora você pode executar o código-fonte na instância experimental do Visual Studio.

Etapa 1. Pressione **F5** para executar o comando **Iniciar Depuração** . Este comando cria seu projeto e inicia o depurador, iniciando uma nova instância do Visual Studio chamada de **instância experimental**.

::: moniker range="vs-2017"

Você verá a instância de palavras **experimentais** na barra de título do Visual Studio.

![barra de título de instância experimental](media/hello-world-exp-instance.png)

::: moniker-end

Etapa 2. No menu **ferramentas** da **instância experimental**, clique em **dizer Olá, mundo!**.

![resultado final](media/hello-world-final-result.png)

Você deve ver a saída do seu novo comando personalizado, neste caso, a caixa de diálogo no centro da tela que fornece a **Olá, mundo!** mensagem.

## <a name="next-steps"></a>Próximas etapas

Agora que você conhece as noções básicas do trabalho com a extensibilidade do Visual Studio, aqui está onde você pode saber mais:

* [Comece a desenvolver as extensões do Visual Studio](starting-to-develop-visual-studio-extensions.md) -exemplos, tutoriais. e publicando sua extensão
* [O que há de novo no SDK do visual studio 2017](what-s-new-in-the-visual-studio-2017-sdk.md) -novos recursos de extensibilidade no Visual Studio 2017
* [O que há de novo no SDK do visual studio 2019](whats-new-visual-studio-2019-sdk.md) -novos recursos de extensibilidade no Visual Studio 2019
* [Dentro do SDK do Visual Studio](internals/inside-the-visual-studio-sdk.md) -Conheça os detalhes da extensibilidade do Visual Studio
