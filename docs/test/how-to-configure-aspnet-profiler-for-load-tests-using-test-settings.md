---
title: Configurar o Criador de Perfil do ASP.NET para testes de carga
ms.date: 10/13/2016
ms.topic: how-to
helpviewer_keywords:
- test settings, ASP.NET
ms.assetid: 6832fe39-04d5-4d94-8a18-3e2730bad423
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c4f82f8f4c518a9c72399b6e28a01d112f5678c9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288202"
---
# <a name="how-to-configure-aspnet-profiler-for-load-tests-using-test-settings-in-visual-studio"></a>Como configurar o criador de perfil do ASP.NET para carregar testes usando configurações de teste no Visual Studio

Você pode usar o adaptador de dados de diagnóstico do criador de perfil do ASP.NET para coletar informações do criador de perfil do ASP.NET. Esse adaptador de dados de diagnóstico coleta dados de desempenho de aplicativos ASP.NET.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> Este adaptador de dados de diagnóstico não pode ser usado para testes que são executados usando Microsoft Test Manager (preterido no Visual Studio 2017). Você pode usar o adaptador de diagnóstico do Criador de Perfil do ASP.NET com testes de carga usando sites que exigem apenas o Visual Studio Enterprise.

O adaptador de dados de diagnóstico do criador de perfil do ASP.NET permite coletar dados do criador de perfil do ASP.NET da camada de aplicativo quando você executa um teste de carga. Você não deve executar o criador de perfis para testes de carga longos, por exemplo, que durem mais de uma hora. Isso porque o arquivo do criador de perfis pode ficar grande, talvez com centenas de megabytes. Em vez disso, execute testes de carga mais curtos usando o criador de perfil do ASP.NET, o que ainda lhe proporcionará o benefício de diagnosticar detalhadamente os problemas de desempenho.

> [!NOTE]
> O adaptador de dados de diagnóstico do criador de perfil do ASP.NET analisa o processo de IIS (Serviços de Informações da Internet). Desse modo, ele não funcionará em um servidor Web de desenvolvimento. Para analisar o site em seu teste de carga, você precisa instalar um agente de teste no computador em que o IIS está sendo executado. O agente de teste não vai gerar carga, mas será um agente apenas de coleta. Para obter mais informações, consulte [Instalar e configurar agentes de teste](../test/lab-management/install-configure-test-agents.md).

Para obter mais informações, confira [Como criar uma configuração de teste para um teste de carga distribuída](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md).

## <a name="configure-the-aspnet-profiler-for-your-test-settings"></a>Configurar o criador de perfil do ASP.NET para suas configurações do teste

Antes de executar as etapas neste procedimento, você deverá abrir as configurações de teste no Visual Studio e selecionar a página **Dados e Diagnósticos**.

1. Selecione a função a ser usada para coletar dados do criador de perfil do ASP.NET.

    > [!WARNING]
    > Essa função deve ser de um servidor Web.

2. Selecione **Criador de Perfil do ASP.NET** para permitir a coleta de dados de criação de perfil do ASP.NET e, então, escolha **Configurar**.

     A caixa de diálogo para configurar a coleta de dados de criação de perfil do ASP.NET é exibida.

3. Em **Intervalo de Amostragem do Criador de Perfil**, digite um valor que indique quantos ciclos de relógio da CPU sem interrupção aguardar entre as coletas de amostras de criação de perfil do ASP.NET.

4. Para habilitar a criação de perfil de interação de camada, selecione **Habilitar Criação de Perfil de Interação de Camada**.

     A criação de perfil de interação de camada conta o número de solicitações que são enviadas ao servidor Web para cada artefato (por exemplo, *MyPage.aspx* ou *CompanyLogo.gif*) e o tempo necessário para atender a cada solicitação. Além disso, a criação de perfil de interação de camada coleta quais conexões ADO.NET foram usadas como parte da solicitação de página, bem como quantas consultas e chamadas de procedimentos armazenados foram executadas como parte de uma prestação de serviços da solicitação.

     Dois conjuntos diferentes de informações de medição de tempo são coletados:

    - As informações de medição de tempo (Mín., Máx., Média e Total) para prestação de serviços de cada solicitação da Web.

    - As informações de medição de tempo (Mín., Máx., Média e Total) da execução de cada consulta.

Com o adaptador de dados de diagnóstico do criador de perfil do ASP.NET definido nas suas configurações de teste, você pode coletar dados de criação de perfil do ASP.NET no seu aplicativo Web ASP.NET.

## <a name="see-also"></a>Veja também

- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
- [Como criar uma configuração de teste para um teste de carga distribuída](../test/how-to-create-a-test-setting-for-a-distributed-load-test.md)
- [Controladores de teste e agentes de teste](configure-test-agents-and-controllers-for-load-tests.md)