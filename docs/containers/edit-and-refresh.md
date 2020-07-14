---
title: Depurar aplicativos em um contêiner do Docker local | Microsoft Docs
description: Saiba como modificar um aplicativo que está sendo executado em um contêiner do Docker local, atualize o contêiner por meio de editar e atualizar e, em seguida, defina pontos de interrupção de depuração.
ms.author: ghogen
author: ghogen
manager: jillfra
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.topic: how-to
ms.workload: multiple
ms.date: 07/25/2019
ms.technology: vs-azure
ms.openlocfilehash: 26562268167abdfc5ee643618ec1610da231f9f0
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283158"
---
# <a name="debug-apps-in-a-local-docker-container"></a>Depurar aplicativos em um contêiner do Docker local

O Visual Studio fornece uma maneira consistente de desenvolver contêineres do Docker e validar seu aplicativo localmente. Você pode executar e depurar seus aplicativos em contêineres do Linux ou do Windows em execução na área de trabalho do Windows local com o Docker instalado e não precisa reiniciar o contêiner sempre que fizer uma alteração no código.

Este artigo ilustra como usar o Visual Studio para iniciar um aplicativo em um contêiner do Docker local, fazer alterações e, em seguida, atualizar o navegador para ver as alterações. Este artigo também mostra como definir pontos de interrupção para depuração de aplicativos em contêineres. Os tipos de projeto com suporte incluem .NET Framework e .NET Core Web e aplicativos de console. Neste artigo, usamos ASP.NET Core aplicativos Web e .NET Framework aplicativos de console.

Se você já tiver um projeto de um tipo com suporte, o Visual Studio poderá criar um Dockerfile e configurar seu projeto para ser executado em um contêiner. Consulte [ferramentas de contêiner no Visual Studio](overview.md).

## <a name="prerequisites"></a>Pré-requisitos

Para depurar aplicativos em um contêiner do Docker local, as seguintes ferramentas devem ser instaladas:

::: moniker range="vs-2017"

* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) com a carga de trabalho de desenvolvimento para a Web instalada

::: moniker-end

::: moniker range="vs-2019"

* [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com a carga de trabalho de desenvolvimento para a Web instalada

::: moniker-end

Para executar os contêineres do Docker localmente, você deve ter um cliente Docker local. Você pode usar a [caixa de ferramentas do Docker](https://www.docker.com/products/docker-toolbox), que requer que o Hyper-V seja desabilitado. Você também pode usar [Docker for Windows](https://www.docker.com/get-docker), que usa o Hyper-V e requer o Windows 10.

Os contêineres do Docker estão disponíveis para projetos .NET Framework e .NET Core. Vamos analisar dois exemplos. Primeiro, examinamos um aplicativo Web .NET Core. Em seguida, examinamos um aplicativo de console .NET Framework.

## <a name="create-a-web-app"></a>Criar um aplicativo Web

Se você tiver um projeto e tiver adicionado o suporte do Docker, conforme descrito na [visão geral](overview.md), ignore esta seção.

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">= vs-2019"
[!INCLUDE [create-aspnet5-app-2019](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

### <a name="edit-your-code-and-refresh"></a>Editar seu código e atualizar

Para iterar alterações rapidamente, você pode iniciar o aplicativo em um contêiner. Em seguida, continue a fazer alterações, exibindo-as como você faria com IIS Express.

1. Verifique se o Docker está configurado para usar o tipo de contêiner (Linux ou Windows) que você está usando. Clique com o botão direito do mouse no ícone do Docker na barra de tarefas e escolha **alternar para contêineres do Linux** ou **alternar para contêineres do Windows** conforme apropriado.

1. (Somente .NET Core 3 e posterior) Editar seu código e atualizar o site em execução, conforme descrito nesta seção, não está habilitado nos modelos padrão no .NET Core >= 3,0. Para habilitá-lo, adicione o pacote NuGet [Microsoft. AspNetCore. Mvc. Razor. RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/). No *Startup.cs*, adicione uma chamada para o método de extensão `IMvcBuilder.AddRazorRuntimeCompilation` ao código no `ConfigureServices` método. Você só precisa dessa habilitação no modo de depuração, portanto, codifique-o da seguinte maneira:

    ```csharp
    public IWebHostEnvironment Env { get; set; }
    
    public void ConfigureServices(IServiceCollection services)
    {
        IMvcBuilder builder = services.AddRazorPages();
    
    #if DEBUG
        if (Env.IsDevelopment())
        {
            builder.AddRazorRuntimeCompilation();
        }
    #endif
    
        // code omitted for brevity
    }
    ```

    Modifique o `Startup` método da seguinte maneira:

    ```csharp
    public Startup(IConfiguration configuration, IWebHostEnvironment webHostEnvironment)
    {
        Configuration = configuration;
        Env = webHostEnvironment;
    }
    ```

   Para obter mais informações, consulte [compilação de arquivo Razor no ASP.NET Core](/aspnet/core/mvc/views/view-compilation?view=aspnetcore-3.1).

1. Defina a **configuração da solução** como **depurar**. Em seguida, pressione **Ctrl** + **F5** para criar a imagem do Docker e executá-la localmente.

    Quando a imagem de contêiner é criada e executada em um contêiner do Docker, o Visual Studio inicia o aplicativo Web no navegador padrão.

1. Vá para a página de *índice* . Vamos fazer alterações nessa página.
1. Retorne ao Visual Studio e abra *index. cshtml*.
1. Adicione o seguinte conteúdo HTML ao final do arquivo e salve as alterações.

    ```html
    <h1>Hello from a Docker container!</h1>
    ```

1. Na janela saída, quando o Build do .NET for concluído e você vir as seguintes linhas, volte para o navegador e atualize a página:

   ```output
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down.
   ```

As alterações foram aplicadas.

### <a name="debug-with-breakpoints"></a>Depurar com pontos de interrupção

Geralmente, as alterações exigem uma inspeção mais detalhada. Você pode usar os recursos de depuração do Visual Studio para essa tarefa.

1. No Visual Studio, abra *index.cshtml.cs*.
2. Substitua o conteúdo do `OnGet` método pelo código a seguir:

   ```csharp
       ViewData["Message"] = "Your application description page from within a container";
   ```

3. À esquerda da linha de código, defina um ponto de interrupção.
4. Para iniciar a depuração e atingir o ponto de interrupção, pressione F5.
5. Alterne para o Visual Studio para exibir o ponto de interrupção. Inspecione os valores.

   ![Ponto de interrupção](media/edit-and-refresh/breakpoint.png)

## <a name="create-a-net-framework-console-app"></a>Criar um aplicativo de console .NET Framework

Quando você usa .NET Framework projetos de aplicativo de console, não há suporte para a opção de adicionar suporte do Docker sem orquestração. Você ainda pode usar o procedimento a seguir, mesmo se você estiver usando apenas um único projeto do Docker.

1. Crie um novo projeto de aplicativo de console .NET Framework.
1. Em Gerenciador de soluções, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **suporte à orquestração de contêiner**.  Na caixa de diálogo que aparece, selecione **Docker Compose**. Um Dockerfile é adicionado ao seu projeto e um Docker Compose projeto com arquivos de suporte associados é adicionado.

### <a name="debug-with-breakpoints"></a>Depurar com pontos de interrupção

1. Em Gerenciador de Soluções, abra *Program.cs*.
2. Substitua o conteúdo do `Main` método pelo código a seguir:

   ```csharp
       System.Console.WriteLine("Hello, world!");
   ```

3. Defina um ponto de interrupção à esquerda da linha de código.
4. Pressione F5 para iniciar a depuração e atingir o ponto de interrupção.
5. Alterne para o Visual Studio para exibir os valores de ponto de interrupção e inspecionar.

   ![Ponto de interrupção](media/edit-and-refresh/breakpoint-console.png)

## <a name="container-reuse"></a>Reutilização de contêiner

Durante o ciclo de desenvolvimento, o Visual Studio recria apenas as imagens de contêiner e o próprio contêiner quando você altera o Dockerfile. Se você não alterar o Dockerfile, o Visual Studio reutiliza o contêiner de uma execução anterior.

Se você modificou manualmente o contêiner e deseja reiniciar com uma imagem de contêiner limpa, use o comando **Compilar**  >  **limpar** no Visual Studio e, em seguida, compile normalmente.

## <a name="troubleshoot"></a>Solucionar problemas

Saiba como [solucionar problemas de desenvolvimento do Docker do Visual Studio](troubleshooting-docker-errors.md).

## <a name="next-steps"></a>Próximas etapas

Obtenha mais detalhes lendo [como o Visual Studio cria aplicativos em contêineres](container-build.md).

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Mais informações sobre o Docker com o Visual Studio, Windows e Azure

* Saiba mais sobre o [desenvolvimento de contêineres com o Visual Studio](/visualstudio/containers).
* Para criar e implantar um contêiner do Docker, consulte [integração do Docker para Azure pipelines](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).
* Para obter um índice de artigos do Windows Server e do nano Server, consulte [informações do contêiner do Windows](/virtualization/windowscontainers/).
* Saiba mais sobre o [serviço kubernetes do Azure](https://azure.microsoft.com/services/kubernetes-service/) e examine a [documentação do serviço kubernetes do Azure](/azure/aks).
