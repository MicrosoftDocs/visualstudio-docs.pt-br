---
title: Mapas de código estão lentos
ms.date: 05/16/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 2dece1e63fffdba67678422ad9241babc63b7abd
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34267693"
---
# <a name="improve-performance-for-code-maps"></a>Melhorar o desempenho de mapas de código

Quando você gera um mapa pela primeira vez, o Visual Studio índices todas as dependências que encontrar. Esse processo pode levar algum tempo, especialmente para grandes soluções, mas melhora o desempenho posterior. Se o código for alterado, o Visual Studio só reindexará o código atualizado. Para minimizar o tempo necessário concluir a renderização do mapa, considere as seguintes sugestões:

- [Mapear apenas as dependências que lhe interessam.](#create-a-code-map-to-see-specific-dependencies)

- Antes de gerar o mapa de uma solução inteira, reduza o escopo da solução.

- Desativar a criação automática para a solução selecionando **Skip Build** na barra de ferramentas de mapa de código.

- Desativar a adição automática de itens pai selecionando **incluem pais** na barra de ferramentas de mapa de código.

   ![Ignorar compilação e incluir pais botões](../modeling/media/codemapsfilterskipbuildicons.png)

- Edite o arquivo de mapa de código diretamente para remover nós e links que não é necessário. Alterar o mapa não afeta o código subjacente. Consulte [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

Pode levar mais tempo para criar mapas ou adicionar itens a um mapa de **Solution Explorer** quando um item de projeto **copiar para diretório de saída** está definida como **copiar sempre**. Para aumentar o desempenho, altere essa propriedade como **copiar se mais recente** ou `PreserveNewest`. Consulte [compilações incrementais](../msbuild/incremental-builds.md).

O mapa concluído mostra dependências somente para código compilado com êxito. Se ocorrerem erros de compilação para determinados componentes, esses erros aparecem no mapa. Certifique-se de que um componente, na verdade, compilações e tem dependências antes de tomar decisões de arquitetura baseadas no mapa.