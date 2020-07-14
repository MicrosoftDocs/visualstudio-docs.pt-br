---
title: 'Designer de Fluxo de Trabalho-como: usar o designer de variável'
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.DesignTimeVariable.UI
ms.assetid: 0318dfb0-bf8f-4f92-9b86-ae4c1b2161ad
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f02aab6c5ecf545e0f754f1a88fa7e26a88f206d
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817405"
---
# <a name="how-to-use-the-variable-designer"></a>Como: Use o designer variável

O designer variável é usado para criar variáveis para uso em cenários e em instruções condicionais de associação de dados. O designer é acessado clicando no botão **variáveis** no canto inferior esquerdo da tela de design. O designer contém uma lista de variáveis que aparecem em um formulário de tabela e podem ser classificadas por cada um dos cabeçalhos de coluna, exceto para a coluna **padrão** . Cada variável contém um nome, um tipo de variável, um escopo, e um valor padrão (se houver). O nome e o valor padrão são campos editáveis de texto, e o tipo e escopo são gota- suspensa. O escopo é a atividade que foi selecionada quando o designer variável foi chamado. Se uma variável não pode ser criado no escopo de seleção, então o escopo usará padrão a atividade a mais próxima de ancestral de seleção que permite variáveis criado em seu escopo. Para obter mais informações, consulte [Variables and Arguments (.net)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments).

 A ordem de classificação não é aplicado até que o usuário explicitamente use um dos controles de classificação, feche e reabra o designer variável, ou cria outra variável.

## <a name="to-create-a-new-variable"></a>Para criar uma nova variável

1. Abra uma solução de fluxo de trabalho ou atividade no Visual Studio.

2. Na tela de design, selecione uma atividade no fluxo de trabalho.

3. Abra o designer de variável clicando no botão **variáveis** no canto inferior esquerdo da tela de design. O designer variável aparece.

4. Clique na linha vazia rotulada **criar variável**. Isso adicionará uma nova linha com uma nova variável usando os seguintes valores padrão: VariableX para o **nome** em que x é um inteiro com um valor inicial de 1 que é incrementado automaticamente para criar nomes de variável exclusivos, **cadeia de caracteres** para o **tipo de variável**e **sequência** para o **escopo**. Nenhum valor é adicionado para o **padrão**. Você pode alterar esses valores a qualquer momento durante o processo de design de fluxo de trabalho.

    > [!NOTE]
    > Para excluir uma variável, selecione a variável clicando nela e pressione a tecla **delete** .

## <a name="see-also"></a>Veja também

- [Usando o Designer de Fluxo de Trabalho](developing-applications-with-the-workflow-designer.md)
- [Variáveis e argumentos](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
- [Como usar o designer de argumento](../workflow-designer/how-to-use-the-argument-designer.md)
