---
title: 'Designer de Fluxo de Trabalho: Depurar XAML'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 9be7c8da251a9698e0fceba64e3941ba8fbdf803
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817509"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>Como: Depuração XAML com designers de Fluxo de Trabalho

Fluxos de trabalho são definidos em termos de XAML. A representação de interface de usuário de fluxo de trabalho é construída sobre a árvore XAML que define o fluxo de trabalho. A experiência de depuração é semelhante à depuração de fluxos de trabalho no Designer de Fluxo de Trabalho. Por exemplo, durante a depuração de XAML, as janelas locais, inspecionar e threads funcionam da mesma maneira que no Designer de Fluxo de Trabalho a depuração. Além disso, a exibição da pilha de chamadas durante a depuração XAML é uma exibição hierárquica linha com base de fluxo de execução do fluxo de trabalho.

> [!NOTE]
> Se o XAML para um fluxo de trabalho está localizado no mesmo assembly que as atividades, a parte do assembly de nomes de classe não é incluído. Sem essa parte dos nomes de classe (atividade), o XAML não pode ser carregado em tempo de execução. Não é recomendável definir atividades no mesmo namespace que o projeto pai; caso contrário, o XAML deverá mão- ser editado após ser editado no designer.

## <a name="to-debug-workflow-xaml"></a>Para depurar o fluxo de trabalho XAML

1. Abra um projeto de fluxo de trabalho ou atividade no Visual Studio.

2. Defina um ponto de interrupção na atividade ou nas atividades que você deseja depurar conforme descrito em [como definir pontos de interrupção em fluxos de trabalho](../workflow-designer/how-to-set-breakpoints-in-workflows.md).

3. Clique com o botão direito do mouse no arquivo. XAML que contém sua definição de fluxo de trabalho e selecione **Exibir código**. Você verá um ponto de interrupção exibido na mesma linha da declaração de elemento XAML de atividade que você definir o ponto de interrupção sobre no modo design.

4. Invoque o depurador conforme descrito em [depurar fluxos de trabalho](debugging-workflows-with-the-workflow-designer.md).

5. Quando a execução de código atinge um de seus pontos de interrupção, o elemento XAML associado com esse ponto de interrupção será realçado. Para mover para o próximo ponto de interrupção, use a tecla **F10** ou **F11** .

## <a name="see-also"></a>Veja também

- [Como definir pontos de interrupção em fluxos de trabalho](../workflow-designer/how-to-set-breakpoints-in-workflows.md)
- [Depurar fluxos de trabalho](debugging-workflows-with-the-workflow-designer.md)
