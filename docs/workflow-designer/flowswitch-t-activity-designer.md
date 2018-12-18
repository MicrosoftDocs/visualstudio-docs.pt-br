---
title: Designer de fluxo de trabalho - FlowSwitch<T> Designer de atividade
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 783f3101f567f5fe45a1de24a8dad866ea619a39
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49848120"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T > Designer de atividade

A atividade de <xref:System.Activities.Statements.FlowSwitch%601> é um nó condicional que fornece a ramificação para o fluxo de controle baseado no critério de correspondência quando mais de duas ramificações alternativas são necessários. Se a ramificação de fluxo requer apenas dois caminhos, use a atividade de <xref:System.Activities.Statements.FlowDecision> em vez disso.

## <a name="the-flowswitcht-activity"></a>O FlowSwitch\<T > atividade

O <xref:System.Activities.Statements.FlowSwitch%601> atividade contém uma <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> que retorna um valor do tipo *T* (especificada pelo parâmetro genérico) quando avaliada. A atividade também contém um conjunto de <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>, que especifica um mapeamento exclusivo de resultados possíveis da avaliação a um conjunto de objetos de <xref:System.Activities.Statements.FlowNode> . O <xref:System.Activities.Statements.FlowNode> executada é aquele cujo objeto do tipo *T* corresponde ao valor do avaliado <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>. Os exemplos de <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> podem opcionalmente () são fornecidos para casos em que nenhuma correspondência for obtida.

### <a name="using-the-flowswitcht-activity-designer"></a>Usando o FlowSwitch\<T > Designer de atividade

O **FlowSwitch\<T >** designer de atividade pode ser encontrado no **fluxograma** categoria do **caixa de ferramentas**, que é acessado clicando-se a **Caixa de ferramentas** guia no lado esquerdo do Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O **FlowSwitch\<T >** designer de atividade pode ser arrastado dos **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho dentro de um **fluxograma** designer de atividade. Use o **selecionar tipos** janela que exibe para especificar o tipo (associado no código com o <xref:System.Activities.Statements.FlowSwitch%601> pelo parâmetro genérico) obtido de avaliar o <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>. Este procedimento cria um <xref:System.Activities.Statements.FlowSwitch%601> atividade rotulada **Switch** dentro de <xref:System.Activities.Statements.Flowchart> atividade. O <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> podem ser digitados em de **expressão** caixa da **propriedades** janela clicando em que o texto de dica que informa "Digite uma expressão de VB".

Passe o mouse sobre o **FlowSwitch\<T >** designer de atividade para fazer com que o quadrado que é usado para o link <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> para aparecer em torno de suas bordas. Após arrastar o **FlowSwitch < T\>**  designer de atividade e outros designers de atividade no **fluxograma**, o <xref:System.Activities.Activity> objetos que representam estão prontos para ser vinculadas entre si para especificar a ordem de execução. Para criar um dos <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> associado com o <xref:System.Activities.Statements.FlowSwitch%601>, clique em uma das alças de quadradas dos casos no perímetro da **FlowSwitch < T\>**  e arraste-a (segurando o botão do mouse) para uma das alças de que aparece de maneira semelhante ao redor de atividade de destino quando o mouse passa sobre o designer. Solte o botão do mouse e uma seta do **FlowSwitch < T\>**  para o designer de destino aparece representação desses casos. O valor padrão para exibe desses casos na seta e ele pode ser editado na **caso** caixa da **propriedades** janela.

### <a name="the-flowswitcht-properties"></a>O FlowSwitch\<T > Propriedades

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.FlowSwitch%601> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|verdadeiro|Especifica a expressão que é avaliada para determinar qual de <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> para alternar o caminho execução.|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|False|Especifica um mapeamento exclusivo de resultados possíveis obtidos de avaliar <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> a um conjunto de objetos de <xref:System.Activities.Statements.FlowNode> .|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|verdadeiro|Especificar o mapeamento quando a avaliação de <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> não coincide com um dos valores contidos no objeto de <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> .|

## <a name="see-also"></a>Consulte também

- [Fluxograma](../workflow-designer/flowchart-activity-designers.md)
- [Fluxograma](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)