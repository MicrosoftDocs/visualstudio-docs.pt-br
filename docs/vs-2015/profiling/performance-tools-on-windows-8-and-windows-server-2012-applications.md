---
title: Ferramentas de Desempenho em aplicativos do Windows 8 e Windows Server 2012 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a704215d-d252-4087-921b-ac81ebe2a9c9
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e02ce9a9ef06574de999620017b96d470a76e6c9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51767528"
---
# <a name="performance-tools-on-windows-8-and-windows-server-2012-applications"></a>Ferramentas de desempenho em aplicativos do Windows 8 e Windows Server 2012
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os recursos de segurança avançada do Windows 8 e Windows Server 2012 exigiam alterações significativas na maneira como as ferramentas de desempenho do Visual Studio coletam dados dessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Este tópico descreve as alterações das ferramentas de desempenho em plataformas Windows 8 e Windows Server 2012.  
  
> [!NOTE]
>  As ferramentas de desempenho para outras versões do Windows com suporte (Windows 7 e Windows Server 2008 R2) não foram alteradas.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [Coletando dados nos aplicativos da Windows Store no IDE do Visual Studio](#BKMK_Profiling_Windows_Store_apps_from_the_Visual_Studio_IDE)  
  
 [Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 do IDE do Visual Studio](#BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_from_the_Visual_Studio_IDE)  
  
- [Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 usando amostragem do IDE do Visual Studio](#BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_by_using_sampling_from_the_Visual_Studio_IDE)  
  
  [Criação de perfil da linha de comando](#BKMK_Profiling_from_the_command_line)  
  
  [Coletando dados de interação entre camadas (TIP)](#BKMK_Collecting_tier_interaction__TIP__data)  
  
##  <a name="BKMK_Profiling_Windows_Store_apps_from_the_Visual_Studio_IDE"></a> Coletando dados nos aplicativos da Windows Store no IDE do Visual Studio  
 Ao analisar um aplicativo da Windows Store escrito em JavaScript e HTML 5, você coleta dados de instrumentação para o código JavaScript. Ao analisar um componente ou aplicativo da Windows Store escrito em Visual C++, Visual C# ou Visual Basic, você coleta dados de amostragem para os códigos nativo e gerenciado. Você pode analisar seu aplicativo localmente ou em um computador remoto.  
  
 Não há suporte para esses recursos e opções de criação de perfil ao criar perfil de aplicativos da Windows Store:  
  
- Criação de perfil de aplicativos JavaScript usando o método de amostragem.  
  
- Criação de perfil de código gerenciado e nativo usando o método de instrumentação.  
  
- Criação de perfil de simultaneidade  
  
- Criação de perfil de memória .NET  
  
- TIP (criação de perfil de interação entre camadas)  
  
- Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.  
  
- Opções de instrumentação, tais como coleta de desempenho e dados do contador da janela ou especificação de opções de linha de comando adicionais.  
  
  Para obter mais informações sobre a criação de perfil de aplicativos da Windows Store, consulte os tópicos a seguir no Centro de desenvolvimento do Windows:  
  
  [Executar aplicativos da Windows Store no computador local](../debugger/run-windows-store-apps-on-the-local-machine.md)  
  
  [Executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md)  
  
  [Analisar o desempenho do aplicativo](http://msdn.microsoft.com/library/58acb30b-8428-41a6-b195-b0fdedb89575)  
  
- [Temporização de função JavaScript](http://msdn.microsoft.com/library/b2bf49fc-aea7-4d9c-8fcf-cff8b8dd0c03)  
  
- [Temporização de função JavaScript em um dispositivo remoto](http://msdn.microsoft.com/library/d78812b6-a97e-46dc-8d99-e724d1d725d8)  
  
- [Analisar dados de temporização de função JavaScript](http://msdn.microsoft.com/library/b5aea8d8-36df-47ba-a7ca-95406700ca9b)  
  
- [Analisar código Visual C++, Visual C# e Visual Basic em aplicativos da Windows Store em um computador local](http://msdn.microsoft.com/en-us/2d0c939e-0bac-48c5-b727-46f6c6113060)  
  
- [Analisar código Visual C++, Visual C# e Visual Basic em aplicativos da Windows Store em um dispositivo remoto](http://msdn.microsoft.com/en-us/b932a2be-11b0-40fd-b996-75c6b6a79d22)  
  
- [Analisar os dados de desempenho de código Visual C++, Visual C# e Visual Basic em aplicativos da Windows Store](http://msdn.microsoft.com/en-us/5de4a413-d924-425f-afc4-e1ecfb0fca18)  
  
  [Neste tópico](#BKMK_In_this_topic)  
  
##  <a name="BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_from_the_Visual_Studio_IDE"></a> Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 do IDE do Visual Studio  
 A criação de perfil usando o método de instrumentação não mudou para o Windows 8.  
  
 Não há suporte para TIP (criação de perfil de interação entre camadas) usando o método de amostragem.  
  
###  <a name="BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_by_using_sampling_from_the_Visual_Studio_IDE"></a> Coletar dados em aplicativos em execução na área de trabalho do Windows 8 ou no Windows Server 2012 usando amostragem do IDE do Visual Studio  
 Não há suporte para os recursos e opções de criação de perfil ao criar o perfil de aplicativos de área de trabalho do Windows 8 ou aplicativos do Windows Server 2012 usando o método de amostragem:  
  
-   TIP (criação de perfil de interação entre camadas). Há suporte para a coleta de dados TIP usando instrumentação.  
  
-   Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.  
  
##  <a name="BKMK_Profiling_from_the_command_line"></a> Criação de perfil da linha de comando  
 Você pode usar duas ferramentas de linha de comando para coletar dados de criação de perfil em dispositivos Windows 8 e Windows Server 2012, incluindo dispositivos que não têm uma instalação do Visual Studio:  
  
|Nome da ferramenta|Descrição|  
|---------------|-----------------|  
|[VSPerf](../profiling/vsperf.md)|Coleta dados de criação de perfil de aplicativos da Windows Store e coleta dados de criação de perfil de amostra de aplicativos da área de trabalho do Windows 8 e aplicativos do Windows Server 2012.|  
|[VSPerfCmd](../profiling/vsperfcmd.md)|Coleta dados de criação de aplicativo de instrumentação, simultaneidade e interação entre camadas de aplicativos em execução na área de trabalho do Windows 8 ou do Windows Server 2012. Coleta todos os tipos de dados de perfil de versões anteriores do Windows.|  
  
 Ambas as ferramentas são instaladas com o Visual Studio para uso no computador local.  
  
 Para analisar aplicativos em dispositivos que não têm o Visual Studio instalado, faça o seguinte:  
  
-   Baixe as ferramentas como parte das Ferramentas Remotas para Visual Studio do [site do MSDN](http://go.microsoft.com/fwlink/?LinkID=219549).  
  
-   Copie e execute o programa de instalação de ferramentas do criador de perfil autônomo do seu computador do Visual Studio. Os programas de instalação estão na pasta *%VSInstallDir%* **\Team Tools\Performance Tools\Setups**. Escolha o programa de instalação do sistema operacional (x86/x64) do computador remoto.  
  
> [!NOTE]
>  Para coletar dados de criação de perfil TIP, você deve instalar o criador de perfil autônomo em seu computador do Visual Studio no computador remoto.  
  
 Não há suporte para os recursos e opções de criação de perfil ao criar o perfil de aplicativos do Windows 8 ou Windows Server 2012 da linha de comando:  
  
-   Coletando dados de aplicativos Web do Windows 8 e Windows Server 2012 usando o modo de amostragem com [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md).  
  
-   Coletando dados de amostragem usando VsPerfCmd.exe.  
  
-   Opções de amostragem como configurar o evento de amostragem e o intervalo de tempo ou coletar dados do contador de desempenho adicional.  
  
##  <a name="BKMK_Collecting_tier_interaction__TIP__data"></a> Coletando dados de interação entre camadas (TIP)  
 A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução de funções de aplicativos de várias camadas que se comunicam com os bancos de dados por meio de serviços do ADO.NET. Os dados são coletados apenas para chamadas de função síncronas.  
  
 **Edições do Visual Studio**  
  
 Os dados de criação de perfil da interação entre camadas podem ser coletados usando [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] ou [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)]. No entanto, os dados de criação de perfil de interação de camadas somente podem ser exibidos no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] e no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
  
 **Windows 8 e Windows Server 2012**  
  
1. Para coletar os dados de interação entre camadas de aplicativos em execução na área de trabalho do Windows 8 ou do Windows Server 2012, será necessário usar o método de instrumentação.  
  
2. Não é possível coletar dados de interação de camada para aplicativos da Windows Store.  
  
3. É possível incluir dados de interação de camada em todos os métodos de criação de perfil em outra versão com suporte do Windows.  
  
   **Assistente de Desempenho e Gerenciador de Desempenho**  
  
   Você deve adicionar a opção de coleta de dados de interação entre camadas para uma execução de criação de perfil do Gerenciador de Desempenho. Também é necessário adicionar o projeto, o executável ou o site ao nó de Destino do Gerenciador de Desempenho. Consulte [Coletando dados de interação entre camadas](../profiling/collecting-tier-interaction-data.md).  
  
   **Coletando dados TIP em um computador remoto**  
  
   Para coletar dados de interação de camadas em um computador remoto, você deve copiar o **vs\_profiler\_**_\<Platform >_ **\_**  _\<Language >_**.exe** arquivo o _% VSInstallDir %_**\Team Tools\Performance Tools\Setups**pasta de um Visual Studio de máquina para o computador remoto e instalá-lo. Você não pode usar as ferramentas de criação de perfil na [as ferramentas remotas do Visual Studio](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) fazer download do pacote.  
  
   Você pode usar [VSPerfCmd](../profiling/vsperfcmd.md) ou [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) para coletar dados de criação de perfil.  
  
   **Relatórios TIP**  
  
   Dados de interação entre camadas só podem ser exibidos no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] ou IDE do [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]. Os relatórios de interação de camadas baseados em arquivo por meio de [VSPerfReport](../profiling/vsperfreport.md) não estão disponíveis.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Desempenho](../profiling/performance-explorer.md)   
 [Configurando sessões de desempenho](../profiling/configuring-performance-sessions.md)   
 [Criando perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)



