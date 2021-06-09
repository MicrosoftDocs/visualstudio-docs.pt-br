---
title: Criar um aplicativo Node.js e Express
description: Neste tutorial, saiba como criar um aplicativo de Node.js usando a estrutura de aplicativo Web Express no Visual Studio.
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
ms.openlocfilehash: 5433ae0e84396f3c16dc5ed50f51ce7e9eb7056f
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760972"
---
# <a name="tutorial-create-a-nodejs-and-express-app-in-visual-studio"></a>Tutorial: Criar um aplicativo Node.js e Express no Visual Studio

Neste tutorial para desenvolvimento no Visual Studio usando Node.js e Express, você criará um aplicativo Web Node.js simples, adicionará código a ele, explorará alguns recursos do IDE e executará o aplicativo. 

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range=">=vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

Neste tutorial, você aprenderá como:
> [!div class="checklist"]
> * Criar um projeto Node.js
> * Adicionar código
> * Usar o IntelliSense para editar o código
> * Executar o aplicativo
> * Atingir um ponto de interrupção no depurador

## <a name="before-you-begin"></a>Antes de começar

Aqui está algumas perguntas frequentes rápidas para apresentar alguns conceitos principais.

### <a name="what-is-nodejs"></a>O que é o Node.js?

O Node.js é um ambiente de runtime do JavaScript do servidor que executa o JavaScript no servidor.

### <a name="what-is-npm"></a>O que é o npm?

npm é o gerenciador de pacotes padrão do Node.js. O gerenciador de pacotes facilita para os programadores publicar e compartilhar o código-fonte das bibliotecas do Node.js e foi projetado para simplificar a instalação, a atualização e a desinstalação de bibliotecas.

### <a name="what-is-express"></a>O que é o Express?

O Express é uma estrutura de aplicativo Web, usada como uma estrutura de servidor do Node.js para criação de aplicativos Web. O Express permite que você escolha diferentes estruturas de front-end para criar uma interface do usuário, como Pug (anteriormente chamado de Jade). O Pug é usado neste tutorial.

## <a name="prerequisites"></a>Pré-requisitos

* Você precisa ter o Visual Studio instalado e a carga de trabalho de desenvolvimento de Node.js.

    ::: moniker range=">=vs-2019"
    Se você ainda não instalou o Visual Studio 2019, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.
    ::: moniker-end

    Se você precisar instalar a carga de trabalho, mas já tiver Visual Studio, acesse Ferramentas Obter Ferramentas e  >  **Recursos...**, que abre o Instalador do Visual Studio. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

    ![Carga de trabalho Node.js no instalador do VS](../ide/media/quickstart-nodejs-workload.png)

* Você precisa ter o runtime do Node.js instalado.

    Se você não o tiver instalado, recomendamos instalar a versão LTS do siteNode.jspara melhor [ compatibilidade ](https://nodejs.org/en/download/) com estruturas e bibliotecas externas. Node.js é criado para arquiteturas de 32 bits e 64 bits. As Node.js de Visual Studio, incluídas na carga de trabalho Node.js, são suportadas em ambas as versões. Apenas um é necessário e o Node.js instalador dá suporte apenas a um que está sendo instalado por vez.
    
    Em geral, o Visual Studio detecta automaticamente o runtime do Node.js instalado. Se ele não detectar um runtime instalado, você poderá configurar seu projeto para referenciar o runtime instalado na página de propriedades (depois de criar um projeto, clicar com o botão direito do mouse no nó do projeto, escolher Propriedades e definir o caminho **Node.exe**). Você pode usar uma instalação global do Node.js ou especificar o caminho para um interpretador local em cada um dos seus projetos Node.js dados. 

    Este tutorial foi testado com o Node.js 8.10.0.

## <a name="create-a-new-nodejs-project"></a>Criar um projeto Node.js

O Visual Studio gerencia arquivos de um único aplicativo em um *projeto*. O projeto inclui os arquivos de configuração, recursos e código-fonte.

Neste tutorial, você começará com um projeto simples que contém o código para um aplicativo Node.js e Express.

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **Node.js** e, em seguida, escolha **Criar um novo Aplicativo Básico Azure Node.js Express 4** (JavaScript). Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **Arquivo**  >  **Novo**  >  **Projeto**. No painel esquerdo da caixa de diálogo **Novo Projeto**, expanda **JavaScript** e escolha **Node.js**. No painel central, escolha **Aplicativo Azure Node.js Express 4 básico** e, em seguida, **OK**.
    ::: moniker-end
    Se você não vir o modelo de projeto **Aplicativo Azure Node.js Express 4 básico**, adicione a carga de trabalho de **desenvolvimento do Node.js**. Confira instruções detalhadas nos [Pré-requisitos](#prerequisites).

    O Visual Studio cria a solução e abre o projeto no painel direito. O arquivo de projeto *app.js* é aberto no editor (painel esquerdo).

    ![Estrutura do projeto](../javascript/media/tutorial-project-structure.png)

    (1) Realçado em **negrito** no projeto, usando o nome fornecido na caixa de diálogo **Novo Projeto**. No sistema de arquivos, este projeto é representado por um arquivo *.njsproj* na pasta do projeto. Você pode definir propriedades e variáveis de ambiente associadas ao projeto clicando com o botão direito do mouse no projeto e escolhendo **Propriedades**. Você pode fazer o ciclo com outras ferramentas de desenvolvimento, porque o arquivo de projeto não faz alterações personalizadas na fonte do projeto Node.js.

    (2) No nível superior, há uma solução que, por padrão, tem o mesmo nome do projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

    (3) O nó do npm mostra os pacotes npm instalados. Clique com o botão direito do mouse no nó do npm para pesquisar e instalar pacotes npm usando uma caixa de diálogo ou instalar e atualizar pacotes usando as configurações de *package.json* e as opções de clique com o botão direito do mouse no nó do npm.

    (4) *package.json* é um arquivo usado pelo npm para gerenciar versões e dependências de pacote para os pacotes instalados localmente. Para obter mais informações, consulte [Gerenciar pacotes npm](../javascript/npm-package-management.md).

    (5) Os arquivos de projeto como *app.js* são mostrados no nó do projeto. *app.js* é o arquivo de inicialização do projeto e é por isso que ele é exibido em **negrito**. Defina o arquivo de inicialização clicando com o botão direito do mouse em um arquivo no projeto e selecionando **Definir como arquivo de inicialização do Node.js**.

1. Abra o nó **npm** e certifique-se de que todos os pacotes de npm necessários estejam presentes.

    Se algum pacote estiver ausente (ícone de ponto de exclamação), você poderá clicar com o botão direito do mouse no nó **npm** e escolher **Instalar pacotes npm**.

## <a name="add-some-code"></a>Adicionar código

O aplicativo usa o Pug para a estrutura front-end de JavaScript. O Pug usa o código de marcação simples que é compilado em HTML. (O Pug é definido como o mecanismo de exibição em *app.js*. O código que define o mecanismo de exibição em *app.js* é `app.set('view engine', 'pug');`.)

1. No Gerenciador de Soluções (painel direito), abra a pasta de exibições e abra *index.pug*.

1. Substitua o conteúdo pela seguinte marcação.

    ```js
    extends layout

    block content
      h1= title
      p Welcome to #{title}
      script.
        var f1 = function() { document.getElementById('myImage').src='#{data.item1}' }
      script.
        var f2 = function() { document.getElementById('myImage').src='#{data.item2}' }
      script.
        var f3 = function() { document.getElementById('myImage').src='#{data.item3}' }

      button(onclick='f1()') One!
      button(onclick='f2()') Two!
      button(onclick='f3()') Three!
      p
      a: img(id='myImage' height='200' width='200' src='')
    ```

    O código anterior é usado para gerar dinamicamente uma página HTML com um título e uma mensagem de boas-vindas. A página também inclui o código para exibir uma imagem que muda sempre que você pressiona um botão.

1. Na pasta de rotas, abra *index.js*.

1. Adicione o código a seguir antes da chamada para `router.get`:

    ```js
    var getData = function () {
        var data = {
            'item1': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-76.jpg',
            'item2': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-77.jpg',
            'item3': 'http://public-domain-photos.com/free-stock-photos-1/flowers/cactus-78.jpg'
        }
        return data;
    }
    ````

    Esse código cria um objeto de dados que você passa para a página HTML gerada dinamicamente.

1. Substitua a chamada da função `router.get` pelo seguinte código:

    ```js
    router.get('/', function (req, res) {
        res.render('index', { title: 'Express', "data" });
    });
    ```

    O código anterior define a página atual usando o objeto roteador Express e renderiza a página, passando o título e o objeto de dados para a página. O arquivo *index.pug* é especificado aqui como a página a ser carregada quando *index.js* for executado. *index.js* é configurado como a rota padrão no código *app.js* (não mostrado).

    Para demonstrar os vários recursos do Visual Studio, há um erro proposital na linha de código que contém `res.render`. Você precisa corrigir o erro para que o aplicativo seja executado, o que você fará na próxima seção.

## <a name="use-intellisense"></a>Usar o IntelliSense

O IntelliSense é uma ferramenta do Visual Studio que ajuda você na codificação.

1. Em *index.js*, vá para a linha de código que contém `res.render`.

1. Coloque o cursor após a cadeia de caracteres `data`, digite `: get` e o IntelliSense mostrará a função `getData` definida anteriormente no código. Selecione `getData`.

    ![Usar o IntelliSense](../javascript/media/tutorial-nodejs-intellisense.png)

1. Adicione os parênteses para torná-lo uma chamada de função, `getData()` .

1. Remova a vírgula (`,`) antes de `"data"` e você verá o realce de sintaxe verde na expressão. Passe o mouse sobre o realce de sintaxe.

    ![Exibir erro de sintaxe](../javascript/media/tutorial-nodejs-syntax-checking.png)

    A última linha desta mensagem informa que o interpretador de JavaScript esperava uma vírgula (`,`).

1. No painel inferior, clique na guia **Lista de** Erros e selecione Build **+ IntelliSense** para o tipo de problemas relatados.

    Você verá o aviso e a descrição juntamente com o nome de arquivo e número de linha.

    ![Exibir lista de erros](../javascript/media/tutorial-nodejs-error-list.png)

1. Corrija o código adicionando a vírgula (`,`) antes de `"data"`.

    Quando for corrigida, a linha de código deverá ter esta aparência: `res.render('index', { title: 'Express', "data": getData() });`

## <a name="set-a-breakpoint"></a>Definir um ponto de interrupção

Em seguida, você executará o aplicativo com o depurador do Visual Studio anexado. Antes de fazer isso, você precisa definir um ponto de interrupção.

1. Em *index.js*, clique na medianiz esquerda antes da seguinte linha de código para definir um ponto de interrupção:

    `res.render('index', { title: 'Express', "data": getData() });`

    Pontos de interrupção são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não.

    ![Definir um ponto de interrupção](../javascript/media/tutorial-nodejs-set-breakpoint.png)

## <a name="run-the-application"></a>Executar o aplicativo

1. Selecione o destino de depuração na barra de ferramentas Depurar, como **Servidor Web (Google Chrome)** ou **Servidor Web (Microsoft Edge).**

    ::: moniker range=">=vs-2019"
    ![Selecionar o destino de depuração](../javascript/media/vs-2019/tutorial-nodejs-deploy-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![Selecionar o destino de depuração](../javascript/media/tutorial-nodejs-deploy-target.png)
    ::: moniker-end

    Se o Chrome estiver disponível em seu computador, mas não aparecer como uma opção, escolha **Procurar com** na lista suspensa de destinos de depuração e selecione Chrome como o destino padrão de navegador (escolha **Definir como padrão**).

1. Pressione **F5** (**Depurar** > **Iniciar Depuração**) para executar o aplicativo.

    O depurador faz uma pausa no ponto de interrupção que você definir. Agora, você pode inspecionar o estado do aplicativo.

1. Passe o mouse sobre `getData` para ver suas propriedades em um DataTip

    ![Inspecionar variáveis](../javascript/media/tutorial-nodejs-inspect-variables.png)

1. Pressione **F5** (**Depurar** > **Continuar**) para continuar.

    O aplicativo é aberto em um navegador.

    Na janela do navegador, você verá “Express” como o título e “Bem-vindo ao Express” no primeiro parágrafo.

1. Clique nos botões para exibir diferentes imagens.

    ![Aplicativo em execução no navegador](../javascript/media/tutorial-nodejs-running-in-browser.png)

1. Feche o navegador da Web.

## <a name="optional-publish-to-azure-app-service"></a>(Opcional) Publicar no Serviço de Aplicativo do Azure

1. No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e escolha **Publicar**.

   ![Publicar no Serviço de Aplicativo do Azure](../javascript/media/tutorial-nodejs-publish-to-azure.png)

1. Escolha **Serviço de Aplicativo do Microsoft Azure**.

    Na caixa de diálogo **Serviço de Aplicativo**, você pode entrar na sua conta do Azure e conectar-se a assinaturas do Azure existentes.

1. Siga as etapas restantes para selecionar uma assinatura, escolha ou crie um grupo de recursos, escolha ou crie um plano de serviço de aplicativo e, em seguida, siga as etapas quando solicitado para publicar no Azure. Para obter instruções mais detalhadas, confira [Publicar no site do Azure usando a implantação da Web](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy).

1. A janela **Saída** mostra o andamento na implantação para o Azure.

    Em uma implantação bem-sucedida, o aplicativo é aberto em um navegador em execução no serviço de aplicativo do Azure. Clique em um botão para exibir uma imagem.

   ![Aplicativo em execução no Serviço de Aplicativo do Azure](../javascript/media/tutorial-nodejs-running-in-azure.png)

Parabéns por concluir este tutorial.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Extensão do serviço de linguagem AngularJS](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)
