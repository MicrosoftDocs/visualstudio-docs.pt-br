---
title: 'Designer de Fluxo de Trabalho: adicionar um novo item ao projeto de fluxo de trabalho'
ms.date: 06/25/2018
ms.topic: how-to
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 53737eb421f4194b00354899e373441ff0a97227
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814610"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>Como: adicionar um novo item a um projeto de fluxo de trabalho

Depois de criar um projeto de fluxo de trabalho, você pode adicionar atividades de fluxo de trabalho, designers e outros itens familiares do Visual Studio ao seu projeto.

A tabela a seguir lista os itens de Windows Workflow Foundation (WF) que você pode adicionar a um projeto de fluxo de trabalho:

| Name | Descrição |
|-| - |
| Atividade | Uma atividade a ser composta de outras atividades. A seleção deste item adiciona o mesmo arquivo XAML ao projeto, como você obteria ao selecionar o modelo de **biblioteca de atividades** para um novo projeto. Para obter mais informações sobre esse procedimento, consulte [criar um projeto de fluxo de trabalho](creating-a-workflow-project.md). |
| Designer de Activity | Um designer para personalizar a experiência em tempo de design de uma atividade. A seleção deste item adiciona os mesmos arquivos ao projeto, como você obteria ao selecionar o modelo de **biblioteca do designer de atividade** para um novo projeto. |
| Atividade do código | Uma atividade com a lógica de execução gravar no código. Um arquivo de código-fonte com uma substituição do método de <xref:System.Activities.CodeActivity.Execute%2A> é gerado para você. |
| WCF Serviço de Fluxo de Trabalho | Um serviço de [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] compilado usando atividades de fluxo de trabalho. A seleção deste item adiciona os mesmos arquivos ao projeto, como você obteria ao selecionar o modelo de **aplicativo do serviço de fluxo de trabalho WCF** para um novo projeto. Para obter mais informações sobre esse procedimento, consulte [como: criar um aplicativo de serviço de fluxo de trabalho WCF](creating-a-workflow-project.md). |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>Para adicionar um novo item em um fluxo de trabalho projeto

1. No menu **Projeto**, selecione **Adicionar novo item**.

   A caixa de diálogo **Adicionar Novo Item** é aberta.

1. No painel esquerdo, selecione a categoria fluxo de **trabalho** e, em seguida, selecione um modelo de item de fluxo de trabalho.

   > [!NOTE]
   > Se você não vir a categoria de **fluxo de trabalho** , primeiro instale o componente de **Windows Workflow Foundation** do Visual Studio. Para obter instruções detalhadas, consulte [instalar Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation).

1. Insira um nome para o item na caixa **nome** na parte inferior da caixa de diálogo.

1. Selecione **Adicionar** para adicionar o item ao projeto.

## <a name="see-also"></a>Veja também

- [Criar um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)
