---
title: Pesquisar tópicos (Help Viewer)
ms.date: 11/02/2017
ms.topic: conceptual
ms.assetid: 683f1b0c-1551-4bba-91fe-3855f03fdd69
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 52818e4f676d6ae9f4c02f26ad8e354b206cb2b8
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67824988"
---
# <a name="how-to-search-for-topics"></a>Como: Pesquisar tópicos

Você pode usar o recurso de pesquisa de texto completo para localizar todos os tópicos que contêm uma palavra específica. Você também pode refinar e personalizar sua pesquisa usando expressões curinga, operadores lógicos e operadores de pesquisa avançada.

Para abrir a guia **Pesquisar**, escolha a guia **Pesquisar** na janela do **Visualizador da Ajuda** ou, se você for um usuário de teclado, escolha **Ctrl**+**E**.

## <a name="to-perform-a-full-text-search"></a>Para realizar uma pesquisa de texto completo

1. Na caixa de pesquisa, digite a palavra que deseja localizar.

2. Na consulta de pesquisa, especifique quais operadores de pesquisa avançados ou lógicos deseja aplicar à pesquisa, se houver. Para pesquisar toda a ajuda disponível, não use operadores.

    > [!NOTE]
    > Na caixa de diálogo **Opções do Visualizador**, você pode especificar preferências adicionais, como o número máximo de resultados da pesquisa a serem exibidos por vez e se deseja incluir conteúdo em inglês se a localidade principal não for inglês.

3. Escolha a tecla **ENTER**.

     Uma pesquisa retorna no máximo 200 ocorrências, por padrão, e as exibe na área de resultados da pesquisa. Informações adicionais de versão para cada resultado podem aparecer, dependendo do conteúdo.

4. Para exibir um tópico, escolha seu título na lista de resultados.

## <a name="full-text-search-tips"></a>Dicas de pesquisa de texto completo

Você pode criar pesquisas mais direcionadas, que retornam somente os tópicos mais interessantes, se você entender como a sintaxe afeta a consulta. A sintaxe inclui caracteres especiais, palavras reservadas e filtros. Este tópico fornece dicas, procedimentos e informações detalhadas de sintaxe para ajudá-lo a construir melhor suas consultas.

### <a name="general-guidelines"></a>Diretrizes gerais

A tabela a seguir inclui algumas regras básicas e diretrizes para o desenvolvimento de consultas de pesquisa na ajuda.

|Sintaxe|DESCRIÇÃO|
|------------|-----------------|
|Diferenciação de maiúsculas e minúsculas|As pesquisas não diferenciam maiúsculas de minúsculas. Desenvolva seus critérios de pesquisa usando caracteres em maiúsculas ou em minúsculas. Por exemplo, "OLE" e "ole" retornam os mesmos resultados.|
|Combinações de caracteres|Não é possível pesquisar somente por letras (a–z) ou números (0–9) individuais. Se você tentar pesquisar determinadas palavras reservadas, como "e", "de" e "com", elas serão ignoradas. Para obter mais informações, consulte [Palavras ignoradas em pesquisas](#stopwords) posteriormente neste tópico.|
|Ordem de avaliação|As consultas de pesquisa são avaliadas da esquerda para a direita.|

### <a name="search-syntax"></a>Pesquisa de sintaxe

Se você especificar uma cadeia de caracteres de pesquisa que inclui várias palavras, como "word1 word2", essa cadeia de caracteres será equivalente a digitar "word1 AND word2", que retornará apenas os tópicos que contêm todas as palavras individuais nessa cadeia de caracteres de pesquisa.

> [!IMPORTANT]
> - Não há suporte para pesquisas de frase. Se você especificar mais de uma palavra em uma cadeia de caracteres de pesquisa, os tópicos retornados conterão todas as palavras especificadas, mas não necessariamente a frase exata especificada.
> - Use operadores lógicos para especificar a relação entre as palavras em sua frase de pesquisa. É possível incluir operadores lógicos como AND, OR, NOT e NEAR para refinar ainda mais a sua pesquisa. Por exemplo, se você pesquisar "declarando NEAR união", os resultados da pesquisa incluirão tópicos que contêm as palavras "declarando" e "união" com poucas palavras entre as duas. Para obter mais informações, consulte [Operadores lógicos em expressões de pesquisa](../help-viewer/logical-operators-search-expressions.md).

### <a name="filters"></a>Filtros

É possível restringir ainda mais os resultados da pesquisa usando operadores de pesquisa avançada. A Ajuda inclui três categorias que você pode usar para filtrar os resultados de uma pesquisa de texto completo: Título, Código e Palavra-chave.

### <a name="ranking-of-search-results"></a>Classificação de resultados da pesquisa

O algoritmo de pesquisa é aplicável a determinados critérios para ajudar a classificar resultados da pesquisa superiores ou inferiores na lista de resultados. No geral:

1. O conteúdo que inclui palavras de pesquisa no título tem uma classificação mais alta do que o conteúdo que não inclui.

2. O conteúdo que inclui palavras de pesquisa muito próximas tem uma classificação mais alta do que o conteúdo que não inclui.

3. O conteúdo com uma densidade maior das palavras de pesquisa tem uma classificação mais alta do que o conteúdo que tem uma densidade menor das palavras de pesquisa.

### <a name="stopwords"> Palavras ignoradas em pesquisas (palavras irrelevantes)</a>

Palavras ou números que ocorrem com frequência, chamados de palavras irrelevantes, são automaticamente ignorados durante uma pesquisa de texto completo. Por exemplo, se você pesquisar a frase "passar por", os resultados da pesquisa exibirão tópicos que contêm a palavra "passar", mas não "por".

## <a name="see-also"></a>Consulte também

- [Operadores lógicos e avançados](../help-viewer/logical-operators-search-expressions.md)
- [Como: Localizar tópicos no índice](../help-viewer/find-topics-index.md)
- [Como: Encontrar tópicos no sumário](../help-viewer/find-topics-toc.md)
- [Microsoft Help Viewer](../help-viewer/overview.md)