---
title: Criar seu primeiro Node.js aplicativo
ms.custom:
- acquisition
- SEO-VS-2020
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
ms.openlocfilehash: d9397cb121ab3aa68d368a0cc7e1ab709411f6b6
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112113160"
---
# <a name="quickstart-create-your-first-nodejs-app-with-visual-studio"></a>Início Rápido: Criar seu primeiro aplicativo Node.js com Visual Studio

Nesta introdução de 5 a 10 minutos ao Visual Studio IDE (ambiente de desenvolvimento integrado) de 5 a 10 minutos, você criará um aplicativo Web Node.js simples.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, instale o Visual Studio e configurar seu ambiente Node.js aplicativo.

### <a name="install-visual-studio"></a>Instalar o Visual Studio

::: moniker range=">=vs-2019"
Se você ainda não instalou o Visual Studio 2019, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.
::: moniker-end
::: moniker range="vs-2017"
Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.
::: moniker-end

### <a name="set-up-your-nodejs-environment"></a>Configurar seu ambiente Node.js ambiente

Visual Studio pode ajudar a configurar seu ambiente, incluindo a instalação de ferramentas comuns com Node.js desenvolvimento.

1. No Visual Studio, acesse **Ferramentas** Obter Ferramentas e  >  **Recursos**.

1. Na Instalador do Visual Studio, escolha a carga **de trabalhoNode.js desenvolvimento** e selecione **Modificar** para baixar e instalar a carga de trabalho.

    ![Node.js carga de trabalho no Instalador do Visual Studio](../ide/media/quickstart-nodejs-workload.png)

1. Instale a versão LTS do [ runtimeNode.js](https://nodejs.org/en/download/). Recomendamos a versão ltS para melhor compatibilidade com estruturas e bibliotecas externas.

    Embora Node.js seja criado para arquiteturas de 32 bits e 64 bits, o Node.js instalador dá suporte apenas a uma versão instalada por vez.

1. Se Visual Studio não detectar o runtime instalado (geralmente, o faz), configure seu projeto para fazer referência ao runtime instalado:

   1. Depois de [criar seu projeto,](#create-your-app-project)clique com o botão direito do mouse no nó do projeto.

   1. Selecione **Propriedades** e de definido o **Node.exe caminho**. Você pode usar uma instalação global do Node.js ou especificar o caminho para um interpretador local em cada um dos seus Node.js projetos.

## <a name="create-your-app-project"></a>Criar seu projeto de aplicativo

1. Se você ainda não fez isso, instale a versão LTS do [runtimeNode.js .](https://nodejs.org/en/download/) Para obter mais informações, confira os [pré-requisitos](#prerequisites).

1. Abra o Visual Studio.

1. Criar um novo projeto.

    ::: moniker range=">=vs-2019"

    1. Pressione **Esc** para fechar a janela de início.

    1. Pressione **Ctrl + Q** para abrir a caixa de pesquisa e digite **Node.js**.

    1. Escolha **Em branco Node.js Aplicativo Web (JavaScript)**. Na caixa de diálogo, selecione **Criar**.

    ::: moniker-end

    ::: moniker range="vs-2017"
    1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

    1. No painel esquerdo da caixa de diálogo **Novo Projeto,** expanda **JavaScript** e escolha **Node.js**.

    1. No painel central, escolha Em **branco Node.js Aplicativo Web** e selecione **OK.**

    ::: moniker-end
    
    Se não vir o modelo de projeto **Aplicativo Web Node.js em Branco**, instale a carga de trabalho de **desenvolvimento de Node.js**. Para obter instruções detalhadas, consulte [os pré-requisitos.](#prerequisites)

    Visual Studio cria e abre o projeto. O arquivo *server.js* do projeto é aberto no editor à esquerda.

## <a name="explore-the-ide"></a>Explorar o IDE

1. No painel direito, veja **Gerenciador de Soluções**.

   ![Gerenciador de Soluções](../ide/media/quickstart-nodejs-solution-explorer.png)

   - Realçada em negrito está seu projeto, usando o nome fornecido quando você configura o projeto. No disco, esse projeto é representado por um *arquivo .njsproj* na pasta do projeto.

   - No nível superior está uma solução que, por padrão, tem o mesmo nome que o projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

   - O **nó npm** mostra pacotes npm instalados. Você pode clicar com o botão direito do mouse no nó npm para pesquisar e instalar pacotes npm usando uma caixa de diálogo.

1. Se você quiser instalar pacotes npm ou Node.js comandos de um prompt de comando, clique com o botão direito do mouse no nó do projeto e escolha **Abrir Prompt de Comando Aqui.**

   ![Prompt de comando do node dot j s](../ide/media/quickstart-nodejs-command-prompt.png)

1. Se você quiser testar a navegação para o código-fonte, *no* arquivoserver.jsaberto, selecione  **http.createServer** e pressione **F12** ou escolha Ir para Definição no menu de contexto (clique com o botão direito do mouse). Esse comando leva você para a definição da `createServer` função em *http.d.ts*.

   ![Menu de contexto de Ir para Definição](../ide/media/quickstart-nodejs-gotodefinition.png)

1. Go back para *server.js* e localizar esta linha de código: `res.end('Hello World\n');` . Modifique o código desta forma:

    `res.end('Hello World\n' + res.connection.`

    Quando você digita **a conexão.**, o IntelliSense fornece opções para concluir automaticamente a entrada de código.

   ![Preenchimento automático do IntelliSense](../ide/media/quickstart-nodejs-intellisense.png)

1. Escolha **localPort** e digite **);** para concluir a instrução :

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-app"></a>Executar o aplicativo

1. Pressione **Ctrl+F5** (ou **Depurar**  >  **Iniciar sem Depuração)** para executar o aplicativo. 
 
   O aplicativo é aberto em um navegador.

1. No navegador, verifique se você vê uma mensagem "Olá, Mundo" e o número da porta local.

Parabéns! Você criou um aplicativo de Node.js simples com Visual Studio. Para se aprofundar, continue na seção **Tutoriais** do índice.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o Express](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Tutorial para o Node.js e o React](../javascript/tutorial-nodejs-with-react-and-jsx.md)
