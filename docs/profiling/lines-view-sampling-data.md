---
title: Exibição de Linhas – Dados de Amostragem | Microsoft Docs
description: Saiba como a exibição de linhas de dados de amostragem lista dados de desempenho para as instruções que estavam sendo executadas quando as amostras foram coletadas na execução da criação de perfil.
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Lines view
ms.assetid: 46497249-c797-42c5-a02c-3e4bb3b4ee60
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 38ae3e9c40204082ea8791ddea4e92d77a0d311e
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98721314"
---
# <a name="lines-view---sampling-data"></a>Exibição de linhas – dados de amostragem
A visualização Linhas de dados de amostragem lista os dados de desempenho das instruções que estavam em execução quando os exemplos foram coletados na criação de perfil.

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

 Em um arquivo de origem, uma instrução pode abranger mais de uma linha em um arquivo de origem, e uma única linha pode incluir mais de uma instrução. Uma instrução é identificada pelo seguinte:

- O arquivo de origem que contém a instrução da função.

- A função que contém a instrução.

- A linha de origem em que a instrução se inicia.

- O caractere na linha de origem em que a instrução se inicia.

- A linha de origem em que a instrução termina.

- O caractere na linha de origem em que a instrução termina.

  A coluna de Nome de Linha fornece uma concatenação classificável dos dados do identificador.

  Por definição, uma instrução não chama outras funções. Portanto, apenas valores exclusivos são listados.

|Coluna|Descrição|
|------------|-----------------|
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|
|**Nome do processo**|O nome do processo.|
|**Nome do módulo**|O nome do módulo que contém a linha de função.|
|**Caminho do Módulo**|O caminho do módulo que contém a linha de função.|
|**Arquivo de Origem**|O arquivo de origem que contém a linha de função.|
|**Nome da função**|O nome da função.|
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|
|**Endereço da função**|O endereço inicial da função.|
|**Início da Linha de Origem**|O número de linha inicial no arquivo de origem em que esse exemplo foi coletado.|
|**Final da Linha de Origem**|O número de linha final no arquivo de origem em que esse exemplo foi coletado.|
|**Início do Caractere de Origem**|O deslocamento do caractere inicial na linha do arquivo de origem em que esse exemplo foi coletado.|
|**Final do Caractere de Origem**|O deslocamento do caractere final na linha do arquivo de origem em que esse exemplo foi coletado.|
|**Nome da Linha**|Um identificador gerado pelo criador de perfil da linha com a seguinte sintaxe: `Source File` **; [** `Line Number Start` **,**`Character Start` **]->; [**`Line Number End`**,**`Character End`**]**|
|**Amostras Exclusivas**|O número total de amostras coletadas durante a execução da linha de função.|
|**% de Amostras Exclusivas**|O percentual de todas as amostras coletadas na criação de perfil durante a execução da linha de função.|

## <a name="see-also"></a>Confira também
- [Exibição de linhas-amostragem](../profiling/lines-view-dotnet-memory-sampling-data.md)
