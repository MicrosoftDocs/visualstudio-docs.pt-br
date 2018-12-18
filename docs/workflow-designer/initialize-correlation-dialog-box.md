---
title: Designer de fluxo de trabalho - caixa de diálogo correlação inicializar
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: edfdef1c1f946e2c5f677d0ff1578a40ea7bcd8f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906228"
---
# <a name="initialize-correlation-dialog-box"></a>Inicializar a caixa de diálogo correlação

O **inicializar correlação** caixa de diálogo é usada no Designer de fluxo de trabalho para editar o <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> propriedade de um <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade. Para obter mais informações, consulte [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md).

A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **inicializar correlação** caixa de diálogo:

|Elemento da Interface do Usuário|Descrição|
|-|-----------------|
|**Correlação**|<xref:System.ServiceModel.Activities.CorrelationHandle> de correlação para inicializar.|
|**Inicializar em**|Um par chave/valor que contém os dados para inicializar. Esse valor corresponde à <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> propriedade. Um exemplo de um par chave/valor válido é uma chave chamada "OrderID" emparelhado com uma variável chamada OrderID.|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>Para iniciar a caixa de diálogo correlação inicializar

Clique em **exibição** sobre o **InitializeCorrelation** atividade designer ou selecione um <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade no Designer de fluxo de trabalho. Em seguida, clique no botão de reticências ao lado de <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> propriedade na grade de propriedade.

## <a name="see-also"></a>Consulte também

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)