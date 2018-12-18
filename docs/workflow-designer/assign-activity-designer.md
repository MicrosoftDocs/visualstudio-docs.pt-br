---
title: Designer de fluxo de trabalho - Designer de atividade Atribuir
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 600f38d7bcd387915ba61fc148805705e8609431
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49905241"
---
# <a name="assign-activity-designer"></a>Atribua o designer de atividades

O **atribua** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Assign> atividade.

## <a name="the-assign-activity"></a>A atividade atribuir

A atividade de <xref:System.Activities.Statements.Assign> atribui um valor a uma variável ou um argumento.

### <a name="using-the-assign-activity-designer"></a>Usando o designer de atividade atribuir

O **atribuir** designer de atividade pode ser encontrado na **primitivos** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia (como alternativa, selecione **caixa de ferramentas** do **exibição** menu ou CTRL + ALT + X.)

O **atribua** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas, como em um <xref:System.Activities.Statements.Sequence>. Descartando o **atribua** designer de atividade cria uma <xref:System.Activities.Statements.Assign> atividade com um padrão **DisplayName** de Assign. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **atribuir** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-assign-properties"></a>As propriedades atribuir

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Assign> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns deles podem ser editados na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Assign> . O padrão é atribui. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.Assign.To%2A>|verdadeiro|A variável ou o argumento para que <xref:System.Activities.Statements.Assign.Value%2A> é atribuído. O valor deve ser um identificador válido Visual Basic. Para definir a propriedade, digite uma expressão do Visual Basic na **para** caixa sobre o **atribuir** atividade designer ou na grade de propriedade.|
|<xref:System.Activities.Statements.Assign.Value%2A>|verdadeiro|O valor que é atribuído à variável. Para definir a <xref:System.Activities.Statements.Assign.Value%2A>, digite uma expressão do Visual Basic na **valor** caixa no **atribuir** atividade designer ou na grade de propriedade.|

## <a name="see-also"></a>Consulte também

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Atrasar](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)