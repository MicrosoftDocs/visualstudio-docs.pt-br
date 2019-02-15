---
title: Introdução ao ASP.NET Core
description: Este artigo descreve como começar a usar o ASP.NET no Visual Studio para Mac, incluindo como instalar e com criar um novo projeto.
author: conceptdev
ms.author: crdun
ms.date: 07/13/2017
ms.assetid: 6E8B0C90-33D6-4546-8207-CE0787584565
ms.custom: video
ms.openlocfilehash: 290c1971e22a0a0f8ffcd7b92441c81a4ec0037b
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55910981"
---
# <a name="getting-started-with-aspnet-core"></a>Introdução ao ASP.NET Core

 O Visual Studio para Mac facilita o desenvolvimento do serviço de seu aplicativo por meio de seu suporte para a plataforma de desenvolvimento na Web ASP.NET Core mais recente. O ASP.NET Core é executado no .NET Core, a evolução mais recente do .NET Framework e o tempo de execução. Ele foi ajustado a fim de proporcionar um desempenho rápido, perfeito para instalações de pequeno porte e recriado para ser executado no Linux, macOS e também no Windows.

## <a name="installing-net-core"></a>Instalando o .NET Core

O .NET Core 1.1 é instalado automaticamente quando você instala o Visual Studio para Mac.

## <a name="creating-an-aspnet-core-app-in-visual-studio-for-mac"></a>Criar um aplicativo do ASP.NET Core no Visual Studio para Mac

Abra o Visual Studio para Mac. Na página inicial, escolha **Novo Projeto...**

![Nova caixa de diálogo de projeto](media/asp-net-core-image1.png)

Isso exibirá a caixa de diálogo Novo projeto, permitindo que você selecione um modelo para criar seu aplicativo.

Diversos projetos fornecem um modelo criado previamente para começar a criar seu aplicativo do ASP.NET Core. Elas são:

- **.NET Core > Aplicativo Web ASP.NET Core vazio**
- **.NET Core > Aplicativo Web ASP.NET Core**
- **.NET Core > API da Web ASP.NET Core**
- **Multiplataforma > Aplicativo > Aplicativo conectado**

![Opções do projeto ASP.NET](media/asp-net-core-image11.png)

Selecione o **Aplicativo Web vazio ASP.NET Core** e pressione **Avançar**. Escolha um nome para o projeto e pressione **Criar**. Isso cria um novo aplicativo ASP.NET Core, que deve ser semelhante à imagem abaixo:

![Nova exibição Projeto ASP.NET Core vazio](media/asp-net-core-image4.png)

O aplicativo Web ASP.NET Core vazio cria um aplicativo Web com dois arquivos padrão: **Program.cs** e **Startup.cs**, que são explicados abaixo. Ele também cria uma pasta de Dependências, que contém as dependências do pacote NuGet do seu projeto, como ASP.NET Core, a estrutura .NET Core e os destinos do MSBuild que compilam o projeto:

![Painel de Soluções exibindo as dependências](media/asp-net-core-image12.png)

### <a name="programcs"></a>Module.vb

Abra e inspecione o arquivo **Program.cs** no seu projeto. Observe que duas coisas ocorrem no método `Main`, a entrada no seu aplicativo:

```csharp
public static void Main(string[] args)
{
    var host = new WebHostBuilder()
        .UseKestrel()
        .UseContentRoot(Directory.GetCurrentDirectory())
        .UseIISIntegration()
        .UseStartup<Startup>()
        .Build();

    host.Run();
}
```
Um aplicativo ASP.NET Core cria um servidor Web em seu método principal configurando e iniciando um host por meio de uma instância de [`WebHostBuilder`](/aspnet/core/fundamentals/hosting). Este construtor fornece métodos para permitir que o host seja configurado. As seguintes configurações são usadas no aplicativo modelo:

* `UseKestrel`: especifica que o servidor Kestrel será usado pelo aplicativo.
* `UseContentRoot(Directory.GetCurrentDirectory())`: usa a pasta raiz do projeto Web como a raiz de conteúdo do aplicativo, quando ele é iniciado nesta pasta.
* `.UseIISIntegration()`: especifica que o aplicativo funcionará com o IIS. Para usar o IIS com o ASP.NET Core, tanto `UseKestrel` quanto `UseIISIntegration` precisam ser especificados.
* `.UseStartup<Startup>()`: especifica a classe Startup.

  Os métodos Build e Run compilam o IWebHost que hospedará o aplicativo e iniciam sua escuta de solicitações HTTP de entrada.

### <a name="startupcs"></a>Startup.cs

A classe Startup para seu aplicativo é especificada no método `UseStartup()` no `WebHostBuilder`. É nessa classe que você especificará a pipeline de tratamento de solicitação e onde você configura todos os serviços.

Abra e inspecione o arquivo **Startup.cs** no seu projeto:

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
    }

    public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
    {
        loggerFactory.AddConsole();

        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.Run(async (context) =>
        {
            await context.Response.WriteAsync("Hello World!");
        });
    }
}
```

Essa classe Startup sempre deve cumprir as seguintes regras:

 - Ele sempre deve ser pública
 - Ela deve conter os dois métodos públicos: `ConfigureServices` e `Configure`

O método `ConfigureServices` define os serviços que serão usados pelo seu aplicativo.

O `Configure` permite compor o pipeline de solicitação usando [Middleware](/aspnet/core/fundamentals/middleware). Esses componentes são usados em um pipeline de aplicativo do ASP.NET para tratar solicitações e respostas. O pipeline HTTP consiste em diversos delegados de solicitação, chamados em sequência. Cada delegado pode escolher tratar a solicitação em si ou passá-la para o próximo delegado.

Você pode configurar delegados usando os métodos `Run`,`Map` e `Use` métodos em `IApplicationBuilder`, mas o método `Run` nunca chama um próximo delegado e sempre deve ser usado no final do pipeline.

O método `Configure` do modelo criado previamente é composto para realizar algumas tarefas. Primeiro, ele configura uma página de tratamento de exceções para ser usada durante o desenvolvimento. Em seguida, ele envia uma resposta para a página da Web solicitante com um simples “Olá, Mundo”.

Esse simples projeto Olá, Mundo agora pode ser executado sem adição de qualquer código adicional. Para executar o aplicativo e exibi-lo no seu navegador, pressione o botão Executar (Triangular) na barra de ferramentas:

![Executar o Aplicativo](media/asp-net-core-image5.png)

O Visual Studio para Mac usa uma porta aleatória para iniciar o projeto Web. Para descobrir qual porta é essa, abra a Saída do Aplicativo, que é listada em **Exibir > Painéis**. Você deve encontrar uma saída semelhante ao que é mostrado abaixo:

![Saída do Aplicativo exibindo a porta de escuta](media/asp-net-core-image6.png)

Abra o navegador de sua escolha e digite `http://localhost:5000/`, substituindo o `5000` pela porta que o Visual Studio usa para produzir a Saída do Aplicativo. Você deverá ver o seguinte texto `Hello World!`:

![navegador mostrando o texto](media/asp-net-core-image7.png)

## <a name="adding-a-controller"></a>Adicionando um controlador

Aplicativos ASP.NET Core usam o padrão de design MVC (Modelo-Exibição-Controlador) para fornecer uma separação lógica de responsabilidades para cada parte do aplicativo. O MVC consiste no seguinte:

- **Modelo**: uma classe que representa os dados do aplicativo.
- **Exibir**: exibe a interface do usuário do aplicativo, que muitas vezes são os dados de modelo.
- **Controlador**: uma classe que trata as solicitações do navegador, responde à entrada e interação do usuário.

Para obter mais informações sobre como usar o MVC, consulte [Visão geral do guia de MVC do ASP.NET Core](/aspnet/core/mvc/overview).

Para adicionar um controlador, faça o seguinte:

1. Clique com o botão direito do mouse no nome do Projeto e selecione **Adicionar > Novos Arquivos**. Selecione **Geral > Classe Vazia** e digite um nome de controlador:

    ![Caixa de diálogo Novo Arquivo](media/asp-net-core-image8.png)

2. Adicione o seguinte código ao novo controlador:

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace Hello_ASP
    {
        public class HelloWorldController : Controller
        {
            //
            // GET: /HelloWorld/

            public string Index()
            {
                return "This is my default action...";
            }

        }
    }
    ```

3. Adicione a dependência `Microsoft.AspNetCore.Mvc` ao projeto clicando com o botão direito do mouse na pasta **Dependência** e selecionando **Adicionar Pacote...**.

4. Use a caixa de Pesquisa para procurar `Microsoft.AspNetCore.Mvc` na biblioteca de NuGet e selecione **Adicionar Pacote**. A instalação pode levar alguns minutos e pode ser solicitado que você aceite várias licenças para as dependências necessárias:

    ![Adicionar Nuget](media/asp-net-core-image9.png)

5. Na classe Startup, remova o lambda `app.Run` e defina a lógica de roteamento de URL usada pelo MVC para determinar qual código deve invocar o seguinte:

    ```csharp
    app.UseMvc(routes =>
    {
        routes.MapRoute(
        name: "default",
        template: "{controller=HelloWorld}/{action=Index}/{id?}");
    });
    ```

    Lembre-se de remover o lambda `app.Run`, pois isso substituirá a lógica de roteamento.

    O MVC usa o formato a seguir para determinar qual o código deve ser executado:

    `/[Controller]/[ActionName]/[Parameters]`

    Ao adicionar o snippet de código acima, você está solicitando que o aplicativo use o controlador `HelloWorld` e o método de ação `Index` como padrão.

6. Adicione a chamada `services.AddMvc();` ao método `ConfigureServices`, conforme ilustrado abaixo:

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }
    ```

    Você também pode passar informações de parâmetro da URL para o controlador.

7. Adicione outro método ao HelloWorldController conforme ilustrado abaixo:

    ```csharp
    public string Xamarin(string name)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, welcome to Visual Studio for Mac");
    }
    ```

8. Se você executar o aplicativo agora, ele deverá abrir automaticamente o navegador:

    ![Executando o aplicativo no navegador](media/asp-net-core-image13.png)

9. Tente navegar para `http://localhost:xxxx/HelloWorld/Xamarin?name=Amy` (substituindo `xxxx` pela porta correta), você deverá ver o seguinte:

    ![Executando o aplicativo no navegador com argumentos](media/asp-net-core-image10.png)


## <a name="troubleshooting"></a>Solução de problemas

Se você precisar instalar o .NET Core manualmente no Mac OS 10.11 (El Capitan) e superior, faça o seguinte:

1. Antes de começar a instalar o .NET Core, verifique se você atualizou todas as atualizações do sistema operacional para a versão estável mais recente. Você pode verificar isso acessando o aplicativo da App Store e selecionando a guia Atualizações.

2. Siga as etapas listadas no [site do .NET Core](https://www.microsoft.com/net/core#macos).

Conclua todas as quatro etapas para garantir que o .NET Core seja devidamente instalado.

## <a name="summary"></a>Resumo

Este guia forneceu uma introdução ao ASP.NET Core. Ele descreve o que é, quando usá-lo e forneceu as informações sobre como usá-lo no Visual Studio para Mac.
Para obter mais informações sobre as próximas etapas a partir daqui, consulte os seguintes guias:
- Documentos do [ASP.NET Core](/aspnet/core/?view=aspnetcore-2.1#build-web-ui-and-web-apis-using-aspnet-core-mvc).
- [Criando serviços de back-end para aplicativos móveis nativos](/aspnet/core/mobile/native-mobile-backend), que mostra como criar um serviço REST usando o ASP.NET Core para um aplicativo Xamarin.Forms.
- [Laboratório prático do ASP.NET Core](https://github.com/Microsoft/vs4mac-labs/tree/master/Web/Getting-Started).

## <a name="related-video"></a>Vídeo relacionados

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Build-Your-First-App/player]