---
title: Visão geral da extensibilidade do Visual Studio abrir pasta | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: dcb2d1d922b4ebd4943c42c478400c5873af9cc4
ms.sourcegitcommit: 498e39e89a89ad7bf9dcb0617424fff999b1c3b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36302970"
---
# <a name="open-folder-extensibility"></a>Extensibilidade de pasta aberta

O [Abrir pasta](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) recurso permite aos usuários abrir qualquer base de código no Visual Studio sem a necessidade de arquivos de projeto ou solução. Abrir pasta fornece que os recursos que os usuários esperam do Visual Studio como:

* Pesquisa e integração do Gerenciador de soluções
* Colorização de editor
* Ir para navegação
* Localizar em arquivos de pesquisa

Quando usado com cargas de trabalho como para desenvolvimento .NET e C++, os usuários também obtém:

* Intellisense avançado
* Funcionalidade específica ao idioma

Com Abrir pasta, os autores de extensão podem criar recursos avançados para qualquer idioma. Existem APIs para dar suporte à construção, depuração e a pesquisa de símbolo para qualquer arquivo em um usuário da Base de código. Extensores atuais podem atualizar seus recursos existentes do Visual Studio para entender o código sem o apoio de projetos ou uma solução.

## <a name="an-api-without-project-systems"></a>Uma API sem sistemas de projeto

Historicamente, o Visual Studio compreendido apenas arquivos em uma solução e seus projetos usando sistemas de projeto. Um sistema de projeto é responsável pelas interações do usuário e a funcionalidade de um projeto carregado. Ele compreende contém quais arquivos seu projeto, a representação visual do conteúdo do projeto, as dependências em outros projetos, e o arquivo de projeto de modificação de subjacente. É por meio dessas hierarquias e os recursos que outros componentes funcionam em nome do usuário. Nem todas as bases de código também são representados em uma estrutura de projeto e solução. Linguagens de script e código-fonte aberto escrito em C++ para Linux são bons exemplos. Com Abrir pasta, o Visual Studio fornece aos usuários uma nova maneira de interagir com seu código-fonte.

As APIs de pasta aberta estão sob o `Microsoft.VisualStudio.Workspace.*` namespace e estão disponíveis para os extensores produzir e consumir dados ou ações em torno de arquivos na pasta aberta. Extensões podem usar essas APIs para fornecer funcionalidade para muitas áreas, incluindo:

- [Espaços de trabalho](workspaces.md) : A partir de extensibilidade do ponto de abrir pasta é o espaço de trabalho e suas APIs.
- [Ações e os contextos de arquivo](workspace-file-contexts.md) -intelligence específicas do código fornecido por meio de contextos de arquivo do arquivo.
- [Indexação](workspace-indexing.md) - coletar e manter os dados sobre espaços de trabalho de abrir pasta.
- [Serviços de linguagem](workspace-language-services.md) -integrar serviços de linguagem em espaços de trabalho de abrir pasta.
- [Compilar](workspace-build.md) -suporte para espaços de trabalho de abrir pasta de compilação.

Serão necessário adotar novas APIs para dar suporte a abrir pasta recursos que usam os seguintes tipos:

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>Comentários, comentários, problemas

Abra a pasta e o `Microsoft.VisualStudio.Workspace.*` APIs estão em desenvolvimento ativo. Se você vir um comportamento inesperado, em seguida, consulte os problemas conhecidos para a versão de seu interesse. [Comunidade de desenvolvedores](https://developercommunity.visualstudio.com) é o local recomendado para votar e crie quaisquer problemas. Para cada comentário, é altamente recomendável obter uma descrição detalhada do problema. Inclua a versão do Visual Studio que você está desenvolvendo para, as APIs que você está usando (o que você já implementou e o que você está interagindo com), o resultado esperado e o resultado real. Se possível, inclua um despejo do processo devenv.exe. Use o problema do GitHub de controle para fornecer comentários sobre isso e documentação relacionada.

## <a name="next-steps"></a>Próximas etapas

* [Espaços de trabalho](workspaces.md) -Saiba mais sobre o espaço de trabalho de abrir pasta API.