---
title: Criar um aplicativo ASP.NET Core com o TypeScript
description: Neste tutorial, você criará um aplicativo usando ASP.NET Core e TypeScript
ms.date: 03/25/2021
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 0728011c05d47996a313c11a18f31a196ec08e10
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306493"
---
# <a name="tutorial-create-an-aspnet-core-app-with-typescript-in-visual-studio"></a>Tutorial: Criar um ASP.NET Core com TypeScript no Visual Studio

Neste tutorial para Visual Studio desenvolvimento ASP.NET Core e TypeScript, você cria um aplicativo Web simples, adiciona um código TypeScript e, em seguida, execute o aplicativo.

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range=">=vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2022"

Se você ainda não tiver instalado o Visual Studio 2022 Preview, acesse a página de downloads do [Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022) para instalá-lo gratuitamente.

::: moniker-end

Neste tutorial, você aprenderá como:
> [!div class="checklist"]
> * Criar um projeto ASP.NET Core
> * Adicionar o pacote NuGet para suporte a TypeScript
> * Adicionar um código TypeScript
> * Executar o aplicativo
> * Adicionar uma biblioteca de terceiros usando npm

## <a name="prerequisites"></a>Pré-requisitos

* Você deve ter Visual Studio e a carga de trabalho ASP.NET desenvolvimento para a Web.

    ::: moniker range=">=vs-2019"
    Se você ainda não instalou o Visual Studio 2019, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.
    ::: moniker-end

    Se você precisar instalar a carga de trabalho, mas já tiver Visual Studio, acesse Ferramentas Obter Ferramentas e  >  **Recursos...**, que abre o Instalador do Visual Studio. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.

## <a name="create-a-new-aspnet-core-mvc-project"></a>Criar um novo projeto ASP.NET Core MVC

O Visual Studio gerencia arquivos de um único aplicativo em um *projeto*. O projeto inclui os arquivos de configuração, recursos e código-fonte.

>[!NOTE]
> Para começar com um projeto ASP.NET Core vazio e adicionar um front-end typeScript, consulte [ASP.NET Core com TypeScript.](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)

Neste tutorial, você começa com um projeto simples que contém código para um ASP.NET Core MVC.

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, escolha **Criar um** novo projeto na janela inicial. Se a janela inicial não estiver aberta, escolha **Janela de** Início  >  **do Arquivo**. Digite **aplicativo Web**, escolha **C#** como o idioma, escolha ASP.NET Aplicativo Web Principal **(Model-View-Controller)** e, em seguida, **escolha Próximo**. Na próxima tela, nomeia o projeto e, em seguida, escolha **Próximo.**

    Escolha a estrutura de destino recomendada (.NET Core 3.1) ou .NET 5 e escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **Arquivo**  >  **Novo**  >  **Projeto**. No painel esquerdo da caixa de **diálogo** Novo Projeto, expanda **Visual C#** e escolha **.NET Core.** No painel central, escolha ASP.NET **Core Web Application – C#** e, em seguida, escolha **OK.**

    Na caixa de diálogo exibida, selecione **Aplicativo Web (Model-View-Controller)** na caixa de diálogo e escolha **Criar** (ou **OK).**

    ![Escolher o modelo MVC](../javascript/media/aspnet-core-ts-mvc-template.png)
    ::: moniker-end
    Se você não vir o modelo de projeto **ASP.NET Core Web Application,** deverá adicionar a carga de trabalho ASP.NET **desenvolvimento para** a Web. Confira instruções detalhadas nos [Pré-requisitos](#prerequisites).

    O Visual Studio cria a solução e abre o projeto no painel direito.

## <a name="add-some-code"></a>Adicionar código

1. No Gerenciador de Soluções (painel direito). Clique com o botão direito do mouse no nó do projeto e **escolha Gerenciar Pacotes NuGet.** Na guia **Procurar,** procure **Microsoft.TypeScript.MSBuild** e  clique em Instalar à direita para instalar o pacote.

   ![Adicionar pacote NuGet](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio adiciona o pacote NuGet no nó **Dependências** no Gerenciador de Soluções.

1. Clique com o botão direito do mouse no nó do projeto **e escolha Adicionar > Novo Item**. Escolha o **Arquivo de Configuração JSON do TypeScript** e clique em **Adicionar**.

   Visual Studio adiciona o *tsconfig.jsno* arquivo à raiz do projeto. Você pode usar esse arquivo para [configurar opções](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) para o compilador TypeScript.

1. Abra *tsconfig.jsem* e substitua o código padrão pelo seguinte código:

   ```json
   {
     "compileOnSave": true,
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "wwwroot/js"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   A *opção outDir* especifica a pasta de saída para os arquivos JavaScript simples que são trans compilados pelo compilador TypeScript.

   Essa configuração fornece uma introdução básica ao uso do TypeScript. Em outros cenários, por exemplo, ao usar gulp ou [webpack](https://www.typescriptlang.org/docs/handbook/asp-net-core.html), você pode querer um local intermediário diferente para os arquivos JavaScript transpilação, dependendo de suas ferramentas e preferências de configuração, em vez *de wwwroot/js*.

1. No Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e **escolha Adicionar > Nova Pasta**. Use os *scripts de nome* para a nova pasta.

1. Clique com o botão direito do mouse na pasta *scripts* e **escolha Adicionar > Novo Item**. Escolha o **Arquivo TypeScript**, digite o nome *app.ts* para o nome do arquivo e clique em **Adicionar**.

   Visual Studio adiciona *app.ts* à *pasta scripts.*

1. Abra *app.ts* e adicione o seguinte código TypeScript.

    ```ts
    function TSButton() {
       let name: string = "Fred";
       document.getElementById("ts-example").innerHTML = greeter(user);
    }

    class Student {
       fullName: string;
       constructor(public firstName: string, public middleInitial: string, public lastName: string) {
           this.fullName = firstName + " " + middleInitial + " " + lastName;
       }
    }

    interface Person {
       firstName: string;
       lastName: string;
    }

    function greeter(person: Person) {
       return "Hello, " + person.firstName + " " + person.lastName;
    }

    let user = new Student("Fred", "M.", "Smith");
    ```

    Visual Studio dá suporte ao IntelliSense para seu código TypeScript.

    Para testar isso, remova da função e, em `.lastName` `greeter` seguida, retipo "." e você verá IntelliSense.

    ![Exibir o IntelliSense](../javascript/media/aspnet-core-ts-intellisense.png)

    Selecione `lastName` para adicionar o sobrenome de volta ao código.

1. Abra a *pasta Views/Home* e, em seguida, *abra Index.cshtml*.

1. Adicione o código HTML a seguir ao final do arquivo.

    ```html
    <div id="ts-example">
        <br />
        <button type="button" class="btn btn-primary btn-md" onclick="TSButton()">
            Click Me
        </button>
    </div>
    ```

1. Abra a *pasta Views/Shared* e, em *seguida, abra _Layout.cshtml*.

1. Adicione a seguinte referência de script antes da chamada para `@RenderSection("Scripts", required: false)` :

    ```js
    <script src="~/js/app.js"></script>
    ````

## <a name="build-the-application"></a>Compilar o aplicativo

1. Escolha **Build > Build Solution**.

   Embora o aplicativo seja construído automaticamente quando você o executar, queremos dar uma olhada em algo que acontece durante o processo de build.

1. Abra a *pasta wwwroot/js* e encontre dois novos arquivos, *app.js* e o arquivo source map, *app.js.map.* Esses arquivos são gerados pelo compilador TypeScript.

   Arquivos de mapa de origem são necessários para depuração.

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **F5** (**Depurar** > **Iniciar Depuração**) para executar o aplicativo.

    O aplicativo é aberto em um navegador.

    Na janela do navegador, você verá o título De **boas-vindas** e o **botão Clicar em** Mim.

    ![ASP.NET Core com TypeScript](../javascript/media/aspnet-core-ts-running-app.png)

1. Clique no botão para exibir a mensagem que especificamos no arquivo TypeScript.

## <a name="debug-the-application"></a>Depurar o aplicativo

1. De definir um ponto de interrupção `greeter` na função em `app.ts` clicando na margem esquerda no editor de código.

    ![Definir um ponto de interrupção](../javascript/media/aspnet-core-ts-set-breakpoint.png)

1. Pressione **F5** para executar o aplicativo.

   Talvez seja necessário responder a uma mensagem para habilitar a depuração de script.

   O aplicativo pausa no ponto de interrupção. Agora, você pode inspecionar variáveis e usar recursos do depurador.

## <a name="add-typescript-support-for-a-third-party-library"></a>Adicionar suporte a TypeScript para uma biblioteca de terceiros

1. Siga as instruções no [gerenciamento de pacotes npm](../javascript/npm-package-management.md#aspnet-core-projects) para adicionar `package.json` um arquivo ao seu projeto. Isso adiciona suporte a npm ao seu projeto.

   >[!NOTE]
   > Para ASP.NET Core, você também pode usar [o Gerenciador](/aspnet/core/client-side/libman/) de Biblioteca ou yarn em vez do npm para instalar arquivos JavaScript e CSS do lado do cliente.

1. Neste exemplo, adicione um arquivo de definição typeScript para jQuery ao seu projeto. Inclua o seguinte no arquivo *package.json.*

   ```json
   "devDependencies": {
      "@types/jquery": "3.3.33"
   }
   ```

   Isso adiciona suporte a TypeScript para jQuery. A biblioteca jQuery em si já está incluída no modelo de projeto do MVC (consulte wwwroot/lib no Gerenciador de Soluções). Se você estiver usando um modelo diferente, talvez seja necessário incluir o pacote npm jquery também.

1. Se o pacote no Gerenciador de Soluções estiver instalado, clique com o botão direito do mouse no nó npm e escolha **Restaurar Pacotes**.

   >[!NOTE]
   > Em alguns cenários, Gerenciador de Soluções pode indicar que um pacote npm está fora de sincronia compackage.js *on* devido a um problema conhecido descrito [aqui](https://github.com/aspnet/Tooling/issues/479). Por exemplo, o pacote pode aparecer como não instalado quando está instalado. Na maioria dos casos, você pode atualizar Gerenciador de Soluções excluindopackage.jsno *,* reiniciando o Visual Studio e adicionando novamente o arquivo *package.jsno* , conforme descrito anteriormente neste artigo.

1. No Gerenciador de Soluções, clique com o botão direito do mouse na pasta scripts e **escolha Adicionar**  >  **Novo Item**.

1. Escolha **Arquivo TypeScript,** digite *library.ts* e escolha **Adicionar**.

1. Em *library.ts*, adicione o código a seguir.

   ```ts
   var jqtest = {
      showMsg: function (): void {
         let v: any = jQuery.fn.jquery.toString();
         let content: any = $("#ts-example-2")[0].innerHTML;
         alert(content.toString() + " " + v + "!!");
         $("#ts-example-2")[0].innerHTML = content + " " + v + "!!";
      }
   };

   jqtest.showMsg();
   ```

   Para simplificar, esse código exibe uma mensagem usando jQuery e um alerta.

   Com as definições de tipo TypeScript para jQuery adicionadas, você obterá suporte ao IntelliSense em objetos jQuery quando digitar um "." após um objeto jQuery, conforme mostrado aqui.

   ![jquery IntelliSense](../javascript/media/aspnet-core-ts-jquery-intellisense.png)

1. Em _Layout.cshtml, atualize as referências de script para incluir `library.js` .

   ```html
   <script src="~/js/app.js"></script>
   <script src="~/js/library.js"></script>
   ```

1. Em Index.cshtml, adicione o HTML a seguir ao final do arquivo.

   ```html
   <div>
      <p id="ts-example-2">jQuery version is:</p>
   </div>
   ```

1. Pressione **F5** (**Depurar** > **Iniciar Depuração**) para executar o aplicativo.

    O aplicativo é aberto no navegador.

    Clique **em OK** no alerta para ver a página atualizada para a versão **jQuery é: 3.3.1!!**.

    ![Exemplo de jquery](../javascript/media/aspnet-core-ts-jquery-example.png)

## <a name="next-steps"></a>Próximas etapas

Talvez você queira saber mais detalhes sobre como usar o TypeScript com ASP.NET Core. Se você estiver interessado em programação AngularJS no Visual Studio, poderá usar a extensão de serviço de [linguagem AngularJS](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio) para Visual Studio.

> [!div class="nextstepaction"]
> [ASP.NET Core e TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)

> [!div class="nextstepaction"]
> [Extensão do serviço de linguagem AngularJS](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)
