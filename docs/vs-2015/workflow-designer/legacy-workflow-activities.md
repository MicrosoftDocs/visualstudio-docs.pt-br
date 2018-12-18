---
title: Atividades de fluxo de trabalho herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- workflows, activities
- activities
- workflow activities
ms.assetid: 4af7a06b-1e82-43c8-aec8-0dc5fb63d08a
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 6ff21a431e380a281ce1261215367b89c4ecf1a3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49205384"
---
# <a name="legacy-workflow-activities"></a>Atividades herdados de fluxo de trabalho
[!INCLUDE[wf](../includes/wf-md.md)] inclui um conjunto padrão de atividades que fornecem a funcionalidade para o fluxo de controle, as condições, manipulação de eventos, o gerenciamento de estado, e a comunicação com aplicativos e serviços. Ao criar fluxos de trabalho, você pode usar sistema forneceu as atividades que são fornecidas por [!INCLUDE[wfd1](../includes/wfd1-md.md)], ou você pode criar suas próprias atividades personalizados.  
  
 A tabela a seguir lista o conjunto de atividade de para fora da estrutura de [!INCLUDE[wf2](../includes/wf2-md.md)] . Muitas, mas não todas, essas atividades são representadas por designers de atividade que podem ser acessados do **caixa de ferramentas** da [!INCLUDE[wfd2](../includes/wfd2-md.md)]. Para criar uma atividade, arraste o designer do **caixa de ferramentas** e solte-o na superfície de design.  
  
|Atividade|Descrição|  
|--------------|-----------------|  
|[CallExternalMethodActivity](http://go.microsoft.com/fwlink?LinkID=65025)|Usado com o **HandleExternalEventActivity** atividade para comunicações de entrada e saídas com um serviço local. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de CallExternalMethodActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65060).|  
|[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)|Usado para conter a lógica de limpeza para uma atividade composta cancelada antes de filhos de quaisquer atividades composto é executar concluído. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de CancellationHandlerActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65061).|  
|[CodeActivity](http://go.microsoft.com/fwlink?LinkID=65026)|Permite que você adicione Visual Basic ou código em c ao fluxo de trabalho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de CodeActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65062).|  
|[Compensatablesequenceactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65027)|Uma versão compensável [SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Compensatablesequenceactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65002).|  
|[Compensatabletransactionscopeactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65051)|Uma versão compensável **TransactionScopeActivity**. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Compensatabletransactionscopeactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65063).|  
|[Compensateactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65052)|Permite que você chamar código para desfazer ou compensar operações já executadas pelo fluxo de trabalho quando ocorre um erro. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Compensateactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65064).|  
|[CompensationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65053)|Um wrapper para uma ou mais atividades que executam a compensação para uma atividade de TransactionScopeActivity concluída [!INCLUDE[crdefault](../includes/crdefault-md.md)] [usando a atividade de CompensationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65065).|  
|[ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)|Executa atividades filho com base em uma condição que aplica-se para o [ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017) atividade em si e com base nas condições que se aplicam separada para cada filho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65066).|  
|[DelayActivity](http://go.microsoft.com/fwlink?LinkID=65028)|Permite que você crie os atrasos no fluxo de trabalho que são baseados em um intervalo de tempo limite. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de DelayActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65067).|  
|[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)|Envolve uma ou mais atividades que são executadas quando ocorre um evento especificado. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65068).|  
|[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)|Fornece uma estrutura para associar eventos com uma atividade. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de EventHandlersActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65069).|  
|[EventHandlingScopeActivity](http://go.microsoft.com/fwlink?LinkID=65030)|Executa a atividade filho principal simultaneamente com uma [EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de EventHandlingScopeActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65070).|  
|[FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054)|Usado para manipular uma exceção de um tipo que você especificar. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de FaultHandlerActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65071).|  
|[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)|Representa uma atividade composta que tem uma lista ordenada de atividades filho do tipo [FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de FaultHandlersActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65072).|  
|[HandleExternalEventActivity](http://go.microsoft.com/fwlink?LinkID=65031)|Usado em conjunto com o [CallExternalMethodActivity](http://go.microsoft.com/fwlink?LinkID=65025) atividade para comunicações de entrada e saídas com um serviço local. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de HandleExternalEventActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65073).|  
|[IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)|Testa uma condição em cada ramificação e executa atividades no primeiro ramificação para o qual a condição é igual a **verdadeira**. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de IfElseActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65074).|  
|[IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)|Representa uma ramificação de uma [IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033). [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65075).|  
|[InvokeWebServiceActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65035)|Permite que seu fluxo de trabalho para chamar um serviço Web. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de InvokeWebServiceActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65076).|  
|[InvokeWorkflowActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65036)|Permite que seu fluxo de trabalho para chamar outro fluxo de trabalho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de InvokeWorkflowActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65077).|  
|[ListenActivity](http://go.microsoft.com/fwlink?LinkID=65037)|Uma atividade composta que contém apenas [EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029) atividades filho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de ListenActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65078).|  
|[ParallelActivity](http://go.microsoft.com/fwlink?LinkID=65038)|Fornece uma maneira de agendar dois ou mais filhos **SequenceActivity** ramificações da atividade para processamento ao mesmo tempo. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de ParallelActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65079).|  
|[PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)|Uso representar um conjunto de regras. Uma regra consiste em circunstâncias e em ações resultantes. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65004).|  
|[ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)|Cria várias instâncias de uma única atividade filho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65080).|  
|[SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020)|Fornece uma maneira simples de vincular várias juntos para atividades a execução sequencial. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de SequenceActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65081).|  
|[SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65041)|Especifica uma transição para um novo estado. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65082).|  
|[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)|Representa um estado em um fluxo de trabalho do computador de estado. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de StateActivity](http://go.microsoft.com/fwlink?LinkID=65083).|  
|[StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65043)|Usado em uma [StateActivity](http://go.microsoft.com/fwlink?LinkID=65042) atividade como um contêiner para as atividades filho que são executadas para deixar o **StateActivity** atividade. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65008).|  
|[StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65044)|Usado em uma [StateActivity](http://go.microsoft.com/fwlink?LinkID=65042) atividade como um contêiner para as atividades filho que são executadas ao inserir o **StateActivity** atividade. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65006).|  
|[Suspendactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65056)|Suspende a operação de seu fluxo de trabalho para ativar a intervenção no caso de alguma condição de erro que requer a atenção especial. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Suspendactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65084).|  
|[Synchronizationscopeactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65057)|Executa sequencialmente atividades contidas em um domínio sincronizado. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Synchronizationscopeactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65085).|  
|[Terminateactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65058)|Permite que você terminar imediatamente a operação de seu fluxo de trabalho no caso de uma condição de erro. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Terminateactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65086).|  
|[Throwactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65059)|Permite que você capturar exceções lançadas corporativos como parte de metadados do processo para um fluxo de trabalho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de Throwactivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65087).|  
|[TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65093)|Fornece uma estrutura para transações e manipulação de exceção. Para obter mais informações, consulte [usando a atividade de TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65088).|  
|[WebServiceFaultActivity](http://go.microsoft.com/fwlink?LinkID=65046)|Permite que você a modelagem a ocorrência de uma falha de serviço Web. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de WebServiceFaultActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65089).|  
|[WebServiceInputActivity](http://go.microsoft.com/fwlink?LinkID=65047)|Receber dados de um serviço Web. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de WebServiceInputActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65090).|  
|[WebServiceOutputActivity](http://go.microsoft.com/fwlink?LinkID=65048)|Responde a uma solicitação de serviço Web feita a um fluxo de trabalho. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de WebServiceOutputActivity&lt;1](http://go.microsoft.com/fwlink?LinkID=65092).|  
|[WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)|Permite que seu fluxo de trabalho para executar um loop até que uma condição seja satisfeita. [!INCLUDE[crdefault](../includes/crdefault-md.md)][Usando a atividade de WhileActivity](http://go.microsoft.com/fwlink?LinkID=65091).|  
  
 [!INCLUDE[crabout](../includes/crabout-md.md)] como criar atividades personalizadas, consulte [desenvolver atividades personalizadas](http://go.microsoft.com/fwlink?LinkID=65023) e [usando o Designer de atividade herdado](../workflow-designer/using-the-legacy-activity-designer.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exibições de atividade (herdado)](../workflow-designer/activity-views-legacy.md)  
 Descreve as diferentes exibições de design das atividades.  
  
 [Como adicionar atividades à caixa de ferramentas (herdado)](../workflow-designer/how-to-add-activities-to-the-toolbox-legacy.md)  
 Mostra como adicionar atividades a caixa de ferramentas.  
  
 [Como criar uma condição de regra declarativa (herdado)](../workflow-designer/how-to-create-a-declarative-rule-condition-legacy.md)  
 Mostra as etapas para criar uma condição declarativa de regra.  
  
 [Como criar um conjunto de regras de PolicyActivity (herdado)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)  
 Mostra as etapas para criar um conjunto de regras de PolicyActivity.  
  
 [Como implementar uma operação de contrato do Windows (herdado)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)  
 Mostra as etapas para implementar uma operação do contrato de [!INCLUDE[indigo2](../includes/indigo2-md.md)] .  
  
 [Como chamar uma operação de contrato do WCF (herdado)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)  
 Mostra as etapas para chamar uma operação do contrato de [!INCLUDE[indigo2](../includes/indigo2-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Atividades do Windows Workflow Foundation](http://go.microsoft.com/fwlink?LinkID=65005)   
 [Desenvolvendo fluxos de trabalho](http://go.microsoft.com/fwlink?LinkID=65010)   
 [Desenvolvimento de atividades de fluxo de trabalho](http://go.microsoft.com/fwlink?LinkID=65023)