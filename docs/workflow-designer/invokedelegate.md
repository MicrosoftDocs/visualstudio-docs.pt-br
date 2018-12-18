---
title: Designer de fluxo de trabalho - InvokeDelegate
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 1e1f91b88d686f3e9a6ddee9573824eb4191e2bf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49927925"
---
# <a name="invokedelegate"></a>InvokeDelegate

O **InvokeDelegate** designer é usado para criar e configurar um <xref:System.Activities.Statements.InvokeDelegate> atividade.

## <a name="the-invokedelegate-activity"></a>A atividade de InvokeDelegate

<xref:System.Activities.Statements.InvokeDelegate> chama um delegate público.

### <a name="use-the-invokedelegate-activity-designer"></a>Use o Designer de atividade de InvokeDelegate

Acesso a **InvokeDelegate** designer de atividade na **primitivos** categoria dos **caixa de ferramentas**. O **InvokeDelegate** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Soltar o designer de atividade cria uma <xref:System.Activities.Statements.InvokeDelegate> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de InvokeDelegate. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **InvokeDelegate** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-invokedelegate-properties"></a>As propriedades de InvokeDelegate

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.InvokeDelegate> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.InvokeDelegate> . O valor padrão é InvokeDelegate.<br /><br /> Embora o <xref:System.Activities.Activity.DisplayName%2A> não é estritamente necessária, é melhor usar um.|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|verdadeiro|O nome de <xref:System.Activities.ActivityDelegate> a ser chamado quando a atividade executar. Essa propriedade pode ser editada na superfície do designer e é obrigatória.|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|A coleção de argumento de representante chamado. As chaves são os nomes dos objetos de parâmetro no <xref:System.Activities.ActivityDelegate>, e os valores são os argumentos cujas expressões são avaliadas e atribuídas a objetos de parâmetro correspondente. Para exibir o **DelegateArguments** caixa de diálogo onde é possível definir essa propriedade, clique no botão de reticências na **DelegateArguments** campo da grade de propriedade. Clique o **criar argumento** campo para adicionar os argumentos.|

## <a name="see-also"></a>Consulte também

- [Como definir e consumir delegados de atividade no Designer de Fluxo de Trabalho](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)