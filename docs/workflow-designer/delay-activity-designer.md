---
title: Designer de fluxo de trabalho - Designer de atividade de atraso
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0bce0be0f6c7953c44601edd090b1e1e7d3b6f6a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832974"
---
# <a name="delay-activity-designer"></a>Atrasar o designer de atividades

O **atraso** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Delay> atividade.

## <a name="the-delay-activity"></a>A atividade do atraso

A atividade de <xref:System.Activities.Statements.Delay> atrasa a execução de um fluxo de trabalho para uma quantidade de tempo especificada.

### <a name="use-the-delay-activity-designer"></a>Use o Designer de atividade de atraso

O **atraso** designer de atividade pode ser encontrado na **primitivos** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia do Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O **atraso** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Soltar o designer de atividade cria uma <xref:System.Activities.Statements.Delay> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de atraso. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **atraso** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-delay-properties"></a>As propriedades de atraso

A tabela a seguir mostra o <xref:System.Activities.Statements.Delay> propriedades e descreve como eles são usados no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns deles podem ser editados na superfície de Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Delay> . O padrão é atraso. Embora o <xref:System.Activities.Activity.DisplayName%2A> valor não é estritamente necessário, ele é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.Delay.Duration%2A>|verdadeiro|A quantidade de tempo para atrasar o fluxo de trabalho. Essa propriedade é definida na grade de propriedade. Digite qualquer um <xref:System.TimeSpan> literal no 00:00 de formato: 00 ou uma expressão do Visual Basic para especificar a quantidade de tempo.|

## <a name="see-also"></a>Consulte também

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Atribuir](../workflow-designer/assign-activity-designer.md)
- [Designer de atividade Delay](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)