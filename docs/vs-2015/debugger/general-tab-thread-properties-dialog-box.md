---
title: Guia geral, caixa de diálogo Propriedades do Thread | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- threading [Visual Studio], thread properties
- thread properties
ms.assetid: 46b6c668-6786-456e-97dc-337bcac0d812
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b1a8e6fd583f6035fc84f0c86adcee059562235d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159951"
---
# <a name="general-tab-thread-properties-dialog-box"></a>Guia Geral, Caixa de diálogo Propriedades do Thread
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use essa caixa de diálogo para obter mais informações sobre um segmento específico. Para exibir essa caixa de diálogo, mova o foco para um [exibição de Threads](../debugger/threads-view.md) janela ou abra [exibição de mensagens](../debugger/messages-view.md) e expandir uma mensagem. Selecione qualquer nó de segmento na árvore e escolha **propriedades** da **exibição** menu.  
  
 O **propriedades do Thread** caixa de diálogo contém um painel, o **geral** guia. As configurações a seguir estão disponíveis:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Nome do Módulo**|O nome do módulo.|  
|**ID do Thread**|A ID exclusiva deste thread. Observe que os números de ID de thread são reutilizados; elas identificam um thread somente para o tempo de vida do thread em questão.|  
|**ID do Processo**|A ID exclusiva desse processo. Números de ID de processo são reutilizados, eles identificam um processo somente para o tempo de vida do processo. O tipo de objeto de processo é criado quando um programa é executado. Todos os threads em um processo compartilham o mesmo espaço de endereço e têm acesso aos mesmos dados. Escolha esse valor para exibir as propriedades de ID do processo.|  
|**Estado da Thread**|O estado atual do thread. Um thread de execução é utilizar um processador. um thread em espera está prestes a usar um. Um Thread pronto está esperando para usar um processador como um não é gratuito. Um thread em transição está aguardando um recurso a ser executado, como aguardar sua pilha de execução ser paginada do disco. Um thread em espera não é necessário o processador porque está aguardando uma operação periférica ser concluída ou um recurso seja liberado.|  
|**Motivo de Espera**|Isso é aplicável somente quando o thread está em estado de espera. Pares de eventos são usados para se comunicar com subsistemas protegidos.|  
|**Tempo de CPU**|Tempo total de CPU gasto sobre esse processo e seus threads. Igual ao tempo de usuário + tempo privilegiado.|  
|**Tempo do Usuário**|O tempo total decorrido que esse thread gastou executando código no modo de usuário. Aplicativos executam no modo de usuário, como fazem os subsistemas, como o Gerenciador de janelas e o mecanismo gráfico.|  
|**Tempo Privilegiado**|O tempo total decorrido que esse thread gastou executando código em modo privilegiado. Quando um serviço de sistema do Windows é chamado, o serviço geralmente será executado em modo privilegiado para obter acesso aos dados privados do sistema. Esses dados são protegidos contra acesso por threads em execução no modo de usuário. Chamadas para o sistema podem ser explícitas ou podem ser implícitas, como quando ocorre uma falha de página ou uma interrupção.|  
|**Tempo Decorrido**|O tempo total decorrido (em segundos) esse thread está sendo executado.|  
|**Prioridade Atual**|A prioridade dinâmica atual deste thread. Threads dentro de um processo podem aumentar e diminuir sua própria prioridade básica em relação a prioridade base do processo.|  
|**Prioridade de Base**|A prioridade base atual deste thread.|  
|**Endereço Inicial**|Iniciando endereço virtual para este thread.|  
|**PC do Usuário**|O contador de programa do usuário para o thread.|  
|**Opções de Contexto**|O número de alternâncias de um thread para outro. Alternâncias de thread podem ocorrer dentro de um único processo ou entre processos. Um comutador de thread pode ser causado por um thread solicitando informações a outro, ou por um thread sendo apropriado quando um thread de prioridade mais alta se torna pronto para ser executado.|
