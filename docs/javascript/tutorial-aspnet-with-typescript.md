---
title: Criar um aplicativo ASP.NET Core com o TypeScript
description: Neste tutorial, você cria um aplicativo usando ASP.NET Core e TypeScript
ms.date: 03/16/2020
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: cb1d5196874956d54c01504288a4d948b12abea8
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283561"
---
# <a name="tutorial-create-an-aspnet-core-app-with-typescript-in-visual-studio"></a>Tutorial: criar um aplicativo ASP.NET Core com TypeScript no Visual Studio

Neste tutorial para o desenvolvimento do Visual Studio ASP.NET Core e TypeScript, você cria um aplicativo Web simples, adiciona um código TypeScript e, em seguida, executa o aplicativo. 

::: moniker range="vs-2017"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

Neste tutorial, você aprenderá a:
> [!div class="checklist"]
> * Criar um projeto ASP.NET Core
> * Adicionar o pacote NuGet para o suporte do TypeScript
> * Adicionar um código TypeScript
> * Executar o aplicativo
> * Adicionar uma biblioteca de terceiros usando NPM

## <a name="prerequisites"></a>Pré-requisitos

* Você deve ter o Visual Studio instalado e a carga de trabalho de desenvolvimento da Web do ASP.NET.

    ::: moniker range=">=vs-2019"
    Se você ainda não instalou o Visual Studio 2019, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/)   para instalá-lo gratuitamente.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Se você ainda não instalou o Visual Studio 2017, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/)   para instalá-lo gratuitamente.
    ::: moniker-end

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre o instalador do Visual Studio. Escolha a carga de trabalho **ASP.NET e desenvolvimento para a Web** e, em seguida, selecione **Modificar**.

## <a name="create-a-new-aspnet-core-mvc-project"></a>Criar um novo projeto ASP.NET Core MVC

O Visual Studio gerencia arquivos de um único aplicativo em um *projeto*. O projeto inclui os arquivos de configuração, recursos e código-fonte.

>[!NOTE]
> Para começar com um projeto de ASP.NET Core vazio e adicionar um front-end do TypeScript, consulte [ASP.NET Core com o TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) em vez disso.

Neste tutorial, você começa com um projeto simples contendo código para um aplicativo ASP.NET Core MVC.

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"
    Se a janela iniciar não estiver aberta, escolha **arquivo**  >  **Iniciar janela**. Na janela iniciar, escolha **criar um novo projeto**. Na lista suspensa idioma, escolha **C#**. Na caixa de pesquisa, digite **ASP.net**e escolha **ASP.NET Core aplicativo Web**. Escolha **Próxima**.

    Digite um nome para o projeto e escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , expanda **Visual C#** e escolha **.NET Core**. No painel central, escolha **ASP.NET Core aplicativo Web-C#** e, em seguida, escolha **OK**.
    ::: moniker-end
    Se você não vir o modelo de projeto de **aplicativo web ASP.NET Core** , deverá adicionar a ASP.net e a carga de trabalho de **desenvolvimento Web** . Confira instruções detalhadas nos [Pré-requisitos](#prerequisites).

1. Na caixa de diálogo exibida, selecione **aplicativo Web (Model-View-Controller)** na caixa de diálogo e escolha **criar** (ou **OK**).

   ![Escolher o modelo MVC](../javascript/media/aspnet-core-ts-mvc-template.png)

    O Visual Studio cria a solução e abre o projeto no painel direito.

## <a name="add-some-code"></a>Adicionar código

1. Na Gerenciador de Soluções (painel direito). Clique com o botão direito do mouse no nó do projeto e escolha **gerenciar pacotes NuGet**. Na guia **procurar** , procure **Microsoft. TypeScript. MSBuild**e clique em **instalar** à direita para instalar o pacote.

   ![Adicionar pacote NuGet](../javascript/media/aspnet-core-ts-nuget.png)

   O Visual Studio adiciona o pacote NuGet sob o nó **dependências** em Gerenciador de soluções.

   > [!NOTE]
   > Este tutorial requer o pacote NuGet. Como alternativa, em seus próprios aplicativos, talvez você queira usar o [pacote NPM TypeScript](https://www.npmjs.com/package/typescript).

1. Clique com o botão direito do mouse no nó do projeto e escolha **adicionar > novo item**. Escolha o **arquivo de configuração JSON do TypeScript**e clique em **Adicionar**.

   O Visual Studio adiciona o *tsconfig.jsno* arquivo à raiz do projeto. Você pode usar esse arquivo para [Configurar opções](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) para o compilador TypeScript.

1. Abra *tsconfig.js* e substitua o código padrão pelo código a seguir:

   ```json
   {
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

   A opção *outDir* especifica a pasta de saída para os arquivos JavaScript simples que são transcompilados pelo compilador do TypeScript.

   Essa configuração fornece uma introdução básica ao uso do TypeScript. Em outros cenários, por exemplo, ao usar o [Gulp ou o webpack](https://www.typescriptlang.org/docs/handbook/asp-net-core.html), talvez você queira um local intermediário diferente para os arquivos JavaScript transcompilados, dependendo de suas ferramentas e preferências de configuração, em vez de *wwwroot/js*.

1. Em Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e escolha **adicionar > nova pasta**. Use os *scripts* de nome para a nova pasta.

1. Clique com o botão direito do mouse na pasta *scripts* e escolha **Adicionar > novo item**. Escolha o **arquivo TypeScript**, digite o nome *app. TS* para o nome de arquivo e clique em **Adicionar**.

   O Visual Studio adiciona *app. TS* à pasta *scripts* .

1. Abra *app. TS* e adicione o código TypeScript a seguir.

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

    O Visual Studio fornece suporte IntelliSense para seu código TypeScript.

    Para testar isso, remova `.lastName` da `greeter` função, em seguida, digite novamente o "." e você verá o IntelliSense.

    ![Exibir IntelliSense](../javascript/media/aspnet-core-ts-intellisense.png)

    Selecione `lastName` para adicionar o sobrenome de volta ao código.

1. Abra a pasta *views/Home* e, em seguida, abra *index. cshtml*.

1. Adicione o código HTML a seguir ao final do arquivo.

    ```html
    <div id="ts-example">
        <br />
        <button type="button" class="btn btn-primary btn-md" onclick="TSButton()">
            Click Me
        </button>
    </div>
    ```

1. Abra os *modos de exibição/pasta compartilhada* e, em seguida, abra *_Layout. cshtml*.

1. Adicione a seguinte referência de script antes da chamada para `@RenderSection("Scripts", required: false)` :

    ```js
    <script src="~/js/app.js"></script>
    ````

## <a name="build-the-application"></a>Compilar o aplicativo

1. Escolha **compilar > Compilar solução**.

   Embora o aplicativo seja criado automaticamente quando você o executa, queremos dar uma olhada em algo que acontece durante o processo de compilação.

1. Abra a pasta *wwwroot/js* e você encontrará dois arquivos novos, *app.js* e o arquivo de mapa de origem, *app.js. map*. Esses arquivos são gerados pelo compilador TypeScript.

   Os arquivos de mapa de origem são necessários para depuração.

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **F5** (**Depurar** > **Iniciar Depuração**) para executar o aplicativo.

    O aplicativo é aberto em um navegador.

    Na janela do navegador, você verá o título de **boas-vindas** e o botão **clicar em mim** .

    ![ASP.NET Core com TypeScript](../javascript/media/aspnet-core-ts-running-app.png)

1. Clique no botão para exibir a mensagem que especificamos no arquivo TypeScript.

## <a name="debug-the-application"></a>Depurar o aplicativo

1. Defina um ponto de interrupção na `greeter` função no clicando `app.ts` na margem esquerda no editor de códigos.

    ![Definir um ponto de interrupção](../javascript/media/aspnet-core-ts-set-breakpoint.png)

1. Pressione **F5** para executar o aplicativo.

   Talvez seja necessário responder a uma mensagem para habilitar a depuração de script.

   O aplicativo pausa no ponto de interrupção. Agora, você pode inspecionar variáveis e usar os recursos do depurador.

## <a name="add-typescript-support-for-a-third-party-library"></a>Adicionar suporte do TypeScript a uma biblioteca de terceiros

1. Siga as instruções em [Gerenciamento de pacotes NPM](../javascript/npm-package-management.md#aspnet-core-projects) para adicionar um `package.json` arquivo ao seu projeto. Isso adiciona suporte a NPM ao seu projeto.

   >[!NOTE]
   > Para projetos ASP.NET Core, você também pode usar o [Gerenciador de biblioteca](https://docs.microsoft.com/aspnet/core/client-side/libman/?view=aspnetcore-3.1) ou yarn em vez de NPM para instalar arquivos JavaScript e CSS do lado do cliente.

1. Neste exemplo, adicione um arquivo de definição do TypeScript para o jQuery ao seu projeto. Inclua o seguinte em seu *package.jsno* arquivo.

   ```json
   "devDependencies": {
      "@types/jquery": "3.3.33"
   }
   ```

   Isso adiciona suporte ao TypeScript para jQuery. A biblioteca jQuery em si já está incluída no modelo de projeto do MVC (procure em wwwroot/lib em Gerenciador de Soluções). Se você estiver usando um modelo diferente, talvez seja necessário incluir também o pacote jQuery NPM.

1. Se o pacote no Gerenciador de Soluções não estiver instalado, clique com o botão direito do mouse no nó NPM e escolha **restaurar pacotes**.

   >[!NOTE]
   > Em alguns cenários, Gerenciador de Soluções pode indicar que um pacote NPM está fora de sincronia com *package.jsem* devido a um problema conhecido descrito [aqui](https://github.com/aspnet/Tooling/issues/479). Por exemplo, o pacote pode aparecer como não instalado quando instalado. Na maioria dos casos, você pode atualizar Gerenciador de Soluções excluindo *package.js*, reiniciando o Visual Studio e adicionando novamente o *package.jsno* arquivo, conforme descrito anteriormente neste artigo.

1. Em Gerenciador de soluções, clique com o botão direito do mouse na pasta scripts e escolha **Adicionar**  >  **novo item**.

1. Escolha o **arquivo TypeScript**, digite *library. TS*e escolha **Adicionar**.

1. Em *library. TS*, adicione o código a seguir.

   ```ts
   var jqtest = {
      showMsg: function (): void {
         let v: any = jQuery.fn.jquery.toString();
         let content: any = $("#ts-example-2")[0].innerHTML;
         alert(content.toString());
         $("#ts-example-2")[0].innerHTML = content + " " + v + "!!";
      }
   };

   jqtest.showMsg();
   ```

   Para simplificar, esse código exibe uma mensagem usando o jQuery e um alerta.

   Com as definições de tipo do TypeScript para o jQuery adicionado, você obtém suporte do IntelliSense em objetos jQuery ao digitar um "." seguindo um objeto jQuery, como mostrado aqui.

   ![jQuery IntelliSense](../javascript/media/aspnet-core-ts-jquery-intellisense.png)

1. Em _Layout. cshtml, atualize as referências de script a serem incluídas `library.js` .

   ```html
   <script src="~/js/app.js"></script>
   <script src="~/js/library.js"></script>
   ```

1. Em index. cshtml, adicione o seguinte HTML ao final do arquivo.

   ```html
   <div>
      <p id="ts-example-2">jQuery version is:</p>
   </div>
   ```

1. Pressione **F5** (**Depurar** > **Iniciar Depuração**) para executar o aplicativo.

    O aplicativo é aberto no navegador.

    Clique em **OK** no alerta para ver a página atualizada para a **versão do jQuery: 3.3.1!!**.

    ![exemplo de jQuery](../javascript/media/aspnet-core-ts-jquery-example.png)

## <a name="next-steps"></a>Próximas etapas

Talvez você queira saber mais detalhes sobre como usar o TypeScript com ASP.NET Core.

> [!div class="nextstepaction"]
> [ASP.NET Core e TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)
