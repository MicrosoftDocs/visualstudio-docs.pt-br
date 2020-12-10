---
title: Definir pontos de interrupção em fluxos de trabalho
description: Saiba como usar o Designer de Fluxo de Trabalho para definir pontos de interrupção em seus fluxos de trabalho gráficos como você faria no código Visual Basic ou C#.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 88516a4160c5236a5a4ef9f01d7f15620aee5cc3
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993296"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>Como definir pontos de interrupção em fluxos de trabalho

Ao usar Designer de Fluxo de Trabalho, você pode definir pontos de interrupção em seus fluxos de trabalho gráficos como faria no código Visual Basic ou C#. Como esperado, a execução de fluxo de trabalho que ele pare em cada ponto de interrupção esse definido.

Um ponto de interrupção tem três Estados: *pendente*, *associado* e *erro*. Quando você definir um ponto de interrupção, ele está pendente, e ele é representado por um ícone vermelho contínuo. Quando o runtime carregado o tipo de fluxo de trabalho, transformações limite. Se você especificar um formato incorreto do ponto de interrupção, como um nome de atividade que não é válida, uma janela de erro aparece. O ponto de interrupção é adicionado ainda para a janela de ponto de interrupção, mas é marcado com um pequeno “x”.

> [!NOTE]
> Os pontos de interrupção em fluxos de trabalho chamados não são suportados.

> [!NOTE]
> Certifique-se de selecionar a opção **habilitar apenas meu código (somente gerenciado)** no   >  menu de depuração **Opções** de ferramentas  >   antes de depurar. Se a opção não estiver selecionada e você tiver duas sequências aninhadas em outra sequência, e definir um ponto de interrupção na primeira sequência interna, pressionar **F11** não será depurado na segunda sequência interna.

> [!NOTE]
> Os pontos de interrupção em um fluxo de trabalho não serão atingidos se o caminho completo para a propriedade do arquivo XAML não for preciso. O caminho completo para o arquivo XAML não é preciso depois de mover o projeto ou a solução para outra pasta ou para outra máquina. Selecione **Ctrl** + **S** para salvar e atualizar a propriedade caminho completo.

## <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>Para definir um ponto de interrupção em uma atividade no modo design

1. Selecione a atividade que você deseja que o depurador para interromper novamente.

2. No menu **depurar** , selecione **alternar ponto de interrupção**. Um ícone vermelho aparecerá na borda superior esquerda da atividade.

   Como alternativa, você pode pressionar **F9** depois de selecionar a atividade, ou clicar com o botão direito do mouse na atividade **e selecionar ponto**  >  de interrupção de **inserção** de ponto de quebra no menu de atalho.

## <a name="see-also"></a>Confira também

- [Fluxos de trabalho de depuração com designers de Fluxo de Trabalho](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)
- [Como: Depuração XAML com designers de Fluxo de Trabalho](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)
