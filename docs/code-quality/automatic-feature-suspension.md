---
title: Suspensão automática de recursos
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
- performance
- low-memory
ms.assetid: 572c15aa-1fd0-468c-b6be-9fa50e170914
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 236a95cd8d4af8da91199bf79e7c9fe3aa0d49af
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769486"
---
# <a name="automatic-feature-suspension"></a>Suspensão automática de recursos

Se a memória do sistema disponível cair em 200 MB ou menos, o Visual Studio exibirá a seguinte mensagem no editor de código:

![Texto de alerta suspendendo análise de solução completa](../code-quality/media/fsa_alert.png)

Quando o Visual Studio detecta uma condição de memória insuficiente, ele suspende automaticamente determinados recursos avançados para ajudá-lo a permanecer estável. O Visual Studio continua a funcionar como antes, mas seu desempenho está degradado.

Em uma condição de memória insuficiente, ocorrem as seguintes ações:

- A análise de código ao vivo para Visual C# e Visual Basic é reduzida para o escopo mínimo.

- O modo de baixa latência da [coleta de lixo](/dotnet/standard/garbage-collection/index) (GC) para Visual C# e Visual Basic está desabilitado.

- Os caches do Visual Studio são liberados.

## <a name="improve-visual-studio-performance"></a>Melhorar o desempenho do Visual Studio

Para obter dicas e truques sobre como melhorar o desempenho do Visual Studio ao lidar com soluções grandes ou condições de memória insuficiente, consulte [considerações de desempenho para soluções grandes](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions).

## <a name="live-code-analysis-is-reduced-to-minimal-scope"></a>A análise de código ao vivo é reduzida para o escopo mínimo

Por padrão, a análise de código ao vivo é executada para projetos e documentos abertos. Você pode personalizar esse escopo de análise para ser reduzido ao documento atual ou aumentado para uma solução inteira. Para obter mais informações, consulte [como: configurar o escopo de análise de código ao vivo para código gerenciado](./configure-live-code-analysis-scope-managed-code.md). Em uma condição de memória insuficiente, o Visual Studio força o escopo da análise ao vivo a ser reduzido para o documento atual. No entanto, você pode reabilitar seu escopo de análise preferencial escolhendo o botão **reabilitar** na barra de informações quando ele aparecer ou reiniciando o Visual Studio. A caixa de diálogo opções sempre mostra as configurações atuais de escopo da análise de código ativo.

## <a name="gc-low-latency-disabled"></a>Baixa latência de GC desabilitada

Para reabilitar o modo de baixa latência do GC, reinicie o Visual Studio. Por padrão, o Visual Studio habilita o modo de baixa latência do GC sempre que você está digitando para garantir que a digitação não bloqueie nenhuma operação GC. No entanto, se uma condição de memória insuficiente fizer com que o Visual Studio exiba o aviso de suspensão automática, o modo de baixa latência do GC será desabilitado para essa sessão. Reiniciar o Visual Studio habilita novamente o comportamento padrão do GC. Para obter mais informações, consulte <xref:System.Runtime.GCLatencyMode>.

## <a name="visual-studio-caches-flushed"></a>Caches do Visual Studio liberados

Se você continuar a sessão de desenvolvimento atual ou reiniciar o Visual Studio, todos os caches do Visual Studio serão imediatamente esvaziados, mas começarão a ser repopulados. Os caches liberados incluem caches para os seguintes recursos:

- Localizar todas as referências

- Navegar para

- Adicionar usando

Além disso, os caches usados para operações internas do Visual Studio também são desmarcados.

> [!NOTE]
> O aviso de suspensão de recurso automático ocorre apenas uma vez por solução, não por sessão. Isso significa que, se você alternar de Visual Basic para Visual C# (ou vice-versa) e executar outra condição de memória insuficiente, poderá obter outro aviso de suspensão de recurso automático.

## <a name="see-also"></a>Confira também

- [Como: configurar o escopo de análise de código ao vivo para código gerenciado](./configure-live-code-analysis-scope-managed-code.md)
- [Noções básicas sobre a coleta de lixo](/dotnet/standard/garbage-collection/fundamentals)
- [Considerações de desempenho para soluções grandes](https://github.com/dotnet/roslyn/wiki/Performance-considerations-for-large-solutions)
