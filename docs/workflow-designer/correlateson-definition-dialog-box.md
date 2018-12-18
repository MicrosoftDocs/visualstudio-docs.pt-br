---
title: Designer de fluxo de trabalho - caixa de diálogo de definição de CorrelatesOn
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3cfd9d43a8152b629635103b399ef0d7566e4867
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933112"
---
# <a name="correlateson-definition-dialog-box"></a>Caixa de diálogo definição de CorrelatesOn

O **CorrelatesOn** caixa de diálogo é usada no Designer de fluxo de trabalho para editar o <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> propriedade de um <xref:System.ServiceModel.Activities.Receive> atividade. Para obter mais informações, consulte [Designer de atividade receber](../workflow-designer/receive-activity-designer.md).

Correlação entre atividades de <xref:System.ServiceModel.Activities.Receive> especifica como as operações de serviço diferentes conectam entre si em um fluxo de trabalho.

A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **CorrelatesOn** caixa de diálogo.

|Elemento da Interface do Usuário|Descrição|
|-|-----------------|
|**CorrelatesWith**|<xref:System.ServiceModel.Activities.CorrelationHandle> que é usado para rotear a mensagem à instância apropriado de fluxo de trabalho.|
|**Consultas XPath**|Um par chave/valor que contém as consultas usadas para extrair dados de correlação das mensagens de entrada. Esse valor corresponde à <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> propriedade. Consultas XPath estão contidas em um objeto de <xref:System.ServiceModel.MessageQuerySet> .|

## <a name="to-launch-the-correlateson-dialog-box"></a>Para iniciar a caixa de diálogo CorrelatesOn

O **Receive** designer de atividade pode ser arrastado de **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho, onde quer que as atividades são colocadas em geral. Soltar o designer de atividade cria uma <xref:System.ServiceModel.Activities.Receive> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de recebimento. Para abrir o **definição de CorrelatesOn** caixa de diálogo, selecione o **Receive** atividade do designer e, em seguida, na grade de propriedades, selecione o botão de reticências ao lado do texto coleção de  **CorrelatesOn** propriedade.

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Activities.Receive>
- [Caixa de diálogo Adicionar CorrelationInitializers](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [Adicionar caixa de diálogo correlação](http://msdn.microsoft.com/en-us/9e41a149-e8ab-41b1-8886-ea06a63041b6)
- [Caixa de diálogo Inicializar Correlação](../workflow-designer/initialize-correlation-dialog-box.md)