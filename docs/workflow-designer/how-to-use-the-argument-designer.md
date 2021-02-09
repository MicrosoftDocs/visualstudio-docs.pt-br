---
title: 'Designer de Fluxo de Trabalho-como: usar o designer de argumentos'
description: Saiba mais sobre o designer de argumentos e como usar o designer de argumentos para permitir que os dados fluam para dentro e fora de uma atividade.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ArgumentDesigner.UI
- System.Activities.Presentation.View.DesignTimeArgument.UI
ms.assetid: 64813fd5-1ea1-499a-98b4-ab2a44b7ee5e
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9b97368a942747046aa7641771f84a9f2ed41e11
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894095"
---
# <a name="how-to-use-the-argument-designer"></a>Como: Use o designer do argumento

O designer de argumentos facilita a permissão de fluxo de dados para dentro e fora de uma atividade. Acesse o Designer clicando no botão **argumentos** no canto inferior esquerdo da tela de design. O designer contém uma lista de argumentos que aparecem em um formulário de tabela e podem ser classificados por cada um dos cabeçalhos de coluna, exceto para a coluna **valor padrão** . Cada argumento contiver um nome, a direção de in/out/in-out/property, o tipo, e o valor padrão de expressão (se houver). O nome e o valor padrão de expressão são campos editáveis de texto, e o tipo e direção são gota- suspensa. Para obter mais informações, consulte [Variables and Arguments (.net)](/dotnet/framework/windows-workflow-foundation/variables-and-arguments).

## <a name="to-create-a-new-argument"></a>Para criar um novo argumento

1. Abra uma solução de fluxo de trabalho ou atividade no Visual Studio.

2. Abra o designer de argumentos clicando no botão **argumentos** no canto inferior esquerdo da tela de design. O designer dos argumentos aparece.

3. Clique na linha vazia rotulada **criar argumento**. Isso adicionará uma nova linha com um novo argumento usando os seguintes valores padrão: argumentx para o **nome** em que x é um inteiro com um valor inicial de 1 que é incrementado automaticamente para criar nomes de argumentos exclusivos, **em** para a **direção** e **cadeia de caracteres** para o tipo de **argumento**. Nenhum valor é adicionado para o **valor padrão**. Você pode alterar esses valores a qualquer momento durante o processo de design de fluxo de trabalho.

    > [!NOTE]
    > Para excluir um argumento, selecione o argumento clicando nele e pressione a tecla **delete** .

## <a name="see-also"></a>Confira também

- [Usando o Designer de Fluxo de Trabalho](developing-applications-with-the-workflow-designer.md)
- [Variáveis e argumentos](/dotnet/framework/windows-workflow-foundation/variables-and-arguments)
