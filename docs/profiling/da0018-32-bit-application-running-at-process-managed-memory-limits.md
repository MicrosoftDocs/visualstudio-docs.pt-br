---
title: Aplicativo DA0018-32-bit em execução em limites de memória gerenciada do processo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.performance.18
- vs.performance.DA0018
- vs.performance.rules.DA0018
ms.assetid: 98eb2d96-f92f-42f9-915c-e5ac2330ffbf
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- dotnet
ms.openlocfilehash: 74fed5f0dcbac45f603f16743eb2635fcf35292a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548142"
---
# <a name="da0018-32-bit-application-running-at-process-managed-memory-limits"></a>DA0018: aplicativo de 32 bits em execução em limites de memória gerenciada do processo

|Item|Valor|
|-|-|
|ID de regra|DA0018|
|Categoria|Uso das ferramentas de criação de perfil|
|Método de criação de perfil|amostragem|
|Mensagem|Alocações de memória gerenciada que se aproximam do limite padrão para um processo de 32 bits. O aplicativo poderá ser associado à memória.|
|Tipo de regra|Aviso|

 Ao criar o perfil usando a amostragem, a memória do .NET ou métodos de contenção de recursos, é necessário coletar pelo menos 10 amostras para disparar essa regra.

## <a name="cause"></a>Causa
 Os dados do sistema coletados durante a execução de criação de perfil indicam que os heaps de memória do .NET Framework se aproximaram do tamanho máximo que os heaps gerenciados podem atingir em um processo de 32 bits. Esse tamanho máximo é um valor padrão. Ele se baseia na quantidade total do espaço de endereço do processo que pode ser alocada a bytes privados. O valor relatado é o valor máximo observado dos heaps enquanto o processo do qual o perfil está sendo criado estava ativo. Considere uma nova criação de perfil usando o método de criação de perfil da memória do .NET e otimização do uso de recursos gerenciados pelo aplicativo.

 Quando o tamanho dos Heaps gerenciados se aproxima do limite padrão, o processo automático de coleta de lixo talvez precise ser invocado com mais frequência. Isso aumenta a sobrecarga de gerenciamento de memória.

 A Regra é acionada apenas para aplicativos de 32 bits em execução em computadores de 32 bits.

## <a name="rule-description"></a>Descrição da regra
 O CLR (Common Language Runtime) do Microsoft .NET fornece um mecanismo de gerenciamento automático de memória que usa um coletor de lixo para recuperar a memória de objetos que não são mais usados pelo aplicativo. O coletor de lixo é orientado a geração, com base na suposição de que muitas alocações são de curta duração. Variáveis locais, por exemplo, devem ser de curta duração. Os objetos recém-criados iniciam na geração 0 (ger 0), em seguida, progridem para a geração 1 quando sobrevivem a uma execução da coleta de lixo e, por fim, fazem a transição para a geração 2 se ainda são usados pelo aplicativo.

 Objetos gerenciados maiores que 85 KB são alocados no Heap de Objetos Grandes, no qual estão sujeitos à coleta de lixo e à compactação menos frequentes do que objetos menores. objetos grandes são gerenciados separadamente porque se presume que são mais persistentes e porque combinar objetos persistentes e grandes com objetos menores frequentemente alocados pode produzir a pior fragmentação do heap.

 Como o tamanho total dos heaps gerenciados se aproxima do limite padrão, a sobrecarga de gerenciamento de memória normalmente aumenta até o ponto em que pode começar a afetar a capacidade de resposta e a escalabilidade do aplicativo.

## <a name="how-to-investigate-a-warning"></a>Como investigar um aviso
 Clique duas vezes na mensagem na janela Lista de Erros para navegar até o modo de exibição de [marcas](../profiling/marks-view.md) . Encontre as colunas **Memória do .NET CLR\\Nº de bytes em todos os heaps** e **Nº total de bytes confirmados**. Determine se há fases específicas da execução do programa em que a alocação de memória gerenciada é mais pesada do que em outras fases. Compare os valores da coluna **Nº de bytes em todos os heaps** com a taxa de coleta de lixo relatada nas colunas **Memória do .NET CLR\\Nº de coletas da Ger 0**, **Memória do .NET CLR\\Nº de coletas da Ger 1** e **Memória do .NET CLR\\Nº de coletas da Ger 2** para determinar se o padrão de alocações de memória gerenciada está afetando a taxa de coleta de lixo.

 Em um aplicativo .NET Framework, o Common Language Runtime limita o tamanho total dos heaps gerenciados a um pouco menos do que uma metade do tamanho máximo da parte de área privada do espaço de endereço de um processo. Para um processo de 32 bits em execução em um computador de 32 bits, 2 GB representa o limite superior da parte privada do espaço de endereço do processo. Como o tamanho total dos Heaps gerenciados começa a se aproximar do limite padrão, a sobrecarga de gerenciamento de memória pode aumentar e o desempenho do aplicativo pode diminuir.

 Se o excesso de sobrecarga de memória gerenciada for um problema, considere uma destas opções:

- otimizando o uso de recursos de memória gerenciada do aplicativo

   -ou-

- tomar medidas para aliviar as restrições de arquitetura em relação ao tamanho máximo de memória virtual para um processo de 32 bits

  Para otimizar o uso de recursos de memória gerenciada do aplicativo, colete dados de alocação de memória gerenciada em uma execução de criação de perfil de Alocação de Memória do .NET. Examine os relatórios de [exibições de dados de memória .net](../profiling/dotnet-memory-data-views.md) para entender o padrão do aplicativo de alocação de memória.

  Use a [exibição de tempo de vida do objeto](../profiling/object-lifetime-view.md) para determinar quais dos objetos de dados do programa estão sobreviventes à geração e, em seguida, recuperados a partir daí.

  Use a [Exibição de Alocações](../profiling/dotnet-memory-allocations-view.md) para determinar o caminho de execução que resultou nessas alocações.

  Para obter mais informações sobre como melhorar o desempenho da coleta de lixo, consulte o artigo técnico sobre o .NET Framework [Garbage Collector Basics and Performance Hints](/previous-versions/dotnet/articles/ms973837(v=msdn.10)) (Noções básicas sobre o coletor de lixo e dicas de desempenho) no site do MSDN.

  Para obter alívio de arquitetura das restrições de memória virtual em relação ao tamanho da parte privada de um espaço de endereço do processo, tente executar esse processo de 32 bits em um computador de 64 bits.  Um processo de 32 bits em um computador de 64 bits pode adquirir até 4 GB de memória virtual privada.

  Um processo de 64 bits em execução em um computador de 64 bits pode adquirir até 8 TB de memória virtual. Considere uma nova compilação do aplicativo para que ele seja executado como um aplicativo nativo de 64 bits. Essa regra se destina apenas a fins informativos e pode não exigir ação corretiva.
