---
title: Exibição de processo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.view.process
helpviewer_keywords:
- performance tools reports, process view
- Process view
- performance tools, process view
- Profiling Tools,process view
- Profiling Tools,process report
ms.assetid: 6d4e2a5d-9f17-4ece-a6f1-75836e1fc382
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 56fb301436b3fbe9374301fa4f7a8fd421485cbb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794498"
---
# <a name="process-view"></a>Exibição de processo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição do processo exibe dados de criação de perfil para os processos e threads executados durante o processo de criação de perfil.  
  
 Os processos são listados por nome. Os threads são listados como nós filhos do processo que os criou. Os threads são nomeados pela função que iniciou o thread ou pelo rótulo **[ntdll.dll]** quando não há símbolos disponíveis.  
  
 Clique com o botão direito do mouse na exibição e, em seguida, selecione **Adicionar/Remover Colunas** para adicionar ou remover colunas. Ou clique no nome da coluna para classificar os dados. Para obter mais informações, consulte [Como personalizar colunas de exibição de relatório](../profiling/how-to-customize-report-view-columns.md).  
  
 As colunas da exibição de processo são as mesmas usadas pelos gerados pelos métodos de amostragem e instrumentação e pelos dados que incluem dados de memória do .NET. A tabela a seguir descreve os valores da coluna.  
  
|Column|Descrição|  
|------------|-----------------|  
|**ID exclusiva**|Um identificador gerado pelo criador de perfil que é exclusivo ao processo ou thread.|  
|**ID**|O identificador do processo ou thread gerado pelo sistema.|  
|**Nome**|O nome do processo ou thread.|  
|**Hora de início**|O número de milissegundos ou ciclos de processador desde o início da criação de perfil até o início do processo ou thread.|  
|**Hora de término**|O número de milissegundos ou ciclos de processador desde o início da criação de perfil até o fim do processo ou thread.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de dados do método de amostragem](../profiling/profiler-sampling-method-data-views.md)   
 [Exibições de dados do método de instrumentação](../profiling/instrumentation-method-data-views.md)   
 [Exibições de dados da memória do .NET](../profiling/dotnet-memory-data-views.md)



