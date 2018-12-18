---
title: Tutorial de extensão do Hello World | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e2122a98778372690990a75269be2f3087653678
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349459"
---
# <a name="create-your-first-extension-hello-world"></a>Criar sua primeira extensão: Olá, mundo

Este exemplo de Hello World explica como criar sua primeira extensão para o Visual Studio. Este tutorial mostra como adicionar um novo comando para o Visual Studio.

O processo, você aprenderá como:

* **[Criar um projeto de extensibilidade](#create-an-extensibility-project)**
* **[Adicionar um comando personalizado](#add-a-custom-command)**
* **[Modificar o código-fonte](#modify-the-source-code)**
* **[Executá-lo](#run-it)**

Neste exemplo, você usará o Visual c# para adicionar que um botão de menu personalizado chamado "Diga Hello World!" Isso se parece com isso:

![Comando do Hello World](media/hello-world-say-hello-world.png)

> [!NOTE]
> Este artigo se aplica ao Visual Studio no Windows. Para o Visual Studio para Mac, consulte [instruções passo a passo de extensibilidade no Visual Studio para Mac](/visualstudio/mac/extending-visual-studio-mac-walkthrough).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você instalou o **desenvolvimento de extensões do Visual Studio** carga de trabalho que inclui o modelo VSIX, você precisará e código de exemplo.

> [!NOTE]
> Você pode usar qualquer edição do Visual Studio (Community, Professional ou Enterprise) para criar um projeto de extensibilidade do Visual Studio.

## <a name="create-an-extensibility-project"></a>Criar um projeto de extensibilidade

Etapa 1. Dos **arquivo** menu, clique em **novo projeto**. Na parte inferior da tela, insira o nome do seu projeto.

Etapa 2. Dos **modelos** menu, clique em **Visual c#**, clique em **extensibilidade**e, em seguida, clique em **projeto VSIX**.

![novo projeto](media/hello-world-new-project.png)

Agora você deve ver a página de Introdução e alguns recursos de exemplo.

Se você precisar deixar este tutorial e volte a ela, você pode encontrar seu novo projeto HelloWorld na **página inicial** na **recentes** seção.

## <a name="add-a-custom-command"></a>Adicionar um comando personalizado

Etapa 1. Se você selecionar o manifesto, você pode ver quais opções estão mutáveis, para a instância, metadados, descrição e versão.

Etapa 2. Clique com botão direito no projeto (não na solução). No menu de contexto, clique em **Add**e, em seguida, clique em **Novo Item**.

Etapa 3. Selecione o **extensibilidade** seção e, em seguida, clique em **comando personalizado**.

Etapa 4. No **nome** campo na parte inferior, dê a ele um nome, por exemplo *Command.cs*.

![comando personalizado](media/hello-world-custom-command.png)

Novo comando está listado na **Gerenciador de soluções** sob o **recursos** branch. Isso também é onde você encontrará outros arquivos relacionados ao seu comando, como os arquivos PNG e ICO, se você quiser modificar a imagem.

## <a name="modify-the-source-code"></a>Modificar o código-fonte

Neste ponto, o botão que você está adicionando está bastante genérico. Você precisará modificar o arquivo VSCT e o arquivo de CS se você quiser fazer alterações.

* O arquivo VSCT é onde você pode renomear os comandos, bem como definir onde eles ficar no sistema de comando do Visual Studio. Conforme você explora o arquivo VSCT, você observará muito código comentado que explica o que cada seção de controles de código.

* O arquivo de CS é onde você pode definir a ações, como o manipulador de clique.

Etapa 1. Na **Gerenciador de soluções**, localize o arquivo VSCT para seu novo comando. Nesse caso, ele será chamado *CommandPackage.vsct*.

![comando pacote vsct](media/hello-world-command-package-vsct.png)

Etapa 2. Alterar o `ButtonText` parâmetro para `Say Hello World!`.

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

Etapa 3. Volte para **Gerenciador de soluções** e localize o *Command.cs* arquivo. Alterar a cadeia de caracteres `message` para o comando `string.Format(..)` para `Hello World!`.

```csharp
  ...
  private void MenuItemCallback(object sender, EventArgs e)
  {
    string message = "Hello World!";
    string title = "Command1";

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

Certifique-se de salvar suas alterações para cada arquivo.

## <a name="run-it"></a>Executá-lo

Agora você pode executar o código-fonte em que a instância Experimental do Visual Studio.

Etapa 1. Clique em **iniciar** na barra de ferramentas. Isso compila seu projeto e inicia o depurador, iniciando uma nova instância do Visual Studio chamada a **instância Experimental**.

Você verá as palavras **instância Experimental** na barra de título do Visual Studio.

![barra de título da instância experimental](media/hello-world-exp-instance.png)

Etapa 2. Sobre o **ferramentas** menu da **instância Experimental**, clique em **Say Hello World!**.

![resultado final](media/hello-world-final-result.png)

Você deverá ver a saída do novo comando personalizado, neste caso, a caixa de diálogo no centro da tela que lhe dá o **Olá, mundo!** .

## <a name="next-steps"></a>Próximas etapas

Agora que você conhece os fundamentos de trabalhar com a extensibilidade do Visual Studio, aqui é onde você pode saber mais:

* [Começar a desenvolver extensões do Visual Studio](starting-to-develop-visual-studio-extensions.md) -exemplos, tutoriais. e publicar sua extensão
* [O que há de novo no SDK do Visual Studio 2017](what-s-new-in-the-visual-studio-2017-sdk.md) -novos recursos de extensibilidade do Visual Studio 2017
* [Dentro do Visual Studio SDK](internals/inside-the-visual-studio-sdk.md) -Conheça os detalhes de extensibilidade do Visual Studio