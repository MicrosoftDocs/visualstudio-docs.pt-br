---
title: Como anexar o criador de perfil a um serviço nativo para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 283a1ee1-b43e-4daf-95ae-1311925a42a8
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6add1c0837e9a1d1308f61112540d00f42617a92
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51731437"
---
# <a name="how-to-attach-the-profiler-to-a-native-service-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um serviço nativo para coletar dados de simultaneidade usando a linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para anexar o criador de perfil a um serviço nativo (C/C++) e coletar dados de simultaneidade de thread e processo usando o método de amostragem.  

> [!NOTE]
>  Os recursos de segurança aprimorados no Windows 8 e no Windows Server 2012 exigiram alterações significativas na maneira como o criador de perfil do Visual Studio coleta dados nessas plataformas. Os aplicativos da Windows Store também requerem novas técnicas de coleta. Consulte [Ferramentas de desempenho em aplicativos do Windows 8 e do Windows Server 2012](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).  

> [!NOTE]
>  As ferramentas de linha de comando das Ferramentas de Criação de Perfil ficam localizadas no subdiretório \Team Tools\Performance Tools do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar o criador de perfil em um prompt de comando, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela **Prompt de Comando** ou ao próprio comando. Para obter mais informações, consulte [Especificando o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Enquanto o criador de perfil estiver anexado ao serviço, você pode pausar e retomar a coleta de dados. Para concluir uma sessão de criação de perfil, o Criador de perfil não pode mais estar anexado ao serviço e o Criador de perfil deve ser desligado explicitamente.  

## <a name="attaching-the-profiler"></a>Anexando o Criador de perfil  
 Para anexar o criador de perfil a um serviço nativo, use as opções **VSPerfCmd/start** e **/attach** para inicializar o criador de perfil e anexá-lo ao aplicativo de destino. Você pode especificar **/start** e **/attach** e suas opções respectivas em uma única linha de comando. Você também pode adicionar a opção **/globaloff** para pausar a coleta de dados no início do aplicativo de destino. Depois, você usa **/globalon** para começar a coletar dados.  

#### <a name="to-attach-the-profiler-to-a-native-service"></a>Para anexar o Criador de perfil a um serviço nativo  

1. Se o serviço não estiver em execução, inicie o serviço.  

2. Inicie o criador de perfil digitando o seguinte em um prompt de comando:  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency   /output:** `OutputFile` [`Options`]  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer opção da tabela a seguir com a opção **/start**.  

   > [!NOTE]
   >  A maioria dos serviços exigem as opções **/user** e **/crosssession**.  

   |                               Opção                               |                                                                     Descrição                                                                      |
   |--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain\`]`UserName` |                           Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil.                           |
   |           [/crosssession](../profiling/crosssession.md)            |                                               Habilita a criação de perfil de processos em outras sessões de logon.                                                |
   |  [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`  |                                      Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil.                                       |
   |       [/automark](../profiling/automark.md) **:** `Interval`       | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500. |
   |     [/events](../profiling/events-vsperfcmd.md) **:** `Config`     |       Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Eventos de ETW são coletados em um arquivo separado (.etl).       |


3. Anexe o criador de perfil ao serviço digitando o seguinte comando em um prompt de comando:  

    **VSPerfCmd /attach:** `PID`  

    `PID` especifica a ID do processo ou o nome do processo do aplicativo de destino. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

## <a name="controlling-data-collection"></a>Controlando coleção de dados  
 Enquanto o aplicativo de destino estiver em execução, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo com opções de VSPerfCmd.exe. Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções na tabela a seguir iniciam e param a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|  

## <a name="ending-the-profiling-session"></a>Encerrando a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um serviço nativo cujo perfil está sendo criado com o método de simultaneidade interrompendo o serviço ou invocando a opção **VSPerfCmd/detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Desanexe o criador de perfil do aplicativo de destino parando o serviço ou digitando o seguinte comando no prompt de comando:  

     Digite **VSPerfCmd /detach**  

2.  Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)



