---
title: Suspensão automática de recursos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c8aee8f4ef46d3621bf569b260d943180abd7ad5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49178172"
---
# <a name="automatic-feature-suspension"></a>Suspensão automática de recursos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Se a memória disponível no sistema cai a 200MB ou menos, o Visual Studio exibe a mensagem a seguir no editor de códigos.

 ![Suspendendo a análise de solução completa de texto de alerta](../code-quality/media/fsa-alert.png "FSA_Alert")

 Quando o Visual Studio detecta uma condição de pouca memória, ele suspende automaticamente determinados recursos avançados para ajudá-lo a permanecer estável. Quando isso avançado recurso suspensão aviso é exibido, Visual Studio continuará a funcionar como antes, mas seu desempenho será degradado um pouco.

 Em uma condição de pouca memória, ocorre o seguinte:

-   Análise de solução completa para o Visual c# e Visual Basic está desabilitado.

-   [Coleta de lixo](http://msdn.microsoft.com/library/22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9) modo de baixa latência (GC) para Visual c# e Visual Basic estão desabilitados.

-   Caches do Visual Studio são liberados.

## <a name="improve-visual-studio-performance"></a>Melhorar o desempenho do Visual Studio
 Para obter dicas e truques sobre como melhorar o desempenho do Visual Studio ao lidar com grandes soluções ou condições de memória baixa, consulte [considerações sobre desempenho para grandes soluções](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions).

## <a name="full-solution-analysis-suspended"></a>Análise de solução completa suspenso
 Por padrão, análise de solução completa é habilitado para o Visual Basic e desabilitada para o Visual c#. No entanto, em uma condição de pouca memória, análise de solução completa é automaticamente desabilitada para Visual Basic e Visual c#, independentemente de suas definições na caixa de diálogo Opções. No entanto, você pode habilitar novamente a análise de solução completa, escolhendo a **reabilitar** botão nas informações da barra quando ele for exibido, selecionando a **habilitar análise de solução completa** caixa de seleção na caixa de diálogo Opções, ou, reiniciar o Visual Studio. A caixa de diálogo Opções sempre mostra a atual solução completa as configurações de análise. Para obter mais informações, consulte [como: habilitar e desabilitar análise completa da solução](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md).

## <a name="gc-low-latency-disabled"></a>GC baixa latência desabilitada
 Para habilitar o modo de baixa latência de GC novamente, reinicie o Visual Studio.  Por padrão, o Visual Studio habilita o modo de baixa latência de GC sempre que você está digitando para garantir que sua digitação não impeça que quaisquer operações de GC. No entanto, se uma condição de pouca memória faz com que o Visual Studio exibir o aviso de suspensão automática, o modo de baixa latência de GC está desabilitado para a sessão. Reiniciar o Visual Studio irá habilitar novamente o comportamento de GC padrão. Para obter mais informações, consulte <xref:System.Runtime.GCLatencyMode>.

## <a name="visual-studio-caches-flushed"></a>Caches do Studio Visual liberados

Todos os caches do Visual Studio são removidos imediatamente, mas começarão a preencher novamente se você continuar sua sessão de desenvolvimento atual ou reinicie o Visual Studio. Os caches liberados incluem caches para os recursos a seguir.

-   Localizar todas as referências

-   Navegar para

-   Adicionar usando

Além disso, os caches usados para operações internas do Visual Studio também são desmarcados.

> [!NOTE]
> O aviso de suspensão do recurso automático ocorre apenas uma vez em uma base por solução, não em uma base por sessão. Isso significa que, se você alterna do Visual Basic para Visual c# (ou vice-versa) e executar em outra condição de pouca memória, você pode, possivelmente, obter outro aviso de suspensão automática de recursos.

## <a name="see-also"></a>Consulte também

- [Como habilitar e desabilitar a análise de solução completa](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md)
- [Conceitos básicos da coleta de lixo](http://msdn.microsoft.com/library/67c5a20d-1be1-4ea7-8a9a-92b0b08658d2)
- [Considerações sobre desempenho para grandes soluções](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)