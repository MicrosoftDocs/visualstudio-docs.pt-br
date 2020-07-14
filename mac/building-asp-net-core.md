---
title: Como compilar aplicativos ASP.NET Core
description: Este artigo descreve como começar a usar o ASP.NET no Visual Studio para Mac, incluindo como instalar e com criar um novo projeto.
author: sayedihashimi
ms.author: sayedha
ms.date: 05/30/2019
ms.assetid: 771C2F8E-46BC-4280-AFE8-ED9D5C7790CE
ms.topic: how-to
ms.openlocfilehash: b0337f283fe5bb78f2f63e2f3da12eb9f2679450
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939200"
---
# <a name="building-aspnet-core-applications-in-visual-studio-for-mac"></a>Como criar aplicativos ASP.NET Core no Visual Studio para Mac

O ASP.NET Core é uma estrutura open-source e multiplataforma para a criação de aplicativos modernos, conectados à Internet e baseados em nuvem, como serviços e aplicativos Web, aplicativos IoT e back-ends móveis. Os aplicativos ASP.NET Core podem ser executados nos runtimes do [.NET Core](https://www.microsoft.com/net/core/platform) ou do .NET Framework. Ele foi projetado para fornecer uma estrutura de desenvolvimento otimizada para aplicativos que são implantados na nuvem ou executados localmente. Ele consiste em componentes modulares com sobrecarga mínima, para que você mantenha a flexibilidade durante a construção de suas soluções. Você pode desenvolver e executar aplicativos ASP.NET Core de multiplataforma no Windows, Mac e Linux. O ASP.NET Core é um software livre no [GitHub](https://github.com/aspnet/home).

Neste laboratório, você criará e explorar um aplicativo ASP.NET Core com o Visual Studio para Mac.

## <a name="objectives"></a>Objetivos

> [!div class="checklist"]
> * Criar um aplicativo Web ASP.NET Core
> * Explorar o modelo de hospedagem, configuração e middleware do ASP.NET Core
> * Depurar um aplicativo Web ASP.NET Core

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio para Mac](https://www.visualstudio.com/vs/visual-studio-mac)

## <a name="intended-audience"></a>Público-alvo

Este laboratório destina-se a desenvolvedores que estão familiarizados com o C#, embora uma ampla experiência não seja necessária.

## <a name="task-1-creating-a-new-aspnet-core-application"></a>Tarefa 1: Criando um novo aplicativo de ASP.NET Core

1. Iniciar **Visual Studio para Mac**.

2. Selecione **Arquivo > Nova Solução**.

3. Selecione a categoria **.NET Core > Aplicativo** e o modelo **Aplicativo Web ASP.NET Core (C#)**. Clique em **Próximo**.

    ![](media/netcore-image1.png)

4. Insira o nome **"CoreLab"** e clique em **Criar** para criar o projeto. Isso levará alguns instantes para ser concluído.

    ![](media/netcore-image2.png)

## <a name="task-2-touring-the-solution"></a>Tarefa 2: Tour pela solução

1. O modelo padrão produzirá uma solução com um único projeto ASP.NET Core chamado **CoreLab**. Expanda o nó do projeto para expor seu conteúdo.

    ![](media/netcore-image3.png)

2. Esse projeto segue o paradigma MVC (Model-View-Controller) para fornecer uma divisão clara das responsabilidades entre os dados (modelos), a apresentação (exibições) e a funcionalidade (controladores). Abra o arquivo **HomeController.cs** da pasta **Controladores**.

    ![](media/netcore-image4.png)

3. Por convenção, a classe **HomeController** manipula todas as solicitações de entrada que começam com **/Home**. O método **Index** manipula solicitações para a raiz do diretório (como `http://site.com/Home`) e outros métodos manipulam as solicitações para seu caminho nomeado baseado em convenção, como **About()** manipula solicitações para `http://site.com/Home/About`. Obviamente, isso tudo é configurável. Um aspecto notável é que o **HomeController** é o controlador padrão em um novo projeto e, portanto, as solicitações para a raiz do site (`http://site.com`) passarão pelo **Index()** do **HomeController**, assim como as solicitações para `http://site.com/Home` ou `http://site.com/Home/Index`.

    ![](media/netcore-image5.png)

4. O projeto também tem uma pasta **Exibições** que contém outras pastas que são mapeadas para cada controlador (bem como uma para exibições **Compartilhadas**). Por exemplo, o arquivo de exibição CSHTML (uma extensão de HTML) para o caminho **/Home/About** seria em **Views/Home/About.cshtml**. Abra esse arquivo.

    ![](media/netcore-image6.png)

5. Esse arquivo CSHTML usa a sintaxe Razor para renderizar HTML com base em uma combinação de marcas padrão e C# embutido. Saiba mais sobre isso na [documentação online](/aspnet/web-pages/overview/getting-started/introducing-razor-syntax-c).

    ![](media/netcore-image7.png)

6. A solução também contém uma pasta **wwwroot** que será a raiz do site. Você pode colocar o conteúdo estático do site, como CSS, imagens e bibliotecas JavaScript, diretamente nos caminhos de que você deseja que eles estejam quando o site for implantado.

    ![](media/netcore-image8.png)

7. Também há uma variedade de arquivos de configuração que servem para gerenciar o projeto, seus pacotes e o aplicativo no runtime. Por exemplo, a [configuração](/aspnet/core/fundamentals/configuration) de aplicativo padrão é armazenada em **appsettings.json**. Aninhado abaixo do appsettings.jsno arquivo é o **appsettings.Development.jsno** arquivo. Aqui, você pode substituir algumas ou todas essas configurações em uma base por ambiente. Visual Studio para Mac aninhará arquivos dessa maneira usando a mesma lógica que o Visual Studio para Windows, para que os arquivos que você precisa acessar com mais frequência estejam no Forefront. 

    ![](media/netcore-build-nested.png)

## <a name="task-3-understanding-how-the-application-is-hosted"></a>Tarefa 3: entendendo como o aplicativo é hospedado

1. No **Gerenciador de Soluções**, abra **Program.cs**. Esse é o bootstrapper que executará seu aplicativo.

    ![](media/netcore-image10.png)

2. Embora haja apenas duas linhas de código aqui, elas são significativas. Vamos detalhá-las. Primeiro, um **WebHostBuilder** é criado. Os aplicativos ASP.NET Core exigem um host no qual serão executados. Um host precisa implementar a interface **IWebHost**, que expõe coleções de funcionalidades e serviços, e um método **Start**. O host é normalmente criado com uma instância de um **WebHostBuilder**, que cria e retorna uma instância de **WebHost**. O **WebHost** referencia o servidor que manipulará as solicitações.

    ![](media/netcore-image11.png)

3. Embora o **WebHostBuilder** seja responsável por criar o host que inicializará o servidor para o aplicativo, ele exige que você forneça um servidor que implementa **IServer**. Por padrão, esse é o **[Kestrel](/aspnet/core/fundamentals/servers/kestrel)**, um servidor Web multiplataforma para o ASP.NET Core baseado no **libuv**, uma biblioteca de E/S assíncrona multiplataforma.

    ![](media/netcore-image12.png)

4. Em seguida, a raiz do conteúdo do servidor é definida. Isso determina o local em que ele pesquisa arquivos de conteúdo, como arquivos de Exibição do MVC. A raiz do conteúdo padrão é a pasta na qual o aplicativo é executado.

    ![](media/netcore-image13.png)

5. Se o aplicativo precisar funcionar com o servidor Web do IIS (Serviços de Informações da Internet), o método **UseIISIntegration** deverá ser chamado como parte da criação do host. Isso não configura um servidor, como **UseKestrel** o faz. Para usar o IIS com o ASP.NET Core, é necessário especificar **UseKestrel** e **UseIISIntegration**. O **Kestrel** foi projetado para ser executado por trás de um proxy e não deve ser implantado diretamente para a Internet. **UseIISIntegration** especifica o IIS como o servidor proxy reverso, mas só é relevante quando executado em computadores que têm o IIS. Se você implanta seu aplicativo no Windows, pode deixá-lo lá. Fazer isso não será prejudicial.

    ![](media/netcore-image14.png)

6. É uma prática mais limpa de separar o carregamento das configurações da inicialização do aplicativo. Para fazer isso com facilidade, **UseStartup** é chamado para especificar que a classe **Startup** será chamada para o carregamento das configurações e outras tarefas de inicialização, como a inserção de middleware no pipeline HTTP. Você pode ter várias chamadas **UseStartup** com a expectativa de que cada uma delas substitua as configurações anteriores, conforme necessário.

    ![](media/netcore-image15.png)

7. A última etapa na criação do **IWebHost** é chamar o **Build**.

    ![](media/netcore-image16.png)

8. Embora as classes **IWebHost** sejam necessárias para implementar o **Start** sem bloqueio, os projetos ASP.NET Core têm um método de extensão chamado **Run** que encapsula **Start** com um código de bloqueio, de modo que você não precisa impedir de forma manual o encerramento do método imediatamente.

    ![](media/netcore-image17.png)

## <a name="task-4-running-and-debugging-the-application"></a>Tarefa 4: executando e Depurando o aplicativo

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto **CoreLab** e selecione **Opções**.

    ![](media/netcore-image18.png)

2. A caixa de diálogo **Opções do Projeto** inclui tudo o que você precisa para ajustar como o aplicativo é criado e executado. Selecione o nó **Executar > Configurações > Padrão** no painel esquerdo.

3. Marque **Executar no console externo** e desmarque **Pausar a saída do console**. Normalmente, o aplicativo auto-hospedado não tem seu console visível, mas em vez disso, registra os resultados em log no painel **Saída**. Para os fins deste laboratório, vamos mostrá-lo em uma janela separada também, embora não seja necessário fazer isso durante o desenvolvimento normal.

4. Clique em **OK**.

    ![](media/netcore-image19.png)

5. Pressione **F5** para compilar e executar o aplicativo. Como alternativa, você pode selecionar **Executar > Iniciar Depuração**.

6. O Visual Studio para Mac iniciará duas janelas. A primeira é uma janela de console que fornece uma exibição do aplicativo para servidores auto-hospedados.

    ![](media/netcore-image20.png)

7. A segunda é uma janela do navegador típica para testar o site. Pelo que o navegador sabe, esse aplicativo pode ser hospedado em qualquer lugar. Clique em **Sobre** para navegar até essa página.

    ![](media/netcore-image21.png)

8. Entre outras coisas, a página Sobre renderiza um texto definido no controlador.

    ![](media/netcore-image22.png)

9. Mantenha ambas as janelas abertas e retorne ao Visual Studio para Mac. Abra **Controllers/HomeController.cs** se ainda não estiver aberto.

    ![](media/netcore-image23.png)

10. Definir um ponto de interrupção na primeira linha do método **Sobre**. Faça isso clicando na margem ou definindo o cursor na linha e pressionando **F9**. Essa linha define alguns dados na coleção **ViewData** que é renderizada na página CSHTML em **Views/Home/About.cshtml**.

    ![](media/netcore-image24.png)

11. Retorne ao navegador e atualize a página Sobre. Isso disparará o ponto de interrupção no Visual Studio para Mac.

12. Passe o mouse sobre o membro **ViewData** para exibir seus dados. Expanda também seus membros filho para ver os dados aninhados.

    ![](media/netcore-image25.png)

13. Remova o ponto de interrupção do aplicativo usando o mesmo método que você usou para adicioná-lo.

14. Abra **Views/Home/About.cshtml**.

15. Altere o texto **“adicional”** para **“alterado”** e salve o arquivo.

    ![](media/netcore-image26.png)

16. Pressione o botão **Continuar** para continuar a execução.

    ![](media/netcore-image27.png)

17. Retornar à janela do navegador para ver o texto atualizado. Essa alteração pode ser feita a qualquer momento e não exige, necessariamente, um ponto de interrupção do depurador. Atualize o navegador se você não vir a alteração refletida imediatamente.

    ![](media/netcore-image28.png)

18. Feche a janela do navegador de teste e o aplicativo de console. Isso interromperá a depuração também.

## <a name="task-5-application-startup-configuration"></a>Tarefa 5: configuração de inicialização do aplicativo

1. No **Gerenciador de Soluções**, abra **Startup.cs**. Você pode observar alguns rabiscos vermelhos inicialmente, conforme os pacotes NuGet são restaurados em segundo plano e o compilador Roslyn cria um panorama completo das dependências do projeto.

    ![](media/netcore-image29.png)

2. Localize o método **Startup**. Essa seção define a configuração inicial para o aplicativo e é densamente compactada. Vamos detalhá-la.

    ![](media/netcore-image30.png)

3. O método começa inicializando um **ConfigurationBuilder** e definindo seu caminho base.

    ![](media/netcore-image31.png)

4. Em seguida, ele carrega um arquivo **appsettings.json** necessário.

    ![](media/netcore-image32.png)

5. Depois disso, ele tenta carregar um arquivo **appsettings.json** específico do ambiente, que substituirá as configurações existentes. Por exemplo, esse é um arquivo **appsettings.Development.json** fornecido usado para esse ambiente específico. Para ler mais sobre a configuração no ASP.NET Core, confira a [documentação](/aspnet/core/fundamentals/configuration).

    ![](media/netcore-image34.png)

6. Por fim, as variáveis de ambiente são adicionadas ao construtor de configuração e a configuração é criada e definida para uso.

    ![](media/netcore-image35.png)

## <a name="task-6-inserting-application-middleware"></a>Tarefa 6: inserindo middleware de aplicativo

1. Localize o método **Configure** na classe **Startup**. É nele em que todo o middleware é configurado para que possa ser inserido no pipeline HTTP e usado para processar cada solicitação ao servidor. Embora esse método seja chamado apenas uma vez, o conteúdo dos métodos (como **UseStaticFiles**) pode ser executado em cada solicitação.

    ![](media/netcore-image36.png)

2. Você também pode adicionar outro middleware a ser executado como parte do pipeline. Adicione o código abaixo após **app.UseStaticFiles** para adicionar automaticamente um cabeçalho **X-Test** a cada resposta de saída. O IntelliSense ajudará a preencher o código conforme você digitar.

    ```csharp
    app.Use(async (context, next) =>
    {
        context.Response.Headers.Add("X-Test", new[] { "Test value" });
        await next();
    });
    ```

3. Pressione **F5** para criar e executar o projeto.

4. Podemos usar o navegador para inspecionar os cabeçalhos para verificar se eles são adicionados. As instruções abaixo referem-se ao Safari, mas você pode fazer o mesmo no [Chrome](https://stackoverflow.com/questions/4423061/view-http-headers-in-google-chrome) ou no [Firefox](https://stackoverflow.com/questions/33974595/in-firefox-how-do-i-see-http-request-headers-where-in-web-console).

5. Depois que o navegador carregar o site, selecione **Safari > Preferências**.

6. Na guia **Avançado**, marque **Mostrar menu Desenvolver na barra de menus** e feche a caixa de diálogo.

    ![](media/netcore-image37.png)

7. Selecione **Desenvolver > Mostrar Recursos da Página**.

8. Atualize a janela do navegador para que as ferramentas para desenvolvedores recém-abertas possam acompanhar e analisar o tráfego e o conteúdo.

9. A página HTML do localhost renderizada pelo servidor será o item selecionado por padrão.

    ![](media/netcore-image38.png)

10. Expanda a **barra lateral de Detalhes**.

    ![](media/netcore-image39.png)

11. Role a página até a parte inferior da barra lateral para ver o cabeçalho de resposta adicionado ao código anteriormente.

    ![](media/netcore-image40.png)

12. Feche a janela do navegador e o console quando estiver satisfeito.

## <a name="summary"></a>Resumo

Neste laboratório, você aprendeu a começar a desenvolver aplicativos ASP.NET Core com o Visual Studio para Mac. Caso deseje explorar o desenvolvimento de um aplicativo de banco de dados de filmes mais completo, confira o tutorial [Introdução ao ASP.NET Core MVC](/aspnet/core/tutorials/first-mvc-app/start-mvc).
