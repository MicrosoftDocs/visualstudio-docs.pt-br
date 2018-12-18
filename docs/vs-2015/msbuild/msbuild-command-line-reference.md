---
title: Referência de linha de comando do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, msbuild.exe
- MSBuild, command line reference
- msbuild.exe
ms.assetid: edaa65ec-ab8a-42a1-84cb-d76d5b2f4584
caps.latest.revision: 61
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3a1827166829686801743ccc98156a0009e50dc3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49245902"
---
# <a name="msbuild-command-line-reference"></a>Referência de linha de comando MSBuild
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você usa MSBuild.exe para criar um arquivo de solução ou projeto, pode incluir várias opções para especificar vários aspectos do processo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
MSBuild.exe [Switches] [ProjectFile]  
```  
  
## <a name="arguments"></a>Arguments  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|`ProjectFile`|Compila os destinos no arquivo de projeto especificado. Se você não especificar um arquivo de projeto, o MSBuild procurará uma extensão de nome de arquivo terminada em “proj” no diretório de trabalho atual e usará esse arquivo. Você também pode especificar um arquivo de solução do Visual Studio para esse argumento.|  
  
## <a name="switches"></a>Opções  
  
|Alternar|Forma abreviada|Descrição|  
|------------|----------------|-----------------|  
|/help|/? ou /h|Exibe informações de uso. O seguinte comando é um exemplo:<br /><br /> `msbuild.exe /?`|  
|/detailedsummary|/ds|Mostra informações detalhadas ao final do log de compilação sobre as configurações que foram criadas e como elas foram agendadas para os nós.|  
|/ignoreprojectextensions:`extensions`|/ignore: `extensions`|Ignora as extensões especificadas ao determinar qual arquivo de projeto deve ser criado. Use um ponto e vírgula ou uma vírgula para separar várias extensões, como mostra o exemplo abaixo:<br /><br /> `/ignoreprojectextensions:.vcproj,.sln`|  
|/maxcpucount[:`number`]|/m[:`number`]|Especifica o número máximo de processos simultâneos a serem usados durante a compilação. Quando você não inclui essa opção, o valor padrão é 1. Se você incluir essa opção sem especificar um valor, o MSBuild usará o número de processadores no computador. Para obter mais informações, consulte [Compilando vários projetos paralelamente](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md).<br /><br /> O exemplo abaixo instrui o MSBuild a compilar usando três processos MSBuild, o que permite que os três projetos sejam compilados ao mesmo tempo:<br /><br /> `msbuild myproject.proj /maxcpucount:3`|  
|/noautoresponse|/noautorsp|Não inclui arquivos MSBuild automaticamente.|  
|/nodeReuse:`value`|/nr:`value`|Habilita ou desabilita a reutilização de nós do MSBuild. Você pode especificar os seguintes valores:<br /><br /> -   **True**. Os nós permanecem após a conclusão da compilação para que as compilações subsequentes possam usá-los (padrão).<br />-   **False**. Os nós não permanecerão após o término da compilação.<br /><br /> Um nó corresponde a um projeto que está em execução. Se você incluir a opção **/maxcpucount**, vários nós poderão ser executados simultaneamente.|  
|/nologo||Não exibe a faixa de inicialização ou a mensagem de direitos autorais.|  
|/preprocess[:`filepath`]|/pp[:`filepath`]|Cria um arquivo de projeto único, agregado pelo alinhamento de todos os arquivos que seriam importados durante a compilação, com seus limites marcados. Você pode usar essa opção para determinar facilmente quais arquivos estão sendo importados, de onde os arquivos estão sendo importados e quais arquivos contribuem para a compilação. Quando você usar essa opção, o projeto não será compilado.<br /><br /> Se você especificar um `filepath`, o arquivo de projeto agregado será a saída para o arquivo. Caso contrário, a saída é exibida na janela do console.<br /><br /> Para obter informações sobre como usar o elemento `Import` para inserir um arquivo de projeto em outro arquivo de projeto, consulte [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md) e [Como usar o mesmo destino em vários arquivos de projeto](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md).|  
|/property:`name`=`value`|/p:`name`=`value`|Define ou substitui as propriedades de nível de projeto especificadas, em que `name` é o nome da propriedade e `value` é o valor da propriedade. Especifique cada propriedade separadamente ou use um ponto e vírgula ou uma vírgula para separar várias propriedades, como mostra o exemplo abaixo:<br /><br /> `/property:WarningLevel=2;OutDir=bin\Debug`|  
|/target:`targets`|/t:`targets`|Cria destinos especificados no projeto. Especifique cada destino separadamente ou use um ponto e vírgula ou uma vírgula para separar vários destinos, como mostra o exemplo abaixo:<br /><br /> `/target:Resources;Compile`<br /><br /> Se você especificar um destino usando essa opção, eles serão executados em vez dos destinos no atributo `DefaultTargets` no arquivo de projeto. Para saber mais, confira [Ordem de build de destinos](../msbuild/target-build-order.md) e [Como especificar qual destino será compilado primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).<br /><br /> Um destino é um grupo de tarefas. Para obter mais informações, consulte [Destinos](../msbuild/msbuild-targets.md).|  
|/toolsversion:`version`|/tv:`version`|Especifica a versão do conjunto de ferramentas a ser usado para compilar o projeto, como mostra o exemplo abaixo:`/toolsversion:3.5`<br /><br /> Usando essa opção, você pode criar um projeto e especificar uma versão diferente da versão definida no [Elemento de projeto (MSBuild)](../msbuild/project-element-msbuild.md). Para obter mais informações, consulte [Substituindo as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).<br /><br /> No caso do MSBuild 4.5, você pode especificar os seguintes valores para `version`: 2.0, 3.5 e 4.0. Se você especificar 4.0, a propriedade de compilação `VisualStudioVersion` especifica qual subconjunto de ferramentas usar. Para saber mais,confira a seção de subconjuntos de ferramentas de [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md).<br /><br /> Um Conjunto de ferramentas consiste em tarefas, destinos e ferramentas que são usados para compilar um aplicativo. As ferramentas incluem compiladores, tais como csc.exe e vbc.exe. Para saber mais sobre conjuntos de ferramentas, confira [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md), [Configurações do conjunto de ferramentas personalizadas e padrão](../msbuild/standard-and-custom-toolset-configurations.md) e [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md). **Observação:** a versão do conjunto de ferramentas não é igual à estrutura de destino, que é a versão do .NET Framework em que um projeto é criado para ser executado. Para saber mais, confira [Estrutura de destino e plataforma de destino](../msbuild/msbuild-target-framework-and-target-platform.md).|  
|/validate:[`schema`]|/val[`schema`]|Valida o arquivo de projeto e, se a validação for bem-sucedida, compila o projeto.<br /><br /> Se você não especificar `schema`, o projeto será validado em relação ao esquema padrão.<br /><br /> Se você especificar `schema`, o projeto será validado em relação ao esquema que você especificar.<br /><br /> A configuração abaixo é um exemplo: `/validate:MyExtendedBuildSchema.xsd`|  
|/verbosity:`level`|/v:`level`|Especifica a quantidade de informações a serem exibidas no log de compilação. Cada agente exibe eventos de acordo com o nível de detalhamento que você definiu para esse agente.<br /><br /> Você pode especificar os seguintes níveis de detalhamento: `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.<br /><br /> A configuração abaixo é um exemplo: `/verbosity:quiet`|  
|/version|/ver|Exibe somente informações de versão. O projeto não é criado.|  
|@`file`||Insere configurações de linha de comando de um arquivo de texto. Se você tiver vários arquivos, especifique-os separadamente. Para saber mais, confira [Arquivos de resposta](../msbuild/msbuild-response-files.md).|  
  
### <a name="switches-for-loggers"></a>Opções para Agentes  
  
|Alternar|Forma abreviada|Descrição|  
|------------|----------------|-----------------|  
|/consoleloggerparameters:<br /><br /> `parameters`|/clp:`parameters`|Passa os parâmetros que você especificar para o agente de console, que exibe informações de compilação na janela do console. Você pode especificar os seguintes parâmetros:<br /><br /> -   **PerformanceSummary**. Mostra o tempo gasto em tarefas, destinos e projetos.<br />-   **Summary**. Mostra o resumo de aviso e erro no final.<br />-   **NoSummary**. Não mostra o resumo de aviso e erro no final.<br />-   **ErrorsOnly**. Mostra somente os erros.<br />-   **WarningsOnly**. Mostra somente os avisos.<br />-   **NoItemAndPropertyList**. Não mostra a lista de itens e propriedades que aparecem no início de cada compilação de projeto se o nível de detalhamento é definido como `diagnostic`.<br />-   **ShowCommandLine**. Mostrar `TaskCommandLineEvent` mensagens.<br />-   **ShowTimestamp**. Mostra o carimbo de data/hora como um prefixo em todas as mensagens.<br />-   **ShowEventId**. Mostra a ID de evento para cada evento iniciado e concluído e a mensagem.<br />-   **ForceNoAlign**. Não alinha o texto com o tamanho do buffer de console.<br />-   **DisableConsoleColor**. Usa as cores de console padrão em todas as mensagens de log.<br />-   **DisableMPLogging**. Desabilita o estilo de registro em log do multiprocessador da saída quando executado no modo não multiprocessador.<br />-   **EnableMPLogging**. Habilita o estilo de registro em log do multiprocessador quando executado no modo não multiprocessador. Esse estilo de registro em log fica ativado por padrão.<br />-   **Verbosity**. Substitui a configuração **/verbosity** para esse agente.<br /><br /> Usa um ponto e vírgula ou uma vírgula para separar vários parâmetros, como mostra o exemplo abaixo:<br /><br /> `/consoleloggerparameters:PerformanceSummary;NoSummary /verbosity:minimal`|  
|/distributedFileLogger|/dfl|A saída da compilação de cada nó do MSBuild para seu próprio arquivo. A localização inicial desses arquivos é o diretório atual. Por padrão, os arquivos são nomeados "MSBuild*NodeId*.log". Você pode usar a opção **/fileLoggerParameters** para especificar o local dos arquivos e outros parâmetros do fileLogger.<br /><br /> Se você nomear um arquivo de log usando a opção **/fileLoggerParameters**, o agente distribuído usará esse nome como modelo e acrescentará a ID do nó para esse nome ao criar um arquivo de log para cada nó.|  
|/distributedlogger:<br /><br /> `central logger`*<br /><br /> `forwarding logger`|/dl:`central logger`*`forwarding logger`|Registra eventos do MSBuild, anexando uma instância do agente diferente a cada nó. Para especificar vários agentes, especifique cada um separadamente.<br /><br /> Você pode usar a sintaxe do agente para especificar um agente. Para obter a sintaxe do agente, confira a opção **/logger** abaixo.<br /><br /> Os exemplos abaixo mostram como usar o essa opção:<br /><br /> `/dl:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/dl:MyLogger,C:\My.dll*ForwardingLogger,C:\Logger.dll`|  
|/fileLogger<br /><br /> *[number]*|/fl[`number`]|Registra a saída da compilação para um único arquivo no diretório atual. Se você não especificar `number`, o arquivo de saída será denominado msbuild.log. Se você especificar `number`, o arquivo de saída será denominado msbuild`n`.log, em que n é `number`. `Number` pode ser um dígito de 1 a 9.<br /><br /> Você pode usar a opção **/fileLoggerParameters** para especificar o local do arquivo e outros parâmetros do fileLogger.|  
|/fileloggerparameters: [número]<br /><br /> `parameters`|/flp:[ `number`] `parameters`|Especifica parâmetros extras para o agente do arquivo e o agente do arquivo distribuído. A presença dessa opção indica que a opção /**filelogger [**`number`**]** correspondente existe. `Number` pode ser um dígito de 1 a 9.<br /><br /> Você pode usar todos os parâmetros listados para **/consoleloggerparameters**. Você também pode usar um ou mais dos seguintes parâmetros:<br /><br /> -   **LogFile**. O caminho para o arquivo de log no qual o log de compilação será gravado. O agente de arquivos distribuído prefixa esse caminho aos nomes dos seus arquivos de log.<br />-   **Append**. Determina se o log de compilação é acrescentado ao arquivo de log ou se o substitui. Quando você definir a opção, o log de compilação será anexado ao arquivo de log. Quando a opção não estiver presente, o conteúdo de um arquivo de log será substituído.<br />     Se você incluir a opção de acréscimo, não importa se ele está definido como true ou false: o log será anexado. Se você não incluir a opção de acréscimo, o log será substituído.<br />     Neste caso, o arquivo é substituído:`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log`<br />     Neste caso, o arquivo é anexado:`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=true`<br />     Neste caso, o arquivo é anexado:`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=false`<br />-   **Codificação**. Especifica a codificação do arquivo (por exemplo, UTF-8, Unicode ou ASCII).<br /><br /> O exemplo abaixo gera arquivos de log separados para avisos e erros:<br /><br /> `/flp1:logfile=errors.txt;errorsonly /flp2:logfile=warnings.txt;warningsonly`<br /><br /> Os exemplos abaixo mostram outras possibilidades:<br /><br /> `/fileLoggerParameters:LogFile=MyLog.log;Append; Verbosity=diagnostic;Encoding=UTF-8`<br /><br /> `/flp:Summary;Verbosity=minimal;LogFile=msbuild.sum`<br /><br /> `/flp1:warningsonly;logfile=msbuild.wrn`<br /><br /> `/flp2:errorsonly;logfile=msbuild.err`|  
|/logger:<br /><br /> `logger`|/l:`logger`|Especifica o agente a ser usado para registrar eventos do MSBuild. Para especificar vários agentes, especifique cada um separadamente.<br /><br /> Use a seguinte sintaxe para `logger`: `[``LoggerClass``,]``LoggerAssembly``[;``LoggerParameters``]`<br /><br /> Use a seguinte sintaxe para `LoggerClass`: `[``PartialOrFullNamespace``.]``LoggerClassName`<br /><br /> Você não precisa especificar a classe do agente se o assembly contiver exatamente um agente.<br /><br /> Use a seguinte sintaxe para `LoggerAssembly`: `{``AssemblyName``[,``StrongName``] &#124;` `AssemblyFile``}`<br /><br /> Os parâmetros de agente são opcionais e são passados ao agente exatamente como são inseridos.<br /><br /> Os exemplos a seguir usam a opção **/logger**.<br /><br /> `/logger:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/logger:XMLLogger,C:\Loggers\MyLogger.dll;OutputAsHTML`|  
|/noconsolelogger|/noconlog|Desabilita o agente de console padrão e não registra eventos no console.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria o destino `rebuild` do projeto `MyProject.proj`.  
  
```  
MSBuild.exe MyProject.proj /t:rebuild  
```  
  
## <a name="example"></a>Exemplo  
 Você pode usar MSBuild.exe para executar compilações mais complexas. Por exemplo, você pode usá-lo para compilar destinos específicos de projetos específicos em uma solução. O exemplo a seguir recria o projeto `NotInSolutionFolder` e limpa o projeto `InSolutionFolder`, que está na pasta da solução `NewFolder`.  
  
```  
msbuild SlnFolders.sln /t:NotInSolutionfolder:Rebuild;NewFolder\InSolutionFolder:Clean  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Propriedades de projeto comuns do MSBuild](../msbuild/common-msbuild-project-properties.md)



