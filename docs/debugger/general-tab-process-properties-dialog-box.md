---
title: Guia geral, caixa de diálogo Propriedades de processo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: 86f4d61d-a594-4aac-8960-c5279b4a10fd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3dcefc8be643c74349102261725c4879c0e161cd
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31471694"
---
# <a name="general-tab-process-properties-dialog-box"></a>Guia Geral, Caixa de diálogo Propriedades do Processo
Use o **geral** tab para obter mais informações sobre um processo específico. Para exibir o [caixa de diálogo de propriedades do processo](../debugger/process-properties-dialog-box.md), mova o foco para um [exibição processos](../debugger/processes-view.md) janela. Selecione qualquer nó de processo na árvore e escolha **propriedades** do **exibição** menu.  
  
 As configurações a seguir estão disponíveis no **geral** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Nome do Módulo**|O nome do módulo.|  
|**ID do Processo**|A ID exclusiva do processo. Números de ID de processo são reutilizados e, portanto eles identificam um processo somente para o tempo de vida do processo. O tipo de objeto de processo é criado quando um programa é executado. Todos os threads em um processo compartilham o mesmo espaço de endereço e têm acesso aos mesmos dados.|  
|**Base de prioridade**|A prioridade base atual desse processo. Threads em um processo podem aumentar e diminuir sua própria prioridade básica em relação a prioridade básica do processo.|  
|**Threads**|O número de threads atualmente ativo neste processo.|  
|**Tempo de CPU**|Tempo total de CPU gasto sobre esse processo e seus threads. Igual ao tempo de usuário mais tempo privilegiado.|  
|**Tempo do usuário**|O tempo decorrido cumulativo que threads desse processador passaram executando código no modo de usuário em threads não ociosos. Aplicativos executam no modo de usuário, assim como os subsistemas, como o Gerenciador de janelas e o mecanismo de gráficos.|  
|**Tempo privilegiado**|O tempo total decorrido esse processo esteve em execução no modo privilegiado em threads não ociosos. A camada de serviço, as rotinas de executivo e Kernel executam no modo privilegiado. Drivers de dispositivo para a maioria dos dispositivos diferentes adaptadores de gráficos e impressoras também executam no modo privilegiado. Algum trabalho que o Windows para o seu aplicativo pode aparecer em outros processos além do tempo privilegiado do subsistema.|  
|**Tempo decorrido**|O tempo total decorrido que esse processo esteve em execução.|