---
title: Como anexar o Criador de perfil a um aplicativo Web ASP .NET para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e215fdd-55f8-43ef-9534-06542eefe223
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea6f642f3178e06127dc21bc115d70c68525bf0e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750131"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar dados de simultaneidade usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o Criador de perfil a um aplicativo ASP.NET e coletar dados de simultaneidade de thread e processo.  

 As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar o criador de perfil em um prompt de comando, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela **Prompt de Comando** ou adicioná-lo ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de simultaneidade, anexe o criador de perfil ao processo de trabalho do ASP.NET que hospeda o site. Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao aplicativo e o Criador de perfil deve ser desligado explicitamente. Na maioria dos casos, você precisa desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  

#### <a name="to-attach-the-profiler-to-a-aspnet-application"></a>Para anexar o Criador de perfil a um aplicativo ASP.NET  

1. Inicie o criador de perfil digitando o seguinte comando:  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md) inicializa o criador de perfil para coletar dados de contenção de recursos.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer opção da tabela a seguir com a opção **/start**.  

   |                               Opção                               |                                                                     Descrição                                                                      |
   |--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain\`]`UserName` |                           Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil.                           |
   |           [/crosssession](../profiling/crosssession.md)            |                                               Habilita a criação de perfil de processos em outras sessões de logon.                                                |
   |  [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`  |                                      Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                       |
   |       [/automark](../profiling/automark.md) **:** `Interval`       | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500. |
   |     [/events](../profiling/events-vsperfcmd.md) **:** `Config`     |       Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).       |


2. Inicie o aplicativo ASP.NET de maneira normal.  

3. Anexe o criador de perfil ao processo de trabalho do ASP.NET digitando o seguinte comando:**VSPerfCmd /attach:**`PID` [**/targetclr:**`Version`]  

   -   `PID` especifica a ID ou o nome do processo de trabalho do ASP.NET. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

   -   [/targetclr](../profiling/targetclr.md) **:** `Version` especifica a versão do CLR (Common Language Runtime) cujo perfil deverá ser criado quando mais de uma versão do tempo de execução for carregada em um aplicativo. Esse parâmetro é opcional.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções de VSPerfCmd.exe. Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções VSPerfCmd na tabela a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID`  [processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de simultaneidade reiniciando o processo de trabalho do ASP.NET ou invocando a opção **VSPerfCmd/detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte no prompt de comando:  

     **VSPerfCmd /detach**  

2.  Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>Consulte também  
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Criação de perfil de site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)



