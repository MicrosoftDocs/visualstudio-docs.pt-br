---
title: Criação de perfil do site rápida com VSPerfASPNETCmd | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- proflilng tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
ms.assetid: 9a9d62a6-549a-45ac-a948-76eb98586ac5
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 80acb5030c61bd986bfbd2a5f2b383ac37a25a0c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760010"
---
# <a name="rapid-web-site-profiling-with-vsperfaspnetcmd"></a>Criação de perfil do site rápida com VSPerfASPNETCmd
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta de linha de comando **VSPerfASPNETCmd** permite analisar facilmente aplicativos Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Em comparação com a ferramenta de linha de comando [VSPerfCmd](../profiling/vsperfcmd.md), as opções são reduzidas, nenhuma variável de ambiente precisa ser definida e não é necessário reinicializar o computador. Usar **VSPerfASPNETCmd** é o método preferencial para a criação de perfil com o criador de perfil autônomo. Para obter informações, consulte [Como instalar o criador de perfil autônomo](../profiling/how-to-install-the-stand-alone-profiler.md).  
  
> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  
  
 Em alguns cenários, tais como coletar dados de simultaneidade ou pausar e retomar a criação de perfil, o uso de **VSPerfCmd** é o método preferencial de criação de perfil.  
  
> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Em computadores de 64 bits, use a ferramenta de VSPerfASPNETCmd localizada no diretório \Team Tools\Performance Tools de 32 bits. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  
  
## <a name="profiling-an-aspnet-application"></a>Criando um perfil de Aplicativo ASP.NET  
 Para analisar um aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], digite um dos comandos descritos nas seções a seguir. O site é iniciado e abre o criador de perfil para coletar dados. Exercite seu aplicativo e, em seguida, feche o navegador. Para interromper a criação de perfil, pressione a tecla Enter na janela do prompt de comando.  
  
> [!NOTE]
>  Por padrão, o prompt de comando não retorna após um comando **vsperfaspnetcmd**. Você pode usar a opção **/nowait** para forçar o prompt de comando a retornar. Consulte [Usando a opção /NoWait](#UsingNoWait).  
  
## <a name="to-collect-application-statistics-by-using-the-sampling-method"></a>Para coletar estatísticas do aplicativo usando o método de amostragem  
 A amostragem é o método de criação de perfil de padrão da ferramenta **VSPerfASPNETCmd** e não precisa ser especificada na linha de comando. A seguinte linha de comando coleta estatísticas de aplicativo do aplicativo Web especificado:  
  
 **vsperfaspnetcmd**  *websiteUrl*  
  
## <a name="to-collect-detailed-timing-data-by-using-the-instrumentation-method"></a>Para coletar dados de tempo detalhados usando o método de instrumentação  
 Use a seguinte linha de comando para coletar dados de tempo detalhados de um aplicativo Web [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] compilado dinamicamente:  
  
 **vsperfaspnetcmd /trace**  *websiteUrl*  
  
 Se desejar analisar arquivos .dll compilados estatisticamente em seu aplicativo Web, você deve instrumentar os arquivos usando a ferramenta de linha de comando [VSInstr](../profiling/vsinstr.md). O comando vsperfaspnetcmd /trace incluirá dados dos arquivos instrumentados.  
  
## <a name="to-collect-net-memory-data"></a>Para coletar dados de memória do .NET  
 A opção **/Memory** coleta dados sobre a alocação de objetos na memória do .NET e pode coletar dados sobre o tempo de vida desses objetos. A coleta de dados de alocação é o modo padrão das opções de dados **/Memory** e não precisa ser especificado na linha de comando.  
  
 **vsperfaspnetcmd /memory** *websiteUrl*  
  
 Use o parâmetro **Tempo de vida** para coletar dados de tempo de vida do objeto além dos dados de alocação:  
  
 **vsperfaspnetcmd /memory:lifetime** *websiteUrl*  
  
 Você também pode usar a opção **/Trace** para incluir informações detalhadas de tempo com os dados de memória do .NET:  
  
 **vsperfaspnetcmd /memory**[**:lifetime**] **/trace**`websiteUrl`  
  
## <a name="to-collect-tier-interaction-data"></a>Para coletar dados de interação entre camadas  
  
> [!WARNING]
>  Os dados TIP (criação de perfil de interação entre camadas) podem ser coletados usando [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] ou [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)]. No entanto, os dados de criação de perfil de interação de camadas somente podem ser exibidos no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] e no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
>   
>  Para coletar dados TIP no Windows 8 ou Windows Server 2012, você deve usar a opção de instrumentação (**/trace**).  
  
 Para coletar dados de interação entre camadas com os dados de amostragem:  
  
 **vsperfaspnetcmd /tip** `websiteUrl`  
  
 Para coletar dados de interação entre camadas com os dados de instrumentação:  
  
 **vsperfaspnetcmd /trace /tip** *websiteUrl*  
  
 Para coletar dados de interação entre camadas com os dados de memória de .NET:  
  
 **vsperfaspnetcmd /memory**[**:lifetime**] **/tip**_websiteUrl_  
  
##  <a name="UsingNoWait"></a> Usando a opção /NoWait  
 Por padrão, o prompt de comando não retorna após um comando **vsperfaspnetcmd**. Você pode usar a opção de sintaxe a seguir para forçar o prompt de comando a retornar. Em seguida, você pode executar outras operações na janela do prompt de comando. Para finalizar a criação de perfil, use a opção **/shutdown** em um comando **vsperfaspnetcmd**.  
  
 Para iniciar a criação de perfil:  
  
 **vsperfaspnetcmd** [*/Options*] **/nowait**_websiteUrl_  
  
 Para encerrar a criação de perfil:  
  
 **vsperfaspnetcmd /shutdown** *websiteUrl*  
  
## <a name="additional-options"></a>Opções Adicionais  
 Você pode adicionar qualquer uma das seguintes opções aos comandos listados anteriormente nesta seção, exceto o **vsperfaspnetcmd /shutdown**.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**/Output:** `VspFile`|Por padrão, o arquivo de dados de criação de perfil (.vsp) é criado no diretório atual com o nome de arquivo **PerformanceReport.vsp**. Use a opção /output para especificar um local diferente, nome do arquivo diferente ou ambos.|  
|**/PackSymbols:Off**|Por padrão, VsPerfASPNETCmd insere símbolos (nomes de função e de parâmetro, etc.) no arquivo .vsp. Inserir os símbolos pode tornar o arquivo de dados de criação de perfil muito grande. Se você tem acesso aos arquivos .pdb que contêm os símbolos ao analisar os dados, use a opção /packsymbols:off para desabilitar a inserção dos símbolos.|



