---
title: Test Controller e requisitos de Test Agent para testes de carga
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- agents, requirements
- controllers, requirements
ms.assetid: 372d97ce-12e4-46a9-9863-da508adba68f
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 8a5cc1f58e0cbdb59458311a1b9a4390bf69bbff
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53051440"
---
# <a name="test-controller-and-test-agent-requirements-for-load-testing"></a>Requisitos do controlador de teste e do agente de teste para teste de carga

Vários tipos de teste, incluindo testes manuais, de unidade, de desempenho Web e de carga, estão integrados ao Visual Studio. O Visual Studio permite que usuários do Gerenciamento do Ciclo de Vida do Aplicativo do Visual Studio executem testes em computadores remotos usando um controlador de teste e um ou mais agentes. Consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="hardware-and-software-requirements"></a>Requisitos de hardware e software

Os computadores do agente de teste e do controlador de teste têm requisitos de hardware e software específicos. Além disso, se desejar implantar os computadores do agente de teste e do controlador de teste em vários idiomas, você deverá planejar como oferecerá suporte a esses idiomas.

### <a name="hardware-requirements"></a>Requisitos de hardware

A tabela a seguir mostra os requisitos de hardware recomendados para a implantação de um controlador de teste e de agentes de teste.

|**Configuração**|**Componente**|**CPU**|**HD**|**Memória**|
|-|-------------------|-|------------|-|
|< 500 usuários virtuais|Agente de teste|2,6 GHz|10 GB|2 GB|
|< 1000 usuários virtuais|Agente de teste|Processador duplo de 2,6 GHz|10 GB|2 GB|
|N x 1000 usuários virtuais|Agente de teste|Expandir para N agentes, cada um com 2,6 Ghz duplo|10GB|2GB|
|\< 30 computadores no ambiente de teste. Isso inclui agentes e servidores em teste.|Controlador de teste|2,6 GHz|||
|N x 30 computadores no ambiente de teste. Isso inclui agentes e servidores em teste.|Controlador de teste|N processadores de 2,6 GHz|||

> [!NOTE]
> O número de usuários virtuais variará muito de teste para teste. Isso se deve principalmente à variação nos *tempos de processamento* ou a atrasos do usuário. Para obter mais informações, confira [Editar tempos de processamento para simular atrasos de interação humana do site](../test/edit-think-times-in-load-test-scenarios.md). Em um teste de carga, os testes na Web geralmente são mais eficientes e geram mais carga que os testes de unidade. Os números da tabela anterior são válidos para execução de testes na Web com tempos de processamento de 3 a 5 segundos em um aplicativo Web comum.

As diretrizes apresentadas aqui são fornecidas como orientação geral para o planejamento de hardware. O desempenho de teste variará consideravelmente com base na quantidade de dados de teste e no número de agentes de teste. Para agentes de teste, a velocidade e a memória de CPU disponíveis limitarão a carga de teste. Os controladores de teste precisam de recursos mais potentes, dependendo do número de agentes de teste e da quantidade de dados envolvidos nos testes.

O servidor que estiver executando o Visual Studio deve ter uma conexão de rede confiável com largura de banda mínima de 1 Mbps e latência máxima de 350 ms. Não deve haver nenhum firewall entre os agentes de teste e o controlador de teste. Se seu desempenho de teste não atender às suas expectativas, considere atualizar sua configuração de hardware.

### <a name="additional-hardware-considerations"></a>Considerações adicionais sobre hardware

Os agentes de teste geram uma grande quantidade de dados nos controladores de teste, dependendo da duração e do tamanho do teste. Em geral, você deve planejar 10 GB adicionais de armazenamento em disco rígido para cada 24 horas de dados de teste.

Além do hardware recomendado aqui, você deve considerar hardware adicional para servidores importantes, como fontes de alimentação e ventoinhas redundantes.

### <a name="language-requirements"></a>Requisitos de idioma

Para evitar confusões e simplificar a operação, um controlador de teste e agentes de teste devem ser configurados para usarem o mesmo idioma do sistema operacional do computador e do Team Foundation Server. Se o agente de teste e o controlador de teste forem instalados em computadores diferentes, eles deverão ser configurados para usar o mesmo idioma. No entanto, é possível instalar outra versão de idioma do Visual Studio em um sistema operacional em inglês, desde que o idioma corresponda ao idioma de implantação do Team Foundation Server.

## <a name="monitor-agent-resources"></a>Monitorar recursos do agente

É possível monitorar computadores de agente para determinar suas necessidades de recursos observando os processos *QTAgent\*.exe* executados e escalados durantes os testes. O gargalo mais comum nos processos *QTAgent\*.exe* é a utilização da CPU. Se a utilização de CPU for consistente na altura nos noventa, então, é uma indicação que o agente está sendo carregado com peso. O próximo gargalo comum é o uso da memória. Para testes de manda, monitorar esses recursos podem ajudar a determinar se você deve melhorar os recursos dos computadores ou distribuir seus testes diferentemente.

## <a name="see-also"></a>Consulte também

- [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md)