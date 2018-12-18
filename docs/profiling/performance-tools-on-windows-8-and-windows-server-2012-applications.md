---
title: Ferramentas de Desempenho em aplicativos do Windows 8 e Windows Server 2012 | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 404a8a3f40d5d84d60fe4822fb692e4f48a57503
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220795"
---
# <a name="performance-tools-on-windows-8-and-windows-server-2012-applications"></a>Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012

Os recursos de segurança avançada a partir do Windows 8 e Windows Server 2012 exigiam alterações significativas na maneira como as ferramentas de desempenho do Visual Studio coletam dados dessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Este tópico descreve as alterações das ferramentas de desempenho a contar das plataformas Windows 8 e Windows Server 2012.

> [!NOTE]
> As ferramentas de desempenho para outras versões do Windows com suporte (Windows 7 e Windows Server 2008 R2) não foram alteradas.

## <a name="collect-data-on-uwp-apps-from-the-visual-studio-ide"></a>Coletar dados em aplicativos UWP no IDE do Visual Studio

Ao analisar um aplicativo UWP escrito em JavaScript e HTML 5, você coleta dados de instrumentação para o código JavaScript. Ao analisar um componente ou aplicativo UWP escrito em Visual C++, Visual C# ou Visual Basic, você coleta dados de amostragem para os códigos nativo e gerenciado. Você pode analisar seu aplicativo localmente ou em um computador remoto.

Não há suporte para esses recursos e opções de criação de perfil ao criar perfil de aplicativos UWP:

- Criação de perfil de aplicativos JavaScript usando o método de amostragem.
- Criação de perfil de código gerenciado e nativo usando o método de instrumentação.
- Criação de perfil de simultaneidade
- Criação de perfil de memória .NET
- TIP (criação de perfil de interação entre camadas)
- Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.
- Opções de instrumentação, tais como coleta de desempenho e dados do contador da janela ou especificação de opções de linha de comando adicionais.

Para saber mais sobre a criação de perfil de aplicativos UWP, veja os seguintes artigos:

- [Executar aplicativos UWP no computador local](../debugger/run-windows-store-apps-on-the-local-machine.md)
- [Executar aplicativos UWP em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md)
- [Introdução às ferramentas de criação de perfil](profiling-feature-tour.md)
- [Memória JavaScript](../profiling/javascript-memory.md)
- [Analisar código Visual C++, Visual C# e Visual Basic em aplicativos UWP em um computador local](https://msdn.microsoft.com/2d0c939e-0bac-48c5-b727-46f6c6113060)
- [Analisar código Visual C++, Visual C# e Visual Basic em aplicativos UWP em um dispositivo remoto](https://msdn.microsoft.com/b932a2be-11b0-40fd-b996-75c6b6a79d22)
- [Analisar os dados de desempenho de código Visual C++, Visual C# e Visual Basic em aplicativos UWP](https://msdn.microsoft.com/5de4a413-d924-425f-afc4-e1ecfb0fca18)

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-from-the-visual-studio-ide"></a>Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 do IDE do Visual Studio

A criação de perfil usando o método de instrumentação não mudou para o Windows 8.

Não há suporte para TIP (criação de perfil de interação entre camadas) usando o método de amostragem.

## <a name="collect-data-on-apps-running-on-the-windows-8-desktop-or-on-windows-server-2012-by-using-sampling-from-the-visual-studio-ide"></a>Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 usando amostragem do IDE do Visual Studio

Não há suporte para os recursos e opções de criação de perfil ao criar o perfil de aplicativos de área de trabalho do Windows 8 ou aplicativos do Windows Server 2012 usando o método de amostragem:

- TIP (criação de perfil de interação entre camadas). Há suporte para a coleta de dados TIP usando instrumentação.

- Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.

## <a name="profile-from-the-command-line"></a>Criar perfis na linha de comando

Você pode usar duas ferramentas de linha de comando para coletar dados de criação de perfil em dispositivos Windows 8 e Windows Server 2012, incluindo dispositivos que não têm uma instalação do Visual Studio:

|Nome da ferramenta|Descrição|
|---------------|-----------------|
|[VSPerf](../profiling/vsperf.md)|Coleta dados de criação de perfil de aplicativos UWP e coleta dados de criação de perfil de amostra de aplicativos da área de trabalho do Windows 8 e aplicativos do Windows Server 2012.|
|[VSPerfCmd](../profiling/vsperfcmd.md)|Coleta dados de criação de aplicativo de instrumentação, simultaneidade e interação entre camadas de aplicativos em execução na área de trabalho do Windows 8 ou do Windows Server 2012. Coleta todos os tipos de dados de perfil de versões anteriores do Windows.|

Ambas as ferramentas são instaladas com o Visual Studio para uso no computador local.

Para analisar aplicativos em dispositivos que não têm o Visual Studio instalado, faça o seguinte:

- Baixe as ferramentas como parte das Ferramentas Remotas para Visual Studio do [site do MSDN](http://go.microsoft.com/fwlink/?LinkID=219549).

- Copie e execute o programa de instalação de ferramentas do criador de perfil autônomo do seu computador do Visual Studio. Os programas de instalação estão na pasta *%VSInstallDir%\Team Tools\Performance Tools\Setups*. Escolha o programa de instalação do sistema operacional (x86/x64) do computador remoto.

> [!NOTE]
> Para coletar dados de criação de perfil TIP, você deve instalar o criador de perfil autônomo em seu computador do Visual Studio no computador remoto.

Não há suporte para os recursos e opções de criação de perfil ao criar o perfil de aplicativos do Windows 8 ou Windows Server 2012 da linha de comando:

- Coletando dados de aplicativos Web do Windows 8 e Windows Server 2012 usando o modo de amostragem com [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md).

- Coletando dados de amostragem usando VsPerfCmd.exe.

- Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.

## <a name="collect-tier-interaction-tip-data"></a>Coletar dados de TIP (interação entre camadas)

A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução de funções de aplicativos de várias camadas que se comunicam com os bancos de dados por meio de serviços do ADO.NET. Os dados são coletados apenas para chamadas de função síncronas.

**Edições do Visual Studio**

Os dados de criação de perfil de interação de camadas podem ser coletados usando qualquer edição do Visual Studio. No entanto, os dados de criação de perfil de interação de camadas só podem ser exibidos no Visual Studio Enterprise.

**Windows 8 e Windows Server 2012**

1. Para coletar os dados de interação entre camadas de aplicativos em execução na área de trabalho do Windows 8 ou do Windows Server 2012, será necessário usar o método de instrumentação.

2. Não é possível coletar dados de interação de camada de aplicativos UWP.

3. É possível incluir dados de interação de camada em todos os métodos de criação de perfil em outra versão com suporte do Windows.

**Assistente de Desempenho e Gerenciador de Desempenho**

Você deve adicionar a opção de coleta de dados de interação entre camadas para uma execução de criação de perfil do Gerenciador de Desempenho. Também é necessário adicionar o projeto, o executável ou o site ao nó de Destino do Gerenciador de Desempenho. Confira [Coletar dados de interação de camada](../profiling/collecting-tier-interaction-data.md).

**Coletando dados TIP em um computador remoto**

Para coletar os dados de interação de camadas em um computador remoto, você precisa copiar o arquivo **vs\_profiler\_**_\<Platform>_**\_**_\<Language>_**.exe** da pasta *%VSInstallDir%\Team Tools\Performance Tools\Setups* de um computador com o Visual Studio para o computador remoto e instalá-lo. Não é possível usar as ferramentas de criação de perfil no pacote de download da [Depuração Remota](../debugger/remote-debugging.md).

Você pode usar [VSPerfCmd](../profiling/vsperfcmd.md) ou [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) para coletar dados de criação de perfil.

**Relatórios TIP**

Os dados de interação entre camadas só podem ser exibidos no Microsoft Visual Studio Enterprise. Os relatórios de interação de camadas baseados em arquivo por meio de [VSPerfReport](../profiling/vsperfreport.md) não estão disponíveis.

## <a name="see-also"></a>Consulte também

[Gerenciador de Desempenho](../profiling/performance-explorer.md)
[Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)
[Criar perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)