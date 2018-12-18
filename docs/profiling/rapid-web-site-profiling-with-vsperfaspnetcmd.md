---
title: Criação de perfil do site rápida com VSPerfASPNETCmd | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- proflilng tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f0ad2c1411a47acd0219223fe928e4150368c80a
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43780677"
---
# <a name="rapid-web-site-profiling-with-vsperfaspnetcmd"></a>Criação rápida de perfil de site com VSPerfASPNETCmd

A ferramenta de linha de comando **VSPerfASPNETCmd** permite criar facilmente o perfil de aplicativos Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. Em comparação com a ferramenta de linha de comando [VSPerfCmd](../profiling/vsperfcmd.md), as opções são reduzidas, nenhuma variável de ambiente precisa ser definida e não é necessário reinicializar o computador. Usar **VSPerfASPNETCmd** é o método preferencial para a criação de perfil com o criador de perfil autônomo. Para obter mais informações, confira [Como instalar o criador de perfil independente](../profiling/how-to-install-the-stand-alone-profiler.md).

> [!NOTE]
> Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos UWP também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

 Em alguns cenários, tais como coletar dados de simultaneidade ou pausar e retomar a criação de perfil, o uso de **VSPerfCmd** é o método preferencial de criação de perfil.

> [!NOTE]
> As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do Visual Studio. Em computadores de 64 bits, use a ferramenta VSPerfASPNETCmd localizada no diretório *\Team Tools\Performance Tools* de 32 bits. Para usar ferramentas de linha de comando do criador de perfil, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela de prompt de comando ou adicioná-lo ao próprio comando. Para saber mais, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).

## <a name="profile-an-aspnet-application"></a>Criar o perfil de um aplicativo ASP.NET

Para criar o perfil de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], digite um dos comandos descritos nas seções a seguir. O site é iniciado e abre o criador de perfil para coletar dados. Exercite seu aplicativo e, em seguida, feche o navegador. Para interromper a criação de perfil, pressione a tecla **Enter** na janela do prompt de comando.

> [!NOTE]
> Por padrão, o prompt de comando não retorna após um comando **vsperfaspnetcmd**. Você pode usar a opção **/nowait** para forçar o prompt de comando a retornar. Confira [Usar a opção /NoWait](#use-the-nowait-option).

## <a name="to-collect-application-statistics-by-using-the-sampling-method"></a>Para coletar estatísticas do aplicativo usando o método de amostragem
 A amostragem é o método de criação de perfil de padrão da ferramenta **VSPerfASPNETCmd** e não precisa ser especificada na linha de comando. A seguinte linha de comando coleta estatísticas de aplicativo do aplicativo Web especificado:

 **vsperfaspnetcmd**  *websiteUrl*

## <a name="to-collect-detailed-timing-data-by-using-the-instrumentation-method"></a>Para coletar dados de tempo detalhados usando o método de instrumentação

Use a seguinte linha de comando para coletar dados de tempo detalhados de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] compilado dinamicamente:

**vsperfaspnetcmd /trace**  *websiteUrl*

Caso deseje criar perfis de arquivos .*dll* compilados estatisticamente no aplicativo Web, instrumente os arquivos usando a ferramenta de linha de comando [VSInstr](../profiling/vsinstr.md). O comando vsperfaspnetcmd /trace incluirá dados dos arquivos instrumentados.

## <a name="to-collect-net-memory-data"></a>Para coletar dados de memória do .NET

A opção **/Memory** coleta dados sobre a alocação de objetos na memória do .NET e pode coletar dados sobre o tempo de vida desses objetos. A coleta de dados de alocação é o modo padrão das opções de dados **/Memory** e não precisa ser especificado na linha de comando.

 **vsperfaspnetcmd /memory** *websiteUrl*

 Use o parâmetro **Tempo de vida** para coletar dados de tempo de vida do objeto além dos dados de alocação:

 **vsperfaspnetcmd /memory:lifetime** *websiteUrl*

 Você também pode usar a opção **/Trace** para incluir informações detalhadas de tempo com os dados de memória do .NET:

 **vsperfaspnetcmd /memory**[**:lifetime**] **/trace**`websiteUrl`

## <a name="to-collect-tier-interaction-data"></a>Para coletar dados de interação entre camadas

> [!WARNING]
> Os dados de TIP (criação de perfil de interação de camadas) podem ser coletados usando qualquer edição do Visual Studio. No entanto, os dados de criação de perfil de interação de camadas só podem ser exibidos no Visual Studio Enterprise.
>
> Para coletar dados TIP no Windows 8 ou Windows Server 2012, você deve usar a opção de instrumentação (**/trace**).

Para coletar dados de interação entre camadas com os dados de amostragem:

**vsperfaspnetcmd /tip** `websiteUrl`

Para coletar dados de interação entre camadas com os dados de instrumentação:

**vsperfaspnetcmd /trace /tip** *websiteUrl*

Para coletar dados de interação entre camadas com os dados de memória de .NET:

**vsperfaspnetcmd /memory**[**:lifetime**] **/tip**_websiteUrl_

## <a name="use-the-nowait-option"></a>Use a opção /NoWait

Por padrão, o prompt de comando não retorna após um comando **vsperfaspnetcmd**. Você pode usar a opção de sintaxe a seguir para forçar o prompt de comando a retornar. Em seguida, você pode executar outras operações na janela do prompt de comando. Para finalizar a criação de perfil, use a opção **/shutdown** em um comando **vsperfaspnetcmd**.

Para iniciar a criação de perfil:

**vsperfaspnetcmd** [*/Options*] **/nowait**_websiteUrl_

Para encerrar a criação de perfil:

**vsperfaspnetcmd /shutdown** *websiteUrl*

## <a name="additional-options"></a>Opções adicionais

Você pode adicionar qualquer uma das seguintes opções aos comandos listados anteriormente nesta seção, exceto o **vsperfaspnetcmd /shutdown**.

|Opção|Descrição|
|------------|-----------------|
|**/Output:** `VspFile`|Por padrão, o arquivo de dados de criação de perfil (.*vsp*) é criado no diretório atual com o nome de arquivo **PerformanceReport.vsp**. Use a opção /output para especificar um local diferente, nome do arquivo diferente ou ambos.|
|**/PackSymbols:Off**|Por padrão, VsPerfASPNETCmd insere símbolos (nomes de função, de parâmetro e assim por diante) no arquivo .*vsp*. Inserir os símbolos pode tornar o arquivo de dados de criação de perfil muito grande. Se você terá acesso aos arquivos .*pdb* que contêm os símbolos ao analisar os dados, use a opção /packsymbols:off para desabilitar a inserção dos símbolos.|
