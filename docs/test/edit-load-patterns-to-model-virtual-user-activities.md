---
title: Padrões de carga para teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, load patterns
- load tests, scenarios
- load tests, virtual users
ms.assetid: 0ba0363b-7f50-4bde-a919-0e3bce7bc115
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: a15f771d2afa2b5c8e02eed99b3168a537365a3f
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895295"
---
# <a name="edit-load-patterns-to-model-virtual-user-activities"></a>Editar padrões de carga para modelar atividades de usuário virtual

As propriedades do padrão de carga especificam como a carga de usuário simulada é ajustada durante um teste de carga. O Visual Studio fornece três padrões de carga internos: constante, etapa e baseado em metas. Escolha o padrão de carga e ajuste as propriedades até os níveis apropriados às metas do teste de carga.

O padrão de carga é um componente de um cenário. Os cenários, com os padrões de carga definidos, compõem um teste de carga.

> [!NOTE]
> Em todos os padrões de carga, a carga que o Visual Studio gera é uma carga simulada de usuários virtuais.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="load-patterns"></a>Padrões de carga

### <a name="constant"></a>Constante

 O padrão de carga constante é usado para especificar uma carga de usuário não alterada durante o teste de carga. Por exemplo, ao executar um smoke test em um aplicativo Web, você talvez queira definir uma carga leve, constante, de 10 usuários.

#### <a name="constant-load-pattern-considerations"></a>Considerações sobre o padrão de carga constante

 Um padrão de carga de constante é usado para executar a mesma carga de usuário durante a execução de um teste de carga. Tome cuidado ao usar um padrão de carga constante com uma contagem de usuários alta; isso pode gerar uma demanda ilógica e irreal sobre seus servidores no início do teste de carga. Por exemplo, se o seu teste de carga contiver um teste na Web que comece com uma solicitação para uma página inicial e você configurar o teste de carga com uma carga constante de 1.000 usuários, o teste de carga enviará as 1.000 primeiras solicitações para a página inicial o mais rápido possível. Essa pode não ser uma simulação realista de acesso do mundo real ao seu site. Para atenuar isso, considere usar uma etapa de padrão de carga que aumente gradualmente até 1.000 usuários, ou especifique um período de aquecimento nas configurações de execução de testes de carga. Se um período de aquecimento for especificado, o teste de carga aumentará automaticamente a carga gradualmente durante o período de aquecimento. Para saber mais, confira [Configurar atrasos de início do cenário](../test/configure-scenario-start-delays.md).

### <a name="step"></a>Etapa

 O padrão de carga em etapa é usado para especificar uma carga do usuário que aumenta com o tempo até uma carga de usuário máxima definida. Para cargas em etapa, você especifica **Contagem inicial de usuários**, **Contagem máxima de usuários**, **Duração da etapa (segundos)** e **Contagem de usuário em etapas**.

 Por exemplo, uma carga em etapa com uma contagem **Usuário inicial** de um, **Contagem máxima de usuários** de 100, **Duração da etapa (segundos)** de 10 e **Contagem de usuário em etapas** de 1 cria um padrão de carga do usuário que começa em 1, aumenta em 1 a cada 10 segundos até alcançar 100 usuários.

> [!NOTE]
> Se a duração total do teste for menor que o tempo necessário para passar à carga de usuário máxima, o teste irá parar depois da duração decorrida e não alcançará o destino **Contagem Máxima de Usuários**.


 Você pode usar a meta da etapa para aumentar a carga até o servidor atingir um ponto em que o desempenho diminui significativamente. À medida que a carga aumentar, o servidor acabará ficando sem recursos. A carga em etapa é uma boa maneira de determinar o número de usuários em que ela ocorre. Com a carga em etapa, você também precisa monitorar recursos do agente atentamente para ter certeza de que os agentes possam gerar a carga desejada.

 Em geral, você deve realizar várias execuções com diferentes durações de etapa e contas de usuário em etapa de forma que possa obter boas medidas para uma determinada carga. Geralmente, as cargas mostram um pico inicial para cada etapa à medida que os usuários são adicionados. Manter a carga nessa taxa permite medir o desempenho do sistema depois que o sistema se recupera do pico inicial.

#### <a name="step-load-pattern-considerations"></a>Considerações sobre o padrão de carga em etapa

 O padrão de carga em pode ser usado para aumentar a carga no servidor ou nos servidores à medida que o teste de carga é executado de modo que você possa ver como o desempenho varia à medida que a carga de usuários aumenta. Por exemplo, para ver como será o desempenho do seu servidor ou dos servidores à medida que a carga de usuário aumenta para 2.000 usuários, você pode executar um teste de carga de 10 horas usando um padrão de carga em etapa com as seguintes propriedades:

- **Contagem inicial de usuários**: 100

- **Contagem máxima de usuários**: 2.000

- **Duração da etapa (segundos)**: 1.800

- **Tempo de rampa de etapa (segundos)**: 20

- **Contagem de usuário em etapas**: 100

  Essas configurações executam o teste de carga durante 30 minutos (1.800 segundos) em cargas de 100, 200, 300 e até 2.000 usuários. A propriedade **Tempo de rampa de etapa** deve ser mencionada, porque é única dessas propriedades não disponível para seleção no **Novo Assistente de Teste de Carga**. Essa propriedade permite que o aumento de uma etapa para a seguinte (por exemplo, de 100 para 200 usuários) ocorra gradualmente, e não de imediato. No exemplo, a carga de usuário seria aumentada de 100 para 200 usuários durante um período de 20 segundos (um aumento de cinco usuários por segundo). Para saber mais, confira [Como especificar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa](../test/how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern.md).

### <a name="goal-based"></a>Baseado em metas

 Um padrão de carga baseado em metas se assemelha ao padrão em etapa, mas ajusta a carga de usuário com base nos limites do contador de desempenho em comparação com os ajustes de carga de usuário periódicos. As cargas baseadas em meta são úteis para várias finalidades diferentes:

- Maximizando saída dos agentes: meça a métrica limitadora principal no agente para maximizar a saída dos agentes. Normalmente, ela é CPU; porém, também pode ser memória.

- Atingindo certo nível de recurso de destino, normalmente CPU, no servidor de destino, e medindo a produtividade nesse nível. Isso permite fazer comparações de execução a execução de produtividade dado um nível consistente de uso de recursos no servidor.

- Atingindo um nível de produtividade de destino no servidor.

  Na tabela a seguir, um exemplo mostra um padrão baseado em meta com as seguintes configurações de propriedades:

|Grupo de propriedades|Propriedade|Valor|
|-|--------------|-|
|Contador de desempenho|Categoria|Processador|
|Contador de desempenho|Computador|ContosoServer1|
|Contador de desempenho|Contador|% de tempo do processador|
|Contador de desempenho|Instância|_Total|
|Intervalo-alvo para o contador de desempenho|Alto nível|90|
|Intervalo-alvo para o contador de desempenho|Baixo nível|70|
|Limites de contagem de usuários|Contagem inicial de usuários|1|
|Limites de contagem de usuários|Contagem máxima de usuários|100|
|Limites de contagem de usuários|Decremento máximo da contagem de usuários|5|
|Limites de contagem de usuários|Incremento máximo da contagem de usuários|5|
|Limites de contagem de usuários|Contagem mínima de usuários|1|

 Essas configurações fazem o **Analisador de Teste de Carga** ajustar a carga de usuário entre 1 e 100 durante uma execução de teste de forma que o **Contador** para `% Processor Time` do WebServer01 fique entre `70%` e `90%.`

 O tamanho de cada ajuste de carga do usuário é determinado pelas configurações **Incremento máximo da contagem de usuários** e **Decremento máximo da contagem de usuários**. Os limites de contagem do usuário são definidos pelas propriedades **Contagem máxima de usuários** e **Contagem mínima de usuários**.

#### <a name="goal-based-load-pattern-considerations"></a>Considerações sobre o padrão de carga baseado em meta

 Um padrão de carga baseado em meta é útil quando você deseja determinar o número de usuários compatível com seu sistema antes de atingir certo nível de utilização de recursos. Essa opção funciona melhor quando você já identificou o recurso limitador (ou seja, o gargalo) no seu sistema.

 Por exemplo, suponhamos que você saiba que o recurso limitador em seu sistema é a CPU no servidor de banco de dados e queira ver quantos usuários podem ser compatíveis quando a CPU no servidor de banco de dados está aproximadamente 75 por cento ocupada. Você poderia usar um padrão de carga baseado em meta que tem o objetivo de manter o valor do contador de desempenho "% de tempo do processador" entre 70 e 80 por cento.

 Algo a ser observado é se algum outro recurso está limitando a produtividade do sistema. Esses recursos podem fazer a meta especificada pelo padrão de carga baseado em meta jamais ser alcançada. Além disso, a carga de usuário continuará crescendo até o valor especificado para a **Contagem máxima de usuários** ser atingida. Como essa não costuma ser a carga desejada, tome cuidado na escolha do contador de desempenho no padrão de carga baseado em meta.

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Especificando o padrão de carga inicial para o teste de carga:** ao criar um teste de carga usando o **Novo Assistente de Teste de Carga**, você seleciona um padrão de carga.|-   [Alterar o padrão de carga](../test/edit-load-patterns-to-model-virtual-user-activities.md#change-the-load-pattern)|
|**Editando o padrão de carga para o teste de carga:** depois de criar o teste de carga, você poderá editar o padrão de carga no **Editor de Teste de Carga**.|-   [Como especificar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa](../test/how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern.md)|
|**Especificando se os usuários virtuais no cenário do teste de carga devem incluir dados de cache na Web:** você pode alterar a propriedade **Percentual de novos usuários** para afetar a maneira como o teste de carga simula o armazenamento em cache na Web que seria executado por um navegador da Web para os usuários virtuais.|-   [Como especificar o percentual de usuários virtuais que usam dados de cache da Web](../test/how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data.md)|
|**Especificando o tempo de rampa de etapa para um padrão de carga em etapa:** a propriedade **Tempo de rampa de etapa** permite que o aumento de uma etapa para a próxima (por exemplo, de 100 para 200 usuários) ocorra gradativamente e não de imediato.|-   [Como especificar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa](../test/how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern.md)|

## <a name="change-the-load-pattern"></a>Alterar o padrão de carga

 Depois de criar seu teste de carga com o **Novo Assistente de Teste de Carga**, você poderá usar o **Editor de Teste de Carga** para alterar as propriedades do padrão de carga associadas a um cenário para níveis que atendam às suas necessidades de teste.

> [!NOTE]
> Para obter uma lista completa das propriedades de cenário de teste de carga e suas descrições, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).


 Um padrão de carga especifica o número de usuários virtuais ativos durante um teste de carga e a taxa em que os novos usuários são adicionados. Você pode escolher um dos três padrões disponíveis: padrão em etapa, constante e baseado em meta. Para saber mais, confira [Especificar o número de usuários virtuais com padrões de carga em um cenário de teste de carga](../test/edit-load-patterns-to-model-virtual-user-activities.md).

> [!NOTE]
> Você também pode alterar as propriedades de carga programaticamente usando um plug-in de teste de carga. Para saber mais, confira [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md).


### <a name="to-change-the-load-pattern"></a>Para alterar o padrão de carga

1.  Abra um teste de carga.

2.  No **Editor de Teste de Carga**, na pasta *Cenários*, expanda o cenário cujo padrão de carga você deseja editar e escolha o padrão de carga do cenário.

    > [!NOTE]
    > A expressão do nó do padrão de carga, como ele é exibido na árvore de cenário do teste de carga, reflete o perfil de carga que você escolheu ao criar o teste de carga. Ela pode ser **Perfil de carga constante** ou **Perfil da carga em etapa**.

3.  Pressione **F4** para exibir a janela **Propriedades**.

     As categorias **Padrão de carga** e **Parâmetros** são exibidas na janela **Propriedades**.

4.  (Opcional) Altere propriedade **Padrão** na categoria **Padrão de carga**.

     As opções escolhidas para a propriedade **Padrão** são **Etapa**, **Constante** e **Baseadas em meta**. Para saber mais sobre os tipos de padrão de carga, confira [Especificar o número de usuários virtuais com padrões de carga em um cenário de teste de carga](../test/edit-load-patterns-to-model-virtual-user-activities.md).

5.  (Opcional) Na categoria **Parâmetros**, altere os valores.

    > [!NOTE]
    > Os valores que você pode definir para **Parâmetros** mudam de acordo com o valor selecionado para a propriedade **Padrão**.

6.  Depois de alterar as propriedades, escolha **Salvar** no menu **Arquivo**. Você pode executar o teste de carga com o novo padrão de carga.

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)
- [Como especificar o percentual de usuários virtuais que usam dados de cache da Web](../test/how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data.md)
- [Como especificar a propriedade de tempo de rampa de etapa para um padrão de carga de etapa](../test/how-to-specify-the-step-ramp-time-property-for-a-step-load-pattern.md)