---
title: 'Designer de fluxo de trabalho - como: adicionar um novo Item a um projeto de fluxo de trabalho'
ms.date: 06/25/2018
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dbed404f2cdd69446d8945fc9ff96703eccd161f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49814216"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>Como: adicionar um novo item a um projeto de fluxo de trabalho

Depois de criar um projeto de fluxo de trabalho, você pode adicionar atividades de fluxo de trabalho, designers e outros itens do Visual Studio familiares ao seu projeto.

A tabela a seguir lista os itens do Windows Workflow Foundation (WF) que você pode adicionar a um projeto de fluxo de trabalho:


| Nome | Descrição |
|-| - |
| Atividade | Uma atividade a ser composta de outras atividades. Selecionando o item adiciona o mesmo arquivo XAML ao projeto como você obteria quando selecionando o **biblioteca de atividades** modelo para um novo projeto. Para obter mais informações sobre esse procedimento, consulte [como: criar uma biblioteca de atividade](../workflow-designer/how-to-create-an-activity-library.md). |
| Designer de Activity | Um designer para personalizar a experiência em tempo de design de uma atividade. Selecionando o item adiciona os mesmos arquivos para o projeto como você obteria quando selecionando o **biblioteca do Designer de atividade** modelo para um novo projeto. Para obter mais informações sobre esse procedimento, consulte [como: criar uma biblioteca do Designer de atividade](../workflow-designer/how-to-create-an-activity-designer-library.md). |
| Atividade do código | Uma atividade com a lógica de execução gravar no código. Um arquivo de código-fonte com uma substituição do método de <xref:System.Activities.CodeActivity.Execute%2A> é gerado para você. |
| WCF Serviço de Fluxo de Trabalho | Um serviço de [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] compilado usando atividades de fluxo de trabalho. Selecionando o item adiciona os mesmos arquivos para o projeto como você obteria quando selecionando o **aplicativo de serviço de fluxo de trabalho WCF** modelo para um novo projeto. Para obter mais informações sobre esse procedimento, consulte [como: criar um aplicativo de serviço de fluxo de trabalho WCF](../workflow-designer/how-to-create-a-wcf-workflow-service-application.md). |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>Para adicionar um novo item em um fluxo de trabalho projeto

1. Sobre o **Project** menu, selecione **Adicionar Novo Item**.

   A caixa de diálogo **Adicionar Novo Item** é aberta.

1. No painel esquerdo, selecione a **fluxo de trabalho** categoria e, em seguida, selecione um modelo de item de fluxo de trabalho.

   > [!NOTE]
   > Se você não vir as **fluxo de trabalho** categoria, primeiro instale o **Windows Workflow Foundation** componente do Visual Studio 2017. Para obter instruções detalhadas, consulte [instalar o Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation).

1. Insira um nome para o item na **nome** caixa na parte inferior da caixa de diálogo.

1. Selecione **adicionar** para adicionar o item ao projeto.

## <a name="see-also"></a>Consulte também

- [Criar um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)