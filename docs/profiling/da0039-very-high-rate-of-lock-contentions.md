---
title: 'DA0039: taxa muito alta de contenções de bloqueio | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.39
- vs.performance.DA0039
- vs.performance.rules.DA0039
ms.assetid: 5a9fc57d-9097-413b-af0c-8726b1a57048
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4548e190b7008c887ccf1c149a95f52bd8d7892d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845700"
---
# <a name="da0039-very-high-rate-of-lock-contentions"></a>DA0039: taxa muito alta de contenções de bloqueio

|||  
|-|-|  
|ID de regra|DA0039|  
|Categoria|Uso do .NET Framework|  
|Métodos de criação de perfil|Amostragem<br /><br /> Instrumentação<br /><br /> Memória do .NET|  
|Mensagem|Uma taxa muito alta de contenções de Bloqueio do .NET está ocorrendo. Investigue o motivo dessa contenção de bloqueio executando um perfil de Simultaneidade.|  
|Tipo de regra|Aviso|  

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 25 amostras para disparar essa regra.  

## <a name="cause"></a>Causa  
 Os dados de desempenho do sistema coletados com os dados de criação de perfil indicam que ocorreu uma taxa excessivamente alta de contenções de bloqueio durante a execução do aplicativo. Considere uma nova criação de perfil usando o método de criação de perfil de simultaneidade para descobrir a causa da contenção.  

## <a name="rule-description"></a>Descrição da regra  
 Os bloqueios são usados para proteger seções críticas do código que devem ser executadas em série por um thread por vez em um aplicativo multi-threaded. O CLR (Common Language Runtime) do Microsoft .NET fornece um conjunto completo de primitivos de sincronização e bloqueio. Por exemplo, a linguagem C# dá suporte a uma instrução de bloqueio (SyncLock no Visual Basic). Um aplicativo gerenciado pode chamar os métodos Monitor.Enter e Monitor.Exit no namespace System.Threading para adquirir e liberar um bloqueio diretamente. O .NET Framework dá suporte a primitivos de sincronização e bloqueio adicionais, incluindo classes que dão suporte a Mutexes, ReaderWriterLocks e Semaphores. Para obter mais informações, consulte [Visão geral dos primitivos de sincronização](http://go.microsoft.com/fwlink/?LinkId=177867) no Guia do Desenvolvedor do .NET Framework no site do MSDN. As classes do .NET Framework são colocadas em camada por conta própria sobre os serviços de sincronização de nível inferior internos do sistema operacional Windows. Eles incluem objetos de seção crítica e várias funções de sinalização de evento e de Espera diferentes. Para obter mais informações, confira a seção [Synchronization](http://go.microsoft.com/fwlink/?LinkId=177869) (Sincronização) do Desenvolvimento do Win32 e COM na Biblioteca MSDN.  

 Subjacentes às classes do .NET Framework e aos objetos nativos do Windows que são usados para sincronização e bloqueio estão os locais de memória compartilhada que devem ser alterados usando operações sincronizadas. As operações sincronizadas usam instruções específicas ao hardware que operam em locais de memória compartilhada para alterar seu estado usando operações atômicas. Operações atômicas têm a garantia de serem consistentes em todos os processadores no computador. Locks e WaitHandles são objetos do .NET que usam operações sincronizadas automaticamente quando são definidos ou redefinidos. Pode haver outras estruturas de dados de memória compartilhada no aplicativo que também exigem o uso de operações sincronizadas para que sejam atualizadas de uma forma thread-safe. Para obter mais informações, confira [Operações interconectadas](http://go.microsoft.com/fwlink/?LinkId=177870) na seção do .NET Framework da biblioteca do MSDN.  

 A sincronização e o bloqueio são mecanismos usados para garantir que aplicativos de vários threads sejam executados corretamente. Cada thread de um aplicativo multi-threaded é uma unidade de execução independente que é agendada de forma independente pelo sistema operacional. Uma contenção de bloqueio ocorre sempre que um thread que está tentando adquirir um bloqueio é atrasado devido a outro thread estar mantendo o bloqueio.  

 Os bloqueios são frequentemente aninhados. O aninhamento ocorre quando um thread que executa uma seção crítica executa uma função que exige outro bloqueio em seguida. Alguma quantidade de aninhamento de bloqueio é inevitável. A seção crítica pode chamar um método do .NET Framework que se baseia em bloqueios para garantir que ele é thread-safe. Uma chamada de alguma seção crítica do aplicativo em um método Framework que também é bloqueada usando um identificador de bloqueio diferente faz com que os bloqueios sejam aninhados. As condições de bloqueio aninhado podem levar a problemas de desempenho que são notoriamente difíceis de serem resolvidos e corrigidos.  

 Essa regra é acionada quando as medições feitas durante uma execução de criação de perfil indicam que há uma quantidade excessivamente alta de contenções de bloqueio. As contenções de bloqueio atrasam a execução de threads que estão aguardando o bloqueio. Até mesmo pequenas quantidades de contenção de bloqueio em testes de unidade ou em testes de carga em execução em um hardware de extremidade inferior devem ser investigadas.  

> [!NOTE]
>  Quando a taxa de contenções de bloqueio relatadas nos dados de criação de perfil for significativa, mas não excessiva, a mensagem de informações [DA0038: alta taxa de contenções de bloqueio](../profiling/da0038-high-rate-of-lock-contentions.md) será acionada em vez dessa mensagem de aviso.  

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso  
 Clique duas vezes na mensagem para navegar para a exibição [Marcas](../profiling/marks-view.md) dos dados de criação de perfil.  Encontre a coluna **.NET CLR LocksAndThreads\Taxa de contenção/s**. Determine se há fases específicas da execução do programa em que a contenção de bloqueio é mais pesada do que em outras fases.  

 Essa regra é acionada somente quando o método de criação de perfil de simultaneidade não está sendo usado. O método de criação de perfil de simultaneidade é a melhor ferramenta a ser usada para diagnosticar problemas de desempenho relacionados à contenção de bloqueio em seu aplicativo. Colete dados de criação de perfil de simultaneidade para entender o comportamento de bloqueio do aplicativo. Isso inclui entender quais bloqueios têm uma contenção pesada, por quanto tempo a execução do thread é atrasada aguardando bloqueios com contenção e qual código específico está envolvido. Os perfis de simultaneidade coletam dados em todas as contenções de bloqueio, incluindo o comportamento de bloqueio de instalações nativas do Windows, classes do .NET Framework e todas as outras bibliotecas de terceiros referenciadas pelo aplicativo. Para obter informações sobre a criação de perfil de simultaneidade com base na IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], confira [Coletar dados de simultaneidade de thread e do processo](../profiling/collecting-thread-and-process-concurrency-data.md). Para obter links para informações sobre criação de perfil de simultaneidade por meio da linha de comando, confira a seção **Use the concurrency method to collect resource contention and thread activity data** (Usar o método de simultaneidade para coletar a contenção de recursos e dados de atividade de thread) de [Use profiling methods from the command line](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md) (Usar métodos de criação de perfil da linha de comando).