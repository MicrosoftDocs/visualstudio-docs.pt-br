---
title: Criar um aplicativo Vue.js usando o Node.js
description: Crie aplicativos Node.js no Visual Studio usando a estrutura Vue.js
ms.custom: seodec18
ms.date: 07/06/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: e16b09a165421d36c67dad1fc657fd36846cd382
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285160"
---
# <a name="create-a-vuejs-application-using-nodejs-tools-for-visual-studio"></a>Criar um aplicativo Vue.js usando as Ferramentas Node.js para Visual Studio

O Visual Studio é compatível com o desenvolvimento de aplicativos com a estrutura [Vue.js](https://vuejs.org/) em JavaScript ou TypeScript.

Os seguintes novos recursos dão suporte ao desenvolvimento de aplicativos Vue.js no Visual Studio:

* Suporte para blocos de Script, Estilo e Modelo em arquivos *.vue*
* Reconhecimento do atributo `lang` em arquivos *.vue*
* Modelos de projeto e de arquivo Vue.js

## <a name="prerequisites"></a>Pré-requisitos

* É necessário ter o Visual Studio 2017 versão 15.8 ou posterior instalado e a carga de trabalho **Desenvolvimento do Node.js**.

    > [!IMPORTANT]
    > Este artigo exige recursos que estão disponíveis apenas a partir do Visual Studio 2017 versão 15.8.

    ::: moniker range=">=vs-2019"
    Se a versão necessária ainda não estiver instalada, instale o [Visual Studio de 2019](https://visualstudio.microsoft.com/downloads).
    ::: moniker-end
    ::: moniker range="vs-2017"
    Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)   para instalá-lo gratuitamente.
    ::: moniker-end

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre o instalador do Visual Studio. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

* Para criar o projeto ASP.NET Core, é necessário ter instaladas as cargas de trabalho de desenvolvimento do ASP.NET e para a Web e de desenvolvimento multiplataforma do .NET Core.

* Você precisa ter o runtime do Node.js instalado.

    Se não o tiver instalado, instale a versão LTS do site do [Node.js](https://nodejs.org/en/download/). Em geral, o Visual Studio detecta automaticamente o runtime do Node.js instalado. Se ele não detectar um runtime instalado, você poderá configurar o projeto para referenciar o runtime instalado na página de propriedades. (Depois de criar um projeto, clique com o botão direito do mouse no nó do projeto e escolha **Propriedades**).

## <a name="create-a-vuejs-project-using-nodejs"></a>Criar um projeto Vue.js usando Node.js

Use os novos modelos do Vue.js para criar um projeto. O uso do modelo é a maneira mais fácil de começar. Para obter etapas detalhadas, confira [Usar o Visual Studio para criar seu primeiro aplicativo Vue.js](../javascript/quickstart-vuejs-with-nodejs.md).

## <a name="create-a-vuejs-project-with-aspnet-core-and-the-vue-cli"></a>Criar um projeto do Vue.js com o ASP.NET Core e a CLI do Vue

O Vue.js fornece uma CLI oficial para o scaffolding rápido de projetos. Caso deseje usar a CLI para criar seu aplicativo, siga as etapas deste artigo para configurar o ambiente de desenvolvimento.

> [!IMPORTANT]
> Essas etapas pressupõem que você já tenha alguma experiência com a estrutura Vue.js. Se esse não for o caso, visite [Vue.js](https://vuejs.org/) para saber mais sobre a estrutura.

### <a name="create-a-new-aspnet-core-project"></a>Criar um projeto ASP.NET Core

Neste exemplo, você usará um aplicativo ASP.NET Core vazio (C#). No entanto, você pode escolher uma opção entre uma variedade de projetos e linguagens de programação.

#### <a name="create-an-empty-project"></a>Criar um projeto Vazio

1. Abra o Visual Studio e crie um projeto.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl+Q** para abrir a caixa de pesquisa, digite **asp.net**, escolha **Criar um novo projeto de Aplicativo Web ASP.NET Core**. Na caixa de diálogo que aparece, digite o nome do **aplicativo cliente** e, em seguida, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **Novo Projeto**, expanda **Visual C#** e escolha **Web**. No painel central, escolha **aplicativo Web ASP.NET Core**, digite o nome do **aplicativo de cliente** e, em seguida, escolha **OK**.
    ::: moniker-end

    Se o modelo de projeto **Aplicativo Web ASP.NET Core** não for exibido, instale as cargas de trabalho **desenvolvimento do ASP.NET e para a Web** e **Desenvolvimento do .NET Core** primeiro. Para instalar as cargas de trabalho, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto** (selecione **Arquivo** > **Novo** > **Projeto**). O Instalador do Visual Studio é iniciado. Selecione as cargas de trabalho necessárias.

1. Selecione **Vazio** e, em seguida, clique em **OK**.

    O Visual Studio criará o projeto, que será aberto no Gerenciador de Soluções (painel direito).

#### <a name="configure-the-project-startup-file"></a>Configurar o arquivo de inicialização do projeto

* Abra o arquivo *./Startup.cs* e adicione as seguintes linhas ao método Configure:

    ```csharp
    app.UseDefaultFiles(); // Enables default file mapping on the web root.
    app.UseStaticFiles(); // Marks files on the web root as servable.
    ```

### <a name="install-the-vue-cli"></a>Instalar a CLI do Vue

Para instalar o módulo npm vue-cli, abra um prompt de comando e digite `npm install --g vue-cli` ou `npm install -g @vue/cli` para a versão 3.0 (atualmente em beta).

### <a name="scaffold-a-new-client-application-using-the-vue-cli"></a>Gerar um novo aplicativo cliente por scaffolding usando a CLI do Vue

1. Vá para o prompt de comando e altere o diretório atual para a pasta raiz do projeto.

1. Digite `vue init webpack client-app` e siga as etapas quando solicitado a responder perguntas adicionais.

    > [!NOTE]
    > Para arquivos *.vue*, você precisa usar o WebPack ou uma estrutura semelhante com um carregador para fazer a conversão. O TypeScript e o Visual Studio não sabem como compilar arquivos *.vue*. O mesmo é verdadeiro para agrupamento; o TypeScript não sabe como converter módulos ES2015 (ou seja, instruções `import` e `export`) em um arquivo único final *.js* a ser carregado no navegador. Novamente, o WebPack é a melhor opção. Para conduzir esse processo a partir do Visual Studio usando o MSBuild, você precisa começar com um modelo do Visual Studio. No momento, não há nenhum modelo do ASP.NET para desenvolvimento integrado do Vue.js.

#### <a name="modify-the-webpack-configuration-to-output-the-built-files-to-wwwroot"></a>Modificar a configuração de webpack para gerar os arquivos compilados em wwwroot

* Abra o arquivo *./client-app/config/index.js* e altere o `build.index` e o `build.assetsRoot` para o caminho wwwroot:

    ```js
    // Template for index.html
    index: path.resolve(__dirname, '../../wwwroot/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../../wwwroot'),
    ```

#### <a name="indicate-the-project-to-build-the-client-app-each-time-that-a-build-is-triggered"></a>Indique o projeto para criar o aplicativo cliente sempre que um build for disparado

1. No Visual Studio, vá para propriedades do **projeto**  >  **Properties**  >  **eventos de compilação**.

1. Na **Linha de comando do evento pré-build**, digite `npm --prefix ./client-app run build`.

#### <a name="configure-webpacks-output-module-names"></a>Configurar os nomes de módulo de saída do webpack

* Abra o arquivo *./client-app/build/webpack.base.conf.js* e adicione as seguintes propriedades à propriedade de saída:

    ```js
    devtoolModuleFilenameTemplate: '[absolute-resource-path]',
    devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
    ```

### <a name="add-typescript-support-with-the-vue-cli"></a>Adicionar suporte a TypeScript com a CLI do Vue

Essas etapas exigem a vue-cli 3.0 que, atualmente, está em versão beta.

1. Vá para o prompt de comando e altere o diretório atual para a pasta raiz do projeto.

1. Digite `vue create client-app` e, em seguida, escolha **Selecionar os recursos manualmente**.

1. Escolha **TypeScript** e, em seguida, selecione outras opções desejadas.

1. Siga as etapas restantes e responda às perguntas.

#### <a name="configure-a-vuejs-project-for-typescript"></a>Configurar um projeto Vue.js para TypeScript

1. Abra o arquivo *./client-app/tsconfig.json* e adicione `noEmit:true` às opções do compilador.

    Definindo essa opção, você impede que o projeto fique desorganizado sempre que criar no Visual Studio.

1. Em seguida, crie um arquivo *vue.config.js* no *./client-app/* e adicione o código a seguir.

    ```js
    module.exports = {
        outputDir: '../wwwroot',

        configureWebpack: {
            output: {
                devtoolModuleFilenameTemplate: '[absolute-resource-path]',
                devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
            }
        }
    };
    ```

    O código anterior configura o webpack e define a pasta wwwroot.

#### <a name="build-with-vue-cli-30"></a>Compilar com a vue-cli 3.0

Um problema desconhecido com a vue-cli 3.0 pode impedir a automatização do processo de build. Cada vez que tentar atualizar a pasta wwwroot, será preciso executar o comando `npm run build` na pasta do aplicativo cliente.

Como alternativa, você pode compilar o projeto vue-cli 3.0 como um evento pré-build usando as propriedades de projeto ASP.NET. Clique com o botão direito no projeto, escolha **Propriedades** e inclua os seguintes comandos na guia **Compilar**, na caixa de texto **Linha de comando do evento de pré-build**.

``` cmd
cd ./client-app
npm run build
cd ../
```

## <a name="limitations"></a>Limitações

* O atributo `lang` só é compatível com as linguagens JavaScript e TypeScript. Os valores aceitos são: js, jsx, ts e tsx.
* O atributo `lang` não funciona com marcas de modelo ou de estilo.
* Não há suporte para blocos de script de depuração em arquivos *.vue* devido à sua natureza pré-processada.
* O TypeScript não reconhece arquivos *.vue* como módulos. Você precisa de um arquivo que contém um código como o mostrado a seguir para informar a aparência dos arquivos *.vue* ao TypeScript (o modelo da vue-cli 3.0 já inclui esse arquivo).

    ```js
    // ./client-app/vue-shims.d.ts
    declare module "*.vue" {
        import Vue from "vue";
        export default Vue;
    }
    ```

* A execução do comando `npm run build` como um evento pré-build nas propriedades do projeto não funciona ao usar a vue-cli 3.0.

## <a name="see-also"></a>Veja também

- [Guia de introdução do Vue](https://vuejs.org/v2/guide).
- [Projeto da CLI do Vue](https://github.com/vuejs/vue-cli).
- [Documentação de configurações do Webpack](https://webpack.js.org/configuration/).
