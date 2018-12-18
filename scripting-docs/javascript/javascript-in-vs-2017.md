---
title: JavaScript no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-javascript
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 74dca14c-5071-416f-a92b-d09f95e3dfb8
caps.latest.revision: 1
author: bowdenk7
ms.author: wilkelly
manager: ghogen
ms.openlocfilehash: 75c234b2a3b16d3bcbe05da9f0818c73be0412db
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48880755"
---
# <a name="javascript-in-visual-studio-2017"></a>JavaScript no Visual Studio 2017

O JavaScript é uma linguagem de primeira classe no Visual Studio. Você pode usar a maioria ou todos os auxílios de edição padrão (snippets de código IntelliSense, e assim por diante) ao escrever o código JavaScript no Visual Studio IDE. Você pode escrever código JavaScript para muitos tipos de aplicativos e serviços.

> [!NOTE]
> Nós reunimos os esforços de toda a comunidade para fazer com que o [Docs da Web do MDN](https://developer.mozilla.org/en-US/) seja o recurso de desenvolvimento principal único da Web, redirecionando todas as (500 ou mais páginas) de referência da API JavaScript da Microsoft do docs.microsoft.com para seu equivalente do MDN. Para obter detalhes, confira o [comunicado](https://blogs.windows.com/msedgedev/2018/06/26/chakra-docs-mdn-web-docs/).

## <a name="ES6"></a> Suporte para ECMAScript 2015 (ES6) e mais

O Visual Studio agora dá suporte à sintaxe para atualizações da linguagem ECMAScript, tais como ECMAScript 2015/2016.

### <a name="what-is-ecmascript-2015"></a>O que é ECMAScript 2015?

O JavaScript ainda está em evolução enquanto uma linguagem de programação e [TC39](http://www.ecma-international.org/memento/TC39.htm) é o comitê responsável por fazer atualizações.
ECMAScript 2015 é uma atualização para a linguagem JavaScript que traz novas sintaxes e funcionalidades úteis. Para um mergulho profundo nos recursos da ES6, confira [este](http://es6-features.org) site de referência.

Além de suporte para ECMAScript 2015, o Visual Studio também dá suporte a ECMAScript 2016 e terá suporte para versões futuras do ECMAScript conforme elas forem lançadas. Para se manter atualizado com TC39 e as alterações mais recentes no ECMAScript, execute o trabalho no [GitHub](https://github.com/tc39).

### <a name="transpile-javascript"></a>Transcompilar JavaScript

Um problema comum com o JavaScript é que você deseja usar os recursos de linguagem ES6+ mais recentes, porque eles lhe ajudam a ser mais produtivo, mas seus ambientes de tempo de execução (geralmente navegadores) ainda não dão suporte a esses novos recursos. Isso significa que você terá que manter o controle de quais navegadores dão suporte a quais recursos (o que pode ser entediante) ou você precisa de uma maneira de converter o código ES6 + em uma versão que seus tempos de execução de destino entendam (geralmente ES5). Convertendo seu código para uma versão que o tempo de execução entende que é conhecido como “transcompilação”.

Um dos principais recursos do TypeScript é a capacidade de transcompilar código ES6+ para ES5 ou ES3 para que você possa escrever o código que lhe torna mais produtivo, sem deixar de poder executar seu código em qualquer plataforma. Já que o JavaScript em [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] usa o mesmo serviço de linguagem que o TypeScript, ele também pode aproveitar a transcompilação do ES6+ para o ES5.

Antes que a transcompilação possa ser configurada, são necessárias algumas noções básicas sobre as opções de configuração.
O TypeScript é configurado por meio de um arquivo `tsconfig.json`.
Na ausência desse arquivo, alguns valores padrão são usados.
Por motivos de compatibilidade, esses padrões são diferentes em um contexto em que apenas arquivos JavaScript (e, opcionalmente, arquivos `.d.ts`) estão presentes.
Para compilar arquivos JavaScript, um arquivo `tsconfig.json` deve ser adicionado e algumas dessas opções devem ser definidas explicitamente.

As configurações necessárias para o arquivo tsconfig são as seguintes:

 - `allowJs`: esse valor deve ser definido como `true` para que os arquivos JavaScript sejam reconhecidos. O valor padrão é `false`, pois TypeScript é compilado em JavaScript e o compilador não deve incluir arquivos, ele apenas é compilado.
 - `outDir`: esse valor deve ser definido com um local não incluído no projeto, para que os arquivos JavaScript emitidos não sejam detectados e então incluídos no projeto (consulte `exclude`).
 - `module`: se estiver usando módulos, essa configuração informará ao compilador qual formato de módulo o código emitido deverá usar (por exemplo, `commonjs` para o Nó ou agregadores como Browserify).
 - `exclude`: essa configuração indica quais pastas não serão incluídas no projeto.
 O local de saída, bem como pastas não pertencentes ao projeto como `node_modules` ou `temp`, devem ser adicionados a essa configuração.
 - `enableAutoDiscovery`: essa configuração habilita a detecção automática e o download de arquivos de definição, conforme descrito anteriormente.
 - `compileOnSave`: essa configuração informa ao compilador se ele deve recompilar sempre que um arquivo de origem é salvo no Visual Studio.
 - `typeAcquisition`: este conjunto de configurações controlam o comportamento de aquisição de tipo automática (explicado com mais detalhes [nesta seção](/visualstudio/ide/javascript-intellisense#Auto))

Para converter arquivos JavaScript em módulos CommonJS e colocá-los em uma pasta `./out`, você pode usar o arquivo `tsconfig.json` a seguir:

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "allowJs": true,
    "outDir": "out"
  },
  "exclude": [
    "node_modules",
    "wwwroot",
    "out"
  ],
  "compileOnSave": true,
  "typeAcquisition": {
    "enable": true
  }
}
```

Com as configurações em vigor, se houver um arquivo de origem (`./app.js`) que contém vários recursos da linguagem ECMAScript 2015, conforme a seguir:

```js
import {Subscription} from 'rxjs/Subscription';  // ES6 import

class Foo {  // ES6 Class
    sayHi(name) {
        return `Hi ${name}, welcome to Salsa!`;  // ES6 template string
    }
}

export let sqr = x => x * x;  //ES6 export, let, and arrow function
export default Subscription;  //ES6 default export
```

Um arquivo será emitido para o `./out/app.js` que tem o ECMAScript 5 como destino (o padrão), semelhante ao exemplo mostrado a seguir:

```js
"use strict";
var Subscription_1 = require('rxjs/Subscription');
var Foo = (function () {
    function Foo() {
    }
    Foo.prototype.sayHi = function (name) {
        return "Hi " + name + ", welcome to Salsa!";
    };
    return Foo;
}());
exports.sqr = function (x) { return x * x; };
Object.defineProperty(exports, "__esModule", { value: true });
exports.default = Subscription_1.Subscription;
```

## <a name="better-intellisense"></a>IntelliSense aprimorado

O JavaScript IntelliSense em [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] agora exibirá muito mais informações sobre listas de parâmetros e de membros. Essas novas informações são fornecidas pelo serviço de linguagem TypeScript, que usa a análise estática nos bastidores para entender melhor o código. Você pode ler mais sobre a nova experiência de IntelliSense e sobre como ele funciona [aqui](/visualstudio/ide/javascript-intellisense/).

## <a name="JSX"></a> Suporte à sintaxe JSX

O JavaScript em [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] conta com suporte avançado à sintaxe JSX. O JSX é um conjunto de sintaxes que permite marcas HTML em arquivos JavaScript.

A ilustração a seguir mostra um componente React definido no arquivo TypeScript `comps.tsx` e, em seguida, esse componente sendo usado no arquivo `app.jsx`, completo com o IntelliSense para conclusões e documentação nas expressões JSX.
Você não precisa do TypeScript aqui; esse exemplo específico eventualmente também contém algum código TypeScript.

<img src="./media/react.png" height="500" width="640"/>

> [!NOTE]
> Para converter a sintaxe JSX em chamadas React, a configuração `"jsx": "react"` deve ser adicionada ao `compilerOptions` no arquivo `tsconfig.json`.

O arquivo JavaScript criado em “./out/app.js” após o build conterá o código:

```js
"use strict";
var comps_1 = require('./comps');
var x = React.createElement(comps_1.RepoDisplay, {description: "test"});
```

## <a name="configure-your-javascript-project"></a>Configurar seu projeto JavaScript

O serviço de linguagem é alimentado por análise estática, o que significa que ele analisa o código-fonte sem efetivamente executá-lo, para retornar resultados do IntelliSense e fornecer outros recursos de edição.
Portanto, quanto maior a quantidade e o tamanho dos arquivos incluídos seu contexto de projeto, mais memória e CPU serão usadas durante a análise.
Por isso, há algumas suposições padrão que são feitas sobre a forma do projeto:

- `package.json` e `bower.json` listam as dependências usadas pelo seu projeto e, por padrão são incluídas na ATA (aquisição de tipo automática)
- Uma pasta `node_modules` de nível superior contém código-fonte de biblioteca e seu conteúdo é excluído do contexto do projeto por padrão
- Qualquer outro arquivo `.js`, `.jsx`, `.ts` e `.tsx` possivelmente é um dos *seus próprios* arquivos de origem e deve ser incluído no contexto do projeto

Na maioria dos casos, você poderá simplesmente abrir seu projeto e ter uma ótima experiência usando a configuração de projeto padrão. No entanto, em projetos grandes ou com estruturas de pasta diferentes, pode ser desejável configurar o serviço de linguagem para um melhor foco apenas em seus próprios arquivos de origem.

### <a name="override-defaults"></a>Substituir padrões

Você pode substituir a configuração padrão adicionando um arquivo `tsconfig.json` à raiz do projeto.
Um `tsconfig.json` tem várias opções diferentes que podem manipular o contexto do projeto.
Algumas delas estão listadas abaixo, mas para um conjunto completo de todas as opções disponíveis, [consulte o armazenamento de esquema](http://json.schemastore.org/tsconfig).

## <a name="important-tsconfigjson-options"></a>Opções `tsconfig.json` importantes

```json
{
  "compilerOptions": {
    "allowJs": true,          // include .js and .jsx in project context (defaults to only .ts and .tsx)
    "noEmit": true            // turns off downlevel compiler
  },
  "files": [],                // list of explicit files to include in the project context. Highest priority.
  "include": [],              // list of folders or glob patterns to include in the project context.
  "exclude": [],              // list of folders or glob patterns to exclude. Overridden by files array.
  "typeAcquisition": {
    "enable": true,           // Defaulted to "false" with a tsconfig. Enables better IntelliSense in JS.
    "include": [ "jquery" ],  // Specific libs to fetch .d.ts files that weren't picked up by ATA
    "exclude": [ "node" ]     // Specific libs to not fetch .d.ts files for
  }
}
```

### <a name="example-project-configuration"></a>Configuração do projeto de exemplo

Dado um projeto com a seguinte configuração:

- os arquivos de origem do projeto estão em `wwwroot/js`
- os arquivos lib do projeto estão em `wwwroot/lib`
- `bootstrap`, `jquery`, `jquery-validation` e `jquery-validation-unobtrusive` estão listados no `bower.json`
- `kendo-ui` foi adicionado manualmente à pasta lib

![Estrutura de pastas](./media/folderStructure.png)

Você pode usar o seguinte `tsconfig.json` para verificar se o serviço de linguagem analisa apenas os arquivos de origem na pasta `js`, mas ainda busca e usa arquivos `.d.ts` para as bibliotecas na sua pasta `lib`.

```json
{
  "compilerOptions": {
    "allowJs": true,
    "noEmit": true
  },
  "exclude": ["wwwroot/lib"],  //ignore lib folders, we will get IntelliSense via ATA
  "typeAcquisition": {
    "enable": true,
    "include": [ "kendo-ui" ]  //kendo-ui wasn't added via bower, so we need to list it here
  }
}
```
# <a name="troubleshooting-the-javascript-language-service-has-been-disabled-for-the-following-projects"></a>Solução de problemas O serviço de linguagem JavaScript foi desabilitado para os seguintes projetos
Quando você abre um projeto do JavaScript que tem bastante conteúdo, pode receber a mensagem "O serviço de linguagem JavaScript foi desabilitado para os seguintes projetos”. O motivo mais comum para ter uma grande quantidade de fontes do JavaScript é devido a incluir bibliotecas com o código-fonte que excede o limite de 20 MB do projeto.

Uma maneira simples de otimizar seu projeto é adicionar um arquivo `tsconfig.json` em sua raiz de projeto para permitir que o serviço de linguagem saiba quais arquivos é seguro ignorar. Use o exemplo a seguir para excluir os diretórios mais comuns em que as bibliotecas estão armazenadas:

```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "maxNodeModuleJsDepth": 2,
    "noEmit": true,
    "skipLibCheck": true
  },
  "exclude": [
    "**/bin",
    "**/bower_components",
    "**/jspm_packages",
    "**/node_modules",
    "**/obj",
    "**/platforms"
  ]
}
```

Adicione mais diretórios conforme considerar adequado. Alguns outros exemplos incluem os diretórios "fornecedor" ou "wwwroot/lib". 

> [!NOTE]
> A propriedade de compilador `disableSizeLimit` pode ser usada também para desabilitar o limite de verificação de 20 MB. Adote precauções especiais ao usar essa propriedade, uma vez que desabilitar o limite pode causar a falha do serviço de linguagem.

## <a name="notable-changes-from-visual-studio-2015"></a>Alterações importantes em relação ao Visual Studio 2015

Já que o [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] apresenta um serviço de linguagem completamente novo, há alguns comportamentos que serão diferentes ou ausentes em relação à experiência anterior.
As alterações mais importantes são a substituição de VSDoc com JSDoc, a remoção de extensões `.intellisense.js` personalizadas e IntelliSense limitado para padrões de código específico.

### <a name="no-more-references-or-referencesjs"></a>Não há mais `///<references/>` nem `_references.js`

Anteriormente era muito difícil compreender, a qualquer momento, quais arquivos que estavam no seu escopo do IntelliSense. Às vezes era desejável ter todos os arquivos no escopo, outras vezes não era, e isso levava a configurações complexas envolvendo o gerenciamento manual de referências. No futuro, você não precisará pensar sobre gerenciamento de referência e, portanto, não precisará de comentários, referências ou arquivos `_references.js` com barras triplas.

Consulte a página [JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense/) para obter mais informações sobre o funcionamento do IntelliSense.

### <a name="vsdoc"></a>VSDoc

Comentários de documentação XML, também conhecidos como VSDocs, anteriormente podiam ser usados para decorar seu código-fonte usando dados adicionais que eram usados para melhorar os resultados do IntelliSense.
Não há mais suporte para o VSDoc em favor do [JSDoc](http://usejsdoc.org/about-getting-started.html), que é mais fácil de escrever e é o padrão aceito para JavaScript.

### <a name="intellisensejs-extensions"></a>Extensões `.intellisense.js`

Anteriormente, você podia criar [extensões do IntelliSense](https://msdn.microsoft.com/library/hh874692.aspx) que permitiam que você adicionasse resultados de conclusão personalizados para bibliotecas de terceiros.
Essas extensões eram bastante difíceis de gravar e instalar e referenciá-las era trabalhoso, então com a atualização, o novo serviço de linguagem não dará suporte a esses arquivos.
Como uma alternativa mais fácil, você pode escrever um arquivo de definição de TypeScript para fornecer os mesmos benefícios do IntelliSense que as antigas extensões `.intellisense.js`.
Você pode aprender mais sobre a criação de arquivos de declaração (`.d.ts`) [aqui](http://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html).

### <a name="unsupported-patterns"></a>Padrões sem suporte

Já que o novo serviço de linguagem é alimentado por análise estática em vez de um mecanismo de execução (leia sobre [esse problema](https://github.com/Microsoft/TypeScript/issues/4789) para obter informações sobre as diferenças), há alguns padrões de JavaScript que não podem mais ser detectados.
O padrão mais comum é o padrão "expando".
Atualmente o serviço de linguagem não pode fornecer o IntelliSense em objetos que têm propriedades incluídas após a declaração.
Por exemplo:

```js
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense won't show properties a or b
```

Você pode contornar esse problema declarando propriedades durante a criação do objeto:

```js
var obj = {
    "a": 10,
    "b": "hello world"
}
obj. // IntelliSense shows properties a and b
```

Você também pode adicionar um comentário JSDoc da seguinte forma:

```js
/**
 * @type {{a: number, b: string}}
 */
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense shows properties a and b
```
