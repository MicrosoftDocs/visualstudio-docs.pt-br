---
title: Guia geral, caixa de diálogo Propriedades de Thread | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- threading [Visual Studio], thread properties
- thread properties
ms.assetid: 46b6c668-6786-456e-97dc-337bcac0d812
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fe6eb87418671b9b070aebaf60d1bb9c84b3623a
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31474600"
---
# <a name="general-tab-thread-properties-dialog-box"></a>Guia Geral, Caixa de diálogo Propriedades do Thread
Use essa caixa de diálogo para obter mais informações sobre um segmento específico. Para exibir essa caixa de diálogo, mova o foco para um [exibição de Threads](../debugger/threads-view.md) janela ou abra [exibição de mensagens](../debugger/messages-view.md) e expanda uma mensagem. Selecione qualquer nó de segmento na árvore e escolha **propriedades** do **exibição** menu.  
  
 O **propriedades de Thread** caixa de diálogo contém um painel, o **geral** guia. As configurações a seguir estão disponíveis:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Nome do Módulo**|O nome do módulo.|  
|**ID do Thread**|A ID exclusiva deste thread. Observe que os números de ID de thread são reutilizados; Eles identificam um thread somente para o tempo de vida do thread.|  
|**ID do Processo**|A ID exclusiva do processo. Números de ID de processo são reutilizados e, portanto eles identificam um processo somente para o tempo de vida do processo. O tipo de objeto de processo é criado quando um programa é executado. Todos os threads em um processo compartilham o mesmo espaço de endereço e têm acesso aos mesmos dados. Escolha esse valor para exibir as propriedades da ID do processo.|  
|**Estado de thread**|O estado atual do thread. Um thread em execução está usando um processador. um thread em espera está prestes a usar um. Um Thread pronto está aguardando para usar um processador porque um não está livre. Um thread em transição está aguardando um recurso executar, como esperar por sua pilha de execução a ser paginada no disco. Um thread de espera não é necessário o processador porque está aguardando uma operação de periférica para concluir ou um recurso seja liberado.|  
|**Razão de espera**|Isso é aplicável somente quando o thread está em estado de espera. Pares de evento são usados para se comunicar com subsistemas protegidos.|  
|**Tempo de CPU**|Tempo total de CPU gasto sobre esse processo e seus threads. Igual ao tempo de usuário + tempo privilegiado.|  
|**Tempo do usuário**|O tempo total decorrido que este thread gastou executando código em modo de usuário. Aplicativos executam no modo de usuário, assim como os subsistemas, como o Gerenciador de janelas e o mecanismo de gráficos.|  
|**Tempo privilegiado**|O tempo total decorrido que este thread gastou executando código em modo privilegiado. Quando um serviço de sistema do Windows é chamado, o serviço geralmente será executado no modo privilegiado para obter acesso aos dados privados do sistema. Esses dados são protegidos contra o acesso por threads executados no modo de usuário. Chamadas para o sistema podem estar explícitas, ou eles podem ser implícitos, como quando ocorre uma falha de página ou uma interrupção.|  
|**Tempo decorrido**|O tempo total decorrido (em segundos) esse thread está sendo executado.|  
|**Prioridade atual**|A prioridade dinâmica atual deste thread. Threads em um processo podem aumentar e diminuir sua própria prioridade básica em relação a prioridade básica do processo.|  
|**Prioridade básica**|A prioridade base atual deste thread.|  
|**Endereço inicial**|Iniciando endereço virtual para este thread.|  
|**Computador do usuário**|O contador de programa de usuário para o thread.|  
|**Alternâncias de contexto**|O número de alternâncias de um thread para outro. Opções de thread podem ocorrer dentro de um único processo ou através dos processos. Um comutador de thread pode ser causado por um thread solicitando informações a outro ou por um thread sendo apropriado quando um segmento de prioridade mais alto estiver pronto para ser executado.|