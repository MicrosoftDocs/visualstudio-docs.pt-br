---
title: Cenários de teste de carga
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, scenarios
- load tests, user activities
- load tests, modeling scenarios
ms.assetid: fec04f2e-bf38-4d44-b2ec-fa50f58fd0d9
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 865be7c7c6371f92f85d853a7dde045274fc5efb
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896530"
---
# <a name="edit-load-test-scenarios"></a>Editar cenários de teste de carga

Um *cenário* de teste de carga especifica o padrão de carga, a combinação de testes, a combinação de navegadores e a combinação de redes. Cenários são importantes porque permitem que você configure testes para simular cargas de trabalho complexas e realistas.

Por exemplo, você pode testar um site de comércio eletrônico que tem um front-end de Internet usado por centenas de clientes simultâneos em muitas velocidades de conexão e que usam diferentes navegadores. O mesmo site também pode ter uma função de administração que é usada por funcionários internos para atualizar produtos e exibir estatísticas. Esses usuários internos acessariam normalmente o site usando o mesmo navegador e uma conexão de alta velocidade de rede local. Você deve encapsular as propriedades desses dois grupos de usuários diferentes em cenários diferentes. Cada cenário pode conter um tipo de usuário virtual. Nesse caso, um cenário de teste de carga poderá ser criado para representar clientes virtuais e outro cenário poderá ser criado para representar usuários internos virtuais de um site.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="scenario-components"></a>Componentes do cenário

Quaisquer opções de configuração iniciais que você especificar ao criar um teste de carga podem ser modificadas posteriormente no **Editor de Teste de Carga**. Você também pode adicionar novos cenários, configurações de execução e conjuntos de contadores a um teste de carga.

![Cenários de teste de carga](../test/media/loadtesteditinscenarios.png)

Os cenários contêm os seguintes componentes:

|Termo|Definição|
|-|-|
|Combinação de Navegadores|Simula que usuários virtuais acessam um site usando uma variedade de navegadores da Web.|
|Padrão de carga|Especifica o número de usuários virtuais ativos durante um teste de carga e a velocidade com que novos usuários são iniciados. Por exemplo: baseado em etapa, constante e meta.|
|Modelo de combinação de testes|Especifica a probabilidade de um usuário virtual executar um determinado teste em um cenário de teste de carga. Por exemplo: 20% de chance de executar o TestA e 80% de chance de executar o TestB. O modelo de combinação de testes deve refletir os objetivos do seu teste para um cenário específico.|
|Combinação de Testes|A combinação de testes é a seleção dos testes de unidade e de desempenho Web que constituem o cenário e a distribuição desses testes.|
|Combinação de Redes|Simula que os usuários virtuais acessam um site por uma variedade de conexões de rede. A combinação de redes oferece opções que incluem rede local (LAN), modem a cabo, entre outras opções.|

Um cenário tem várias outras propriedades que você pode editar usando o **Editor de Teste de Carga**. Para saber mais, confira [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md).

## <a name="tasks"></a>Tarefas

|Tarefas|Tópicos associados|
|-|-----------------------|
|**Adicionar pausas artificiais de interação humana em seu cenário:** tempos de processamento são usados para simular o comportamento humano que faz com que as pessoas esperem entre interações com um site. Os tempos de processamento ocorrem entre as solicitações em um teste de desempenho na Web e entre as iterações de teste em um cenário de teste de carga. Usar tempos de processamento em um teste de carga pode ser útil ao criar simulações de carga mais precisas.|-   [Editar tempos de processamento para simular atrasos de interação humana no site](../test/edit-think-times-in-load-test-scenarios.md)|
|**Especificar o número de usuários virtuais para seu cenário:** você pode configurar as propriedades do padrão de carga para especificar como a carga simulada do usuário é definida durante um teste de carga. Você obtém três padrões de carga internos: constante, etapa e baseado em metas. Escolha o padrão de carga e ajuste as propriedades até os níveis apropriados às metas do teste de carga.|-   [Editar padrões de carga para modelar atividades de usuário virtual](../test/edit-load-patterns-to-model-virtual-user-activities.md)|
|**Configurar a probabilidade de um usuário virtual que executa um teste no cenário:** é possível usar a combinação de testes, que especifica a probabilidade de um usuário virtual que executa um teste determinado em um cenário de teste de carga. Isso permite a você simular a carga de forma mais realista. Em vez de ter apenas um fluxo de trabalho com seus aplicativos, você pode ter vários fluxos de trabalho, que é uma aproximação de como os usuários finais interagem com seus aplicativos.|-   [Editar modelos de cominação de testes](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md)|
|**Adicionar ou remover um teste de unidade ou desempenho na Web para um cenário de teste de carga:** você pode adicionar ou remover um teste de unidade ou desempenho Web de um teste de carga em um cenário. Um teste de carga contém um ou vários cenários, cada um deles contém um ou mais testes de desempenho na Web ou de unidade.|-   [Editar a combinação de testes](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)|
|**Configurar a combinação de redes desejada para seu cenário:** usando a combinação de redes, é possível simular a carga de rede de modo mais realista em um cenário de teste de carga. A carga é gerada usando uma combinação heterogênea de tipos de rede, em vez de um único tipo de rede. Você cria uma situação mais parecida com a forma que os usuários finais interagem com seus aplicativos. O modelo de combinação de redes deve refletir os objetivos desse cenário.|-   [Especificar tipos de rede virtuais](../test/specify-virtual-network-types-in-a-load-test-scenario.md)|
|**Selecionar a combinação de navegadores da Web apropriada para seu cenário:** usando a combinação de navegadores, é possível simular a carga da Web de modo mais realista em um cenário de teste de carga. A carga é gerada usando uma combinação heterogênea de navegadores em vez de um único navegador. Você cria uma melhor aproximação dos navegadores que serão usados com seus aplicativos.|-   [Especificar tipos de navegadores da Web](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md)|
|**Configurar as configurações de iteração de teste para seu cenário:** é possível editar um cenário de teste de carga para definir as configurações de iteração de teste usando o Editor de Teste de Carga e a janela Propriedades. Por padrão, um cenário é definido sem iterações máximas de teste. Você tem a opção de configurar o número máximo de iterações no cenário e duração da pausa entre elas.|-   [Configurar iterações de teste para cenários](../test/configure-test-iterations-in-a-load-test-scenario.md)|
|**Configurar as configurações de atraso para seu cenário:** usando o **Editor de Teste de Carga** e a janela **Propriedades**, é possível especificar um atraso antes de iniciar um cenário em um teste de carga. Um exemplo de quando você talvez queira usar a propriedade **Atrasar tempo de início** é se precisar de um cenário para começar a produzir itens consumidos por outro cenário. Você pode atrasar o cenário de consumo para habilitar o cenário de produção a fim de popular alguns dados.|-   [Configurar atrasos de início do cenário](../test/configure-scenario-start-delays.md)|
|**Especificar computadores remotos para usar em um cenário de teste de carga:** depois de criar um teste de carga, você pode editar as propriedades do seu cenário de teste de carga para indicar que agentes de teste você deseja incluir. Para obter mais informações, consulte [Controladores e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md).|-   [Como especificar agentes de teste para usar](../test/how-to-specify-test-agents-to-use-in-load-test-scenarios.md)|

## <a name="see-also"></a>Consulte também

- [Editar testes de carga](../test/edit-load-tests.md)
- [Propriedades do cenário de teste de carga](../test/load-test-scenario-properties.md)