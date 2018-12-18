---
title: 'Início rápido: Criar um serviço Web ASP.NET Core no F#'
description: Saiba como criar um serviço Web do ASP.NET Core no Visual Studio com F#, passo a passo.
ms.date: 08/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: quickstart
author: cartermp
ms.author: phcart
manager: andrehal
dev_langs:
- FSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 884dfec4d3b8050fa6059cb0f505e1c7619336f9
ms.sourcegitcommit: d705e015cb525bfa87a0b93e93376c3956ec2707
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43224766"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-service-in-f"></a>Início rápido: Usar o Visual Studio para criar seu primeiro serviço Web ASP.NET Core no F#

Nesta introdução de 5 a 10 minutos para o F# no Visual Studio, você criará um aplicativo Web ASP.NET Core em F#.

Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de API Web do ASP.NET Core. O tipo de projeto vem com arquivos de modelo que constituem um serviço Web funcional, mesmo sem adicionar nada!

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

3. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda **Visual F#** e, em seguida, escolha **Web**. No painel central, escolha **Aplicativo Web ASP.NET Core** e, em seguida, selecione **OK**.

     Se você não vir a categoria de modelo de projeto **.NET Core**, escolha o link **Abrir Instalador do Visual Studio** no painel esquerdo. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho ASP.NET no instalador do VS](../ide/media/quickstart-aspnet-workload.png)

4. Na caixa de diálogo **Novo aplicativo Web ASP.NET Core**, selecione **ASP.NET Core 2.1** no menu suspenso superior. (Se o **ASP.NET Core 2.1** não aparecer na lista, instale-o seguindo o link **Baixar** que deve aparecer em uma barra amarela próxima à parte superior da caixa de diálogo.) Escolha **OK**.

## <a name="explore-the-ide"></a>Explorar o IDE

1. Na barra de ferramentas **Gerenciador de Soluções**, expanda a pasta **Controladores** e, em seguida, escolha **ValuesController.fs** para abri-lo no editor.

   ![Gerenciador de Soluções com a pasta Controladores expandida no projeto de API Web em F#](../ide/media/hello-world-fs-sln-explorer.png)

2. Em seguida, modifique o membro `Get()` para que ele seja o seguinte:

   ```fsharp
   [<HttpGet>]
   member this.Get() =
       let values = [|"Hello"; "World"; "First F#/ASP.NET Core web API!"|]
       ActionResult<string[]>(values)
   ```

O código é simples. Uma matriz de valores de F# é associada ao nome de `values` e, em seguida, é passada para a estrutura MVC do ASP.NET Core como um `ActionResult`. O ASP.NET Core cuida do resto para você.

Isso deve ter esta aparência no editor:

![Membro Get modificado](../ide/media/hello-world-fs-get-member.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **Ctrl**+**F5** para executar o aplicativo e abri-lo em um navegador da Web.

2. A página deverá navegar até a rota `/api/values`, mas, se isso não ocorrer, insira `https://localhost:44396/api/values` no seu navegador.

Agora, o navegador da Web exibirá um JSON correspondente ao que você digitou anteriormente.

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este Guia de Início Rápido! Esperamos que você tenha aprendido um pouco sobre o F#, o ASP.NET Core e o IDE do Visual Studio. Para ver o aplicativo em execução em um servidor público, selecione o botão a seguir.

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Azure](../deployment/quickstart-deploy-to-azure.md)

Para saber mais sobre o F#, confira o [Guia de F#](/dotnet/fsharp/index) oficial.