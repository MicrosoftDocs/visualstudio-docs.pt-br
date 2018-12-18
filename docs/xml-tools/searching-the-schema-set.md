---
title: XML Schema Explorer - pesquisar o conjunto de esquema
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: ec1395e0-d03c-4130-810d-f2db656937bd
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1133d6a67442bde5a9f949553efcffd07e2d3ffe
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34751735"
---
# <a name="search-the-schema-set"></a>Pesquisar o conjunto de esquema

O **XML Schema Explorer** permite que você pesquise o esquema definido das seguintes maneiras:

-   Pesquisa de palavras-chave.

-   Pesquisa Esquema- específica.

## <a name="keyword-search"></a>Pesquisa de palavra-chave

 Executar pesquisas de palavra-chave inserindo uma subcadeia de caracteres no **pesquisa SchemaSet** caixa de texto do **XML Schema Explorer** barra de ferramentas.

 ![Pesquisa de palavra-chave do XML Schema Explorer](../xml-tools/media/schemaexplorersearch.gif)

 O **XML Schema Explorer** procura o esquema definido para os seguintes atributos:

-   Alguns atributos de `name` ou de `ref` que corresponderem a palavra-chave especificada. Você pode encontrar elementos, atributos, tipos e assim por diante, por nome.

-   Atributos de `schemaLocation` de incluem instruções.

-   Atributos de `namespace` de instruções de importação.

## <a name="schema-specific-search"></a>Pesquisa de esquema específico

 O **XML Schema Explorer** também inclui pesquisas internas que você pode acessar usando o menu de contexto a **XML Schema Explorer**. Para obter mais informações sobre menus de contexto disponíveis, consulte [menus de contexto](../xml-tools/context-menus-xml-schema-explorer.md). Você também pode executar uma pesquisa específica do esquema de exibição início; Para obter mais informações, consulte a seção "Esquema definir detalhes" o [exibição início](../xml-tools/start-view.md) tópico.

## <a name="display-and-navigate-search-results"></a>Exibir e navegar os resultados da pesquisa

 Depois que a pesquisa é concluída, o painel de resultados de resumo é adicionado à barra de ferramentas com os resultados da pesquisa. Os resultados da pesquisa também são realçados no **XML Schema Explorer** e marcado pelo tiques na barra de rolagem vertical. Você pode navegar os resultados da pesquisa usando o **ir para próximo resultado da pesquisa** e **vá ao resultado da pesquisa anterior** botões no painel de resultados de resumo do **XML Schema Explorer**barra de ferramentas. usando as teclas **F3** e **Shift**+**F3**; ou clicando na barra de rolagem, as marcas de escala.

 Você pode adicionar os resultados da pesquisa para o espaço de trabalho clicando o **adicionar nós realçados ao espaço de trabalho** botão no painel de resultados de resumo.

 ![Resultado da pesquisa do XML Schema Explorer](../xml-tools/media/schemaexplorersearchresult.gif)

## <a name="clear-search-results"></a>Limpar resultados da pesquisa

 Para limpar os resultados da pesquisa, clique o **x** botão no painel de resultados de resumo do **XML Schema Explorer** barra de ferramentas de pesquisa.

## <a name="see-also"></a>Consulte também

- [XML Schema Explorer](../xml-tools/xml-schema-explorer.md)