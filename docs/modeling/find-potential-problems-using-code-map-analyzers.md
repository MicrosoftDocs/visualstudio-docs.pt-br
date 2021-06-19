---
title: Encontrar possíveis problemas usando analisadores de mapa de códigos
description: Saiba como você pode executar analisadores em mapas de código para ajudá-lo a identificar código que pode ser muito complexo ou que pode precisar de melhoria.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.progression.codemapanalyzers
helpviewer_keywords:
- code analysis, dependency graphs
- dependency graphs, analyzing code
- graph documents, analyzing
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8817e50ae96a27f6b3b76e28262390271c1fdf4c
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388848"
---
# <a name="find-potential-problems-using-code-map-analyzers"></a>Encontrar possíveis problemas usando analisadores de mapa de códigos

Execute analisadores em mapas de código para ajudá-lo a identificar código que pode ser muito complexo ou que pode precisar de melhoria. Por exemplo, você pode usar estes analisadores:

|**Para encontrar o código que tem**|**Examine essas áreas para ver se**|
|-|-|
|Loops ou dependências circulares|Você pode simplificá-los e considerar se pode quebrar esses ciclos.|
|Muitas dependências|Eles estão executando muitas funções ou para determinar o impacto da alteração dessas áreas. Um mapa de código bem formado mostrará um número mínimo de dependências. Para facilitar a manutenção, alteração, teste e reutilização do código, considere se você pode refactorar essas áreas para que elas sejam mais claramente definidas ou se você pode mesclar código que executa funções semelhantes.|
|Sem dependências|Eles são necessários ou se você deve remover esse código.|

## <a name="analyze-code-maps"></a>Analisar mapas de código

Na barra de ferramentas do mapa, escolha **Analisadores** de Layout  >  e, em seguida, o analisador que você deseja executar:

|**Analisador**|**Para identificar nós que**|
|-|-|
|**Analisador de Referências Circulares**|Têm dependências circulares entre si. **Observação:**  As dependências circulares que estão **no grupo Genéricos** não são mostradas no mapa quando você expande o grupo.|
|**Find Hubs Analyzer**|Estão nos 25% principais nós altamente conectados<br /><br /> **Para ocultar todos os outros nós no mapa**<br /><br /> – Abra o menu de atalho para o mapa, escolha **Avançado,** **Selecione**, **Ocultar Não Selecionado.**<br />     O mapa oculta os nós não selecionados e o analisador identifica novos nós como hubs.|
|**Analisador de nós não marcados**|Não têm referências de nenhum outro nós. **Cuidado:**  Verifique cada um desses casos antes de pressupondo que o código não seja usado. Determinadas dependências, como dependências XAML e dependências de tempo de run-time, não podem ser encontradas estaticamente no código.|

Os analisadores de mapa de código continuarão a ser executados depois que você aplicá-los. Se você alterar o mapa, todos os analisadores aplicados reprocessarão automaticamente o mapa atualizado. Para interromper a execução de um analisador, na barra de ferramentas do mapa, escolha   >  **Analisadores de Layout**. Desligue o analisador selecionado.

> [!TIP]
> Se você tiver um mapa muito grande, executar um analisador poderá causar uma exceção de memória inossa. Se isso ocorrer, edite o mapa para reduzir seu escopo ou gerar um menor e, em seguida, execute o analisador.

## <a name="see-also"></a>Confira também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
