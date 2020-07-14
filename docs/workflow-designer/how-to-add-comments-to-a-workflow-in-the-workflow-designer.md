---
title: 'Designer de Fluxo de Trabalho-como: adicionar comentários a um fluxo de trabalho'
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 77fb43671a45d5d53d2fe23fa3e4e7a9a98c4373
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815494"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>Como: Adicionar comentários a um fluxo de trabalho em Designer de Fluxo de Trabalho

Para facilitar a criação de fluxos de trabalho maiores e mais complicados, .NET Framework 4,5 permite que o desenvolvedor adicione anotações aos seguintes tipos de item no designer:

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- Classes derivadas de <xref:System.Activities.Statements.FlowNode>

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> O conteúdo de uma anotação são salvos como texto sem formatação ao arquivo XAML associado com o fluxo de trabalho, e podem potencialmente ser lidas por outro. Seja cuidadoso ao inserir informações sigilosas em uma anotação.

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>Adicionando uma anotação a uma atividade no designer

1. No designer de fluxo de trabalho, clique com o botão direito do mouse em um item no designer de fluxo de trabalho e selecione **anotações**, **Adicionar anotação**.

1. Adicione o texto de anotação no espaço fornecido.

   O item mostra um ícone de anotação. Passar o mouse sobre o ícone de anotação exibe o texto da anotação.

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>Exibindo uma anotação no designer de uma atividade

1. Com um designer de atividade que tem uma anotação exibindo fora da atividade, clique no ícone de **pino** no adorno de anotação.

   A anotação é exibida no designer da atividade. Em captura de tela abaixo, a anotação “que inicia a atividade no fluxo de trabalho” é exibida no designer de atividade.

   ![Anotação mostrada no designer de atividade](../workflow-designer/media/annotationindesigner.png)

2. Para exibir a anotação fora do designer da atividade, passe o mouse sobre a área de anotação no designer da atividade e clique no ícone **Desafixar**

   ![Anotação exibida fora do designer de uma atividade](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>Mostrar ou ocultar todas as anotações

1. Clique com o botão direito do mouse uma atividade que tenha uma anotação. Selecione **anotações**, **Mostrar todas as anotações**.

   Todas as anotações são exibidas nos designers da atividade.

1. Para exibir todas as anotações fora dos designers da atividade, clique com o botão direito do mouse na atividade e selecione **anotações**, **ocultar todas as anotações**.

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>Editando ou excluindo uma anotação para uma atividade

1. Clique com o botão direito do mouse em uma atividade que tenha uma anotação.

1. Selecione **anotações**, **Editar Anotação** ou **excluir anotação**.

   A anotação está aberta para edição ou exclusão.

1. Para excluir todas as anotações de uma vez, clique com o botão direito do mouse no designer de fluxo de trabalho e selecione **anotação**, **excluir todas as anotações**.

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>Adicionando, editar, e excluir uma anotação para uma variável ou um argumento

1. Clique com o botão direito do mouse em uma variável ou o argumento e selecione adicionar a anotação.

1. Digite o texto de anotação. A variável ou o argumento exibe um ícone de anotação.

1. Clique com o botão direito do mouse em uma variável ou em um argumento que tenha uma anotação. Selecione a anotação de edição.

   A anotação é aberta para edição.

1. Clique com o botão direito do mouse em uma variável ou em um argumento que tenha uma anotação. Selecione a anotação excluir.

   A anotação é excluída.
