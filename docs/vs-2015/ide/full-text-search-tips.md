---
title: Dicas de pesquisa de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- hv_search
helpviewer_keywords:
- Help Viewer 2.0, full-text search tips
- full-text search tips [Help Viewer 2.0]
ms.assetid: bcaad23d-2ca7-4bec-8b54-b884bc34e70b
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 85770dfd3c610f92bcb190b7a2c151b40cd31a4c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850042"
---
# <a name="full-text-search-tips"></a>Dicas de pesquisa de texto completo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um dos métodos mais úteis para localizar informações na Ajuda é executando uma pesquisa de texto completo. Para refinar e personalizar os resultados, é necessário compreender como a sintaxe afeta sua consulta. Este tópico fornece dicas, procedimentos e informações detalhadas de sintaxe para ajudá-lo a construir melhor suas consultas.  
  
## <a name="full-text-search-tips"></a>Dicas de pesquisa de texto completo  
 Será possível criar pesquisas mais direcionadas que retornam somente os tópicos mais interessantes para você se você entender como a Ajuda interpreta a formatação que você usa nas consultas. Esses formatos incluem caracteres especiais, palavras reservadas e filtros.  
  
### <a name="general-guidelines"></a>Diretrizes gerais  
 A tabela a seguir inclui algumas regras básicas e diretrizes para o desenvolvimento de consultas de pesquisa na Ajuda.  
  
|Sintaxe|Descrição|  
|------------|-----------------|  
|Diferenciação de maiúsculas e minúsculas|As pesquisas não diferenciam maiúsculas de minúsculas. Desenvolva seus critérios de pesquisa usando caracteres em maiúsculas ou em minúsculas. Por exemplo, "OLE" e "ole" retornam os mesmos resultados.|  
|Combinações de caracteres|Não é possível pesquisar somente por letras individuais (a–z) ou números (0–9). Se você tentar pesquisar determinadas palavras reservadas, como "and", "from" e "with", elas serão ignoradas. Para obter mais informações, consulte "Palavras ignoradas em pesquisas (palavras irrelevantes)" posteriormente neste tópico.|  
|Ordem de avaliação|As consultas de pesquisa são avaliadas da esquerda para a direita.|  
  
### <a name="search-syntax"></a>Sintaxe de pesquisa  
 Se você especificar uma cadeia de caracteres de pesquisa que inclui várias palavras, como "word1 word2", essa cadeia de caracteres será equivalente a digitar "word1 AND word2", que retornará apenas os tópicos que contêm todas as palavras individuais nessa cadeia de caracteres de pesquisa.  
  
> [!IMPORTANT]
> 1. Não há suporte para pesquisas de frase. Se você especificar mais de uma palavra em uma cadeia de caracteres de pesquisa, os tópicos retornados conterão todas as palavras especificadas, mas não necessariamente a frase exata especificada.  
>    2.  Use operadores lógicos para especificar a relação entre as palavras em sua frase de pesquisa. É possível incluir operadores lógicos como AND, OR, NOT e NEAR para refinar ainda mais a sua pesquisa. Por exemplo, se você pesquisar "declarando NEAR união", os resultados da pesquisa incluirão tópicos que contêm as palavras "declarando" e "união" com poucas palavras entre as duas. Para obter mais informações, consulte [Operadores lógicos em expressões de pesquisa](../ide/logical-operators-in-search-expressions.md).  
  
### <a name="filters"></a>Filtros  
 É possível restringir ainda mais os resultados da pesquisa usando operadores de pesquisa avançada. A Ajuda inclui três categorias que você pode usar para filtrar os resultados de uma pesquisa de texto completo: Título, Código e Palavra-chave. Para obter mais informações, consulte [Operadores de pesquisa avançada em expressões de pesquisa](../ide/advanced-search-operators-in-search-expressions.md).  
  
### <a name="ranking-of-search-results"></a>Classificação de resultados da pesquisa  
 O algoritmo de pesquisa é aplicável a determinados critérios para ajudar a classificar resultados da pesquisa superiores ou inferiores na lista de resultados. No geral:  
  
1.  O conteúdo que inclui palavras de pesquisa no título tem uma classificação mais alta do que o conteúdo que não inclui.  
  
2.  O conteúdo que inclui palavras de pesquisa muito próximas tem uma classificação mais alta do que o conteúdo que não inclui.  
  
3.  O conteúdo com uma densidade maior das palavras de pesquisa tem uma classificação mais alta do que o conteúdo que tem uma densidade menor das palavras de pesquisa.  
  
### <a name="words-ignored-in-searches-stop-words"></a>Palavras ignoradas em pesquisas (palavras irrelevantes)  
 Palavras ou números que ocorrem com frequência, chamados de palavras irrelevantes, são automaticamente ignorados durante uma pesquisa de texto completo. Por exemplo, se você pesquisar a frase "passar por", os resultados da pesquisa exibirão tópicos que contêm a palavra "passar", mas não "por".  
  
## <a name="see-also"></a>Consulte também  
 [Localizar informações](../ide/locate-information.md)   
 [Operadores lógicos em expressões de pesquisa](../ide/logical-operators-in-search-expressions.md)



