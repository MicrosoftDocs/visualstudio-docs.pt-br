---
title: Exibição de IPs (ponteiros de instrução) – Dados de Amostragem da Memória do .NET | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Instruction Pointers view
ms.assetid: 7d91cc14-e8e9-4ebb-b14f-b9f0da770508
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 295dd3c490495f481ca9568524ee83eb0b1b59be
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54966823"
---
# <a name="instruction-pointers-ips-view---net-memory-sampling-data"></a>Exibição de IPs (ponteiros de instrução) – dados de amostragem da memória do .NET
A exibição de IPs dos dados de criação de perfil de alocação de memória do .NET que foi coletada ao usar o método de amostragem lista as instruções de assembly que alocaram memória durante o processo de criação de perfil. As colunas da exibição também listam o tamanho e o número de alocações.  
  
 Apenas valores exclusivos são listados.  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID do Processo**|A ID de processo (PID) da criação de perfil.|  
|**Nome do Processo**|O nome do processo.|  
|**Nome do Módulo**|O nome do módulo que contém a instrução.|  
|**Caminho do Módulo**|O caminho do módulo que contém a instrução.|  
|**Arquivo de Origem**|O arquivo de origem que contém a instrução.|  
|**Nome da Função**|O nome da função.|  
|**Número de linha da função**|O número de linha do início dessa função no arquivo de origem.|  
|**Endereço da Função**|O endereço inicial da função.|  
|**Início da Linha de Origem**|O número de linha inicial no arquivo de origem em que a alocação ocorreu.|  
|**Final da Linha de Origem**|O número de linha final no arquivo de origem em que a alocação ocorreu.|  
|**Início do Caractere de Origem**|O deslocamento do caractere inicial na linha do arquivo de origem em que a alocação ocorreu.|  
|**Final do Caractere de Origem**|O deslocamento do caractere final na linha do arquivo de origem em que a alocação ocorreu.|  
|**Endereço da Instrução**|O endereço da instrução.|  
|**Alocações Exclusivas**|O número total de objetos que foram criados pela instrução.|  
|**% de Alocações Exclusivas**|O percentual de todos os objetos criados na criação de perfil que foram alocados pela instrução.|  
|**Bytes Exclusivos**|O número de bytes de memória que foram alocados na criação de perfil que foram alocados pela instrução.|  
|**% de Bytes Exclusivos**|O percentual de todos os bytes de memória que foram alocados na criação de perfil que foram alocados pela instrução.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de IPs (ponteiros de instrução)](../profiling/instruction-pointers-ips-view-sampling-data.md)