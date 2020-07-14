---
title: Otimizando as configurações do criador de perfil | Microsoft Docs
ms.date: 4/29/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, improve performance
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 1ef802958817b43dd66973db66a80d328454aa83
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329254"
---
# <a name="optimizing-profiler-settings"></a>Otimizando as configurações do criador de perfil

O criador de perfil de desempenho e a janela de Ferramentas de Diagnóstico no Visual Studio têm muitas configurações diferentes que afetam o desempenho geral das ferramentas. Alterar algumas configurações pode fazer com que a análise seja executada rapidamente ou causar tempos de espera adicionais durante o processamento de resultados em ferramentas. Veja abaixo um resumo de determinadas configurações e seu impacto sobre o desempenho.

## <a name="symbol-settings"></a>Configurações de Símbolo

As configurações de símbolos encontradas nas opções do depurador (**Debug > options > Symbols**) têm um impacto significativo sobre o tempo necessário para gerar resultados nas ferramentas. Habilitar servidores de símbolo ou usar o **_NT_SYMBOL_PATH** faz com que o criador de perfil solicite símbolos para cada módulo carregado em um relatório. Atualmente, o criador de perfil sempre carrega automaticamente todos os símbolos, independentemente da preferência de carregamento automático de símbolos.

![Página de carregamento de símbolos](../profiling/media/symbolloading.png "Carregamento de símbolos")

O progresso no carregamento de símbolos pode ser visto na janela **saída** sob o cabeçalho **ferramentas de diagnóstico** .

![Progresso do carregamento de símbolos](../profiling/media/symbolloadingprogress.png "Progresso do carregamento de símbolos")

Depois de baixados, os símbolos são armazenados em cache, o que acelerará a análise futura, mas ainda exigirá o carregamento e a análise dos arquivos. Se o carregamento de símbolos estiver diminuindo a análise, tente desativar os servidores de símbolos e limpar o cache de símbolos. Em vez disso, conte com símbolos criados localmente para seu projeto.

## <a name="show-external-code"></a>Mostrar Código Externo

Muitas das ferramentas no criador de **perfil de desempenho** e na janela de **ferramentas de diagnóstico** têm um conceito de código de usuário versus código externo. O código do usuário é qualquer código criado pela solução aberta ou abrir espaço de trabalho. O código externo é qualquer outra coisa. Mantendo a configuração **Mostrar código externo** desabilitada ou **Mostrar apenas meu código** habilitado, você permite que as ferramentas agreguem código externo a um único quadro de primeiro nível, reduzindo muito a quantidade de processamento necessária para mostrar os resultados. Isso permite que os usuários vejam o que foi chamado no código externo que criou a lentidão enquanto mantém os dados a serem processados para um mínimo. Quando possível, deixe **Mostrar código externo** desabilitado e verifique se você tem a solução ou o espaço de trabalho aberto para o diagsession que você está analisando.

## <a name="trace-duration"></a>Duração do rastreamento

A criação de perfil de durações menores resulta em menos dados, o que é mais rápido de analisar. Normalmente, recomendamos que você tente limitar seus rastreamentos para não mais do que cinco minutos de dados de desempenho. Algumas ferramentas, como a ferramenta de [uso da CPU](../profiling/cpu-usage.md) , permitem pausar a coleta de dados enquanto a ferramenta está em execução, para que você possa limitar a quantidade de dados coletados para o cenário que você está interessado em analisar.

## <a name="sampling-frequency"></a>Frequência de amostragem

Determinadas ferramentas, como a ferramenta de [uso da CPU](../profiling/cpu-usage.md) e a ferramenta de [alocação de objeto net](../profiling/dotnet-alloc-tool.md) , permitem que você ajuste uma frequência de amostragem. Aumentar essa frequência de amostragem permite que você meça com mais precisão, mas aumenta a quantidade de dados gerados. Normalmente, é melhor deixar essa configuração na taxa padrão, a menos que um problema específico esteja sendo investigado.

![Página de propriedades do hub de diagnóstico](../profiling/media/diaghubpropertiespage.png "Página de propriedades do hub de diagnóstico")

## <a name="see-also"></a>Veja também

- [Executando ferramentas de criação de perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md)
- [Usando várias ferramentas de criador de perfil simultaneamente](../profiling/use-multiple-profiler-tools-simultaneously.md)
- [Entendendo sobre os métodos de coleta de desempenho](../profiling/understanding-performance-collection-methods-perf-profiler.md)
