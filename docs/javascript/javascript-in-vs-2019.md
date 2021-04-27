---
title: JavaScript e TypeScript no Visual Studio 2019
description: Saiba como o Visual Studio 2019 fornece suporte avançado para o desenvolvimento de JavaScript, usando JavaScript diretamente e também usando a linguagem de programação TypeScript.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 03/16/2020
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2019'
ms.openlocfilehash: 267bd8567b60a66bcf9d78c3aef8f02bbc942e0d
ms.sourcegitcommit: e12d6cdaeb37564f05361965db2ec8ad0d4f21ad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108025872"
---
# <a name="javascript-and-typescript-in-visual-studio-2019"></a>JavaScript e TypeScript no Visual Studio 2019

## <a name="overview"></a>Visão geral

O Visual Studio 2019 oferece suporte avançado para desenvolvimento de JavaScript, usando JavaScript diretamente ou a [linguagem de programação TypeScript](http://www.typescriptlang.org/), desenvolvida para proporcionar uma experiência de desenvolvimento de JavaScript mais produtiva e agradável, especialmente ao desenvolver projetos em escala. É possível escrever código JavaScript ou TypeScript no Visual Studio para muitos tipos de aplicativos e serviços.

## <a name="javascript-language-service"></a>Serviço de linguagem JavaScript

A experiência de JavaScript no Visual Studio de 2019 é alimentada pelo mesmo mecanismo que oferece suporte a TypeScript. Isso oferece um melhor suporte a recursos, sofisticação e integração prontos para uso.

A opção de restaurar o serviço de linguagem JavaScript herdado não está mais disponível. Os usuários agora têm o novo serviço de linguagem JavaScript pronto para uso. O novo serviço de linguagem baseia-se exclusivamente no serviço de linguagem TypeScript, que é alimentado por análise estática. Isso permite fornecer a você melhores ferramentas, para que seu código JavaScript possa se beneficiar de um IntelliSense mais sofisticado com base nas definições de tipo. O novo serviço é leve e consome menos memória do que o serviço herdado, fornecendo a você um melhor desempenho conforme o escalonamento do seu código. Também melhoramos o desempenho do serviço de linguagem para lidar com projetos maiores.

## <a name="typescript-support"></a>Suporte a TypeScript

O Visual Studio 2019 fornece várias opções para a integração de compilação de TypeScript ao seu projeto:

* O [pacote NuGet do TypeScript](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild). Quando o pacote do NuGet para o TypeScript 3.2 ou posterior está instalado em seu projeto, a versão correspondente do serviço de linguagem TypeScript é carregada no editor.
* O [pacote NPM TypeScript](https://www.npmjs.com/package/typescript). Quando o pacote npm para o TypeScript 2.1 ou posterior está instalado em seu projeto, a versão correspondente do serviço de linguagem TypeScript é carregada no editor.
* O TypeScript SDK, disponível por padrão no instalador do Visual Studio, bem como um download de SDK autônomo do [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-395).

> [!TIP]
> Para projetos desenvolvidos no Visual Studio 2019, incentivamos você a usar o NuGet do TypeScript ou o pacote NPM do TypeScript para maior portabilidade em diferentes plataformas e ambientes. Para obter mais informações, consulte [compilar código typescript usando o NuGet](../javascript/compile-typescript-code-nuget.md) e [compilar código typescript usando o TSC](../javascript/compile-typescript-code-npm.md).

## <a name="projects"></a>Projetos

Aplicativos JavaScript da UWP não são mais compatíveis com o Visual Studio 2019. Não é possível criar ou abrir projetos da UWP em JavaScript (arquivos com extensão *.jsproj*). Você pode saber mais na documentação sobre como [criar PWAs (Aplicativos Web Progressivos)](/microsoft-edge/progressive-web-apps-chromium) que são executados perfeitamente no Windows.
