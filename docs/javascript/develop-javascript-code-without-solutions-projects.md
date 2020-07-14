---
title: Escrever o código JavaScript no Visual Studio sem nenhuma solução ou projeto
titleSuffix: ''
description: O Visual Studio dá suporte para a criação de código sem uma dependência de um arquivo de projeto ou de solução
ms.custom: seodec18
ms.date: 09/24/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 187ca5ea0d0232e0ca8b99165e77ee265b81e801
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285082"
---
# <a name="develop-javascript-and-typescript-code-in-visual-studio-without-solutions-or-projects"></a>Desenvolver código JavaScript e TypeScript no Visual Studio sem projetos ou soluções

Com o Visual Studio 2017 ou posterior, é possível [desenvolver o código sem projetos nem soluções](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md), o que permite que você abra uma pasta de códigos e comece a trabalhar imediatamente com o suporte avançado do editor, como IntelliSense, pesquisa, refatoração, depuração, entre outros. Além desses recursos, as Ferramentas Node.js para Visual Studio adicionam suporte para criação de arquivos TypeScript, o gerenciamento de pacotes npm e a execução de scripts npm.

Para começar, selecione **arquivo**  >  **abrir**  >  **pasta** na barra de ferramentas. O Gerenciador de Soluções exibe todos os arquivos na pasta, e você pode abrir qualquer um dos arquivos para começar a editar. Em segundo plano, o Visual Studio indexa os arquivos para habilitar recursos de npm, build e depuração.

> [!IMPORTANT]
> Muitos dos recursos descritos neste artigo, incluindo a integração com npm, exigem o Visual Studio 2017 versão 15.8 ou posterior. A carga de trabalho de desenvolvimento do Visual Studio **Node.js** deve ser instalada.

## <a name="npm-integration"></a>Integração com npm

Se a pasta que você abrir contiver um arquivo *package.json*, clique com o botão direito do mouse em *package.json* para mostrar um menu de contexto (menu de atalho) específico do npm.

![Menu do npm no Gerenciador de Soluções](../javascript/media/solution-explorer-npm-ctx.png)

No menu de atalho, você pode gerenciar os pacotes instalados pelo npm da mesma maneira que você [gerencia pacotes de npm](npm-package-management.md) ao usar um arquivo de projeto.

Além disso, o menu também permite a execução de scripts definidos no elemento `scripts` no *package.json*. Esses scripts usarão a versão do Node.js disponível na variável de ambiente `PATH`. Os scripts são executados em uma nova janela. Essa é uma ótima maneira de executar scripts de build ou de execução.

## <a name="build-and-debug"></a>Build e depuração

### <a name="packagejson"></a>package.json
Se o *package.json* na pasta especificar um elemento `main`, o comando **Depurar** estará disponível no menu de atalho com clique do botão direito do mouse para *package.json*.
Se você clicar nele, o *node.exe* será iniciado com o script especificado como seu argumento.

### <a name="javascript-files"></a>Arquivos JavaScript
Você pode depurar arquivos JavaScript clicando com o botão direito do mouse em um arquivo e selecionando **Depurar** no menu de atalho. Isso inicia o *node.exe* com esse arquivo JavaScript como seu argumento.

### <a name="typescript-files-and-tsconfigjson"></a>Arquivos TypeScript e tsconfig.json
Se não houver nenhum *tsconfig.json* presente na pasta, você poderá clicar com o botão direito do mouse em um arquivo TypeScript para ver os comandos do menu de atalho para criar e depurar esse arquivo. Ao usar esses comandos, você cria ou depura usando *tsc.exe* com as opções padrão. (É necessário criar o arquivo antes de depurar).

> [!NOTE]
> Ao compilar o código TypeScript, é usada a versão mais recente instalada no `C:\Program Files (x86)\Microsoft SDKs\TypeScript`.

Se houver um arquivo *tsconfig* presente na pasta, você poderá clicar com o botão direito do mouse em um arquivo TypeScript para ver um comando de menu para depurar esse arquivo TypeScript. A opção somente será exibida se não houver nenhum `outFile` especificado em *tsconfig.json*. Se houver um `outFile` especificado, você poderá depurar esse arquivo clicando com o botão direito do mouse em *tsconfig.json* e selecionando a opção correta. O arquivo `tsconfig.json` também oferece uma opção de build para permitir que você especifique as opções do compilador.

> [!NOTE]
> Encontre mais informações sobre *o tsconfig.json* na [Página do manual do TypeScript tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html).

## <a name="unit-tests"></a>Testes de Unidade
Você pode habilitar a integração de teste de unidade no Visual Studio especificando uma raiz de teste em seu *package.json*:

```json
{
    // ...
    "vsTest":{
        "testRoot": "./tests"
    }
    // ...
}
```

O executor de teste enumera os pacotes instalados localmente para determinar a estrutura de teste a ser usada.
Se nenhuma das estruturas com suporte for reconhecida, o executor de teste padrão será *ExportRunner*. As outras estruturas com suporte são:
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))

Depois de abrir o Gerenciador de testes (escolha **testar**o  >  **Windows**  >  **Test Explorer**), o Visual Studio descobre e exibe os testes.

> [!NOTE]
> O executor de teste enumerará somente os arquivos JavaScript na raiz do teste. Se o aplicativo for escrito em TypeScript, você precisará criá-los primeiro.
