---
title: API de gráficos e estatísticas de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.apistatistics
- vs.graphics.memorystatistics
ms.assetid: 27d2f303-e3ed-4219-9009-345a0d849506
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 48c8ed3c8c2ebffc57ac46e987dbc37950cba0fd
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31481522"
---
# <a name="graphics-api-and-memory-statistics"></a>API de gráficos e estatísticas de memória
<!-- VERSIONLESS -->
2017 do Visual Studio e maior suporte a estatísticas de API de gráficos e ferramentas de estatísticas de memória.  Essas duas ferramentas permitem exibir várias partes de informações sobre o uso da API do Direct3D, bem como o consumo de memória GPU de vários recursos.

## <a name="graphics-api-statistics"></a>Estatísticas de API de gráficos
As estatísticas de API de gráficos no diagnóstico de gráficos do Visual Studio permite que você exiba todas as chamadas Direct3D que foram feitas e a contagem de cada chamada.  Para exibir a janela, selecione o **exibição > estatísticas API** item de menu.

![Estatísticas de API](media/gfx_diag_api_statistics.png)

Essa ferramenta pode ser útil para descobrir fazendo chamadas DirectX que talvez não percebam chamadas ou que você estiver fazendo com muita frequência.

Clique na janela para copiar todos os dados como CSV, que pode ser colado em algo como o Excel para análise posterior.

## <a name="memory-statistics"></a>Estatísticas de memória
Essa ferramenta exibirá a quantidade de memória está alocando o driver de gráficos para os recursos que você criar em um quadro.  Para exibir essa janela, selecione o **exibição > estatísticas de memória** item de menu.

![Estatísticas de memória](media/gfx_diag_memory_statistics.png)

O **alocação de GPU** coluna exibe a quantidade de memória usada pelo evento exibido no **evento** coluna.  Você também pode selecionar o ícone de Observação ![ícone inspecionar](media/gfx_watch.png) para exibir o [recurso histórico](graphics-event-list.md#resource-history) para o evento selecionado.

Assim como acontece com a ferramenta de estatísticas de API, clique na janela para copiar todos os dados como CSV, que pode ser colado em algo como o Excel para análise posterior.

## <a name="see-also"></a>Consulte também  
[Diagnóstico de gráficos (depuração DirectX Graphics)](visual-studio-graphics-diagnostics.md)   
[Histórico de recursos](graphics-event-list.md#resource-history)
<!-- /VERSIONLESS -->