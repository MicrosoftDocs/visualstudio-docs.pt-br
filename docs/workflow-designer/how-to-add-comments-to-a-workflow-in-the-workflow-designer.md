---
title: 'Designer de fluxo de trabalho - como: adicionar comentários a um fluxo de trabalho'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 43b17390f077238a6874784f186eb8add3819f6d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883285"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>Como: Adicionar comentários a um fluxo de trabalho em Designer de Fluxo de Trabalho

Para facilitar a criação de fluxos de trabalho maiores, mais complicados, o .NET Framework 4.5 permite que o desenvolvedor adiciona anotações aos seguintes tipos de item no designer:

-   <xref:System.Activities.Activity>

-   <xref:System.Activities.Statements.State>

-   <xref:System.Activities.Statements.Transition>

-   Classes derivadas de <xref:System.Activities.Statements.FlowNode>

-   <xref:System.Activities.Variable>

-   <xref:System.Activities.Argument>

> [!IMPORTANT]
> O conteúdo de uma anotação são salvos como texto sem formatação ao arquivo XAML associado com o fluxo de trabalho, e podem potencialmente ser lidas por outro. Seja cuidadoso ao inserir informações sigilosas em uma anotação.

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>Adicionando uma anotação a uma atividade no designer

1. No designer de fluxo de trabalho, clique com botão direito em um item no designer e selecione o fluxo de trabalho **anotações**, **Adicionar anotação**.

1. Adicione o texto de anotação no espaço fornecido.

   O item mostrará um ícone de anotação. Passar o mouse sobre o ícone de anotação exibirá o texto da anotação.

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>Exibindo uma anotação no designer de uma atividade

1. Com um designer de atividade que tem uma anotação que exibe fora da atividade, clique o **Pin** ícone no adorno de anotação.

   A anotação é exibida no designer de atividade. Em captura de tela abaixo, a anotação “que inicia a atividade no fluxo de trabalho” é exibida no designer de atividade.

   ![Anotação mostrada no designer de atividade](../workflow-designer/media/annotationindesigner.png)

2. Para exibir a anotação fora do designer de atividade, passe o mouse sobre a área de anotação no designer de atividade e clique no **Desafixar** ícone

   ![Anotação exibida fora do designer de uma atividade](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>Mostrar ou ocultar todas as anotações

1. Clique com o botão direito do mouse uma atividade que tenha uma anotação. Selecione **anotações**, **Mostrar todas as anotações**.

   Todas as anotações são exibidas no designer de atividade.

1. Para exibir todas as anotações fora do Designer de atividade, clique com botão direito na atividade e selecione **anotações**, **ocultar todas as anotações**.

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>Editando ou excluindo uma anotação para uma atividade

1. Clique com o botão direito do mouse em uma atividade que tenha uma anotação.

1. Selecione **anotações**, **editar anotação** ou **excluir anotação**.

   A anotação é aberta para edição ou excluída.

1. Para excluir todas as anotações ao mesmo tempo, clique com botão direito do fluxo de trabalho no designer e selecione **anotação**, **excluir todas as anotações**.

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>Adicionando, editar, e excluir uma anotação para uma variável ou um argumento

1. Clique com o botão direito do mouse em uma variável ou o argumento e selecione adicionar a anotação.

1. Digite o texto de anotação. A variável ou argumento exibe um ícone de anotação.

1. Clique com o botão direito do mouse em uma variável ou em um argumento que tenha uma anotação. Selecione a anotação de edição.

   A anotação é aberta para edição.

1. Clique com o botão direito do mouse em uma variável ou em um argumento que tenha uma anotação. Selecione a anotação excluir.

   A anotação será excluída.