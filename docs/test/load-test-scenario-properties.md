---
title: Carregar propriedades do cenário de teste
ms.date: 10/19/2016
ms.topic: reference
helpviewer_keywords:
- load tests, properties
- load tests, scenarios
ms.assetid: 4414a638-1fa2-40ad-b1f4-b99f90b62e62
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 65508c3a7594c0943b80fbbb898c62b0fc013557
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894593"
---
# <a name="load-test-scenario-properties"></a>Propriedades do cenário de teste de carga

Altere as configurações das propriedades do cenário de teste de carga no Visual Studio para atender seus requisitos de teste de carga. Este artigo lista as diferentes propriedades de cenário de teste de carga por categoria.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="general"></a>Geral

|Propriedade|Definição|
|-|----------------|
|**Nome**|O nome do cenário.|

## <a name="mix"></a>Combinação

|Propriedade|Definição|
|-|----------------|
|**Combinação de navegadores**|Especifica a combinação de navegadores da Web para o teste de carga. É possível especificar diferentes tipos de navegador da Web e sua distribuição de carga.<br /><br />Escolha o botão de reticências **(…)** para abrir a caixa de diálogo **Editar Combinação de Navegadores** e use **Adicionar** e **Remover** para selecionar os tipos de navegador da Web no teste de carga.<br /><br />Para obter mais informações, confira [Especificar tipos de navegadores da Web](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md).|
|**Combinação de redes**|Especifica a combinação de redes para o teste de carga. Você pode especificar quais tipos de rede incluir e sua distribuição de carga.<br /><br />Escolha o botão de reticências **(…)** para abrir a caixa de diálogo **Editar Combinação de Redes** e use **Adicionar** e **Remover** para selecionar os tipos de rede no teste de carga.<br /><br />Para obter mais informações, confira [Especificar tipos de rede virtual](../test/specify-virtual-network-types-in-a-load-test-scenario.md).|
|**Combinação de testes**|Especifica a combinação de teste de unidade e desempenho na Web para o teste de carga. Você pode especificar quais testes incluir e sua distribuição de carga.<br /><br />Escolha o botão de reticências **(…)** para abrir a caixa de diálogo **Editar Combinação de Testes** e use **Adicionar** e **Remover** para selecionar os testes no teste de carga.<br /><br />Para obter mais informações, [Editar a combinação de testes para um cenário de teste de carga](../test/edit-the-test-mix-to-specify-which-web-browsers-types-in-a-load-test-scenario.md).|
|**Tipo de combinação de testes**|Especifica o modelo de combinação de testes para o teste de carga.<br /><br />Escolha o botão de reticências **(…)** para abrir a caixa de diálogo **Editar Combinação de Testes** e use o menu suspenso em **Modelo de combinação de testes** para selecionar o modelo de combinação de testes a ser usado no teste de carga.<br /><br />Para obter mais informações, confira [Editar modelos de combinação de testes](../test/edit-test-mix-models-to-specify-the-probability-of-a-virtual-user-running-a-test.md).|

## <a name="options"></a>Opções

|Propriedade|Definição|
|-|----------------|
|**Agentes a usar**|Especifica os agentes que você deseja que seu cenário use se você estiver executando o teste de carga remotamente. Por exemplo, talvez seja conveniente especificar um determinado conjunto de agentes para que você possa manter consistência ao analisar tendências de desempenho. Além disso, os agentes podem ser distribuídos geograficamente para que haja uma afinidade entre quais scripts eles executam e onde o agente está localizado.<br /><br />Os agentes devem ser separados por vírgulas, por exemplo, "**Agent1, Agent2, Agent3**". Deixar a propriedade em branco especifica que esse cenário deve usar todos os agentes disponíveis.<br /><br />Para obter mais informações, confira [Como especificar agentes de teste a serem usados](../test/how-to-specify-test-agents-to-use-in-load-test-scenarios.md).|
|**Aplicar distribuição à definição dos atrasos**|O valor booliano que é usado para especificar se você deseja aplicar atrasos comuns de distribuição no modelo de combinação de testes no ritmo do usuário. Essa propriedade será aplicada somente se a propriedade **Tipo de Combinação de Testes** for definida como **Com base no ritmo do usuário**.<br /><br />Para obter mais informações, confira [Como aplicar a distribuição à definição dos atrasos](../test/how-to-apply-distribution-to-pacing-delay-when-using-a-user-pace-test-mix-model.md)|
|**Troca de IPs**|O valor booliano usado para especificar se a troca de IP é usada.<br /><br />A troca de IP permite que um agente de teste envie solicitações para um servidor usando um intervalo de endereços IP diferentes. Isso simula chamadas que venham de computadores cliente diferentes. A troca de IP é importante ao testar com base em um Web farm de balanceamento de carga. A maioria dos balanceadores de carga estabelece afinidade entre um cliente e um servidor Web específico usando o endereço IP do cliente. Se todas as solicitações estiverem vindo aparentemente de um único cliente, o balanceador de carga não balanceará a carga. Para obter um bom balanceamento de carga no Web farm, verifique se as solicitações vêm de um intervalo de endereços IP.<br /><br />A troca de IP está disponível somente com o agente de teste.|
|**Número máximo de iterações de teste**|Valor numérico que é usado para especificar o número máximo de testes a serem executados no cenário. Um valor de 0 especifica que não há máximo.<br /><br />Para obter mais informações, confira [Configurar iterações de teste para cenários](../test/configure-test-iterations-in-a-load-test-scenario.md).|
|**Percentual de novos usuários**|Valor numérico que especifica a porcentagem de novos usuários ou a primeira vez dos visitantes no cenário.<br /><br />Para obter mais informações, confira [Como especificar o percentual de usuários virtuais que usam dados de cache da Web](../test/how-to-specify-the-percentage-of-virtual-users-that-use-web-cache-data.md).|
|**Perfil de processamento**|Especifica se o cenário usará a **Distribuição Normal** ou se o perfil de processamento está **Ativado** ou **Desativado**.<br /><br />Para obter mais informações, confira [Editar tempos de processamento para simular atrasos de interação humana do site](../test/edit-think-times-in-load-test-scenarios.md).|

## <a name="timing"></a>Timing

|Propriedade|Definição|
|-|----------------|
|**Atrasar tempo de início**|Um valor de tempo que indica quantas horas, minutos e segundos atrasar o início do cenário após o início do teste de carga. Se a propriedade **Desabilitar durante aquecimento** for definida como **Verdadeiro**, o tempo de espera será aplicado após a conclusão do período de aquecimento.<br /><br />Para saber mais, confira [Configurar atrasos de início do cenário](../test/configure-scenario-start-delays.md).|
|**Desabilitar durante aquecimento**|Valor booliano que é usado para especificar se o cenário deve ser executado ou não durante o valor temporal da propriedade **Duração de aquecimento** especificado na configuração da execução do teste de carga.<br /><br />Para obter mais informações sobre as propriedades da configuração da execução de teste de carga, confira [Propriedades das configurações de execução de teste de carga](../test/load-test-run-settings-properties.md).<br /><br />Para saber mais, confira [Configurar atrasos de início do cenário](../test/configure-scenario-start-delays.md).|
|**Tempos de processamento entre iterações de teste**|Valor numérico que é usado para especificar o tempo de espera em segundos entre iterações de teste.<br /><br />Para obter mais informações, confira [Editar tempos de processamento para simular atrasos de interação humana do site](../test/edit-think-times-in-load-test-scenarios.md).|

## <a name="see-also"></a>Consulte também

- [Editar cenários de teste de carga](../test/edit-load-test-scenarios.md)