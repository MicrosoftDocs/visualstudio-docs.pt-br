---
title: Conjuntos de contadores e regras de limite para testes de carga no Visual Studio
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- counters, counter sets
- load tests, thresholds
- counter sets
- load tests, performance
- load tests, counter sets
- load tests, threshold rules
ms.assetid: 9e14d955-f3a4-4717-bbfe-7f08cdda5678
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: dba28aea3a4859c9767925a0ac3c7b2ec8e75275
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894502"
---
# <a name="specify-counter-sets-and-threshold-rules-for-computers-in-a-load-test"></a>Especificar conjuntos de contadores e regras de limite para computadores em um teste de carga

Os testes de carga oferecem conjuntos de contadores nomeados úteis para quando você analisar dados de contadores de desempenho. Conjuntos do contador são organizados pela tecnologia e incluem Application, ASP.NET, .NET Application, IIS e SQL. Quando você cria um teste de carga com o **Novo Assistente de Teste de Carga**, um conjunto inicial de contadores é adicionado. Esses oferecem a você uma seleção de conjuntos de contadores importantes e predefinidos para o seu teste de carga. Você gerencia os contadores no **Editor de Teste de Carga**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Se os testes de carga forem distribuídos por computadores remotos, os contadores de agente e controlador serão mapeados para os conjuntos de contadores de agente e controlador. Para obter mais informações sobre como usar computadores remotos no teste de carga, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

Conjuntos de contadores são coletados em computadores que você especifica. A associação entre um conjunto de contadores e um computador que é usado durante um teste de carga é um *mapa do conjunto de contadores*. Por exemplo, o servidor Web que você está testando poderia ter mapeamentos de conjuntos de contadores do aplicativo ASP.NET, IIS e .NET.

Por padrão, os contadores de desempenho são coletados no controlador e nos agentes. Para obter mais informações, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).

É importante que você adicione os servidores em teste à lista de computadores nos quais é para coletar contadores. Em seguida, todos os dados importantes do sistema são coletados e monitorados durante o teste de carga.

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Gerenciar conjuntos de contadores para o teste de carga:** depois de criar o teste de carga, você pode editar o conjunto de contadores definido no Editor de Teste de Carga. Gerenciar conjuntos de contadores envolve escolher o conjunto de computadores dos quais você deseja coletar dados de desempenho e atribuir um conjunto de contadores para coletar de cada computador individual. Você gerencia os contadores no Editor de testes de carga.|-   [Como gerenciar conjuntos de contadores](../test/how-to-manage-counter-sets-using-the-load-test-editor.md)|
|**Adicionar conjuntos de contadores ao teste de carga:** quando você cria um teste de carga com o **Novo Assistente de Teste de Carga**, um conjunto inicial de contadores é adicionado. Isso oferece um conjunto de contadores predefinidos para seu teste de carga. Depois de criar um teste de carga, você pode adicionar novos contadores aos conjuntos de contadores existentes usando o Editor de testes de carga.|-   [Como adicionar contadores a conjuntos de contadores](../test/how-to-add-counters-to-counter-sets-using-the-load-test-editor.md)<br />-   [Como adicionar conjuntos de contadores personalizados](../test/how-to-add-custom-counter-sets-using-the-load-test-editor.md)|
|**Especificar uma regra de limite usando contadores para o teste de carga:** uma regra de limite é uma regra que é definida em um contador de desempenho individual para monitorar o uso de recursos do sistema durante um teste de carga. As definições de conjunto de contadores contêm regras de limite predefinidas para muitos contadores de desempenho importantes. As regras de limite nos testes de carga comparam um valor de contador de desempenho ou com um valor constante, ou outro valor de contador de desempenho.|-   [Como adicionar uma regra de limite](../test/how-to-add-a-threshold-rule-using-the-load-test-editor.md)|
|**Atribuir nomes amigáveis aos computadores para os quais conjuntos de contadores são mapeados:** você pode adicionar marcas do computador que permitem aplicar um nome com facilidade reconhecido a um computador. As marcas são exibidas no nó **Mapeamentos de conjuntos de contadores** da árvore no Editor de Teste de Carga. Mais importante, as marcas são exibidas em relatórios do Excel que ajudam os participantes a identificar que função o computador tem no teste de carga, por exemplo, "Web Server1 em lab2" ou "SQL Server2 no escritório Phoenix".<br /><br /> Para saber mais, confira [Relatar resultados do teste de carga para comparações de testes ou análise de tendências](../test/compare-load-test-results.md).||

## <a name="use-counter-sets"></a>Usar conjuntos de contadores

As ferramentas de teste de carga coletam e representam graficamente dados de desempenho usando contadores ao longo do tempo. Os dados dos contadores são coletados em intervalos especificados pelo usuário durante a execução do teste de carga. Para saber mais, confira [Como especificar a taxa de amostragem](../test/how-to-specify-the-sample-rate-for-a-load-test.md). Você pode exibir os contadores no tempo de execução ou após a execução de teste de carga usando o *Analisador de Teste de Carga*.

Os dados dos contadores são coletados no servidor e em qualquer computador em que um teste é executado. Se você tiver configurado um conjunto de computadores agentes nos quais executar os testes, os contadores serão coletados nesses computadores também.

Há três categorias de contador: porcentagens, contagens e médias. Alguns exemplos são % de uso de CPU, contagens de bloqueio do SQL Server, e solicitações por segundo do IIS.

![Conjuntos de contadores de teste de carga](../test/media/loadtestcountersets.png)

Os dados de desempenho para solicitações HTTP individuais são relatados pelo computador que executa um teste. como um computador agente. Para solicitações, você pode monitorar dados como o tempo médio para o primeiro byte, o tempo de resposta e solicitações por segundo.

Para facilitar a coleção de dados de desempenho em um servidor Web, o Visual Studio Enterprise também fornece conjuntos de contadores denominados predefinidos, com base na tecnologia para uso em testes de carga. Esses conjuntos são úteis quando você está analisando um servidor que está executando IIS, ASP.NET ou SQL Server. Os contadores não fornecidos no conjunto padrão de contadores podem ser adicionados usando o Editor de testes de carga. É importante que você adicione os computadores ou os servidores em teste ao seu teste de carga para certificar-se de que você possa monitorar o uso de recursos nesses computadores. Para obter mais informações, confira [Como gerenciar conjuntos de contadores](../test/how-to-manage-counter-sets-using-the-load-test-editor.md).

Os resultados da análise de execuções de carga normalmente exigem o conhecimento domínio específico de uma área específica para saber quais dados coletar, onde definir regras de limite, e como saber quando uma medida reflete um problema específico no aplicativo. Para obter mais informações, confira [Sobre as regras de limite](#about-threshold-rules).

### <a name="performance-counter-sampling-interval-considerations"></a>Considerações sobre o intervalo de amostragem do contador de desempenho

Selecione um valor para a propriedade **Taxa de Amostragem** nas configurações de execução de teste de carga com base na duração do seu teste de carga. Uma taxa de amostragem menor, como o valor padrão de cinco segundos, requer mais espaço no banco de dados dos resultados de testes de carga. Para testes de carga mais longos, aumentar a taxa de amostragem reduzirá a quantidade de dados coletados. Para saber mais, confira [Como especificar a taxa de amostragem](../test/how-to-specify-the-sample-rate-for-a-load-test.md).

A seguir estão algumas diretrizes para taxas de amostragem.

|Duração do teste de carga|Taxa de amostragem recomendada|
|-|-----------------------------|
|\< 1 hora|5 segundos|
|1 a 8 horas|15 segundos|
|8−24 horas|30 segundos|
|> 24 horas|60 segundos|

## <a name="store-performance-data"></a>Armazenar dados de desempenho

Durante a execução de teste de carga, os dados do contador de desempenho são coletados e armazenados no *Repositório de Resultados do Teste de Carga*. Para saber mais, confira [Gerenciar resultados do teste de carga no repositório de resultados do teste de carga](../test/manage-load-test-results-in-the-load-test-results-repository.md).

## <a name="about-threshold-rules"></a>Sobre regras de limite

Uma *regra de limite* é uma regra definida em um contador de desempenho individual para monitorar o uso de recursos do sistema durante um teste de carga. As definições de conjunto de contadores contêm regras de limite predefinidas para muitos contadores de desempenho importantes. Para obter mais informações, confira [Usar conjuntos de contadores para ajudar a analisar dados do contador de desempenho em testes de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

## <a name="threshold-rules-and-levels"></a>Regras e níveis de limite

Ao criar regras de limite nos testes de carga, você escolhe entre dois tipos de regras:

Comparar constante&mdash;Comparar um valor do contador de desempenho com um valor de constante.

Comparar contadores&mdash;Compare um valor do contador de desempenho com outro valor do contador de desempenho.

Quando você cria regras associadas, também define os níveis para a regra. Os níveis são o limite de aviso e o limite crítico. Quando você exibe um execução do teste de carga, as violações do limite do nível de aviso são indicadas por um símbolo amarelo, e as violações do limite do nível crítico são indicadas por um símbolo vermelho.

## <a name="the-alert-if-over-property"></a>A propriedade Alertar caso seja superado

Defina a propriedade **Alertar caso seja superado** como **Verdadeiro** para indicar que exceder um limite é um problema. Por exemplo, se a regra de limite for definida em **% de tempo do processador** e você quiser ser alertado se o valor for maior que 90, use o tipo de regra **Comparar constante**, defina o **Valor de limite crítico** como 90 e defina **Alertar caso seja superado** como **Verdadeiro**.

Defina a propriedade **Alertar caso seja superado** como **Falso** para indicar que ficar abaixo de um limite é um problema. Por exemplo, se a regra de limite for definida em **Solicitações/s** e você quiser ser alertado se o valor estiver abaixo de 50, use o tipo de regra **Comparar constante**, defina o **Valor de limite crítico** como 50 e defina **Alertar caso seja superado** como **Falso**.

## <a name="see-also"></a>Consulte também

- [Como adicionar uma regra de limite](../test/how-to-add-a-threshold-rule-using-the-load-test-editor.md)
- [Analisar violações de regra de limite](../test/analyze-threshold-rule-violations-in-load-tests.md)