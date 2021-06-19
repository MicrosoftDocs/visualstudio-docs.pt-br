---
title: Os mapas de código estão lentos
description: Saiba como melhorar o desempenho do mapa de código e como você pode minimizar o tempo necessário para concluir a renderização.
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5a279a04b1bd76933df335bc0b2527ab4b2418f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389638"
---
# <a name="improve-performance-for-code-maps"></a>Melhorar o desempenho para mapas de código

Quando você gera um mapa pela primeira vez, o Visual Studio indexa todas as dependências que ele encontra. Esse processo pode levar algum tempo, especialmente para soluções grandes, mas melhora o desempenho posterior. Se o código for alterado, o Visual Studio só reindexará o código atualizado. Para minimizar o tempo necessário para o mapa concluir a renderização, considere as seguintes sugestões:

- Mapeie somente as dependências que lhe interessam.

- Antes de gerar o mapa para uma solução inteira, reduza o escopo da solução.

- Desative a compilação automática para a solução selecionando **ignorar compilação** na barra de ferramentas do mapa de códigos.

- Desative a adição automática de itens pai selecionando **incluir pais** na barra de ferramentas do mapa de códigos.

   ![Ignorar os botões criar e incluir pais](../modeling/media/codemapsfilterskipbuildicons.png)

- Edite o arquivo de mapa de código diretamente para remover nós e links desnecessários. A alteração do mapa não afeta o código subjacente. Consulte [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

Pode levar mais tempo para criar mapas ou adicionar itens a um mapa de **Gerenciador de soluções** quando a propriedade **copiar para o diretório de saída** de um item de projeto é definida como **copiar sempre**. Para aumentar o desempenho, altere essa propriedade para **copiar se mais recente** ou `PreserveNewest` . Consulte [Builds incrementais](../msbuild/incremental-builds.md).

O mapa concluído mostra dependências somente para o código criado com êxito. Se ocorrerem erros de compilação para determinados componentes, esses erros aparecerão no mapa. Certifique-se de que um componente realmente cria e tem dependências nele antes de tomar decisões arquitetônicas com base no mapa.
