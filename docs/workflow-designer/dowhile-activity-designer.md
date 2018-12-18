---
title: Designer de fluxo de trabalho - Designer de atividade DoWhile
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 19817fb23bd8a22532df7d349262b689f632a3a7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839616"
---
# <a name="dowhile-activity-designer"></a>Designer de atividade DoWhile

O <xref:System.Activities.Statements.DoWhile> atividade executa a atividade contida em seu <xref:System.Activities.Statements.DoWhile.Body%2A> pelo menos uma vez, até que uma condição especificada for avaliada como **falso**. Se você precisar a atividade contida em um corpo de loop para ser executado zero ou mais vezes, use a atividade de <xref:System.Activities.Statements.While> em vez disso.

## <a name="dowhile-properties-in-the-workflow-designer"></a>Propriedades DoWhile em Designer de Fluxo de Trabalho

A tabela a seguir mostra os mais úteis <xref:System.Activities.Statements.DoWhile> propriedades da atividade e descreve como usá-los no designer:

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|False|A atividade a executar quando a condição for **verdadeira**. Para adicionar o <xref:System.Activities.Statements.DoWhile.Body%2A> atividade, soltar uma atividade na caixa de ferramentas para o **corpo** caixa no **DoWhile** designer de atividade com o texto de dica "Descartar atividade aqui".|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|verdadeiro|A condição a ser avaliada após cada iteração do loop. Para definir a <xref:System.Activities.Statements.DoWhile.Condition%2A>, digite uma expressão do Visual Basic na **condição** caixa no **DoWhile** atividade designer ou na grade de propriedade.|

## <a name="see-also"></a>Consulte também

- [While](../workflow-designer/while-activity-designer.md)
- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)