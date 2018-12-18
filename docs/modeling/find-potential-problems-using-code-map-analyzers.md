---
title: Encontrar possíveis problemas usando analisadores de mapas de códigos
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.progression.codemapanalyzers
helpviewer_keywords:
- code analysis, dependency graphs
- dependency graphs, analyzing code
- graph documents, analyzing
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: afc2915a5d1bfb6cf361a4b84a0235db296bac67
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49856740"
---
# <a name="find-potential-problems-using-code-map-analyzers"></a>Encontrar possíveis problemas usando analisadores de mapa de códigos

Executar analisadores em mapas de código para ajudá-lo a identificar o código que pode ser excessivamente complexo ou que pode ser aperfeiçoado. Por exemplo, você pode usar esses analisadores:

|**Para localizar o código que tem**|**Examinar essas áreas para ver se**|
|-|-|
|Loops ou dependências circulares|Você pode simplificá-los e considere se é possível dividir esses ciclos.|
|Muitas dependências|Eles estão realizando a muitas funções ou para determinar o impacto da alteração nessas áreas. Um mapa de código bem formado mostrará um número mínimo de dependências. Para tornar o código mais fácil de manter, alterar, testar e reutilizar, considere se você pode refatorar essas áreas para que eles são mais claramente definidos, ou se é possível mesclar o código que executa funções semelhantes.|
|Sem dependências|Eles são necessários ou se você deve remover esse código.|

## <a name="analyze-code-maps"></a>Analisar os mapas de código

Na barra de ferramentas do mapa, escolha **Layout** > **analisadores**e, em seguida, o analisador que você deseja executar:

|**Analisador**|**Para identificar nós que**|
|-|-|
|**Analisador de referências circulares**|Possuem dependências circulares entre si. **Observação:** dependências circulares que estão em de **genéricos** grupo não são mostrados no mapa, ao expandir o grupo.|
|**Localizar Hubs Analyzer**|Estão na 25% principais de nós altamente conectado<br /><br /> **Para ocultar todos os outros nós no mapa**<br /><br /> -Abra o menu de atalho para o mapa, escolha **Advanced**, **selecionar**, **ocultar não selecionados**.<br />     O mapa oculta os nós não selecionados e o Analisador identifica novos nós, como hubs.|
|**Analisador de nós não referenciados**|Não tem referências de outros nós. **Cuidado:** Verifique se cada um desses casos antes, supondo que o código não é usado. Determinadas dependências como dependências XAML e dependências de tempo de execução não podem ser encontradas estaticamente no código.|

Analisadores de mapa de código continuará a ser executado após você aplicá-las. Se você alterar o mapa, quaisquer analisadores aplicados serão automaticamente reprocessar o mapa atualizado. Para interromper a execução de um analisador, na barra de ferramentas do mapa, escolha **Layout** > **analisadores**. Desative o analisador selecionado.

> [!TIP]
> Se você tiver um mapa muito grande, executar um analisador pode causar uma exceção de falta de memória. Se isso ocorrer, edite o mapa para reduzir seu escopo ou gerar uma menor e, em seguida, executar o analisador.

## <a name="see-also"></a>Consulte também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
