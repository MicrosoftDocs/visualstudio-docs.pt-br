---
title: Criar um aplicativo Vue.js usando as Ferramentas Node.js para Visual Studio
description: Crie aplicativos Node.js no Visual Studio usando a estrutura Vue.js
ms.custom: ''
ms.date: 07/06/2018
ms.technology: vs-nodejs
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 8ffe7a2a730f10d0f29a13b5123fbd7f56beda13
ms.sourcegitcommit: 12d6398c02e818de4fbcb4371bae9e5db6cf9509
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050151"
---
# <a name="create-a-vuejs-application-using-nodejs-tools-for-visual-studio"></a>Criar um aplicativo Vue.js usando as Ferramentas Node.js para Visual Studio

O Visual Studio 2017 inclui o suporte aprimorado para a estrutura [Vue.js](https://vuejs.org/), o que melhora a experiência de desenvolvimento ao criar um aplicativo com o Vue.js, o JavaScript e o TypeScript.

Os seguintes novos recursos dão suporte ao desenvolvimento de aplicativos Vue.js no Visual Studio:

* Suporte para blocos de Script, Estilo e Modelo em arquivos *.vue*
* Reconhecimento do atributo `lang` em arquivos *.vue*
* Modelos de projeto e de arquivo Vue.js

## <a name="prerequisites"></a>Pré-requisitos

* É necessário ter o Visual Studio 2017 versão 15.8 Versão Prévia 3 ou posterior instalado e a carga de trabalho **Desenvolvimento do Node.js**.

    > [!IMPORTANT]
    > Este artigo exige recursos que estão disponíveis apenas a partir do Visual Studio 2017 versão 15.8 Versão Prévia 3.

    Se você ainda não instalou o Visual Studio, acesse a página  [Downloads do Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)  para instalá-lo gratuitamente.

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto** (selecione **Arquivo** > **Novo** > **Projeto**). O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

* Para criar o projeto ASP.NET Core, é necessário ter instaladas as cargas de trabalho de desenvolvimento do ASP.NET e para a Web e de desenvolvimento multiplataforma do .NET Core.

* Você precisa ter o tempo de execução do Node.js instalado.

    Se não o tiver instalado, instale a versão LTS do site do [Node.js](https://nodejs.org/en/download/). Em geral, o Visual Studio detecta automaticamente o tempo de execução do Node.js instalado. Se ele não detectar um tempo de execução instalado, você poderá configurar o projeto para referenciar o tempo de execução instalado na página de propriedades. (Depois de criar um projeto, clique com o botão direito do mouse no nó do projeto e escolha **Propriedades**).

## <a name="create-a-vuejs-project-using-a-template"></a>Criar um projeto Vue.js usando um modelo

Use os novos modelos do Vue.js para criar um projeto. O uso do modelo é a maneira mais fácil de começar. Para obter etapas detalhadas, confira [Usar o Visual Studio para criar seu primeiro aplicativo Vue.js](../javascript/quickstart-vuejs-with-nodejs.md).

## <a name="create-a-vuejs-project-with-aspnet-core-and-the-vue-cli"></a>Criar um projeto do Vue.js com o ASP.NET Core e a CLI do Vue

O Vue.js fornece uma CLI oficial para o scaffolding rápido de projetos. Caso deseje usar a CLI para criar seu aplicativo, siga as etapas deste artigo para configurar o ambiente de desenvolvimento.

> [!IMPORTANT]
> Essas etapas pressupõem que você já tenha alguma experiência com a estrutura Vue.js. Se esse não for o caso, visite [Vue.js](https://vuejs.org/) para saber mais sobre a estrutura.

### <a name="create-a-new-aspnet-core-project"></a>Criar um projeto ASP.NET Core

Neste exemplo, você usará um aplicativo ASP.NET Core vazio (C#). No entanto, você pode escolher uma opção entre uma variedade de projetos e linguagens de programação.

#### <a name="create-an-empty-project"></a>Criar um projeto Vazio

1. Abra o Visual Studio e escolha **Arquivo** > **Novo** > **Projeto** no menu principal.

1. Em **Visual C#** > **Web**, escolha **Aplicativo Web ASP.NET Core** e, em seguida, clique em **OK**.

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

1. Digite `vue init webpack ClientApp` e siga as etapas quando solicitado a responder perguntas adicionais.

#### <a name="modify-the-webpack-configuration-to-output-the-built-files-to-wwwroot"></a>Modificar a configuração de webpack para gerar os arquivos compilados em wwwroot

* Abra o arquivo *./ClientApp/config/index.js* e altere o `build.index` e a `build.assetsRoot` para o caminho wwwroot:

    ```js
    // Template for index.html
    index: path.resolve(__dirname, '../../wwwroot/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../../wwwroot'),
    ```

#### <a name="indicate-the-project-to-build-the-clientapp-each-time-that-a-build-is-triggered"></a>Indicar ao projeto para criar o ClientApp sempre que um build é disparado

1. No Visual Studio, acesse **Projeto** > **Propriedades** > **Eventos de Build**.

1. Na **Linha de comando do evento pré-build**, digite `npm --prefix ./ClientApp run build`.

#### <a name="configure-webpacks-output-module-names"></a>Configurar os nomes de módulo de saída do webpack

* Abra o arquivo *./ClientApp/build/webpack.base.conf.js* e adicione as seguintes propriedades à propriedade de saída:

    ```js
    devtoolModuleFilenameTemplate: '[absolute-resource-path]',
    devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
    ```

### <a name="add-typescript-support-with-the-vue-cli"></a>Adicionar suporte a TypeScript com a CLI do Vue

Essas etapas exigem a vue-cli 3.0 que, atualmente, está em versão beta.

1. Vá para o prompt de comando e altere o diretório atual para a pasta raiz do projeto.

1. Digite `vue create ClientApp` e, em seguida, escolha **Selecionar os recursos manualmente**.

1. Escolha **TypeScript** e, em seguida, selecione outras opções desejadas.

1. Siga as etapas restantes e responda às perguntas.

#### <a name="configure-a-vuejs-project-for-typescript"></a>Configurar um projeto Vue.js para TypeScript

1. Abra o arquivo *./ClientApp/tsconfig.json* e adicione `noEmit:true` às opções do compilador.

    Definindo essa opção, você impede que o projeto fique desorganizado sempre que criar no Visual Studio.

1. Em seguida, crie um arquivo *vue.config.js* em *./ClientApp/* e adicione o código a seguir.

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

Um problema desconhecido com a vue-cli 3.0 impede a automatização do processo de build. Sempre que você tentar atualizar a pasta wwwroot, precisará executar o comando `npm run build` na pasta ClientApp.

## <a name="limitations"></a>Limitações

* O atributo `lang` só é compatível com as linguagens JavaScript e TypeScript. Os valores aceitos são: js, jsx, ts e tsx.
* O atributo `lang` não funciona com marcas de modelo ou de estilo.
* Não há suporte para blocos de script de depuração em arquivos *.vue* devido à sua natureza pré-processada.
* O TypeScript não reconhece arquivos *.vue* como módulos. Você precisa de um arquivo que contém um código como o mostrado a seguir para informar a aparência dos arquivos *.vue* ao TypeScript (o modelo da vue-cli 3.0 já inclui esse arquivo).

    ```js
    // ./ClientApp/vue-shims.d.ts
    declare module "*.vue" {
        import Vue from "vue";
        export default Vue;
    }
    ```

* A execução do comando `npm run build` como um evento pré-build nas propriedades do projeto não funciona ao usar a vue-cli 3.0.

## <a name="see-also"></a>Consulte também
https://vuejs.org/v2/guide – guia de introdução do Vue.  
https://github.com/vuejs/vue-cli – projeto da CLI do Vue.  
https://webpack.js.org/configuration/ – documentação de configurações de webpack.
