---
title: Designer de atividade de FinalState | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: aa186893-8775-40dd-981f-8593ead831d0
caps.latest.revision: 5
author: steved0x
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 48c44dc585ce1c9cf4e7b29970b4014f128b873d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49209164"
---
# <a name="finalstate-activity-designer"></a>Designer de atividade de FinalState
O designer de <xref:System.Activities.Core.Presentation.FinalState> é usado para criar <xref:System.Activities.Statements.State> que termina uma instância do computador de estado.  
  
## <a name="using-the-finalstate-activity-designer"></a>Usando o designer de atividade de FinalState  
 O **FinalState** designer é usado para criar um <xref:System.Activities.Statements.State> que é pré-configurado como um estado de terminação em um computador de estado. Um <xref:System.Activities.Statements.State> que é criado usando o <xref:System.Activities.Core.Presentation.FinalState> designer de atividade tem seu <xref:System.Activities.Statements.State.IsFinal%2A> propriedade definida como **verdadeira**, não tem nenhum <xref:System.Activities.Statements.State.Exit%2A> atividade e nenhuma transição que originam a ele. Para usar o <xref:System.Activities.Core.Presentation.FinalState> designer de atividade para adicionar uma <xref:System.Activities.Statements.State> atividade que é pré-configurado como um estado de terminação em um computador de estado, arraste o **FinalState** designer de atividade do **máquina de estado**seção o **caixa de ferramentas** e solte-o para o designer de fluxo de trabalho. O designer de atividade de <xref:System.Activities.Core.Presentation.FinalState> pode ser solto em <xref:System.Activities.Statements.StateMachine> e as transições adicionados posteriormente; ou uma transição pode ser criada como o designer de atividade de <xref:System.Activities.Core.Presentation.FinalState> é descartada. Para obter mais informações sobre como criar transições, consulte [transição](../workflow-designer/transition-activity-designer.md).  
  
### <a name="state-activity-properties-in-the-workflow-designer"></a>Propriedades de atividade do estado em Designer de Fluxo de Trabalho  
 A tabela a seguir mostra as propriedades que podem ser definidas usando o designer de <xref:System.Activities.Core.Presentation.FinalState> e descreve como elas são usadas no designer. Algumas dessas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície de designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.State.DisplayName%2A>|False|Especifica o nome amigável do designer de atividade de <xref:System.Activities.Statements.State> no cabeçalho. O valor padrão é **estado**. O valor pode ser editado na grade de propriedade ou diretamente no cabeçalho do designer de atividade. <xref:System.Activities.Statements.State.DisplayName%2A> é usado em navegação de rastreamento que é exibida na parte superior do designer de fluxo de trabalho.<br /><br /> Embora não seja necessário <xref:System.Activities.Statements.State.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.State.Entry%2A>|False|Especifica a ação que ocorre quando esse estado é feito a transição para. Esse valor pode ser definido arrastar uma atividade do **caixa de ferramentas** e soltando-os ao <xref:System.Activities.Statements.State.Entry%2A> seção do estado.|  
  
## <a name="see-also"></a>Consulte também  
 [StateMachine](../workflow-designer/statemachine-activity-designer.md)   
 [Estado](../workflow-designer/state-activity-designer.md)   
 [Transição](../workflow-designer/transition-activity-designer.md)