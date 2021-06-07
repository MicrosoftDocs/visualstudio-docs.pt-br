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
ms.openlocfilehash: 8a36986842cdac85a8a3e6ab474024b8db552ee7
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433708"
---
# <a name="quickstart-create-your-first-nodejs-app-with-visual-studio"></a>Início rápido: criar seu primeiro aplicativo Node.js com o Visual Studio

Nesta introdução de 5 a 10 minutos ao IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará um aplicativo Web simples Node.js.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, instale o Visual Studio e configure seu ambiente de Node.js.

### <a name="install-visual-studio"></a>Instalar o Visual Studio

::: moniker range=">=vs-2019"
Se você ainda não instalou o Visual Studio 2019, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.
::: moniker-end
::: moniker range="vs-2017"
Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.
::: moniker-end

### <a name="set-up-your-nodejs-environment"></a>Configurar seu ambiente de Node.js

O Visual Studio pode ajudar a configurar seu ambiente, incluindo a instalação de ferramentas comuns com o desenvolvimento de Node.js.

1. No Visual Studio, acesse **ferramentas**  >  **obter ferramentas e recursos**.

1. Na Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento deNode.js** e selecione **Modificar** para baixar e instalar a carga de trabalho.

    ![Carga de trabalho de Node.js no Instalador do Visual Studio](../ide/media/quickstart-nodejs-workload.png)

1. Instale a versão LTS do [ tempo de execução doNode.js](https://nodejs.org/en/download/). Recomendamos a versão LTS para obter a melhor compatibilidade com estruturas e bibliotecas externas.

    Embora Node.js seja criada para arquiteturas de 32 bits e 64 bits, o instalador do Node.js oferece suporte apenas a uma versão instalada por vez.

1. Se o Visual Studio não detectar seu tempo de execução instalado (geralmente faz isso), configure seu projeto para referenciar o tempo de execução instalado:

   1. Depois de [criar seu projeto](#create-your-app-project), clique com o botão direito do mouse no nó do projeto.

   1. Selecione **Propriedades** e defina o **caminhoNode.exe**. Você pode usar uma instalação global do Node.js ou especificar o caminho para um intérprete local em cada um de seus projetos de Node.js.

## <a name="create-your-app-project"></a>Criar seu projeto de aplicativo

1. Se você ainda não fez isso, instale a versão LTS do [ tempo de execução doNode.js](https://nodejs.org/en/download/). Para obter mais informações, confira os [pré-requisitos](#prerequisites).

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"

    1. Pressione **Esc** para fechar a janela de início.

    1. Pressione **Ctrl + Q** para abrir a caixa de pesquisa e digite **Node.js**.

    1. Escolha **em branco Node.js aplicativo Web (JavaScript)**. Na caixa de diálogo, selecione **criar**.

    ::: moniker-end

    ::: moniker range="vs-2017"
    1. Na barra de menus superior, escolha **arquivo** > **novo** > **projeto**.

    1. No painel esquerdo da caixa de diálogo **novo projeto** , expanda **JavaScript** e escolha **Node.js**.

    1. No painel central, escolha **Node.js aplicativo Web em branco** e selecione **OK**.

    ::: moniker-end
    
    Se não vir o modelo de projeto **Aplicativo Web Node.js em Branco**, instale a carga de trabalho de **desenvolvimento de Node.js**. Para obter instruções detalhadas, consulte os [pré-requisitos](#prerequisites).

    O Visual Studio cria e abre o projeto. O arquivo de *server.js* do projeto é aberto no editor à esquerda.

## <a name="explore-the-ide"></a>Explorar o IDE

1. No painel direito, veja **Gerenciador de soluções**.

   ![Gerenciador de Soluções](../ide/media/quickstart-nodejs-solution-explorer.png)

   - Realçado em negrito é o seu projeto, usando o nome fornecido quando você configura o projeto. No disco, esse projeto é representado por um arquivo *. njsproj* na pasta do projeto.

   - No nível superior está uma solução que, por padrão, tem o mesmo nome que o projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

   - O nó **NPM** mostra os pacotes NPM instalados. Você pode clicar com o botão direito do mouse no nó NPM para procurar e instalar os pacotes do NPM usando uma caixa de diálogo.

1. Se você quiser instalar pacotes NPM ou comandos de Node.js em um prompt de comando, clique com o botão direito do mouse no nó do projeto e escolha **abrir prompt de comando aqui**.

   ![Prompt de comando do node dot j s](../ide/media/quickstart-nodejs-command-prompt.png)

1. Se você quiser testar a navegação para o código-fonte, no arquivo aberto *server.js* , selecione **http. createserver** e pressione **F12** ou escolha **ir para definição** no menu do contexto (clique com o botão direito do mouse). Esse comando leva você para a definição da `createServer` função em *http. d. TS*.

   ![Menu de contexto de Ir para Definição](../ide/media/quickstart-nodejs-gotodefinition.png)

1. Volte para *server.js* e localize esta linha de código: `res.end('Hello World\n');` . Modifique o código desta forma:

    `res.end('Hello World\n' + res.connection.`

    Quando você digita a **conexão.** o IntelliSense fornece opções para completar automaticamente a entrada do código.

   ![Preenchimento automático do IntelliSense](../ide/media/quickstart-nodejs-intellisense.png)

1. Escolha **localPort** e tipo **);** para concluir a instrução:

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-app"></a>Executar o aplicativo

1. Pressione **Ctrl + F5** (ou   >  **inicie a depuração sem depuração**) para executar o aplicativo. 
 
   O aplicativo é aberto em um navegador.

1. No navegador, verifique se você vê uma mensagem "Olá, Mundo" e o número da porta local.

Parabéns! Você criou um aplicativo Node.js simples com o Visual Studio. Para aprofundar-se, continue na seção **tutoriais** do Sumário.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o Express](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o React](../javascript/tutorial-nodejs-with-react-and-jsx.md)
