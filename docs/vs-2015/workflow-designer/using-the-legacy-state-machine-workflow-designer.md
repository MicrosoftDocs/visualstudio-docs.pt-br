---
title: Usando o Designer de fluxo de trabalho de máquina de estado herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- StateFinalizationActivity activity
- StateActivity activity
- SetStateActivity activity
- EventDrivenActivity activity
- state machine workflow designer
- state machine workflows, designer
- state machine workflows, activities
- StateInitializationActivity activity
ms.assetid: 2cd21123-35c2-4eaf-82f6-86fce7a8f04d
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 30eaf026d0558538c51b4cbda313e051348a5120
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49231680"
---
# <a name="using-the-legacy-state-machine-workflow-designer"></a>Usando o computador de estado herdado Designer de Fluxo de Trabalho
Quando você estiver criando um novo projeto de fluxo de trabalho de máquina de estado no [!INCLUDE[vs2010](../includes/vs2010-md.md)] que tem como alvo o [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou o [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)], você pode optar por usar o **aplicativo de Console do fluxo de trabalho de máquina de estado** ou o  **Biblioteca de fluxo de trabalho de máquina de estado** modelo de projeto herdados. Se você escolher um desses modelos de projeto do computador de estado, o designer do computador de estado é apresentado como a interface do usuário herdado do designer de fluxo de trabalho. Para obter informações sobre os modelos de projeto de máquina de estado herdado, consulte [como: Criar estado de fluxo de trabalho de aplicativos de Console computador (herdado)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md) e [como: criar uma biblioteca de fluxo de trabalho de máquina de estado (herdado)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md).  
  
 Um fluxo de trabalho do computador de estado consiste em um conjunto de estados. Um estado denotado é como um estado inicial. Cada estado pode receber um determinado conjunto de eventos. Baseado em um evento, uma transição pode ser feita para outro estado. O fluxo de trabalho do computador de estado pode ter um estado final. Quando uma transição é feita ao estado final, o fluxo de trabalho completa.  
  
## <a name="state-machine-designer-views"></a>Modos de exibição do designer do computador de estado  
 O designer do computador de estado é um designer de forma livre, o que significa que as atividades podem ser movidos para o redor livremente na superfície de design. O designer de máquina de estado tem dois modos de exibição: *estado* exibição e *controlado por evento* modo de exibição.  
  
 Modo de estado mostra as atividades de estado e as atividades corretamente eventos que podem ser contidas dentro de uma atividade de estado. Nesta exibição, as transições de um estado para outro são representadas por linhas que estendem de atividade de baseada em um estado para outro estado. Você também pode criar transições desenhando a linha você mesmo. Para desenhar a transição, selecione a atividade de baseada e em seguida, selecione uma das alças da atividade e arraste-a. Esta ação desenha uma linha. Esta linha é anexada no estado de destino, indicando uma transição entre estados.  
  
 Para acessar a exibição orientada evento, clique duas vezes em uma atividade de baseada. O designer que aparece é bem como o designer sequencial de fluxo de trabalho. Na parte superior do designer, uma barra de navegação mostra a hierarquia de atividades até a atividade de baseada que é exibida. Você pode navegar de volta para o modo de estado clicando em qualquer elemento na hierarquia exibida. Se você desenhou uma transição de um estado para outro no modo de estado, e se você está exibindo a exibição orientada a eventos da atividade, uma atividade do estado é adicionada à atividade de baseada para você. Se você alterar as propriedades de atividade do estado, é passado refletida no modo de estado.  
  
## <a name="state-machine-workflow-activities"></a>Atividades de fluxo de trabalho do computador de estado  
 A tabela a seguir descreve as atividades principais que são usadas em um designer de fluxo de trabalho do computador de estado.  
  
|Nome da caixa de ferramentas|Atividade|Descrição|  
|------------------|--------------|-----------------|  
|**Estado**|[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)|Representa um estado em uma máquina de estado. pode conter adicionais **StateActivity** atividades. Para obter mais informações, consulte [usando a atividade de StateActivity](http://go.microsoft.com/fwlink?LinkID=65083).|  
|**SetState**|[SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65041)|Especifica uma transição para um novo estado. Para obter mais informações, consulte [usando a atividade de SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65082).|  
|**StateInitialization**|[StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65044)|Executa quando um estado estiver conectado; pode conter outras atividades. Para obter mais informações, consulte [usando a atividade de StateInitialization](http://go.microsoft.com/fwlink?LinkID=65006).|  
|**StateFinalization**|[StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65043)|Executes continha atividades deixando uma [StateActivity](http://go.microsoft.com/fwlink?LinkID=65042) atividade. Para obter mais informações, consulte [usando a atividade de StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65008).|  
|**EventDriven**|[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)|Usado para os estados que contam com um evento externa para iniciar executar. O **EventDrivenActivity** atividade deve ter uma atividade que implementa o [IEventActivity](http://go.microsoft.com/fwlink?LinkID=65032) interface como a primeira atividade filho. Para obter mais informações, consulte [usando a atividade de EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65068).|  
  
 O componente principal em um fluxo de trabalho de máquina de estado é o [StateActivity](http://go.microsoft.com/fwlink?LinkID=65042) atividade. Como os eventos são capturados em vários pontos em um fluxo de trabalho do computador de estado, os estados diferentes estão conectados para manipular as tarefas associadas com eventos. Durante o tempo de vida de fluxo de trabalho, o fluxo de trabalho pode sair e inserir vários estados diferentes. Esses estados conectam entre si usando o [SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65041) atividade.  
  
 Quando você arrasta uma nova **StateActivity** para a superfície de design de fluxo de trabalho, você pode adicionar [EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029), [StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65044), [ StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65043), ou adicionais **StateActivity** atividades como filhos.  
  
> [!CAUTION]
>  Quando você usa o designer de fluxo de trabalho de máquina de estado para criar fluxos de trabalho, você deve monitorar a estrutura do fluxo de trabalho que você está criando com o **Document Outline** janela modo de exibição. O modo de exibição da estrutura do fluxo de trabalho de máquina de estado de na **Document Outline** janela espelha o layout lógico de atividades no arquivo de marcação de fluxo de trabalho do modo de exibição. O layout físico das atividades de fluxo de trabalho como aparecem na superfície de design não pode espelhar o layout lógico de atividades no arquivo de marcação de fluxo de trabalho.  
>   
>  Para abrir o **Document Outline** janela diante a **exibição** , aponte para **Other Windows**e, em seguida, selecione **Document Outline**.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar aplicativos de Console de fluxo de trabalho de máquina de estado (herdado)](../workflow-designer/how-to-create-state-machine-workflow-console-applications-legacy.md)   
 [Como: criar uma biblioteca de fluxo de trabalho de máquina de estado (herdado)](../workflow-designer/how-to-create-a-state-machine-workflow-library-legacy.md)   
 [Fluxos de trabalho de máquina de estado](http://go.microsoft.com/fwlink?LinkID=65016)   
 [Usando a atividade de StateActivity](http://go.microsoft.com/fwlink?LinkID=65083)   
 [Usando a atividade de StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65006)   
 [Usando a atividade de StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65008)   
 [Usando a atividade de SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65082)   
 [Usando a atividade de EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65068)