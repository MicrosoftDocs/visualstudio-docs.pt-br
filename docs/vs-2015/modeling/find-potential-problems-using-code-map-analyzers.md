---
title: Localizar possíveis problemas usando analisadores de mapa de código | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.progression.codemapanalyzers
helpviewer_keywords:
- code analysis, dependency graphs
- dependency graphs, analyzing code
- graph documents, analyzing
ms.assetid: 9dd799a7-f7eb-42ff-8612-b19dde7ff4eb
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: db54fef40914dc234f507935a646292eb8d4914e
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929716"
---
# <a name="find-potential-problems-using-code-map-analyzers"></a>Encontrar possíveis problemas usando analisadores de mapa de códigos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Executar analisadores em mapas de código para ajudá-lo a identificar o código que pode ser excessivamente complexo ou que pode ser aperfeiçoado. Por exemplo, você pode usar esses analisadores:  
  
|**Para localizar o código que tem**|**Examinar essas áreas para ver se**|  
|-------------------------------|--------------------------------------------|  
|Loops ou dependências circulares|Você pode simplificá-los e considere se é possível dividir esses ciclos.|  
|Muitas dependências|Eles estão realizando a muitas funções ou para determinar o impacto da alteração nessas áreas. Um mapa de código bem formado mostrará um número mínimo de dependências. Para tornar o código mais fácil de manter, alterar, testar e reutilizar, considere se você pode refatorar essas áreas para que eles são mais claramente definidos, ou se é possível mesclar o código que executa funções semelhantes.|  
|Sem dependências|Eles são necessários ou se você deve remover esse código.|  
  
## <a name="analyze-code-maps"></a>Analisar os mapas de código  
  
1. Na barra de ferramentas do mapa, escolha **Layout**, **analisadores**e, em seguida, o analisador que você deseja executar:  
  
   |**Analisador**|**Para identificar nós que**|  
   |------------------|--------------------------------|  
   |**Analisador de referências circulares**|Possuem dependências circulares entre si. **Observação:**  As dependências circulares que estão na **genéricos** grupo não são mostrados no mapa, ao expandir o grupo.|  
   |**Localizar Hubs Analyzer**|Estão na 25% principais de nós altamente conectado<br /><br /> **Para ocultar todos os outros nós no mapa**<br /><br /> -Abra o menu de atalho para o mapa, escolha **Advanced**, **selecionar**, **ocultar não selecionados**.<br />     O mapa oculta os nós não selecionados e o Analisador identifica novos nós, como hubs.|  
   |**Analisador de nós não referenciados**|Não tem referências de outros nós. **Cuidado:**  Verifique se cada um desses casos antes supondo que o código não é usado. Determinadas dependências como dependências XAML e dependências de tempo de execução não podem ser encontradas estaticamente no código.|  
  
   Analisadores de mapa de código continuará a ser executado após você aplicá-las. Se você alterar o mapa, quaisquer analisadores aplicados serão automaticamente reprocessar o mapa atualizado. Para interromper a execução de um analisador, na barra de ferramentas do mapa, escolha **Layout**, **analisadores**. Desative o analisador selecionado.  
  
> [!TIP]
>  Se você tiver um mapa muito grande, executar um analisador pode causar uma exceção de falta de memória. Se isso ocorrer, edite o mapa para reduzir seu escopo ou gerar uma menor e, em seguida, executar o analisador.  
  
## <a name="see-also"></a>Consulte também  
 [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)   
 [Usar mapas de códigos para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)   
 [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
