---
title: Coletar informações de diagnóstico usando configurações de teste
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, configuring run settings
ms.assetid: 0c86918b-cd63-4468-8f49-6d547a1276dc
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 288d1ce5511d33a48006c97030d2b9c2f12ec88c
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895204"
---
# <a name="collect-diagnostic-information-using-test-settings"></a>Coletar informações de diagnóstico usando configurações de teste

Você pode usar *Configurações de teste* no Visual Studio para coletar dados adicionais quando você executa os testes. Por exemplo, você pode querer fazer uma gravação de vídeo enquanto executa seu teste. Há adaptadores de dados de diagnóstico para:

-   Coletar cada etapa de ação IU em formato de texto

-   Gravar cada ação de interface de usuário para reprodução

-   Coletar informações do sistema

-   Coletar dados de log de eventos

-   Coletar dados do IntelliTrace para ajudar a isolar bugs não reproduzíveis

Os adaptadores de dados de diagnóstico também podem ser usados para alterar o comportamento de um computador de teste. Por exemplo, com uma configuração de teste no Visual Studio, você pode emular vários gargalos de topologia de rede para avaliar o desempenho do aplicativo de sua equipe.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="use-test-settings-with-visual-studio"></a>Usar configurações de teste com o Visual Studio

Para executar a unidade, interface do usuário codificado, desempenho na Web ou testes de carga usando o Visual Studio, você pode adicionar, configurar e selecionar as configurações de teste para utilizar quando executar os testes. Para executar testes, coletar dados ou afetar remotamente um computador de teste, você deve especificar um controlador de teste para usar nas configurações de teste. O controlador de teste tem agentes que podem ser usados para cada função nas configurações de teste.

## <a name="diagnostic-data-adapter-details"></a>Detalhes do adaptador de dados de diagnóstico

A tabela a seguir fornece uma visão geral das várias maneiras que os adaptadores de dados de diagnóstico podem ser configurados para usar com funções de computador local ou remoto.

|Adaptador de dados de diagnóstico usado na configuração de teste|Teste manuais no computador local|Testes Automatizados|Teste manuais: coletando dados usando um conjunto de funções e um ambiente|Observações|
|-|-|-|-|-|
|**Proxy de Cliente do ASP.NET para IntelliTrace e Impacto de Teste:** esse proxy permite que você colete informações sobre as chamadas HTTP de um cliente para um servidor Web para os adaptadores de dados de diagnóstico do IntelliTrace e de Impacto de Teste.|Sim|Sim|Sim|– Use isso somente enquanto adaptadores de dados de diagnóstico do impacto de teste ou IntelliTrace são selecionados para uma função de cliente.|
|**Criador de Perfil do ASP.NET:** você pode criar uma configuração de teste que inclui a criação de perfis do ASP.NET, que coleta dados de desempenho em aplicações Web ASP.NET.|Não|Sim (veja observações)|Não|– Este adaptador de dados de diagnóstico tem suporte apenas quando você executa testes de carga do Visual Studio.|
|**Cobertura de código:** você pode criar uma configuração de teste que inclui informações de cobertura de código usadas para investigar quanto de seu código é abordado por teste.|Não|Sim (veja observações)|Não|– Você pode usar a cobertura de código somente ao executar um teste automatizado do Visual Studio ou de *mstest.exe* e somente do computador que executa o teste. A coleção remota não tem suporte.<br />– A coleta de dados de cobertura de código não funcionará se você também tiver a configuração de teste definida para coletar informações do IntelliTrace. **Observação:** esse adaptador de dados de diagnóstico só se aplica às configurações de teste do Visual Studio. Ele não é usado para configurações de teste no Microsoft Test Manager. Além disso, este adaptador é para compatibilidade com projetos de teste do Visual Studio 2010. **Observação:** para compatibilidade, a cobertura de código se aplica quando testes automatizados são executados do Microsoft Test Manager ou em um agente de teste remoto do Visual Studio usando o MSTest Runner herdado.|
|**Log de eventos:** você pode definir uma configuração de teste para incluir a coleta de logs de eventos nos resultados do teste.|Sim|Sim|Sim||
|**IntelliTrace:** você pode configurar o adaptador de dados de diagnóstico para que o *IntelliTrace* colete informações de diagnóstico específicas de rastreamento para ajudar a isolar os erros que são difíceis de reproduzir. Isso cria um arquivo IntelliTrace que contém essas informações. Um arquivo do IntelliTrace com uma extensão *.iTrace*. Quando um teste falha, você pode criar um erro. O arquivo do IntelliTrace salvo junto com os resultados do teste é automaticamente vinculado a este bug. Os dados coletados no arquivo do IntelliTrace aumentam a produtividade de depuração reduzindo o tempo necessário para reproduzir e diagnosticar um erro no código. Nesse arquivo do IntelliTrace, a sessão local pode ser simulada em outro computador. Isso reduz o risco de um bug ser irreproduzível.|Sim|Sim|Sim|– Se você habilitar a coleta de dados do IntelliTrace, a coleta de dados de cobertura de código não funcionará.<br />– Se você usar o IntelliTrace para uma função de cliente da Web, também deverá selecionar o adaptador de dados de diagnóstico Proxy de Cliente do ASP.NET para IntelliTrace e Impacto de Teste.<br />– Somente as seguintes versões do IIS têm suporte: IIS 7.0, IIS 7.5 e IIS 8.0.|
|**Emulação de rede:** você pode especificar que você deseja colocar uma carga artificial de rede em seu teste usando uma configuração de teste. A emulação de rede afeta a comunicação para e do computador emulando uma velocidade de conexão de rede específica, como a conexão discada. |Não|Sim (veja observações)|Não|Você pode usar o adaptador de dados de diagnóstico de emulação de rede para uma função de cliente ou do servidor. Você não precisa usar o adaptador em ambas essas funções que se comunicam. **Observação:** esse adaptador de dados de diagnóstico só se aplica às configurações de teste do Visual Studio. Ele não é usado para configurações de teste no Microsoft Test Manager. **Observação:** a emulação de rede não pode ser usada para aumentar a velocidade de conexão de rede. **Aviso:** se você incluir o adaptador de dados de diagnóstico de emulação de rede nas configurações de teste e se pretende usar no seu computador local, então também deverá associar o driver de emulação de rede para um dos adaptadores de rede do computador. O driver de emulação de rede é necessário para que o adaptador de dados de diagnóstico de emulação de rede funcione. O driver de emulação de rede é instalado e associado ao seu adaptador de duas maneiras: <ul><li>**Driver de emulação de rede instalado com o Agente de Teste do Microsoft Visual Studio:** o Agente de Teste do Visual Studio pode ser usado em computadores remotos e no seu computador local. Quando você instala o Visual Studio Test Agent, o processo de instalação inclui uma etapa de configuração que associa o driver de emulação de rede em seu cartão de rede. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).</li><li>**Driver de emulação de rede instalado com o Microsoft Visual Studio Test Professional:** quando você usar a emulação de rede pela primeira vez, será solicitada a associação do driver de emulação de rede a uma placa de rede.</li></ul> Você também pode instalar o driver de emulação de rede de linha de comando em seu computador local sem instalar o agente de teste do Visual Studio, usando o seguinte comando: **VSTestConfig NETWORKEMULATION /install** **Aviso:** o adaptador de emulação de rede é ignorado por testes de carga. Em vez disso, os testes de carga usam as configurações especificadas na mistura de rede do cenário de teste de carga.|
|**Informações do sistema:** uma configuração de teste pode ser definida para incluir informações sobre o computador em que o teste é executado.|Sim|Sim|Sim||
|**Impacto de teste:** você pode reunir informações sobre quais métodos do seu código de aplicativos foram usados quando um caso de teste estava sendo executado. Podem ser usadas em conjunto com as alterações feitas no código do aplicativo por desenvolvedores para determinar quais testes foram afetados pelas alterações de desenvolvimento.|Sim|Sim|Sim|– Se você usar o IntelliTrace para uma função de cliente da Web, também deverá selecionar o adaptador de dados de diagnóstico Proxy de Cliente do ASP.NET para IntelliTrace e Impacto de Teste.<br />– Somente as seguintes versões do IIS têm suporte: IIS 7.0, IIS 7.5 e IIS 8.0.|
|**Gravador de exibição:**  você pode criar uma gravação de vídeo da sessão de área de trabalho ao executar um teste. O vídeo pode ajudar outros membros de equipe a isolar problemas de aplicativo que sejam difíceis de reproduzir.|Sim|Sim (veja observações)|Sim|– Se habilitar o software do agente de teste para ser executado como um processo de um serviço, você poderá criar uma gravação de vídeo ao executar testes automatizados.|