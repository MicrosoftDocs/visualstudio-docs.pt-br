---
title: Designer de fluxo de trabalho - Designer de atividade Pick
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5bd37c78567ea11d53899bcbaefb2e3809a00057
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49826005"
---
# <a name="pick-activity-designer"></a>Escolha o designer de atividades

A atividade de <xref:System.Activities.Statements.Pick> fornece o fluxo de controle baseado. A atividade executa um dos vários ramificações em resposta a um evento disparando.

## <a name="the-pick-activity"></a>A atividade de picareta

Uma atividade de <xref:System.Activities.Statements.Pick> contém uma coleção de objetos <xref:System.Activities.Statements.PickBranch> , uma que a atividade de <xref:System.Activities.Statements.Pick> pode executar devido a qualquer evento de entrada que serve como um disparador. Dessa forma o Designer de fluxo de trabalho fornece a modelagem de fluxo de controle baseado em evento. Cada <xref:System.Activities.Statements.PickBranch> contém <xref:System.Activities.Statements.PickBranch.Trigger%2A> e <xref:System.Activities.Statements.PickBranch.Action%2A>. No início de uma <xref:System.Activities.Statements.Pick> execução da atividade, todas as atividades de gatilho a <xref:System.Activities.Statements.PickBranch> elementos estão agendados. Quando a primeira atividade concluir, a atividade correspondente de ação está agendada, e quaisquer atividades restantes do disparador serão canceladas.

### <a name="how-to-use-the-pick-activity-designer"></a>Como usar o designer de atividade de picareta

Acesso a **escolher** designer de atividade na **fluxo de controle** categoria dos **caixa de ferramentas**. O **escolher** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que os designers de atividade são colocados normalmente, por exemplo, dentro de um  **Sequência** designer de atividade. Depois de soltá-la no Designer de fluxo de trabalho, ele cria um <xref:System.Activities.Statements.Pick> atividade, que, por padrão, contém dois vazio <xref:System.Activities.Statements.PickBranch> atividades como elementos com nomes para exibição de Branch1 e de Branch2. Esses respectivos <xref:System.Activities.Statements.PickBranch.DisplayName%2A> valores de propriedade podem ser editados na **PickBranch** cabeçalho do designer de atividade ou dentro de **propriedades** janela para cada ramificação.

Há duas maneiras de adicionar <xref:System.Activities.Statements.PickBranch> atividades para a coleção de um <xref:System.Activities.Statements.Pick> objeto: arrastando e soltando o **PickBranch** designer dos **caixa de ferramentas** ou usando o menu de contexto do dentro de **escolher** superfície de design. Para obter detalhes, consulte o [PickBranch](../workflow-designer/pickbranch-activity-designer.md) tópico. Observe que o único item que pode ser colocado dentro de um **escolher** designer de atividade é um **PickBranch** designer de atividade.

### <a name="pick-activity-properties-in-the-workflow-designer"></a>Escolha propriedades de atividade em Designer de Fluxo de Trabalho

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Pick> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável do designer de atividade de <xref:System.Activities.Statements.Pick> no cabeçalho. O valor padrão é picareta. O valor pode ser editado na grade de propriedade ou diretamente no cabeçalho do designer de atividade.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|

## <a name="see-also"></a>Consulte também

- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)
- [Escolher atividade](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Usando a atividade de Pick](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)