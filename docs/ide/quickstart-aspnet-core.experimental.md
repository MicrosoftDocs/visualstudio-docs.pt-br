---
title: Usar o Visual Studio para criar um aplicativo Web ASP.NET Core em C#
description: Saiba como criar um aplicativo Web simples do Olá, Mundo no Visual Studio com C# e ASP.NET Core, passo a passo.
ms.custom: mvc
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: quickstart
author: TerryGLee
ms.author: tglee
manager: douge
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: e85650f6671684f2d0ed313603f1af88e608e1d9
ms.sourcegitcommit: 401be39a42ffe007593528b5bba62583ca9fcafd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244418"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-app"></a>Início rápido: Usar o Visual Studio para criar seu primeiro aplicativo Web ASP.NET Core

Nesta introdução de 5 a 10 minutos que mostra como usar o Visual Studio, você criará um aplicativo Web "Olá, Mundo" simples usando um modelo de projeto ASP.NET e a linguagem de programação C#.

## <a name="before-you-begin"></a>Antes de começar

### <a name="install-visual-studio"></a>Instalar o Visual Studio

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

### <a name="update-visual-studio"></a>Atualizar o Visual Studio

Se você já tiver instalado o Visual Studio, verifique se está executando a versão mais recente. Para obter mais informações de como atualizar sua instalação, confira a página [Atualizar o Visual Studio 2017 para a versão mais recente](../install/update-visual-studio.md).

### <a name="choose-your-theme-optional"></a>Escolher o tema (opcional)

Este tutorial de início rápido inclui capturas de tela que usam o tema escuro. Se você não estiver usando o tema escuro, mas quiser usá-lo, confira a página [Personalizar o IDE e o Editor do Visual Studio](quickstart-personalize-the-ide.md) para saber como.

## <a name="create-a-project"></a>Criar um projeto

Para começar, você criará um projeto de aplicativo Web ASP.NET Core. Veja como.

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. No painel esquerdo da caixa de diálogo **Novo Projeto**, expanda **Visual C#** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo Web ASP.NET Core**. Em seguida, nomeie o arquivo `HelloWorld` e escolha **OK**.

1. Na caixa de diálogo **Novo Aplicativo Web ASP.NET Core**, selecione **ASP.NET Core 2.0** ou posterior no menu suspenso superior e, em seguida, escolha **Aplicativo Web**.

   > [!NOTE]
   > Se o **ASP.NET Core 2.0** ou posterior não for exibido no menu suspenso superior, verifique se você está executando a versão mais recente do Visual Studio. Para obter mais informações de como atualizar sua instalação, confira a página [Atualizar o Visual Studio 2017 para a versão mais recente](../install/update-visual-studio.md).

   ![Exibir o arquivo .gif animado que mostra como criar um projeto ASP.NET Core C# no Visual Studio](../ide/media/csharp-aspnet-animated-create-project.gif)

   Logo depois, o Visual Studio abre o arquivo de projeto.

   > [!NOTE]
   > Se você não vir a categoria de modelo de projeto **.NET Core**, escolha o link **Abrir Instalador do Visual Studio** no painel esquerdo. (Dependendo das suas configurações de exibição, talvez seja necessário rolar para vê-la.)
   >
   > ![Abrir Instalador do Visual Studio na caixa de diálogo Novo Projeto](../ide/media/open-visual-studio-installer.png)
   >
   > O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.
   >
   > ![Carga de trabalho ASP.NET no instalador do VS](../ide/media/quickstart-aspnet-workload.png)
   >
   > (Talvez você precise fechar o Visual Studio antes de continuar a instalar a nova carga de trabalho.)

## <a name="create-and-run-the-app"></a>Criar e executar o aplicativo

Em seguida, você criará e executará o aplicativo Web "Olá, Mundo". Veja como.

1. No Visual Studio, no **Gerenciador de Soluções**, expanda a pasta **Páginas**. Em seguida, escolha **About.cshtml**.

   ![Escolha o arquivo About.cshtml no Gerenciador de Soluções](../ide/media/csharp-aspnet-about-page-html-file.png)

   Este arquivo corresponde a uma página chamada **Sobre** no aplicativo web, que é executada no navegador da web.

   ![A página Sobre no aplicativo Web](../ide/media/csharp-aspnet-about-page.png)

1. No editor de código do Visual Studio, altere o texto de "informações adicionais" para dizer "**Olá, Mundo!**".

1. No **Gerenciador de Soluções**, expanda **About.cshtml** e, em seguida, escolha **About.cshtml.cs**.

1. Alterar o texto da mensagem de "Descrição do aplicativo" para dizer "**Qual é a minha mensagem?**".

1. Escolha **IIS Express** ou pressione **Ctrl**+**F5** para executar o aplicativo e abri-lo em um navegador da Web.

   ![Exibir o arquivo .gif animado que mostra como criar e executar um aplicativo Web ASP.NET Core C# no Visual Studio](../ide/media/csharp-aspnet-animated-hello-world.gif)

   > [!NOTE]
   > Se você receber uma mensagem de erro informando **Não é possível conectar ao servidor Web 'IIS Express'** ou uma mensagem de erro que mencione um certificado SSL, feche o Visual Studio. Em seguida, abra o Visual Studio usando a opção **Executar como administrador** no menu de contexto ou no menu acessado ao clicar com o botão direito do mouse. Em seguida, execute o aplicativo novamente.

1. No navegador da Web, verifique se a página **Sobre** inclui o texto atualizado.

1. Feche o navegador da Web.

Parabéns por concluir este Guia de Início Rápido! Esperamos que você tenha aprendido um pouco sobre o C#, o ASP.NET Core e o IDE (ambiente de desenvolvimento integrado) do Visual Studio.

## <a name="next-steps"></a>Próximas etapas

Para saber mais, continue com o tutorial a seguir:

> [!div class="nextstepaction"]
> [Introdução ao C# e ao ASP.NET no Visual Studio](tutorial-csharp-aspnet-core.md)

## <a name="see-also"></a>Consulte também

[Publicar seu aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio](..//deployment/quickstart-deploy-to-azure.md)
