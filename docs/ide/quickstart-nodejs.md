---
title: 'Início rápido: usar o Visual Studio para criar seu primeiro aplicativo Node.js'
description: Neste guia de início rápido, você cria um aplicativo Node.js no Visual Studio
ms.date: 06/27/2018
ms.prod: visual-studio-dev15
ms.technology: vs-nodejs
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: e18f1e2063fd4007eba13d76473d634265b6a51f
ms.sourcegitcommit: 7a11a094a353f2e2a2077ad863ca4c0fb97f7ec5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39131850"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-nodejs-app"></a>Início rápido: usar o Visual Studio para criar seu primeiro aplicativo Node.js

Nesta introdução de 5 a 10 minutos do IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo Web Node.js simples. Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) para instalá-lo gratuitamente.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo Web Node.js.

1. Se não tiver o tempo de execução do Node.js instalado, instale a versão LTS do site do [Node.js](https://nodejs.org/en/download/).

    Em geral, o Visual Studio detecta automaticamente o tempo de execução do Node.js instalado. Se ele não detectar um tempo de execução instalado, você poderá configurar seu projeto para fazer referência ao tempo de execução instalado na página de propriedades (depois de criar um projeto, clique com botão direito do mouse no nó do projeto e escolha **Propriedades**).

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. Na caixa de diálogo **Novo Projeto**, no painel esquerdo, expanda **JavaScript** e escolha **Node.js**. No painel central, escolha **Aplicativo Web Node.js em branco** e, em seguida, escolha **OK**.

     Se você não vir o modelo de projeto do **Aplicativo Web Node.js em branco**, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho Node.js no instalador do VS](../ide/media/quickstart-nodejs-workload.png)

    Depois que você escolher o modelo **Aplicativo Web Node.js em Branco** e clicar em **OK**, o Visual Studio criará a solução e abrirá o projeto. *server.js* é aberto no editor no painel esquerdo.

## <a name="explore-the-ide"></a>Explorar o IDE

1. Observe o **Gerenciador de Soluções** no painel direito.

   ![Gerenciador de Soluções](../ide/media/quickstart-nodejs-solution-explorer.png)

   - O seu projeto está realçado em negrito, usando o nome que você forneceu na caixa de diálogo **Novo Projeto**. No disco, este projeto é representado por um arquivo *.njsproj* na pasta do projeto.

   - No nível superior está uma solução que, por padrão, tem o mesmo nome que o projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

   - O nó de npm mostra os pacotes npm instalados. Você pode clicar com o botão direito do mouse no nó de npm para pesquisar e instalar pacotes de npm usando uma caixa de diálogo.

1. Caso deseje instalar pacotes npm ou comandos do Node.js por meio de um prompt de comando, clique com o botão direito do mouse no nó do projeto e escolha **Abrir Prompt de Comando Aqui**.

   ![Prompt de comando do Node.js](../ide/media/quickstart-nodejs-command-prompt.png)

1. No arquivo *server.js* no editor (painel esquerdo), escolha `http.createServer` e pressione **F12** ou escolha **Ir para Definição** no menu de contexto (acessado com o clique do botão direito do mouse). Esse comando acessará a definição da função `createServer` em *index.d.ts*.

   ![Menu de contexto de Ir para Definição](../ide/media/quickstart-nodejs-gotodefinition.png)

1. Volte para *server.js*, coloque o cursor no final da cadeia de caracteres nesta linha de código, `res.end('Hello World\n');` e modifique-a para que fique assim:

    `res.end('Hello World\n' + res.connection.`

    Quando você digita `connection.`, o IntelliSense fornece opções para completar automaticamente a entrada de código.

   ![Preenchimento automático do IntelliSense](../ide/media/quickstart-nodejs-intellisense.png)

1. Escolha **localPort**e, em seguida, digite `);` para completar a instrução para que ela fique assim:

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **Ctrl**+**F5** (ou **Depurar > Iniciar sem Depuração**) para executar o aplicativo. O aplicativo é aberto em um navegador.

1. Na janela do navegador, você verá “Olá, Mundo”, além do número da porta local.

1. Feche o navegador da Web.

Parabéns por concluir este Início Rápido! Nele, você se familiarizou com o IDE do Visual Studio e o Node.js. Caso deseje se aprofundar mais nas funcionalidades, continue com um tutorial na seção **Tutoriais** do sumário.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)

- [Tutorial para o Node.js e o Express](../javascript/tutorial-nodejs.md)
- [Tutorial para o Node.js e o React](../javascript/tutorial-nodejs-with-react-and-jsx.md)