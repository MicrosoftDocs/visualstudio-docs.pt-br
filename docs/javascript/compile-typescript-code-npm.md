---
title: Compilar e compilar código TypeScript usando NPM
description: Saiba como adicionar suporte ao typescript a seus projetos do Visual Studio usando o Gerenciador de pacotes do nó (NPM).
ms.date: 7/23/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 96e5689c0108231be26ddf7d598227137f7bc1f7
ms.sourcegitcommit: ab5735d64a6ad7aecabf5d6df159888e3246bff5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111433773"
---
# <a name="compile-typescript-code-nodejs"></a>Compilar código TypeScript (Node.js)

Você pode adicionar suporte do TypeScript aos seus projetos usando o TypeScript SDK, disponível por padrão no instalador do Visual Studio ou usando o NPM. Para projetos desenvolvidos no Visual Studio 2019, incentivamos você a usar o pacote NPM TypeScript para maior portabilidade em diferentes plataformas e ambientes.

Para projetos ASP.NET Core, é recomendável que você use o [pacote NuGet](../javascript/compile-typescript-code-nuget.md) em vez disso.

## <a name="add-typescript-support-using-npm"></a>Adicionar suporte ao TypeScript usando NPM

O [pacote NPM do typescript](https://www.npmjs.com/package/typescript) adiciona suporte a typescript. Quando o pacote npm para o TypeScript 2.1 ou posterior está instalado em seu projeto, a versão correspondente do serviço de linguagem TypeScript é carregada no editor.

1. [Siga as instruções](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json) para instalar a carga de trabalho de desenvolvimento Node.js e o tempo de execução Node.js.

   Para a integração mais simples com o Visual Studio, crie seu projeto usando um dos modelos Node.js TypeScript, como o modelo de aplicativo Web em branco Node.js. Caso contrário, use um modelo Node.js JavaScript incluído com o Visual Studio e siga as instruções aqui ou use um projeto de [pasta aberta](../javascript/develop-javascript-code-without-solutions-projects.md) .

1. Se seu projeto ainda não o inclui, instale o [pacote NPM TypeScript](https://www.npmjs.com/package/typescript).

   Em Gerenciador de Soluções (painel direito), abra o *package.jsna* raiz do projeto. Os pacotes listados correspondem aos pacotes sob o nó NPM no Gerenciador de Soluções. Para obter mais informações, consulte [Manage NPM Packages](../javascript/npm-package-management.md).

   Para um projeto Node.js, você pode instalar o pacote NPM TypeScript usando a linha de comando ou o IDE. Para instalar usando o IDE, clique com o botão direito do mouse no nó NPM em Gerenciador de Soluções, escolha **instalar novo pacote NPM**, pesquise por **TypeScript** e instale o pacote.

   Verifique a opção **NPM** na janela **saída** para ver o progresso da instalação do pacote. O pacote instalado aparece no nó **NPM** no Gerenciador de soluções.

1. Se o seu projeto ainda não o incluir, adicione um arquivo *. tsconfig* à raiz do projeto. Para adicionar o arquivo, clique com o botão direito do mouse no nó do projeto e escolha **adicionar > novo item**. Escolha o **arquivo de configuração JSON do TypeScript** e clique em **Adicionar**.

   O Visual Studio adiciona o *tsconfig.jsno* arquivo à raiz do projeto. Você pode usar esse arquivo para [Configurar opções](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) para o compilador TypeScript.

1. Abra o *tsconfig.jsem* e atualize para definir as opções de compilador que você deseja.

   Veja a seguir um exemplo de um *tsconfig.jssimples no* arquivo.

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "dist"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   Neste exemplo:
   - *include* informa ao compilador onde encontrar arquivos TypeScript (*. TS).
   - a opção *outDir* especifica a pasta de saída para os arquivos JavaScript simples que são transcompilados pelo compilador do TypeScript.
   - a opção *sourceMap* indica se o compilador gera arquivos *sourceMap* .

   A configuração anterior fornece apenas uma introdução básica à configuração do TypeScript. Para obter informações sobre outras opções, consulte [tsconfig.jsem](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).

## <a name="build-the-application"></a>Compilar o aplicativo

1. Adicione arquivos TypeScript (*. TS*) ou typescript JSX (*. TSX*) ao seu projeto e, em seguida, adicione o código TypeScript. Para obter um exemplo simples de TypeScript, use o seguinte:

   ```typescript
   let message: string = 'Hello World';
   console.log(message);
   ```

1. No *package.jsno*, adicione suporte para comandos de compilação e limpeza do Visual Studio usando os scripts a seguir.

   ```json
   "scripts": {
     "build": "tsc --build",
     "clean": "tsc --build --clean"
   },
   ```

   Se você precisar criar usando uma ferramenta de terceiros como o webpack, poderá adicionar um script de compilação de linha de comando à sua *package.jsno* arquivo:

   ```json
   "scripts": {
      "build": "webpack-cli app.tsx --config webpack-config.js"
   }
   ```

   Para obter um exemplo de como usar o webpack com o arquivo de configuração reagir e um webpack, consulte [criar um aplicativo Web com Node.js e reagir](../javascript/tutorial-nodejs-with-react-and-jsx.md).

   Para obter um exemplo de como usar Vue.js com TypeScript, consulte [criar um aplicativo Vue.js](/javascript/create-application-with-vuejs).

1. Se você precisar configurar opções como a página de inicialização, o caminho para o tempo de execução do Node.js, a porta do aplicativo ou os argumentos de tempo de execução, clique com o botão direito do mouse no nó do projeto em Gerenciador de Soluções e escolha **Propriedades**.

   >[!NOTE]
   > Ao configurar ferramentas de terceiros, Node.js projetos não usam os caminhos configurados em **ferramentas**  >  **Opções**  >  **projetos e soluções**  >  **Web gerenciamento de pacotes**  >  **ferramentas da Web externas**. Essas configurações são usadas para outros tipos de projeto.

1. Escolha **compilar > Compilar solução**.

   Embora o aplicativo seja criado automaticamente quando você o executa, queremos dar uma olhada em algo que acontece durante o processo de compilação:

   Se você gerou mapas de origem, abra a pasta especificada na opção *outDir* e localize os arquivos de \*.js gerados juntamente com os \* arquivos js. map gerados.

   Os arquivos de mapa de origem são necessários para [depuração](../javascript/debug-nodejs.md).

### <a name="run-the-application"></a>Executar o aplicativo

Para obter instruções para executar o aplicativo depois de compilá-lo, consulte [criar seu primeiro Node.js aplicativo](../ide/quickstart-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json#run-the-app).

## <a name="automate-build-tasks"></a>Automatizar tarefas de compilação

Você pode usar o Task Runner Explorer no Visual Studio para ajudar a automatizar tarefas para ferramentas de terceiros como o NPM e o webpack.

- [Executor de tarefa NPM](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.NPMTaskRunner) – adiciona suporte para scripts NPM definidos no *package.jsem*. Dá suporte a yarn.
- [Executor de tarefas do webpack](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebPackTaskRunner) – adiciona suporte para webpack.
