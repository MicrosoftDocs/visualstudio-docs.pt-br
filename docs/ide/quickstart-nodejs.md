---
title: Criar seu primeiro aplicativo Node.js
ms.custom: SEO-VS-2020
description: Neste guia de início rápido, você cria um aplicativo Node.js no Visual Studio
ms.date: 03/25/2021
ms.technology: vs-javascript
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: ecd65c0348ac16a2097061726e3896961ae04482
ms.sourcegitcommit: 00e16b9afe6b22ba0591e4d0d92690544e6d4357
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2021
ms.locfileid: "105617046"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-nodejs-app"></a>Início rápido: usar o Visual Studio para criar seu primeiro aplicativo Node.js

Nesta introdução de 5 a 10 minutos do IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo Web Node.js simples.

## <a name="prerequisites"></a>Pré-requisitos

* Você precisa ter o Visual Studio instalado e a carga de trabalho de desenvolvimento de Node.js.

    ::: moniker range=">=vs-2019"
    Se você ainda não instalou o Visual Studio 2019, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.
    ::: moniker-end

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre o instalador do Visual Studio. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

    ![Carga de trabalho Node.js no instalador do VS](../ide/media/quickstart-nodejs-workload.png)

* Você precisa ter o runtime do Node.js instalado.

    Se você não o tiver instalado, recomendamos que instale a versão LTS do site [Node.js](https://nodejs.org/en/download/) para obter a melhor compatibilidade com estruturas e bibliotecas externas. Node.js é compilado para arquiteturas de 32 bits e 64 bits. As ferramentas de Node.js no Visual Studio, incluídas na carga de trabalho do Node.js, dão suporte a ambas as versões. Apenas um é necessário e o instalador do Node.js dá suporte apenas a uma instalação de cada vez.
    
    Em geral, o Visual Studio detecta automaticamente o runtime do Node.js instalado. Se ele não detectar um tempo de execução instalado, você poderá configurar seu projeto para fazer referência ao tempo de execução instalado na página Propriedades (depois de criar um projeto, clique com o botão direito do mouse no nó do projeto, escolha **Propriedades** e defina o **Node.exe caminho**). Você pode usar uma instalação global do Node.js ou pode especificar o caminho para um intérprete local em cada um de seus projetos de Node.js. 

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo Web Node.js.

1. Se não tiver o runtime do Node.js instalado, instale a versão LTS do site do [Node.js](https://nodejs.org/en/download/).

    Para obter mais informações, consulte os pré-requisitos.

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **Node.js** e, em seguida, escolha **Criar novo projeto de Aplicativo Web Node.js em Branco** (JavaScript). Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **Novo Projeto**, expanda **JavaScript** e escolha **Node.js**. No painel central, escolha **Aplicativo Web Node.js em branco** e, em seguida, escolha **OK**.
    ::: moniker-end
    Se não vir o modelo de projeto **Aplicativo Web Node.js em Branco**, instale a carga de trabalho de **desenvolvimento de Node.js**. Confira instruções detalhadas nos [Pré-requisitos](#prerequisites).

    O Visual Studio cria a nova solução e abre o projeto. *server.js* é aberto no editor no painel esquerdo.

## <a name="explore-the-ide"></a>Explorar o IDE

1. Observe o **Gerenciador de Soluções** no painel direito.

   ![Gerenciador de Soluções](../ide/media/quickstart-nodejs-solution-explorer.png)

   - O seu projeto está realçado em negrito, usando o nome que você forneceu na caixa de diálogo **Novo Projeto**. No disco, esse projeto é representado por um arquivo *. njsproj* na pasta do projeto.

   - No nível superior está uma solução que, por padrão, tem o mesmo nome que o projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

   - O nó de npm mostra os pacotes npm instalados. Você pode clicar com o botão direito do mouse no nó de npm para pesquisar e instalar pacotes de npm usando uma caixa de diálogo.

1. Se você quiser instalar pacotes NPM ou comandos de Node.js em um prompt de comando, clique com o botão direito do mouse no nó do projeto e escolha **abrir prompt de comando aqui**.

   ![Prompt de comando do Node.js](../ide/media/quickstart-nodejs-command-prompt.png)

1. No arquivo *server.js* no editor (painel esquerdo), escolha `http.createServer` e pressione **F12** ou escolha **Ir para Definição** no menu de contexto (acessado com o clique do botão direito do mouse). Esse comando leva você para a definição da `createServer` função em *index. d. TS*.

   ![Menu de contexto de Ir para Definição](../ide/media/quickstart-nodejs-gotodefinition.png)

1. Volte para *server.js*, coloque o cursor no final da cadeia de caracteres nesta linha de código, `res.end('Hello World\n');` e modifique-a para que fique assim:

    `res.end('Hello World\n' + res.connection.`

    Quando você digita `connection.`, o IntelliSense fornece opções para completar automaticamente a entrada de código.

   ![Preenchimento automático do IntelliSense](../ide/media/quickstart-nodejs-intellisense.png)

1. Escolha **localPort** e, em seguida, digite `);` para completar a instrução para que ela fique assim:

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **Ctrl** + **F5** (ou **debug > iniciar sem depuração**) para executar o aplicativo. O aplicativo é aberto em um navegador.

1. Na janela do navegador, você verá “Olá, Mundo”, além do número da porta local.

1. Feche o navegador da Web.

Parabéns por concluir este Início Rápido! Nele, você se familiarizou com o IDE do Visual Studio e o Node.js. Caso deseje se aprofundar mais nas funcionalidades, continue com um tutorial na seção **Tutoriais** do sumário.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o Express](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o React](../javascript/tutorial-nodejs-with-react-and-jsx.md)