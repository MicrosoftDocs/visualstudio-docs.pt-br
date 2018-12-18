---
title: Suspensão automática de recursos
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: b97a58a7f5ba3808c658b838de942e94c12b9b79
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53049088"
---
# <a name="automatic-feature-suspension"></a>Suspensão automática de recursos

Se a memória disponível no sistema cai a 200 MB ou menos, o Visual Studio exibe a mensagem a seguir no editor de código:

![Suspendendo a análise de solução completa de texto de alerta](../code-quality/media/fsa_alert.png)

Quando o Visual Studio detecta uma condição de pouca memória, ele suspende automaticamente determinados recursos avançados para ajudá-lo a permanecer estável. O Visual Studio continua a funcionar como antes, mas seu desempenho é degradado.

Em uma condição de pouca memória, as seguintes ações ocorrem:

- Análise de solução completa para o Visual c# e Visual Basic está desabilitado.

- [Coleta de lixo](/dotnet/standard/garbage-collection/index) modo de baixa latência (GC) para Visual c# e Visual Basic está desabilitado.

- Caches do Visual Studio são liberados.

## <a name="improve-visual-studio-performance"></a>Melhorar o desempenho do Visual Studio

Para obter dicas e truques sobre como melhorar o desempenho do Visual Studio ao lidar com grandes soluções ou condições de memória baixa, consulte [considerações sobre desempenho para grandes soluções](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions).

## <a name="full-solution-analysis-suspended"></a>Análise de solução completa suspenso

Por padrão, análise de solução completa é habilitado para o Visual Basic e desabilitada para o Visual c#. No entanto, em uma condição de pouca memória, análise de solução completa é automaticamente desabilitada para Visual Basic e Visual c#, independentemente de suas definições na caixa de diálogo Opções. No entanto, você pode habilitar novamente a análise de solução completa, escolhendo a **reabilitar** botão nas informações da barra quando ele for exibido, selecionando a **habilitar análise de solução completa** caixa de seleção na caixa de diálogo Opções, ou, reiniciar o Visual Studio. A caixa de diálogo Opções sempre mostra a atual solução completa as configurações de análise. Para obter mais informações, consulte [como: habilitar e desabilitar análise completa da solução](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md).

## <a name="gc-low-latency-disabled"></a>GC baixa latência desabilitada

Para habilitar o modo de baixa latência de GC novamente, reinicie o Visual Studio. Por padrão, o Visual Studio habilita o modo de baixa latência de GC sempre que você está digitando para garantir que sua digitação não impeça que quaisquer operações de GC. No entanto, se uma condição de pouca memória faz com que o Visual Studio exibir o aviso de suspensão automática, o modo de baixa latência de GC está desabilitado para a sessão. Reiniciar o Visual Studio habilita novamente o comportamento de GC padrão. Para obter mais informações, consulte <xref:System.Runtime.GCLatencyMode>.

## <a name="visual-studio-caches-flushed"></a>Caches do Studio Visual liberados

Se você continuar sua sessão de desenvolvimento atual ou reinicie o Visual Studio, todos os caches do Visual Studio são removidos imediatamente, mas começa a preencher novamente. Os caches liberados incluem caches para os seguintes recursos:

- Localizar todas as referências

- Navegar para

- Adicionar usando

Além disso, os caches usados para operações internas do Visual Studio também são desmarcados.

> [!NOTE]
> O aviso de suspensão do recurso automático ocorre apenas uma vez em uma base por solução, não em uma base por sessão. Isso significa que, se você alterna do Visual Basic para Visual c# (ou vice-versa) e executar em outra condição de pouca memória, você pode, possivelmente, obter outro aviso de suspensão automática de recursos.

## <a name="see-also"></a>Consulte também

- [Como habilitar e desabilitar a análise de solução completa](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)
- [Conceitos básicos da coleta de lixo](/dotnet/standard/garbage-collection/fundamentals)
- [Considerações sobre desempenho para grandes soluções](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)