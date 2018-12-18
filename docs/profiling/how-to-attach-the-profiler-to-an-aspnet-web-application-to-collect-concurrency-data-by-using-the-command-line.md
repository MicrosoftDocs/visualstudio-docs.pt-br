---
title: Como anexar o Criador de perfil a um aplicativo Web ASP .NET para coletar dados de simultaneidade usando a linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 0e215fdd-55f8-43ef-9534-06542eefe223
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 9c18b96f794f8317dacc890345ae544765bcb204
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831699"
---
# <a name="how-to-attach-the-profiler-to-an-aspnet-web-application-to-collect-concurrency-data-by-using-the-command-line"></a>Como anexar o criador de perfil a um aplicativo Web ASP.NET para coletar dados de simultaneidade usando a linha de comando
Este artigo descreve como usar as ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para anexar o criador de perfil a um aplicativo ASP.NET e coletar dados de simultaneidade de thread e do processo.  

 As ferramentas de linha de comando das Ferramentas de Criação de Perfil estão localizadas no subdiretório *\Team Tools\Performance Tools* do diretório de instalação do Visual Studio. Em computadores de 64 bits, as versões de 64 e de 32 bits das ferramentas estão disponíveis. Para usar o criador de perfil em um prompt de comando, você precisa adicionar o caminho das ferramentas à variável de ambiente PATH da janela **Prompt de Comando** ou adicioná-lo ao próprio comando. Para obter mais informações, confira [Especificar o caminho para ferramentas de linha de comando](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).  

 Para coletar dados de simultaneidade, anexe o criador de perfil ao processo de trabalho do ASP.NET que hospeda o site. Enquanto o criador de perfil estiver anexado ao aplicativo, você pode pausar e retomar a coleta de dados. Para encerrar uma sessão de criação de perfil, o criador de perfil não deve mais estar anexado ao aplicativo e precisa ser desligado explicitamente. Na maioria dos casos, você precisa desmarcar as variáveis de ambiente de criação de perfil no final de uma sessão.  

## <a name="attach-the-profiler"></a>Anexar o criador de perfil  

#### <a name="to-attach-the-profiler-to-a-aspnet-application"></a>Para anexar o criador de perfil a um aplicativo ASP.NET  

1. Inicie o criador de perfil digitando o seguinte comando:  

    [VSPerfCmd](../profiling/vsperfcmd.md) **/start:concurrency /output:** `OutputFile` [`Options`]  

   - A opção [/start](../profiling/start.md) inicializa o criador de perfil para coletar dados de contenção de recursos.  

   - A opção [/output](../profiling/output.md)**:**`OutputFile` é necessária com **/start**. `OutputFile` especifica o nome e o local do arquivo de dados de criação de perfil (.vsp).  

     É possível usar qualquer opção da tabela a seguir com a opção **/start**.  

   | Opção | Descrição |
   | - | - |
   | [/user](../profiling/user-vsperfcmd.md) **:**[`Domain\`]`UserName` | Especifica o domínio e o nome de usuário opcional da conta que receberá acesso ao criador de perfil. |
   | [/crosssession](../profiling/crosssession.md) | Habilita a criação de perfil de processos em outras sessões de logon. |
   | [/wincounter](../profiling/wincounter.md) **:** `WinCounterPath` | Especifica um contador de desempenho do Windows que deve ser coletado durante a criação de perfil. |
   | [/automark](../profiling/automark.md) **:** `Interval` | Use somente com **/wincounter**. Especifica o número de milissegundos entre eventos de coleta do contador de desempenho do Windows. O valor padrão é 500. |
   | [/events](../profiling/events-vsperfcmd.md) **:** `Config` | Especifica um evento de ETW (Rastreamento de Eventos para Windows) a ser coletado durante a criação de perfil. Os eventos do ETW são coletados em um arquivo separado (.*etl*). |


2. Inicie o aplicativo ASP.NET de maneira normal.  

3. Anexe o criador de perfil ao processo de trabalho do ASP.NET digitando o seguinte comando:**VSPerfCmd /attach:**`PID` [**/targetclr:**`Version`]  

   -   `PID` especifica a ID ou o nome do processo de trabalho do ASP.NET. É possível exibir as IDs de processo de todos os processos em execução no Gerenciador de Tarefas do Windows.  

   -   [/targetclr](../profiling/targetclr.md) **:** `Version` especifica a versão do CLR (Common Language Runtime) cujo perfil deverá ser criado quando mais de uma versão do tempo de execução for carregada em um aplicativo. Esse parâmetro é opcional.  

## <a name="control-data-collection"></a>Controlar a coleta de dados  
 Durante a execução do aplicativo, você pode controlar a coleta de dados iniciando e parando a gravação de dados no arquivo usando as opções do *VSPerfCmd.exe*. Controlando a coleta de dados, é possível coletar dados de uma parte específica da execução do programa, como o início ou o desligamento do aplicativo.  

#### <a name="to-start-and-stop-data-collection"></a>Para iniciar e interromper a coleta de dados  

-   Os pares de opções VSPerfCmd na tabela a seguir iniciam e interrompem a coleta de dados. Especifique cada opção em uma linha de comando separada. É possível ativar e desativar a coleta de dados várias vezes.  

    |Opção|Descrição|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|Inicia (**/globalon**) ou interrompe (**/globaloff**) a coleta de dados para todos os processos.|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID`  [processoff](../profiling/processon-and-processoff.md) **:** `PID`|Inicia (**/processon**) ou interrompe (**/processoff**) a coleta de dados para o processo que a ID de processo (`PID`) especificar.|  
    |[/attach](../profiling/attach.md) **:**{`PID`&#124;`ProcName`} [/detach](../profiling/detach.md)[**:**{`PID`&#124;`ProcName`}]|**/attach** começa a coletar dados para o processo que a ID de processo (`PID`) ou o nome de processo (*ProcName*) especificar. **/detach** interrompe a coleta de dados para o processo especificado ou para todos os processos se nenhum processo for especificado.|  

## <a name="end-the-profiling-session"></a>Encerrar a sessão de criação de perfil  
 Para encerrar uma sessão de criação de perfil, o criador de perfil não pode estar coletando dados. É possível interromper a coleta de dados de um aplicativo cujo perfil foi criado com o método de simultaneidade reiniciando o processo de trabalho do ASP.NET ou invocando a opção **VSPerfCmd/detach**. Depois, você invoca a opção **VSPerfCmd /shutdown** para desligar o criador de perfil e fechar o arquivo de dados de criação de perfil. O comando **VSPerfClrEnv /globaloff** limpa as variáveis de ambiente de criação de perfil, mas a configuração do sistema não é redefinida até que o computador seja reiniciado.  

#### <a name="to-end-a-profiling-session"></a>Para encerrar uma sessão de criação de perfil  

1.  Desanexe o criador de perfil do aplicativo de destino fechando-o ou digitando o seguinte no prompt de comando:  

     **VSPerfCmd /detach**  

2.  Desligue o criador de perfil digitando o seguinte comando em um prompt de comando:  

     **VSPerfCmd**  [/shutdown](../profiling/shutdown.md)  

## <a name="see-also"></a>Consulte também  
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Criação rápida de perfil de site com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)