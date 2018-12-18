---
title: 'Início Rápido: Usar o Visual Studio para criar seu primeiro aplicativo Vue.js'
description: Neste início rápido, você criará um aplicativo Vue.js no Visual Studio usando as Ferramentas Node.js para Visual Studio
ms.date: 09/24/2018
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
ms.openlocfilehash: 3862f62439bd9b919d3c0534a8c2fe2d3c16fea9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926612"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-vuejs-app"></a>Início Rápido: Usar o Visual Studio para criar seu primeiro aplicativo Vue.js

Nesta introdução de 5 a 10 minutos do IDE (ambiente de desenvolvimento integrado) do Visual Studio, você criará e executará um aplicativo Web Vue.js simples. Se você ainda não tiver instalado o Visual Studio 2017, acesse a página [Downloads do Visual Studio](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) para instalá-lo gratuitamente.

> [!IMPORTANT]
> Este artigo requer o modelo Vue.js, disponível no Visual Studio 2017 versão 15.8 e posteriores.

## <a name="create-a-project"></a>Criar um projeto

Primeiro, você criará um projeto de aplicativo Web Vue.js.

1. Se não tiver o tempo de execução do Node.js instalado, instale a versão LTS do site do [Node.js](https://nodejs.org/en/download/).

    Em geral, o Visual Studio detecta automaticamente o tempo de execução do Node.js instalado. Se ele não detectar um tempo de execução instalado, você poderá configurar seu projeto para fazer referência ao tempo de execução instalado na página de propriedades (depois de criar um projeto, clique com botão direito do mouse no nó do projeto e escolha **Propriedades**).

1. Abra o Visual Studio 2017.

1. Na barra de menus superior, escolha **Arquivo** > **Novo** > **Projeto**.

1. Na caixa de diálogo **Novo Projeto**, em **JavaScript** > **Node.js** ou **TypeScript** > **Node.js**, escolha **Aplicativo Web Vue.js Básico** e, em seguida, insira um nome de projeto e clique em **OK**.

     ![Modelo do Vue.js](../javascript/media/vuejs-template.png)

    O Visual Studio cria o projeto. O novo projeto é aberto no Gerenciador de Soluções (painel direito).

     Se o modelo de projeto do **Aplicativo Web Vue.js Básico** não for exibido, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de Node.js** e, em seguida, selecione **Modificar**.

     ![Carga de trabalho Node.js no instalador do VS](../ide/media/quickstart-nodejs-workload.png)

    O Visual Studio cria a nova solução e abre o projeto.

1. Verifique a janela de Saída (painel inferior) para ver o progresso da instalação dos pacotes npm necessários para o aplicativo.

1. No Gerenciador de Soluções, abra o nó **npm** e verifique se todos os pacotes npm listados estão instalados.

    Se um pacote estiver ausente (ícone de ponto de exclamação), clique com o botão direito do mouse no nó **npm** e escolha **Instalar Pacotes npm Ausentes**.

## <a name="explore-the-ide"></a>Explorar o IDE

1. Observe o **Gerenciador de Soluções** no painel direito.

     ![Solução do Vue.js](../javascript/media/vuejs-solution.png)

   - O seu projeto está realçado em negrito, usando o nome que você forneceu na caixa de diálogo **Novo Projeto**. No disco, esse projeto é representado por um arquivo *.njsproj* na pasta do projeto.

   - No nível superior está uma solução que, por padrão, tem o mesmo nome que o projeto. Uma solução, representada por um arquivo *.sln* no disco, é um contêiner para um ou mais projetos relacionados.

   - O nó **npm** mostra os pacotes npm instalados. Você pode clicar com o botão direito do mouse no nó de npm para pesquisar e instalar pacotes de npm usando uma caixa de diálogo.

2. Caso deseje instalar pacotes npm ou executar comandos do Node.js em um prompt de comando, clique com o botão direito do mouse no nó do projeto e escolha **Abrir Prompt de Comando Aqui**.

## <a name="add-a-vue-file-to-the-project"></a>Adicionar um arquivo .vue ao projeto

1. No Gerenciador de Soluções, clique com o botão direito do mouse em qualquer pasta, como a pasta *src* e, em seguida, escolha **Adicionar** > **Novo Item**.

1. Selecione **Componente de Arquivo Único JavaScript Vue** ou **Componente de Arquivo Único TypeScript Vue** e, em seguida, clique em **Adicionar**.

    O Visual Studio adiciona o novo arquivo ao projeto.

## <a name="build-the-project"></a>Compilar o projeto

1. (Somente projeto TypeScript) No Visual Studio, escolha **Compilar** > **Limpar Solução**.

1. Em seguida, escolha **Compilar** > **Compilar Solução** para criar o projeto. Verifique a janela de **Saída** para ver os resultados do build.

    O modelo de projeto Vue.js usa o script npm `build`, configurando um evento pós-build. Caso deseje modificar essa configuração, abra o arquivo de projeto (*\<projectname\>.njsproj*) no Windows Explorer e localize esta linha de código:

    ```xml
    <PostBuildEvent>npm run build</PostBuildEvent>
    ```

## <a name="run-the-application"></a>Executar o aplicativo

1. Pressione **Ctrl**+**F5** (ou **Depurar > Iniciar sem Depuração**) para executar o aplicativo.

   No console, você verá a mensagem *Iniciando Development Server*.

   Em seguida, o aplicativo será aberto em um navegador.

   ![Aplicativo Vue.js em execução no navegador](../javascript/media/vuejs-running-app.png)

1. Feche o navegador da Web.

Parabéns por concluir este Guia de Início Rápido! Esperamos que você tenha aprendido um pouco sobre como usar o IDE do Visual Studio e com o Vue.js. Se você quiser se aprofundar mais em seus recursos, continue com um tutorial na seção **Tutoriais** do sumário.

## <a name="next-steps"></a>Próximas etapas

- Veja o [Tutorial para Node.js e Express](../nodejs/tutorial-nodejs.md)
- Veja o [Tutorial para Node.js e React](../nodejs/tutorial-nodejs-with-react-and-jsx.md)
- [Implantar o aplicativo no Serviço de Aplicativo do Linux](../javascript/publish-nodejs-app-azure.md)