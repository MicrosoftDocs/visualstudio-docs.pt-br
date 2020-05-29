---
title: Referência de linha de comando do MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 625dd9517325d83348021681f6b5fbfa0272a12d
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173493"
---
# <a name="msbuild-command-line-reference"></a>Referência de linha de comando do MSBuild

Ao usar o *MSBuild.exe* para criar um arquivo de solução ou de projeto, inclua várias opções para especificar vários aspectos do processo.

Cada opção está disponível em dois formulários: -switch e /switch. A documentação mostra apenas o formulário -switch. As opções não diferenciam maiúsculas de minúsculas. Se você executar o MSBuild a partir de um shell diferente do prompt de comando do Windows, as listas de argumentos para um comutador (separados por ponto-e-vírgulas ou separações) podem precisar de aspas simples ou duplas para garantir que as listas sejam passadas para o MSBuild em vez de interpretadas pelo shell.

## <a name="syntax"></a>Sintaxe

```cmd
MSBuild.exe [Switches] [ProjectFile]
```

## <a name="arguments"></a>Argumentos

|Argumento|Descrição|
|--------------|-----------------|
|`ProjectFile`|Compila os destinos no arquivo de projeto especificado. Se você não especificar um arquivo de projeto, o MSBuild pesquisará uma extensão de nome de arquivo que termina com *proj* no diretório de trabalho atual e usará esse arquivo. Você também pode especificar um arquivo de solução do Visual Studio para esse argumento.|

## <a name="switches"></a>Opções

|Alternar|Formato curto|Descrição|
|------------|----------------|-----------------|
|-detailedSummary|-ds|Mostra informações detalhadas ao final do log de compilação sobre as configurações que foram criadas e como elas foram agendadas para os nós.|
|-graphBuild [: `True` ou `False` ]|-grafo [: `True` ou `False` ]|Faz com que o MSBuild construa e crie um grafo de projeto. Construir um grafo envolve identificar referências de projeto para formar dependências. A criação desse grafo envolve a tentativa de criar referências de projeto antes dos projetos que as referenciam, diferente do agendamento do MSBuild tradicional.|
|-help|/? ou -h|Exibir informações de uso. O seguinte comando é um exemplo:<br /><br /> `msbuild.exe -?`|
|-ignoreProjectExtensions:`extensions`|-ignore: `extensions`|Ignora as extensões especificadas ao determinar qual arquivo de projeto deve ser criado. Use um ponto e vírgula ou uma vírgula para separar várias extensões, como mostra o exemplo abaixo:<br /><br /> `-ignoreprojectextensions:.vcproj,.sln`|
|-interativo [: `True` ou `False` ]|-|Indica que as ações na compilação têm permissão para interagir com o usuário.  Não use esse argumento em um cenário automatizado em que interatividade não é esperada. Especificar-Interactive é o mesmo que especificar-Interactive: true.  Use o parâmetro para substituir um valor proveniente de um arquivo de resposta.
|-isolateProjects [: `True` ou `False` ]|-isolar [: `True` ou `False` ]|Faz com que o MSBuild compile cada projeto isoladamente. Esse é um modo mais restritivo do MSBuild, pois ele requer que o grafo do projeto seja detectável de forma estática no tempo de avaliação, mas pode melhorar o agendamento e reduzir a sobrecarga de memória ao criar um grande conjunto de projetos.|
|-maxCpuCount [: `number` ]|-m[:`number`]|Especifica o número máximo de processos simultâneos a serem usados durante a compilação. Quando você não inclui essa opção, o valor padrão é 1. Se você incluir essa opção sem especificar um valor, o MSBuild usará o número de processadores no computador. Para obter mais informações, confira [Compilando vários projetos em paralelo](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md).<br /><br /> O exemplo abaixo instrui o MSBuild a compilar usando três processos MSBuild, o que permite que os três projetos sejam compilados ao mesmo tempo:<br /><br /> `msbuild myproject.proj -maxcpucount:3`|
|-noAutoResponse|-noautorsp|Não inclui arquivos *MSBuild.rsp* automaticamente.|
|-nodeReuse:`value`|-nr:`value`|Habilita ou desabilita a reutilização de nós do MSBuild. É possível especificar os seguintes valores:<br /><br /> -   **True**. Os nós permanecem após a conclusão da compilação para que as compilações subsequentes possam usá-los (padrão).<br />-   **Falso**. Os nós não permanecerão após o término da compilação.<br /><br /> Um nó corresponde a um projeto que está em execução. Se você incluir a opção **-maxcpucount**, vários nós poderão ser executados simultaneamente.|
|-nologo||Não exibe a faixa de inicialização ou a mensagem de direitos autorais.|
|<a name="preprocess"></a>-pré-processar [: `filepath` ]|-pp[:`filepath`]|Cria um arquivo de projeto único, agregado pelo alinhamento de todos os arquivos que seriam importados durante a compilação, com seus limites marcados. Você pode usar essa opção para determinar facilmente quais arquivos estão sendo importados, de onde os arquivos estão sendo importados e quais arquivos contribuem para a compilação. Quando você usar essa opção, o projeto não é criado.<br /><br /> Se você especificar um `filepath`, o arquivo de projeto agregado será a saída para o arquivo. Caso contrário, a saída é exibida na janela do console.<br /><br /> Para obter informações sobre como usar o elemento `Import` para inserir um arquivo de projeto em outro arquivo de projeto, confira [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md) e [Como usar o mesmo destino em vários arquivos de projeto](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md).|
|-outputResultsCache [: cachefile]|-Orc [: cachefile]|Arquivo de cache de saída em que o MSBuild gravará o conteúdo de seus caches de resultados de compilação no final da compilação. Definir isso também ativa compilações isoladas (-isolar).|
|-profileEvaluation:`<file>`|-|Gera perfis de avaliação do MSBuild e grava o resultado no arquivo especificado. Se a extensão do arquivo especificado for '. MD ', o resultado será gerado no formato de redução. Caso contrário, um arquivo separado por tabulações será produzido.|
|-property:`name`=`value`|-p:`name`=`value`|Define ou substitui as propriedades de nível de projeto especificadas, em que `name` é o nome da propriedade e `value` é o valor da propriedade. Especifique cada propriedade separadamente ou use um ponto e vírgula ou uma vírgula para separar várias propriedades, como mostra o exemplo abaixo:<br /><br /> `-property:WarningLevel=2;OutDir=bin\Debug`|
|-restore|-r|Executa o destino do `Restore` antes de criar os destinos reais.|
|-restoreproperty:`name=value`|RP`name=value`|Defina ou substitua essas propriedades no nível do projeto somente durante a restauração e não use as propriedades especificadas com o argumento-Property. `name`é o nome da propriedade e `value` é o valor da propriedade. Use um ponto-e-vírgula ou uma vírgula para separar várias propriedades ou especifique cada propriedade separadamente.|
|-target:`targets`|-t:`targets`|Cria destinos especificados no projeto. Especifique cada destino separadamente ou use um ponto e vírgula ou uma vírgula para separar vários destinos, como mostra o exemplo abaixo:<br /><br /> `-target:PrepareResources;Compile`<br /><br /> Se você especificar um destino usando essa opção, eles serão executados em vez dos destinos no atributo `DefaultTargets` no arquivo de projeto. Para obter mais informações, confira [Ordem de build de destino](../msbuild/target-build-order.md) e [Como especificar o destino a ser criado primeiro](../msbuild/how-to-specify-which-target-to-build-first.md).<br /><br /> Um destino é um grupo de tarefas. Para obter mais informações, consulte [Destinos](../msbuild/msbuild-targets.md).|
|-destinos [: `file` ]|-TS [: `file` ]|Gravar a lista de destinos disponíveis para o arquivo especificado (ou o dispositivo de saída, se nenhum arquivo for especificado), sem realmente executar o processo de compilação.|
|ToolsVersion`version`|-tv:`version`|Especifica a versão do conjunto de ferramentas a ser usado para compilar o projeto, como mostra o exemplo abaixo:`-toolsversion:3.5`<br /><br /> Usando essa opção, você pode criar um projeto e especificar uma versão diferente da versão especificada no [elemento Project (MSBuild)](../msbuild/project-element-msbuild.md). Para obter mais informações, confira [Substituindo as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).<br /><br /> No caso do MSBuild 4.5, você pode especificar os seguintes valores para `version`: 2.0, 3.5 e 4.0. Se você especificar 4.0, a propriedade de compilação `VisualStudioVersion` especifica qual subconjunto de ferramentas usar. Para saber mais,confira a seção de subconjuntos de ferramentas de [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md).<br /><br /> Um Conjunto de ferramentas consiste em tarefas, destinos e ferramentas que são usados para compilar um aplicativo. As ferramentas incluem compiladores, como *csc.exe* e *vbc.exe*. Para obter mais informações sobre Conjuntos de ferramentas, confira [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md), [Configurações padrão e personalizadas do conjunto de ferramentas](../msbuild/standard-and-custom-toolset-configurations.md) e [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md). **Observação:**  A versão do conjunto de ferramentas não é igual à estrutura de destino, que é a versão do .NET Framework em que um projeto é criado para ser executado. Para obter mais informações, confira [Estrutura de destino e plataforma de destino](../msbuild/msbuild-target-framework-and-target-platform.md).|
|-validate:[`schema`]|-val[`schema`]|Valida o arquivo de projeto e, se a validação for bem-sucedida, compila o projeto.<br /><br /> Se você não especificar `schema`, o projeto será validado em relação ao esquema padrão.<br /><br /> Se você especificar `schema`, o projeto será validado em relação ao esquema que você especificar.<br /><br /> A configuração abaixo é um exemplo: `-validate:MyExtendedBuildSchema.xsd`|
|-verbosity:`level`|-v:`level`|Especifica a quantidade de informações a serem exibidas no log de compilação. Cada agente exibe eventos de acordo com o nível de detalhamento que você definiu para esse agente.<br /><br /> Você pode especificar os seguintes níveis de detalhamento: `q[uiet]` , `m[inimal]` , `n[ormal]` (padrão), `d[etailed]` e `diag[nostic]` .<br /><br /> A configuração abaixo é um exemplo: `-verbosity:quiet`
|-version|-ver|Exibe somente informações de versão. O projeto não é criado.|
|@`file`||Insere configurações de linha de comando de um arquivo de texto. Se você tiver vários arquivos, especifique-os separadamente. Para obter mais informações, confira [Arquivos de resposta](../msbuild/msbuild-response-files.md).|
|-warnAsError [: `code` [ `;code2` ]|-Err [ `:code` [ `;code2` ]|Lista de códigos de aviso a serem tratados como erros.  Use um ponto-e-vírgula ou uma vírgula para separar vários códigos de aviso. Para tratar todos os avisos como erros, use a opção sem valores. Quando um aviso é tratado como um erro, o destino continua a ser executado como se fosse um aviso, mas a compilação geral falha.<br/><br/>Exemplo: `-err:MSB4130`|
|-warnAsMessage [: `code` [ `;code2` ]|-nowarn [: `code` [ `;code2` ]|Lista de códigos de aviso para tratar como mensagens de baixa importância.  Use um ponto-e-vírgula ou uma vírgula para separar vários códigos de aviso.<br/><br/>Exemplo: `-noWarn:MSB3026`|

### <a name="switches-for-loggers"></a>Opções para agentes

|Alternar|Formato curto|Descrição|
|------------|----------------|-----------------|
|-binaryLogger [: [LogFile =]`output.binlog`<br/>[; ProjectImports = [nenhum, inserir, ZipFile]]]|-bl|Serializa todos os eventos de build para um arquivo binário comprimido. Por padrão, o arquivo está no diretório atual e é nomeado *msbuild.binlog*. O log binário é uma descrição detalhada do processo de build que posteriormente pode ser usado para reconstruir os logs de texto e ser usado por outras ferramentas de análise. Um log binário é geralmente 10 a 20x menor do que o log de nível de diagnóstico de texto mais detalhado, mas ele contém mais informações.<br /><br />O agente binário coleta por padrão o texto de origem dos arquivos de projeto, incluindo todos os projetos importados e arquivos de destino encontrados durante o build. A opção `ProjectImports` opcional controla esse comportamento:<br /><br /> -   **ProjectImports=None**. Não coletar as importações do projeto.<br /> -   **ProjectImports=Embed**. Inserir importações do projeto no arquivo de log (padrão).<br /> -   **ProjectImports=ZipFile**. Salve arquivos de projeto em * \<output> . projectimports. zip* , em que \<output> é o mesmo nome que o nome do arquivo de log binário.<br /><br />A configuração padrão para ProjectImports é Embed.<br />**Observação**: o agente não coleta arquivos de origem não MSBuild, como *.cs*, *.cpp* etc.<br />Um arquivo *.binlog* pode ser "reproduzido" passando-o para *msbuild.exe* como um argumento, em vez de um projeto/uma solução. Outros agentes receberão as informações contidas no arquivo de log como se o build original estivesse ocorrendo. Você pode ler mais sobre o log binário e seus usos em: https://github.com/Microsoft/msbuild/wiki/Binary-Log <br /><br />**Exemplos**:<br /> -   `-bl`<br /> -    `-bl:output.binlog`<br /> -   `-bl:output.binlog;ProjectImports=None`<br /> -   `-bl:output.binlog;ProjectImports=ZipFile`<br /> -   `-bl:..\..\custom.binlog`<br /> -   `-binaryLogger`|
|-consoleLoggerParameters:<br /><br /> `parameters`|-clp:`parameters`|Passa os parâmetros que você especificar para o agente de console, que exibe informações de compilação na janela do console. É possível especificar os seguintes parâmetros:<br /><br /> -   **PerformanceSummary**. Mostra o tempo gasto em tarefas, destinos e projetos.<br />-   **Resumo**. Mostra o resumo de aviso e erro no final.<br />-   **NoSummary**. Não mostra o resumo de aviso e erro no final.<br />-   **ErrorsOnly**. Mostra somente os erros.<br />-   **WarningsOnly**. Mostra somente os avisos.<br />-   **NoItemAndPropertyList**. Não mostra a lista de itens e propriedades que aparecem no início de cada compilação de projeto se o nível de detalhamento é definido como `diagnostic`.<br />-   **ShowCommandLine**. Mostrar `TaskCommandLineEvent` mensagens.<br />-   **ShowTimestamp**. Mostra o carimbo de data/hora como um prefixo em todas as mensagens.<br />-   **ShowEventId**. Mostra a ID de evento para cada evento iniciado e concluído e a mensagem.<br />-   **ForceNoAlign**. Não alinha o texto com o tamanho do buffer de console.<br />-   **DisableConsoleColor**. Usa as cores de console padrão em todas as mensagens de log.<br />-   **DisableMPLogging**. Desabilita o estilo de registro em log do multiprocessador da saída quando executado no modo não multiprocessador.<br />-   **EnableMPLogging**. Habilita o estilo de registro em log do multiprocessador quando executado no modo não multiprocessador. Esse estilo de registro em log fica ativado por padrão.<br />-   **Detalhes**. Substitui a configuração **-verbosity** para esse agente.<br /><br /> Use um ponto e vírgula para separar vários parâmetros, como mostra o exemplo a seguir:<br /><br /> `-consoleloggerparameters:PerformanceSummary;NoSummary -verbosity:minimal`<br/><br/> O agente de log do console padrão está em detalhes normais e inclui um `Summary` .|
|-distributedFileLogger|-dfl|A saída da compilação de cada nó do MSBuild para seu próprio arquivo. A localização inicial desses arquivos é o diretório atual. Por padrão, os arquivos são nomeados *MSBuild \<NodeId> . log*. Você pode usar a opção **-fileLoggerParameters** para especificar o local dos arquivos e outros parâmetros do fileLogger.<br /><br /> Se você nomear um arquivo de log usando a opção **-fileLoggerParameters** , o agente distribuído usará esse nome como um modelo e acrescentará a ID do nó a esse nome ao criar um arquivo de log para cada nó.|
|-distributedLogger:<br /><br /> `central logger`*<br /><br /> `forwarding logger`|-dl:`central logger`*`forwarding logger`|Registra eventos do MSBuild, anexando uma instância do agente diferente a cada nó. Para especificar vários agentes, especifique cada um separadamente.<br /><br /> Você pode usar a sintaxe do agente para especificar um agente. Para obter a sintaxe do agente, consulte a opção **-logger** abaixo.<br /><br /> Os exemplos abaixo mostram como usar o essa opção:<br /><br /> `-dl:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `-dl:MyLogger,C:\My.dll*ForwardingLogger,C:\Logger.dll`|
|-fileLogger<br /><br /> *automática*|-fl[`number`]|Registra a saída da compilação para um único arquivo no diretório atual. Se você não especificar `number`, o arquivo de saída será denominado *msbuild.log*. Se você especificar `number` , o arquivo de saída será denominado *MSBuild \<n> . log*, onde \<n> é `number` . `Number` pode ser um dígito de 1 a 9.<br /><br /> Você pode usar a opção **-Fileloggervalue** para especificar o local do arquivo e outros parâmetros para o FileLogger.|
|-fileLoggerParameters: [número]<br /><br /> `parameters`|-FLP [ `number` ]:`parameters`|Especifica parâmetros extras para o agente do arquivo e o agente do arquivo distribuído. A presença dessa opção implica que a opção-**FileLogger [** `number` **]** correspondente está presente. `Number` pode ser um dígito de 1 a 9.<br /><br /> Você pode usar todos os parâmetros listados para **-consoleloggerparameters**. Você também pode usar um ou mais dos seguintes parâmetros:<br /><br /> -   Arquivo de **log**. O caminho para o arquivo de log no qual o log de compilação será gravado. O agente de arquivos distribuído prefixa esse caminho aos nomes dos seus arquivos de log.<br />-   **Acrescentar**. Determina se o log de compilação é acrescentado ao arquivo de log ou se o substitui. Quando você definir a opção, o log de compilação será anexado ao arquivo de log. Quando a opção não estiver presente, o conteúdo de um arquivo de log será substituído.<br />     Se você incluir a opção de acréscimo, não importa se ele está definido como true ou false: o log será anexado. Se você não incluir a opção de acréscimo, o log será substituído.<br />     Neste caso, o arquivo é substituído:`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log`<br />     Neste caso, o arquivo é anexado:`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log;append=true`<br />     Neste caso, o arquivo é anexado:`msbuild myfile.proj -l:FileLogger,Microsoft.Build;logfile=MyLog.log;append=false`<br />-   **Codificação**. Especifica a codificação do arquivo (por exemplo, UTF-8, Unicode ou ASCII).<br /><br /> O exemplo abaixo gera arquivos de log separados para avisos e erros:<br /><br /> `-flp1:logfile=errors.txt;errorsonly -flp2:logfile=warnings.txt;warningsonly`<br /><br /> Os exemplos abaixo mostram outras possibilidades:<br /><br /> `-fileLoggerParameters:LogFile=MyLog.log;Append; Verbosity=diagnostic;Encoding=UTF-8`<br /><br /> `-flp:Summary;Verbosity=minimal;LogFile=msbuild.sum`<br /><br /> `-flp1:warningsonly;logfile=msbuild.wrn`<br /><br /> `-flp2:errorsonly;logfile=msbuild.err`|
|-logger:<br /><br /> `logger`|-l:`logger`|Especifica o agente a ser usado para registrar eventos do MSBuild. Para especificar vários agentes, especifique cada um separadamente.<br /><br /> Use a seguinte sintaxe para `logger`: `[``LoggerClass``,]``LoggerAssembly``[;``LoggerParameters``]`<br /><br /> Use a seguinte sintaxe para `LoggerClass`: `[``PartialOrFullNamespace``.]``LoggerClassName`<br /><br /> Você não precisa especificar a classe do agente se o assembly contiver exatamente um agente.<br /><br /> Use a seguinte sintaxe para `LoggerAssembly`: `{``AssemblyName``[,``StrongName``] &#124;` `AssemblyFile``}`<br /><br /> Os parâmetros de agente são opcionais e são passados ao agente exatamente como são inseridos.<br /><br /> Os exemplos a seguir usam a opção **-logger** .<br /><br /> `-logger:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `-logger:XMLLogger,C:\Loggers\MyLogger.dll;OutputAsHTML`|
|-noConsoleLogger|-noconlog|Desabilita o agente de console padrão e não registra eventos no console.|

## <a name="example"></a>Exemplo

 O exemplo a seguir compila o destino `rebuild` do projeto *MyProject.proj*.

```cmd
MSBuild.exe MyProject.proj -t:rebuild
```

## <a name="example"></a>Exemplo

 Use o *MSBuild.exe* para executar builds mais complexos. Por exemplo, você pode usá-lo para compilar destinos específicos de projetos específicos em uma solução. O exemplo a seguir recompila o projeto `NotInSolutionFolder` e limpa o projeto `InSolutionFolder`, que está na pasta de solução *NewFolder*.

```cmd
msbuild SlnFolders.sln -t:NotInSolutionfolder:Rebuild;NewFolder\InSolutionFolder:Clean
```

## <a name="see-also"></a>Veja também

- [Referência do MSBuild](../msbuild/msbuild-reference.md)
- [Propriedades de projeto comuns do MSBuild](../msbuild/common-msbuild-project-properties.md)
