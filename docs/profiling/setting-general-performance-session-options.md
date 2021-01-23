---
title: Configurando opções de sessão de desempenho geral | Microsoft Docs
description: Saiba como você pode definir o método de coleta e as convenções de nomenclatura de dados de criação de perfil para uma sessão de desempenho Ferramentas de Criação de Perfil.
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.general
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2691d9d8868343291f3be4d9f5b3002e24605b85
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720183"
---
# <a name="set-general-performance-session-options"></a>Configurar opções gerais da sessão de desempenho

Você pode definir o método de coleção e convenções de nomenclatura de dados de criação de perfil para uma sessão de desempenho das Ferramentas de Criação de Perfil do no Visual Studio na página **Geral** da caixa de diálogo Propriedades da sessão de desempenho. Para abrir a caixa de diálogo **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Propriedades**.

## <a name="choosing-data-collection-methods"></a>Escolher os métodos de coleta de dados

Definir o método de coleção base selecionando uma das opções em **Coleção de Perfis**. As opções estão descritas na tabela a seguir:

|Opção|Artigo|
|-|-|
|**Amostragem**. O método de amostragem coleta informações de perfil em intervalos regulares. Este método é útil para localizar problemas de utilização do processador e é o método sugerido para iniciar a maioria das investigações de desempenho.|- [Coletando estatísticas de desempenho usando amostragem](../profiling/collecting-performance-statistics-by-using-sampling.md)|
|**Instrumentação**. O método de instrumentação injeta em uma cópia de um módulo de código que registra cada entrada, saída e a chamada de função das funções no módulo durante uma geração de perfil de criação de perfil. Este método é útil para coletar informações detalhadas de tempo sobre uma seção de seu código e para compreender o impacto das operações de entrada e de saída no desempenho do aplicativo.|- [Coletando dados de tempo detalhados usando a instrumentação](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)|
|**Simultaneidade**. O método de simultaneidade coleta dados para cada evento que bloqueia a execução de seu código, como quando um thread aguarda que o acesso bloqueado a um recurso de aplicativo seja liberado. Este método é útil para analisar aplicativos multi-threaded.|- [Coletando dados de simultaneidade de processo e thread](../profiling/collecting-thread-and-process-concurrency-data.md)|

 Você pode coletar dados de memória do .NET usando os métodos de amostragem ou instrumentação. Selecione o tipo de dados na **criação de perfil de memória do .NET**.

|Opção|Artigo|
|-|-|
|**Coletar informações de alocação de objeto do .NET**. Por padrão, os dados incluem o número e tamanho dos objetos alocados. Marque ou desmarque esta caixa de seleção para habilitar ou desabilitar a coleta de dados de memória do .NET. |- [Coletando a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)|
|**Também coletar informações de tempo de vida do objeto .NET**. Marque esta caixa de seleção para incluir dados sobre as gerações de coleta de lixo que foram usados para recuperar os objetos de memória.|- [Coletando a alocação de memória do .NET e os dados de tempo de vida](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md) |

 Uma página de sessão de criação de perfil aparece quando você começar a criar o perfil de um aplicativo, no qual você pode pausar, retomar e parar criação de perfil.

 ![Página de sessão de criação de perfil](../profiling/media/prof_profilingsessionpage.png "PROF_ProfilingSessionPage")

## <a name="set-profiling-data-file-options"></a>Configurar opções de arquivo de dados de criação de perfil

|Opção|Artigo|
|-|-|
|**Relatório**. Por padrão, o arquivo de dados (.vsp) de criação de perfil é dado o nome do aplicativo com perfil e está localizado na pasta de solução ou projeto. Uma cadeia de caracteres de data também é acrescentada ao nome e um número incrementado é adicionado aos arquivos de dados que outra forma, teriam nomes duplicados. Você pode alterar essas opções.|- [Como definir opções de nome de arquivo de dados de desempenho](../profiling/how-to-set-performance-data-file-name-options.md)|
