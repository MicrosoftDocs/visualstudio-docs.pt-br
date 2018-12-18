---
title: Emular o uso real esperado de um site para teste de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load model, specifying
- load test load model, specifying
ms.assetid: b7fae849-0538-40d1-ab35-2bb3a0fe4393
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 33f44051025310072972ef3c15a1d4a4325c0efe
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896569"
---
# <a name="emulate-expected-real-world-usage-of-a-website-or-application-in-a-load-test-using-a-test-mix-model"></a>Emular o uso real esperado de um site ou aplicativo em um teste de carga usando modelos de combinação de testes

Você usa opções de modelagem de carga para prever com maior precisão o uso real esperado de um site ou aplicativo que está passando por teste de carga. É importante fazer isso porque um teste de carga não baseado em um modelo de carga preciso pode gerar resultados enganadores.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="test-mix-model-enhancements"></a>Aprimoramentos do modelo da combinação de testes

Usando o Editor de testes de carga ou o assistente de modelo de combinação de testes, você pode especificar os seguintes tipos de combinação de testes para um cenário de teste de carga. Para saber mais, confira [Alterar o modelo de combinação de testes em um cenário](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

Você pode especificar uma das seguintes opções de modelo da combinação de testes para seu cenário de teste de carga:

-   **Baseado no número total de testes:** determina qual teste de desempenho Web ou teste de unidade é executado quando um usuário virtual inicia uma iteração de teste. No final do teste de carga, o número de vezes que um teste específico foi executado corresponde à distribuição de teste atribuída. Use esse modelo da combinação de testes quando você estiver baseando a combinação em porcentagens de transações em um log do IIS ou em dados de produção. Para saber mais, confira [Percentual baseado em testes iniciados](#BasedOnTestsStarted).

-   **Baseado no número de usuários virtuais:** determina o percentual de usuários virtuais que executarão um teste de desempenho Web ou um teste de unidade específico. A qualquer momento do teste de carga, o número usuários que estão executando um teste específico corresponde à distribuição atribuída. Use esse modelo da combinação de testes quando você estiver baseando a combinação na porcentagem de usuários que estão executando um teste específico. Para obter mais informações, consulte [Percentual baseado em usuários virtuais](#PercentageBasedonVirtualUsers).

-   **Baseado no ritmo do usuário:** no decorrer do teste de carga, cada teste de desempenho Web ou teste de unidade é executado um número especificado de vezes por usuários, por hora. Use esse modelo da combinação de testes quando quiser que os usuários virtuais executem o teste em um determinado ritmo durante o teste de carga. Para obter mais informações, consulte [Definindo o ritmo da combinação de testes](#PacingTestMix).

    > [!TIP]
    > Quando escolher **Percentual de combinação de testes** e quando escolher **Percentual baseado em usuários virtuais**? A diferença entre essas duas opções é importante quando alguns testes na combinação de testes têm uma duração muito maior do que outros testes. Nessa situação, você provavelmente deve escolher **Percentual baseado em usuários virtuais**. Essa opção ajuda a evitar um execução do teste em que aumenta a probabilidade de que muitos usuários executarão testes de longa duração. No entanto, se todos os testes tiverem durações semelhantes, você poderá escolher **Percentual de combinação de testes** com mais segurança.

-   **Baseado na ordem sequencial:** cada usuário virtual executa os testes de desempenho Web ou de unidade na ordem em que os testes são definidos no cenário. O usuário virtual continua a alternar entre os testes nesta ordem até que o teste de carga seja concluído. Para saber mais, confira [Ordem sequencial](#SequentialOrder).

###  <a name="BasedOnTestsStarted"></a> Percentual baseado em testes iniciados
 Para cada teste na combinação, você pode especificar uma porcentagem que determine com que frequência o teste será selecionado como o próximo teste a ser executado. Por exemplo, você pode atribuir os seguintes valores de porcentagem a três testes:

- TestA (50%)

- TestB (35%)

- TestC (15%)

  Se você usar essa configuração, o próximo teste a ser iniciado será baseado nas porcentagens atribuídas. Você faz isso sem levar em conta o número de usuários virtuais que estão executando atualmente cada teste.

###  <a name="PercentageBasedonVirtualUsers"></a> Percentual baseado em usuários virtuais
 Esse modelo da combinação de testes determina a porcentagem de usuários virtuais que executarão um teste específico. Se você usar esse modelo de combinação de testes, o próximo teste a ser iniciado será baseado não apenas nas porcentagens atribuídas, mas também na porcentagem de usuários virtuais que estão executando atualmente um teste específico. A qualquer momento do teste de carga, o número usuários que estão executando um teste específico corresponde à distribuição atribuída o mais próximo possível.

###  <a name="PacingTestMix"></a> Definição do ritmo da combinação de testes
 Se você especificar um ritmo para a combinação de testes, definirá uma taxa de execução de testes para cada usuário virtual para cada teste da combinação. Para cada teste, essa taxa é expressa como testes executados por usuário virtual por hora. Por exemplo, você pode atribuir o seguinte ritmo de combinação de testes para os testes a seguir:

- TestA: 4 testes por usuário por hora

- TestB: 2 testes por usuário por hora

- TestC: 0,125 testes por usuário por hora

  Se você usar o modelo de ritmo de combinação de testes, o mecanismo de tempo de execução do teste de carga garantirá que a taxa real em que os testes são iniciados seja menor ou igual à taxa especificada. Se a execução dos testes demorar muito para que o número atribuído seja concluído, um erro será retornado.

  A configuração de **Tempo de processamento entre iterações de teste** não se aplica quando você usa o ritmo de combinação de testes.

#### <a name="apply-distribution-to-pacing-delay"></a>Aplicar distribuição à definição dos atrasos
 O valor da propriedade de **Aplicar distribuição à definição dos atrasos** em um cenário de teste de carga poderá ser definida como verdadeiro ou falso:

- **Verdadeiro**: o cenário aplicará atrasos de distribuição estatística típicos especificados pelo valor na coluna **Testes por usuário por hora** na caixa de diálogo **Editar Combinação de Testes**. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

   Por exemplo, suponhamos que você tenha o valor de **Testes por Usuário por Hora** na caixa de diálogo **Editar Combinação de Testes** definido como 2 usuários por hora. Se a propriedade **Aplicar distribuição à definição dos atrasos** for definida como **Verdadeiro**, uma distribuição estatística típica será aplicada ao tempo de espera entre os testes. Os testes ainda serão executados 2 vezes por hora, mas não haverá necessariamente 30 minutos entre eles. O primeiro teste pode ser executado depois de 4 minutos e o segundo teste, depois de 45 minutos.

- **Falso**: os testes serão executados no ritmo especificado no valor na coluna **Testes por usuário por hora** na caixa de diálogo **Editar Combinação de Testes**. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

   Por exemplo, suponhamos que você tenha o valor de **Testes por Usuário por Hora** na caixa de diálogo **Editar Combinação de Testes** definido como 2 usuários por hora. Se a propriedade **Aplicar distribuição à definição dos atrasos** for definida como **Falso**, basicamente não haverá intervalo na execução dos testes. O teste será executado a cada 30 minutos. Isso garante que você execute 2 testes por hora.

  Para saber mais, confira [Como aplicar distribuição à definição dos atrasos durante o uso de um modelo de combinação de testes](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md).

###  <a name="SequentialOrder"></a> Ordem sequencial
 Selecionar a opção Com base na ordem sequencial faz com que cada usuário virtual execute todos os testes no cenário na ordem em que os testes foram definidos.

## <a name="test-iterations-property"></a>Propriedade de iterações de teste
 Nas propriedades de Configurações de Execução, você pode especificar um valor para a propriedade de iterações de teste. Esse valor é o número de iterações de teste para execução em um teste de carga. Depois que o número especificado de iterações de teste for iniciado, nenhuma iteração adicional de teste será iniciada independentemente das configurações dos perfis de carga. Depois que o número de iterações de teste especificado tiver sido concluído, o teste de carga terminará. Para saber mais, confira [Como especificar o número de iterações de teste em uma configuração de execução](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md).

## <a name="initialize-and-terminate-tests"></a>Inicializar e terminar testes
 Você pode selecionar testes para execução no início e o término da sessão de teste de carga de cada usuário virtual. Para saber mais, veja [Editar modelos de combinação de texto para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).

- **Inicializar teste**. Esse teste é executado por cada usuário virtual antes que qualquer um dos testes na combinação de testes seja executado.

- **Encerrar teste**. Esse teste é executado depois que todos os testes de um usuário virtual específico são executados.

  Observe o seguinte sobre o teste de inicialização e o teste de encerramento:

- Você pode especificar a duração do teste de carga por tempo em vez de por contagem de iterações. Nesse caso, quando a duração da execução do teste de carga terminar, o teste de encerramento não será executado.

- Se o teste de inicialização for um teste de unidade ou um teste de desempenho na Web, o estado do objeto TestContext ou WebTestContext após a conclusão do teste de inicialização será salvo. Em seguida, ele será usado como o contexto inicial para iterações de testes na combinação de testes.

- Os novos usuários, conforme definido na propriedade de Porcentagem de Novos Usuários do cenário, sempre executam o teste de inicialização, uma iteração de um teste da combinação de testes, e o teste de encerramento.

## <a name="see-also"></a>Consulte também

- [Editar modelos de combinação de testes para especificar a probabilidade de um usuário virtual executar um teste](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)
- [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)
- [Editar a combinação de testes para especificar quais testes incluir em um cenário de teste de carga](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)
- [Definir configurações de execução de teste de carga](../test/configure-load-test-run-settings.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)
- [Alterar o modelo de combinação de testes em um cenário](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)