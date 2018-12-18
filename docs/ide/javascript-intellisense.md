---
title: JavaScript IntelliSense
ms.date: 06/28/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript]
- <reference> JavaScript XML tag
- JavaScript Code Editor
- XML code comments, JavaScript IntelliSense
- reference JavaScript XML tag
- JavaScript, IntelliSense
- code comments, JavaScript IntelliSense
- JavaScript, reference groups
- JavaScript Editor
- reference directives [JavaScript]
- JavaScript, XML documentation comments
- reference groups [JavaScript]
- JavaScript, reference directives
- IntelliSense [JavaScript], about
- IntelliSense extensibility [JavaScript]
- XML documentation comments [JavaScript]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 666ce7d65269992af486e59c6b5ce11e94da736b
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51348105"
---
# <a name="javascript-intellisense"></a>JavaScript IntelliSense

O [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] fornece uma experiência de edição de JavaScript avançada pronta para o uso. Ativado por um serviço de linguagem baseado no TypeScript, o Visual Studio oferece um IntelliSense mais sofisticado, suporte para recursos modernos do JavaScript e recursos aprimorados de produtividade como Ir para Definição, refatoração e muito mais.

> [!NOTE]
> O serviço de linguagem JavaScript do [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] usa um novo mecanismo para o serviço de linguagem (chamado “Salsa”). Os detalhes estão incluídos neste tópico e você também pode ler esta [postagem no blog](https://blogs.msdn.microsoft.com/visualstudio/2016/11/28/more-productive-javascript-in-visual-studio-2017-rc/). A nova experiência de edição também se aplica ao Visual Studio Code. Consulte os [documentos do Código do VS](https://code.visualstudio.com/docs/languages/javascript) para obter mais informações.

Para obter mais informações sobre a funcionalidade geral do IntelliSense no Visual Studio, consulte [Usando o IntelliSense](../ide/using-intellisense.md).

## <a name="whats-new-in-the-javascript-language-service-in-includevsdev15miscincludesvsdev15mdmd"></a>Novidades no serviço de linguagem JavaScript no [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]

A começar do [!include[vs_dev15](../misc/includes/vs_dev15_md.md)], o JavaScript IntelliSense exibe muito mais informações sobre listas de parâmetro e de membros.
Essas novas informações são fornecidas pelo serviço de linguagem TypeScript, que usa a análise estática nos bastidores para entender melhor o código.
O TypeScript usa várias fontes para criar essas informações:

- [IntelliSense baseado na inferência de tipos](#TypeInference)
- [IntelliSense baseado no JSDoc](#JsDoc)
- [IntelliSense baseado em arquivos de declaração do TypeScript](#TsDeclFiles)
- [Aquisição automática de definições de tipo](#Auto)

<a name="TypeInference"></a>
### <a name="intellisense-based-on-type-inference"></a>IntelliSense com base em inferência de tipos

No JavaScript, na maioria das vezes, não há nenhuma informação de tipo explícita disponível. Felizmente, geralmente é bastante fácil descobrir um tipo dado o contexto de código ao redor.
Esse processo é chamado de inferência de tipos.

Para uma variável ou uma propriedade, em geral, o tipo é o tipo do valor usado para inicializá-lo ou a atribuição de valor mais recente.

```js
var nextItem = 10;
nextItem; // here we know nextItem is a number

nextItem = "box";
nextItem; // now we know nextItem is a string
```

Para uma função, o tipo de retorno pode ser inferido de instruções de returno.

Para parâmetros de função, atualmente, não há nenhuma inferência, mas existem maneiras de resolver esse problema usando arquivos JSDoc ou TypeScript *.d.ts* (confira as próximas seções).

Além disso, há uma inferência especial para o seguinte:

- Classes de “estilo ES3”, especificadas usando uma função de construtor e atribuições à propriedade de protótipo.
- Padrões de módulo de estilo CommonJS, especificados como atribuições de propriedade no objeto `exports` ou atribuições à propriedade `module.exports`.

```js
function Foo(param1) {
    this.prop = param1;
}
Foo.prototype.getIt = function () { return this.prop; };
// Foo will appear as a class, and instances will have a 'prop' property and a 'getIt' method.

exports.Foo = Foo;
// This file will appear as an external module with a 'Foo' export.
// Note that assigning a value to "module.exports" is also supported.
```

<a name="JsDoc"></a>
### <a name="intellisense-based-on-jsdoc"></a>IntelliSense com base em JSDoc

Nos casos em que a inferência de tipos não fornecer as informações de tipo desejadas (ou para dar suporte à documentação), as informações de tipo podem ser fornecidas explicitamente por meio de anotações do JSDoc.  Por exemplo, para fornecer um tipo específico a um objeto parcialmente declarado, é possível usar a marcação `@type` conforme mostrado abaixo:

```js
/**
 * @type {{a: boolean, b: boolean, c: number}}
 */
var x = {a: true};
x.b = false;
x. // <- "x" is shown as having properties a, b, and c of the types specified
```

Conforme mencionado, os parâmetros de função nunca são inferidos. No entanto, usando a marcação `@param` do JSDoc, é possível adicionar tipos a parâmetros de função também.

```js
/**
 * @param {string} param1 - The first argument to this function
 */
function Foo(param1) {
    this.prop = param1; // "param1" (and thus "this.prop") are now of type "string".
}
```

Confira [Suporte para JSDoc em JavaScript](https://github.com/Microsoft/TypeScript/wiki/JsDoc-support-in-JavaScript) para obter as anotações JsDoc com suporte no momento.

<a name="TsDeclFiles"></a>
### <a name="intellisense-based-on-typescript-declaration-files"></a>IntelliSense com base em arquivos de declaração TypeScript

Como o JavaScript e o TypeScript agora são baseados no mesmo serviço de linguagem, eles podem interagir de forma mais sofisticada. Por exemplo, o JavaScript IntelliSense pode ser fornecido para valores declarados em um arquivo *.d.ts* (confira a [Documentação do TypeScript](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)), e tipos como interfaces e classes declaradas em TypeScript estão disponíveis para serem usados como tipos em JsDoc.

Abaixo, mostramos um exemplo simples de um arquivo de definição TypeScript que fornece essas informações de tipo (por meio de uma interface) para um arquivo JavaScript no mesmo projeto (usando uma marca `JsDoc`).

<img src="https://raw.githubusercontent.com/wiki/Microsoft/TypeScript/images/decl1.png" height="400" width="640" alt="TypeScript definition file" />

<a name="Auto"></a>
### <a name="automatic-acquisition-of-type-definitions"></a>Aquisição automática das definições de tipo

No mundo do TypeScript, as bibliotecas mais populares do JavaScript têm suas APIs descritas por arquivos *.d.ts* e o repositório mais comum dessas definições está em [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped).

Por padrão, o serviço de linguagem Salsa tentará detectar quais bibliotecas do JavaScript estão em uso e baixará e referenciará automaticamente o arquivo *.d.ts* correspondente que descreve a biblioteca, a fim de fornecer um IntelliSense mais completo. Os arquivos são baixados em um cache localizado na pasta do usuário em *%LOCALAPPDATA%\Microsoft\TypeScript*.

> [!NOTE]
> Esse recurso estará **desabilitado** por padrão se um arquivo de configuração *tsconfig.json* estiver sendo usado, mas poderá ser definido como habilitado, conforme descrito mais abaixo.

Atualmente, a detecção automática funciona para dependências baixadas do npm (com a leitura do arquivo *package.json*), no Bower (com a leitura do arquivo *bower.json*) e em arquivos soltos no projeto que correspondem a uma lista com aproximadamente as 400 bibliotecas mais populares do JavaScript. Por exemplo, se você tiver *jquery-1.10.min.js* em seu projeto, o arquivo *jquery.d.ts* será buscado e carregado para proporcionar uma experiência melhor de edição. Esse arquivo *.d.ts* não afetará o projeto.

Se você não desejar usar a aquisição automática, desabilite-a adicionando um arquivo de configuração, conforme descrito abaixo. Ainda é possível colocar arquivos de definição para uso diretamente no projeto manualmente.

## <a name="see-also"></a>Consulte também

- [Usando o IntelliSense](../ide/using-intellisense.md)
- [Suporte a JavaScript (Visual Studio para Mac)](/visualstudio/mac/javascript)