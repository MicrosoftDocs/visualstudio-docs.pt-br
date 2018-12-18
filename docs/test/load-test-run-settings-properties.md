---
title: Carregar configurações de execução de teste
ms.date: 10/19/2016
ms.topic: reference
helpviewer_keywords:
- load tests, run settings
ms.assetid: de10dabb-02ed-403b-9e6f-0b735524988c
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 9b0123ba4e6f9565cc31f63a23bb0be0b5bee344
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895490"
---
# <a name="load-test-run-settings-properties"></a>Propriedades das configurações de execução de teste de carga

As configurações de execução de um teste de carga determinam uma variedade de outras configurações, incluindo a duração de teste, o nível de detalhes da coleta de resultados, e os conjuntos de contadores que são coletados quando o teste é executado. Você pode criar e armazenar várias configurações de execução para cada teste de carga e selecionar uma configuração específica a ser usada quando executar o teste. Uma configuração de execução inicial é adicionada ao teste de carga quando você cria o teste de carga usando o **Novo Assistente de Teste de Carga**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

As tabelas a seguir descrevem as várias propriedades para configurações de execução do teste de carga. Você pode alterar essas propriedades para atender aos seus requisitos específicos de teste de carga.

Para obter mais informações, confira [Definir as configurações de execução de teste de carga](../test/configure-load-test-run-settings.md).

## <a name="general-properties"></a>Propriedades gerais

|Propriedade|Definição|
|-|----------------|
|**Descrição**|Uma descrição das configurações de execução.|
|**Máximo de erros por tipo**|O número máximo de erros por tipo para salvar para o teste de carga.<br /><br /> Você pode aumentar esse número se for necessário, mas isso também aumentará o tamanho e o tempo de processamento do resultado do teste de carga.|
|**Máximo de URLs de solicitação reportadas**|O número máximo de urls exclusivas de solicitação de teste de desempenho na Web no qual reportar resultados neste teste de carga.<br /><br /> Você pode aumentar esse número se for necessário, mas isso também aumentará o tamanho e o tempo de processamento do resultado do teste de carga.|
|**Violações de limite máximo**|O número máximo de violações de limite para salvar para esse teste de carga.<br /><br /> Você pode aumentar esse número se for necessário, mas isso também aumentará o tamanho e o tempo de processamento do resultado do teste de carga.|
|**Executar testes de unidade no domínio do aplicativo**|Um valor booliano que determina se cada assembly de teste de unidade será executado em um domínio de aplicativo separado quando o teste de carga contém testes de unidade. A configuração padrão é True.<br /><br /> Se os testes de unidade não exigirem um domínio de aplicativo separado ou um arquivo app.config para funcionar corretamente, os testes de unidade poderão ser executados mais rapidamente definindo o valor dessa propriedade para `False`.|
|**Nome**|O nome da configuração de execução como aparece no nó **Configurações de Execução** do **Editor de teste de carga**.|
|**Nível de validação**|Isso define o nível mais alto da regra de validação que será executado em um teste de carga. As regras de validação são associadas às solicitações de teste de desempenho na Web. Cada regra de validação tem um nível de validação associado: **Alto**, **Médio** ou **Baixo**. Essa configuração de execução do teste de carga especificará quais regras de validação serão executadas enquanto o teste de desempenho na Web for executado no teste de carga. Por exemplo, se essa configuração de execução for definida como **Médio**, todas as regras de validação marcadas como **Médio** ou **Baixo** serão executadas.|

## <a name="logging-properties"></a>Propriedades de log

|Propriedade|Definição|
|-|----------------|
|**Máximo de logs de teste**|Especifica o número máximo de logs de teste para salvar para o teste de carga. Quando o valor inserido para o número máximo de logs de teste for atingido, o teste de carga parará de coletar logs. Portanto, os logs serão coletados no início de teste, não no final. O teste de carga continuará sendo executado até ser concluído.|
|**Salvar frequência de logs para testes concluídos**|Especifica a frequência com que o log de teste será gravado. O número que indica que um de cada número inserido de testes será salvo no log de teste. Por exemplo, inserindo o valor de dez especifica que o décimo, vigésimo, trigésimo etc. será gravado no log de teste. Definindo o valor como 0 especifica que nenhum log de teste será salvo.|
|**Salvar log em caso de falha do teste**|Um valor booliano que determina se os logs de teste são salvos se um teste falhar em um teste de carga. O padrão é `True`.<br /><br /> Para obter mais informações, confira [Como especificar se as falhas no teste são salvas em logs de teste](../test/how-to-specify-if-test-failures-are-saved-to-test-logs.md)|

 Para obter mais informações, confira [Modificar as configurações de log de teste de carga](../test/modify-load-test-logging-settings.md).

## <a name="results-properties"></a>Propriedades de resultados

|Propriedade|Definição|
|-|----------------|
|**Tipo de armazenamento**|A forma de armazenar os contadores de desempenho que são obtidos em um teste de carga. As opções são as seguintes:<br /><br /> -   **Banco de dados** – Requer um banco de dados SQL que tenha um **Repositório de Resultados de Teste de Carga**.<br />-   **Nenhum**.|
|**Armazenamento de detalhes de medição de tempo**|Usado para determinar quais detalhes serão armazenados no **Repositório de Resultados de Teste de Carga**. Três valores estão disponíveis:<br /><br /> -   **AllIndividualDetails** – Coleta e armazena valores de medição de tempo individuais para cada teste, transação e página executados ou emitidos durante o teste de carga no **Repositório de Resultados de Teste de Carga**. É necessário quando você pretende usar o **Gráfico de Atividade de Usuário Virtual** no **Analisador de Teste de Carga**.<br />     Para saber mais, confira [Análise da atividade de usuário virtual na exibição Detalhes](../test/analyze-load-test-virtual-user-activity-in-the-details-view.md).<br />-   **Nenhum** – Não coleta valores de medição de tempo individuais. É o valor padrão para a Atualização 4 do Visual Studio 2013 e versões posteriores.<br />-   **StatisticsOnly** – Coleta e armazena somente as estatísticas em vez de armazenar os valores de medição de tempo individuais para cada teste, transação e página executados ou emitidos durante o teste de carga no **Repositório de Resultados de Teste de Carga**.<br /><br /> Para saber mais, confira [Como especificar a propriedade de armazenamento dos detalhes de medição de tempo](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md).|

## <a name="sql-tracing-properties"></a>Propriedades do rastreamento do SQL

|Propriedade|Definição|
|-|----------------|
|**Duração mínima das operações de SQL rastreadas**|A duração mínima de uma operação SQL a ser capturada pelo Rastreamento do SQL, em milissegundos. Por exemplo, isso permite ignorar operações que terminam rapidamente se você estiver tentando localizar operações SQL que são lentas sob carga.|
|**String de conexão do rastreamento SQL**|A cadeia de conexão que é usada para acessar o banco de dados a ser rastreado.|
|**Diretório do rastreamento SQL**|O local onde o arquivo do Rastreamento SQL é colocado quando o rastreamento termina. Esse diretório deve ter permissões de gravação para o SQL Server e permissões de leitura para o controlador.|
|**Rastreamento SQL habilitado**|Isso habilita o rastreamento de operações SQL. O valor padrão é `False`.|

## <a name="test-iterations-properties"></a>Propriedades das iterações de teste

|Propriedade|Definição|
|-|----------------|
|**Iterações de teste**|Especifica o número total de teste individuais para executar antes que o teste de carga seja concluído. Essa propriedade só se aplica quando a propriedade “Usar iterações de teste” é `True`.|
|**Usar iterações de teste**|Se Usar iterações de teste for `True`, o teste de carga será executado até que o número de testes individuais concluídos no teste de carga atinja o número especificado de pela propriedade “Iterações de teste”. Nesse caso, as configurações baseadas em tempo, que são Duração do aquecimento, Duração da execução e Duração do desaquecimento, são ignoradas. Se “Usar iterações de teste” for `False`, todas as configurações de tempo se aplicarão, e "Iterações teste” é ignorada.|

 Para saber mais, confira [Como especificar o número de iterações de teste em uma configuração de execução](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md).

## <a name="timing-properties"></a>Propriedades de tempo

|Propriedade|Definição|
|-|----------------|
|**Duração do desaquecimento**|A duração do período de desaquecimento do teste, expressa no formato hh:mm:ss. Os testes individuais em um teste de carga podem ainda estar em execução quando o teste de carga é concluído. Durante o período de desaquecimento, esses testes podem continuar até que sejam concluídos ou o até o término do período de desaquecimento ser atingido. Por padrão, não existe período de desaquecimento, e os testes individuais são encerrados quando o teste de carga termina com base na configuração de Duração da execução.|
|**Duração da execução**|A duração do teste, no formato hh:mm:ss.|
|**Taxa de amostragem**|O intervalo no qual capturar valores do contador de desempenho, no formato hh:mm:ss.<br /><br /> Para saber mais, confira [Como especificar a taxa de amostragem](../test/how-to-specify-the-sample-rate-for-a-load-test.md).|
|**Duração do aquecimento**|O período entre o início do teste e quando amostras de dados começam a ser gravadas, no formato hh:mm:ss. Isso é frequentemente usado para carregar usuários virtuais em incrementos para atingir determinado nível de carga antes de gravar valores de exemplo. Os valores de exemplo que são capturados antes do término do período de aquecimento sejam mostrados no **Analisador de Teste de Carga**.|

## <a name="webtest-connections-properties"></a>Propriedades de conexões WebTest

|Propriedade|Definição|
|-|----------------|
|**Modelo de conexão do WebTest**|Controla o uso de conexões do agente de teste de carga ao servidor Web para testes de desempenho na Web que são executados em um teste de carga. Três opções de modelo de conexão de teste de desempenho na Web estão disponíveis:<br /><br /> – O modelo **Conexões por usuário** simula o comportamento de um usuário que está usando um navegador real. Quando o Internet Explorer 6 ou o Internet Explorer 7 é simulado, cada usuário virtual que está executando um teste de desempenho na Web usa uma ou duas conexões dedicadas ao servidor Web. A primeira conexão é estabelecida quando a primeira solicitação no teste de desempenho na Web é emitida. Uma segunda conexão pode ser usada quando uma página contiver mais de uma solicitação dependente. Essas solicitações são emitidas em paralelo usando as duas conexões. Essas conexões são reutilizadas para solicitações subsequentes no teste de desempenho na Web. As conexões são fechadas quando o teste de desempenho na Web é concluído. Uma desvantagem desse modelo é que o número de conexões que é mantido aberto no computador do agente pode ser alto (até duas vezes a carga do usuário). Consequentemente, os recursos que são necessários para oferecer suporte a essa contagem alta de conexão podem limitar a carga do usuário que pode ser gerada por um único agente de teste de carga. Quando o Internet Explorer 8 é simulado, seis conexões simultâneas são aceitas.<br />– O modelo **Pool de conexões** preserva os recursos do agente de teste de carga compartilhando conexões com o servidor Web entre vários usuários virtuais do teste de desempenho Web. Se a carga do usuário for maior que o tamanho do pool de conexões, os testes de desempenho na Web que são executados por usuários virtuais diferentes compartilharão uma conexão. Isso poderia significar que um teste de desempenho na Web pode ter de esperar antes de emitir uma solicitação quando outro teste de desempenho na Web estiver usando a conexão. O tempo médio que um teste de desempenho na Web espera antes de enviar uma solicitação é acompanhado pelo contador de desempenho de teste de carga Tempo Médio de Espera por Conexão. Esse número deve ser menor que o tempo médio de resposta para uma página. Se não for, o tamanho do pool de conexões provavelmente é muito pequeno.<br />– O modelo **Conexões por iteração do teste** especifica o uso de conexões dedicadas para cada iteração de teste.|
|**Tamanho do pool de conexão do WebTest**|Especifica o número máximo de conexões para fazer entre o agente de teste de carga e o servidor Web. Isso se aplica apenas ao modelo **Pool de conexões**.|

##  <a name="change-run-setting-properties"></a>Alterar as propriedades da configuração de execução
 Você pode adicionar mais configurações de execução ao teste de carga com configurações de propriedade diferentes para que possa executar o teste de carga em condições diferentes. Por exemplo, você pode adicionar uma nova configuração de teste e usar uma taxa de amostragem diferente ou especificar uma duração de execução mais longa. Você só pode usar uma configuração de execução de cada vez e deve especificar que configuração de execução usar tornando-a ativa. Para obter um exemplo, confira [Como selecionar a configuração de execução ativa para um teste de carga](../test/how-to-select-the-active-run-setting-for-a-load-test.md).

### <a name="to-change-run-settings"></a>Para alterar as configurações de execução

1.  Abra um teste de carga.

2.  Expanda a pasta **Configurações de Execução**.

3.  Escolha um nó de **Configurações de Execução**.

4.  No menu **Exibir**, escolha **Janela de Propriedades**.

     A **Janela de Propriedades** é exibida e as propriedades da configuração de execução selecionada são exibidas.

5.  Use a **Janela de Propriedades** para alterar as configurações de execução. Por exemplo, altere a duração da execução para **00:05:00** a fim de executar o teste por cinco minutos.

    > [!NOTE]
    > Para obter uma lista completa das propriedades das configurações de execução e suas descrições, confira [Propriedades das configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).

6.  Quando terminar de alterar as propriedades, salve o teste de carga. No menu **Arquivo**, clique em **Salvar**.

> [!NOTE]
> Os mapeamentos do conjunto de contadores também fazem parte das configurações de execução. Para saber mais, confira [Especificar os conjuntos de contadores e as regras de limite para computadores em um teste de carga](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md).

## <a name="see-also"></a>Consulte também

- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)