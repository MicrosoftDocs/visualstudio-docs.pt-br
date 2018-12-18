---
title: Guia geral, caixa de diálogo Propriedades de processar | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: 86f4d61d-a594-4aac-8960-c5279b4a10fd
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cd05c82c33349f4a783204538ab47232fa6fcbc4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798942"
---
# <a name="general-tab-process-properties-dialog-box"></a>Guia Geral, Caixa de diálogo Propriedades do Processo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o **geral** tab para obter mais informações sobre um processo específico. Para exibir o [caixa de diálogo de propriedades do processo](../debugger/process-properties-dialog-box.md), mova o foco para um [exibição de processos](../debugger/processes-view.md) janela. Selecione qualquer nó de processo na árvore e escolha **propriedades** da **exibição** menu.  
  
 As seguintes configurações estão disponíveis sobre o **geral** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Nome do Módulo**|O nome do módulo.|  
|**ID do Processo**|A ID exclusiva desse processo. Números de ID de processo são reutilizados, eles identificam um processo somente para o tempo de vida do processo. O tipo de objeto de processo é criado quando um programa é executado. Todos os threads em um processo compartilham o mesmo espaço de endereço e têm acesso aos mesmos dados.|  
|**Base de prioridade**|A prioridade base atual desse processo. Threads dentro de um processo podem aumentar e diminuir sua própria prioridade básica em relação à prioridade de base do processo.|  
|**Threads**|O número de threads atualmente ativo neste processo.|  
|**Tempo de CPU**|Tempo total de CPU gasto sobre esse processo e seus threads. Igual ao tempo de usuário mais tempo privilegiado.|  
|**Tempo do usuário**|O tempo decorrido cumulativo que os threads desse processador passaram executando código no modo de usuário em threads não ociosos. Aplicativos executam no modo de usuário, como fazem os subsistemas, como o Gerenciador de janelas e o mecanismo gráfico.|  
|**Tempo privilegiado**|O tempo total decorrido esse processo tiver sido executado no modo privilegiado em threads não ociosos. A camada de serviço, as rotinas de executivo e o Kernel executar no modo privilegiado. Drivers de dispositivo para a maioria dos dispositivos que não seja de impressoras e adaptadores de gráficos também são executadas em modo privilegiado. Algum trabalho que faz do Windows para o seu aplicativo pode aparecer em outros processos além do tempo privilegiado do subsistema.|  
|**Tempo decorrido**|O tempo total decorrido que esse processo de execução.|



