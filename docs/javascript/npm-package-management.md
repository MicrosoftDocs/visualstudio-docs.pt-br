---
title: Gerenciar pacotes npm
description: O Visual Studio ajuda você a gerenciar pacotes usando o npm (gerenciador de pacotes do Node.js)
ms.custom: seodec18
ms.date: 02/23/2021
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 2fcf1bd9e9ef5c3ff0663cf12684e6e638d1e5e4
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729280"
---
# <a name="manage-npm-packages-in-visual-studio"></a>Gerenciar pacotes de npm no Visual Studio

O npm permite que você instale e gerencie pacotes a serem usados em seus aplicativos Node.js. O Visual Studio facilita a interação com o npm e emite comandos do npm diretamente ou por meio da interface do usuário. Se você não conhece o npm e quer saber mais, acesse a [documentação do npm](https://docs.npmjs.com/).

Visual Studio integração com npm é diferente dependendo do tipo de projeto.
* [Node.js](#nodejs-projects)
* [ASP.NET Core](#aspnet-core-projects)
* [Abrir pasta (Node.js)](../javascript/develop-javascript-code-without-solutions-projects.md)

> [!Important]
> npm espera a *pasta node_modules* epackage.js *na* raiz do projeto. Se a estrutura de pastas do aplicativo for diferente, você deverá modificar sua estrutura de pastas se quiser gerenciar pacotes npm usando Visual Studio.

## <a name="nodejs-projects"></a>Node.js projetos

Para Node.js, você pode executar as seguintes tarefas:
* [Instalar os pacotes usando o Gerenciador de Soluções](#npmInstallWindow)
* [Gerenciar pacotes instalados usando o Gerenciador de Soluções](#solutionExplorer)
* [Usar o comando `.npm` na janela interativa do Node.js](#interactive)

Esses recursos funcionam juntos e são sincronizados com o sistema de projeto e o arquivo *package.json* no projeto.

### <a name="prerequisites"></a>Pré-requisitos

Você precisa da carga **Node.js de** desenvolvimento e do runtime Node.js instalado para adicionar suporte ao npm ao seu projeto. Para ver as etapas detalhadas, [consulte Criar um Node.js projeto](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json).

> [!NOTE]
> Para projetos Node.js existentes, use  o modelo de solução de código Node.js existente ou o tipo de projeto Abrir pasta [(Node.js)](../javascript/develop-javascript-code-without-solutions-projects.md) para habilitar o npm em seu projeto.

### <a name="install-packages-from-solution-explorer-nodejs"></a><a name="npmInstallWindow"></a> Instalar pacotes do Gerenciador de Soluções (Node.js)

Para Node.js, a maneira mais fácil de instalar pacotes npm é por meio da janela de instalação do pacote npm. Para acessar essa janela, clique com o botão direito do mouse no nó do **npm** no projeto e selecione **Instalar Novos Pacotes do npm**.

:::image type="content" source="../javascript/media/solution-explorer-install-package.png" alt-text="Instalar o novo pacote do npm usando o Gerenciador de Soluções" border="true":::

Nessa janela, você pode procurar por um pacote, especificar as opções e instalar.

![Captura de tela da caixa de diálogo Instalar Novos Pacotes npm. O pacote azure 2.2.1-preview está selecionado e os detalhes e as opções para esse pacote são mostrados.](../javascript/media/search-package.png)

* **Tipo de dependência** – escolha entre os pacotes **Padrão**, **Desenvolvimento** e **Opcional**. Padrão especifica que o pacote é uma dependência de runtime, enquanto Desenvolvimento especifica que o pacote só é necessário durante o desenvolvimento.
* **Adicionar ao package.json** – recomendado. Essa opção configurável foi preterida.
* **Versão selecionada** – selecione a versão do pacote que você deseja instalar.
* **Outros argumentos do npm** – especifique outros argumentos padrão do npm. Por exemplo, você pode inserir um valor de versão como `@~0.8` para instalar uma versão específica que não está disponível na lista de versões.

Você pode ver o progresso da instalação na  saída **npm** na janela Saída (para abrir a janela, escolha Exibir Saída ou  >   pressione **Ctrl**  +  **Alt**  +  **O**). Isso pode levar algum tempo.

![saída npm](../javascript/media/npm-output.png)

> [!TIP]
> É possível pesquisar pacotes com escopo acrescentando a consulta de pesquisa com o escopo desejado, por exemplo, digite `@types/mocha` para procurar por arquivos de definição de TypeScript para moca. Além disso, ao instalar definições de tipo para TypeScript, você pode especificar a versão do TypeScript que você está direcionando adicionando no `@ts2.6` campo de argumento npm.

### <a name="manage-installed-packages-in-solution-explorer-nodejs"></a><a name="solutionExplorer"></a>Gerenciar pacotes instalados no Gerenciador de Soluções (Node.js)

Os pacotes do npm são mostrados no Gerenciador de Soluções. As entradas no nó **npm** imitam as dependências do arquivo *package.json*.

![Captura de tela do nó npm no Gerenciador de Soluções mostrando o status de instalação dos pacotes npm.](../javascript/media/solution-explorer-status.png)

### <a name="package-status"></a>Status do pacote

* ![Pacote instalado](../javascript/media/installed-npm.png) – Instalado e listado no package.json
* ![Pacote desconhecido](../javascript/media/extraneous-npm.png) – instalado, mas não listado explicitamente no package.json
* ![Pacote ausente](../javascript/media/missing-npm.png) – Não instalado, mas listado no package.json

::: moniker range=">=vs-2019"
Clique com o botão direito do mouse no nó **NPM** para executar uma das seguintes ações:

* **Instalar novos pacotes do NPM** Abre a interface do usuário para instalar novos pacotes.
* **Instalar pacotes do NPM** Executa o comando NPM install para instalar todos os pacotes listados em *package.jsem*. (É executado `npm install` .)
* **Atualizar pacotes NPM** Atualiza pacotes para as versões mais recentes, de acordo com o intervalo de controle de versão semântico (SemVer) especificado no *package.jsem*. (Executa `npm update --save` .). Os intervalos de SemVer normalmente são especificados usando "~" ou "^". Para obter mais informações, [package.jsna configuração](../javascript/configure-packages-with-package-json.md).

Clique com o botão direito do mouse em um nó de pacote para executar uma das seguintes ações:

* **Instalar pacote (s) NPM** Executa o comando NPM install para instalar a versão do pacote listada em *package.jsem*. (É executado `npm install` .)
* **Atualizar pacote (s) NPM** Atualiza o pacote para a versão mais recente, de acordo com o intervalo de SemVer especificado em *package.jsem*. (Executar `npm update --save` .) Os intervalos de SemVer normalmente são especificados usando "~" ou "^".
* **Desinstalar pacote (s) NPM** Desinstala o pacote e o Remove do *package.jsem* (executado `npm uninstall --save` .)
::: moniker-end
::: moniker range="vs-2017"
Clique com o botão direito do mouse em um nó de pacote ou no nó do **npm** para executar uma das seguintes ações:
* **Instalar pacotes ausentes** listados em *package.json*
* **Atualizar pacotes NPM** para a versão mais recente
* **Desinstalar um pacote** e remover do *package.json*
::: moniker-end

>[!NOTE]
> Para obter ajuda para resolver problemas com pacotes do NPM, consulte [solução de problemas](#troubleshooting-npm-packages).

### <a name="use-the-npm-command-in-the-nodejs-interactive-window-nodejs"></a><a name="interactive"></a>Usar o comando. NPM na janela interativa de Node.js (Node.js)

Você também pode usar o comando `.npm` na janela interativa do Node.js para executar comandos do npm. Para abrir a janela, clique com o botão direito do mouse no projeto em Gerenciador de soluções e escolha **abrir Node.js janela interativa** (ou pressione **Ctrl**  +  **K**, **N**).

Na janela, você pode usar comandos como o seguinte para instalar um pacote:

`.npm install azure@4.2.3`

 > [!Tip]
 > Por padrão, o npm será executado no diretório inicial do projeto. Se houver vários projetos na solução, especifique o nome ou o caminho do projeto entre colchetes.
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > Se seu projeto não contiver um arquivo package.json, use `.npm init -y` para criar um novo arquivo package.json com as entradas padrão.

 ## <a name="aspnet-core-projects"></a>Projetos de ASP.NET Core

Para projetos como ASP.NET Core projetos, você pode integrar o suporte do NPM em seu projeto e usar o NPM para instalar pacotes.
* [Adicionar suporte a npm a um projeto](#npmAdd)
* [Instalar pacotes usando package.json](#npmInstallPackage)

>[!NOTE]
> Para ASP.NET Core, você também pode usar [o Gerenciador](/aspnet/core/client-side/libman/?view=aspnetcore-3.1&preserve-view=true) de Biblioteca ou yarn em vez do npm para instalar arquivos JavaScript e CSS do lado do cliente.

### <a name="add-npm-support-to-a-project-aspnet-core"></a><a name="npmAdd"></a> Adicionar suporte a npm a um projeto (ASP.NET Core)

Se o projeto ainda não incluir um *package.jsno* arquivo , você poderá adicionar um para habilitar o suporte a npm adicionando um *package.jsno* arquivo ao projeto.

1. Se você não tiver o Node.js instalado, recomendamos instalar a versão LTS do siteNode.jspara melhor [ compatibilidade ](https://nodejs.org/en/download/) com estruturas e bibliotecas externas.

   npm requer Node.js.

1. Para adicionar o *package.jsno* arquivo , clique com o botão direito do mouse no projeto no Gerenciador de Soluções e escolha Adicionar Novo  >  **Item** (ou pressione **Ctrl**  +  **SHIFT**  +  **A**). Escolha o **arquivo de configuração npm**, use o nome padrão e clique em **Adicionar**.

   ![Adicionar package.jsao seu projeto](../javascript/media/npm-add-package-json.png)

   Se você não vir o arquivo de configuração npm listado, Node.js ferramentas de desenvolvimento não estão instaladas. Você pode usar o Instalador do Visual Studio para adicionar a carga de trabalhoNode.js **desenvolvimento.** Em seguida, repita a etapa anterior.

1. Inclua um ou mais pacotes npm na `dependencies` seção ou dopackage.js`devDependencies` *no*. Por exemplo, você pode adicionar o seguinte ao arquivo:

   ```json
   "devDependencies": {
      "gulp": "4.0.2",
      "@types/jquery": "3.3.33"
   }
   ```

Quando você salva o arquivo, Visual Studio adiciona o pacote sob o nó **Dependencies/npm** no Gerenciador de Soluções. Se você não vir o nó, clique com o botão direito do mouse **package.jsem** e escolha **Restaurar Pacotes**.

>[!NOTE]
> Em alguns cenários, Gerenciador de Soluções pode não mostrar o status correto para pacotes npm instalados. Para saber mais, consulte a [Solução de problemas](#troubleshooting-npm-packages).

### <a name="install-packages-using-packagejson-aspnet-core"></a><a name="npmInstallPackage"></a>Instalar pacotes usando package.json (ASP.NET Core)

Para projetos com npm incluído, você pode configurar pacotes npm usando `package.json` . Clique com o botão direito do mouse no nó NPM em Gerenciador de Soluções e escolha **abrir package.jsem**.

![Captura de tela da Gerenciador de Soluções com o nó NPM selecionado. Um menu de contexto de clique com o botão direito do mouse está aberto e abrir package.jsem está selecionado.](../javascript/media/npm-add-package.png)

O IntelliSense no *package.jsno* ajuda a selecionar uma versão específica de um pacote NPM.

:::image type="content" source="../javascript/media/npm-add-package-intellisense.png" alt-text="Selecione a versão do pacote NPM" border="true":::

Quando você salva o arquivo, o Visual Studio adiciona o pacote no nó **Dependencies/NPM** em Gerenciador de soluções. Se você não vir o nó, clique com o botão direito do mouse em **package.js** e escolha **restaurar pacotes**.

Pode levar vários minutos para instalar um pacote. Verifique o andamento na instalação do pacote alternando para a saída do **NPM** na janela de **saída** .

![saída de NPM](../javascript/media/npm-output.png)

## <a name="troubleshooting-npm-packages"></a>Solução de problemas de pacotes do NPM

* NPM requer Node.js se você não tiver o Node.js instalado, recomendamos que instale a versão LTS do site [Node.js](https://nodejs.org/en/download/) para obter melhor compatibilidade com estruturas e bibliotecas externas.

* Para projetos Node.js, você deve ter a carga de trabalho de **desenvolvimentoNode.js** instalada para suporte NPM.

* Em alguns cenários, Gerenciador de Soluções pode não mostrar o status correto dos pacotes NPM instalados devido a um problema conhecido descrito [aqui](https://github.com/aspnet/Tooling/issues/479). Por exemplo, o pacote pode aparecer como não instalado quando instalado. Na maioria dos casos, você pode atualizar Gerenciador de Soluções excluindo *package.js*, reiniciando o Visual Studio e adicionando novamente o *package.jsno* arquivo, conforme descrito anteriormente neste artigo. Ou, ao instalar pacotes, você pode usar a janela saída do NPM para verificar o status da instalação.

* Em alguns cenários de ASP.NET Core, o nó NPM no Gerenciador de Soluções pode não estar visível após a compilação do projeto. Para tornar o nó visível novamente, clique com o botão direito do mouse no nó do projeto e escolha **descarregar projeto.** Em seguida, clique com o botão direito do mouse no nó do projeto e escolha **recarregar projeto**.

* Se você vir erros ao criar seu aplicativo ou transcompilar o código TypeScript, verifique se há incompatibilidades de pacote npm como uma possível fonte de erros. Para ajudar a identificar erros, verifique a janela saída npm ao instalar os pacotes, conforme descrito anteriormente neste artigo. Por exemplo, se uma ou mais versões de pacote npm foram preterida e resulta em um erro, talvez seja necessário instalar uma versão mais recente para corrigir erros. Para obter informações sobre como usar *package.json* para controlar as versões do pacote de npm, confira [Configuração de package.json](../javascript/configure-packages-with-package-json.md).
