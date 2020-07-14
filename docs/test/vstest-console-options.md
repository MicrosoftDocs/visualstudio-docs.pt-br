---
title: Opções da linha de comando de VSTest.Console.exe
ms.date: 07/12/2018
ms.topic: reference
helpviewer_keywords:
- vstest.console.exe
- command-line tests
ms.author: mikejo
author: mikejo5000
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eaf282ca647310010c2e75e7279f11cbc90aad76
ms.sourcegitcommit: 5e82a428795749c594f71300ab03a935dc1d523b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211568"
---
# <a name="vstestconsoleexe-command-line-options"></a>Opções da linha de comando de VSTest.Console.exe

O *VSTest.Console.exe* é a ferramenta de linha de comando para execução de testes. É possível especificar várias opções em qualquer ordem na linha de comando. Essas opções são listadas em [Opções gerais de linha de comando](#general-command-line-options).

> [!NOTE]
> O adaptador MSTest no Visual Studio também funciona no modo herdado (equivalente à execução de testes com *mstest.exe*) para compatibilidade. No modo herdado, ele não pode aproveitar o recurso TestCaseFilter. O adaptador pode alternar para o modo herdado quando um arquivo *testsettings* é especificado, **forcelegacymode** é definido como **true** em um arquivo *runsettings* ou usando atributos como **HostType**.
>
> Para executar testes automatizados em um computador baseado na arquitetura ARM, use o *VSTest.Console.exe*.

Abra um [prompt de comando do desenvolvedor](/dotnet/framework/tools/developer-command-prompt-for-vs) para usar a ferramenta de linha de comando ou você pode encontrar a ferramenta em *% arquivos de programas (x86)% \ Microsoft Visual Studio \\<versão \> \\<Edition \> \common7\ide\CommonExtensions \\<plataforma | Microsoft>*.

## <a name="general-command-line-options"></a>Opções gerais de linha de comando

A tabela a seguir lista todas as opções para o *VSTest.Console.exe*, além de breves descrições sobre elas. É possível ver um resumo semelhante digitando `VSTest.Console/?` na linha de comando.

| Opção | Descrição |
|---|---|
|**[*nomes dos arquivos de teste*]**|Executa testes dos arquivos especificados. Separa vários nomes de arquivo de teste com espaços.<br />Exemplos: `mytestproject.dll`, `mytestproject.dll myothertestproject.exe`|
|**/Settings:[*nome do arquivo*]**|Execute testes com configurações adicionais, como coletores de dados.<br />Exemplo: `/Settings:Local.RunSettings`|
|**/Tests:[*nome do teste*]**|Executa testes com nomes que contêm os valores fornecidos. Para fornecer vários valores, separe-os por vírgulas.<br />Exemplo: `/Tests:TestMethod1,testMethod2`<br />A opção de linha de comando **/Tests** não pode ser usada com a opção de linha de comando **/TestCaseFilter**.|
|**/Parallel**|Especifica que os testes sejam executados em paralelo. Por padrão, todos os núcleos disponíveis no computador podem ser usados. Você pode configurar o número de núcleos a serem usados em um arquivo de configurações.|
|**/Enablecodecoverage**|Permite o adaptador de diagnóstico de dados CodeCoverage na execução de teste.<br />As configurações padrão serão usadas se não forem especificadas usando o arquivo de configurações.|
|**/InIsolation**|Executa os testes em um processo isolado.<br />Esse isolamento torna o processo *vstest.console.exe* menos suscetível a ser interrompido acidentalmente nos testes. Entretanto, os testes podem ser executados mais lentamente.|
|**/UseVsixExtensions**|Essa opção faz com que o processo *vstest.console.exe* use ou ignore as extensões VSIX instaladas (se houver) na execução de teste.<br />Essa opção foi preterida. A partir da próxima versão principal do Visual Studio, essa opção poderá ser removida. A migração para o consumo de extensões foi disponibilizada como um pacote NuGet.<br />Exemplo: `/UseVsixExtensions:true`|
|**/TestAdapterPath:[*caminho*]**|Força o processo *vstest.console.exe* a usar adaptadores de teste personalizados de um caminho especificado (se houver) na execução de teste.<br />Exemplo: `/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[*tipo de plataforma*]**|Arquitetura da plataforma de destino a ser usada para a execução de teste.<br />Os valores válidos são x86, x64 e ARM.|
|**/Framework: [*versão do framework*]**|Versão do .NET de destino a ser usada na execução do teste.<br />Exemplos de valores são `Framework35`, `Framework40`, `Framework45`, `FrameworkUap10` e `.NETCoreApp,Version=v1.1`.<br />TargetFrameworkAttribute é usado para detectar automaticamente essa opção a partir de seu assembly e o padrão `Framework40` é quando o atributo não está presente. Você deve especificar essa opção explicitamente se remover o [TargetFrameworkAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.versioning.targetframeworkattribute) de seus assemblies do .NET Core.<br />Se a estrutura de destino for especificada como **Framework35**, os testes serão executados no CLR 4,0 "modo de compatibilidade".<br />Exemplo: `/Framework:framework40`|
|**/TestCaseFilter:[*expressão*]**|Execute testes que correspondam à expressão fornecida.<br /><Expressão\> é do formato <propriedade\>=<valor\>[\|<Expressão\>].<br />Exemplo: `/TestCaseFilter:"Priority=1"`<br />Exemplo: `/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />A opção de linha de comando **/TestCaseFilter** não pode ser usada com a opção de linha de comando **/Tests**. <br />Para obter informações sobre como criar e usar expressões, confira [Filtro TestCase](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md).|
|**/?**|Exibe informações de uso.|
|**/Logger:[*uri/nome_amigável*]**|Especificar um agente para resultados do teste. Especifique o parâmetro várias vezes para habilitar vários agentes.<br />Exemplo: para registrar os resultados em um arquivo de Resultados de Teste do Visual Studio (TRX), use<br />**/Logger: TRX**<br />**[; LogFilename = \<Defaults to unique file name> ]**|
|**/ListTests:[*nome do arquivo*]**|Lista testes descobertos do contêiner de teste fornecido.|
|**/ListDiscoverers**|Lista detectores de testes instalados.|
|**/ListExecutors**|Lista executores de testes instalados.|
|**/ListLoggers**|Lista agentes de testes instalados.|
|**/ListSettingsProviders**|Lista provedores de configurações de teste instalados.|
|**/Blame**|Executa os testes no modo blame. Essa opção é útil para isolar testes problemáticos que causam falha no host de teste. Quando uma falha é detectada, ela cria um arquivo de sequência no `TestResults/<Guid>/<Guid>_Sequence.xml` que captura a ordem dos testes que foram executados antes da falha. Para obter mais informações, consulte [coletor de dados do culpado](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md).|
|**/Diag:[*nome do arquivo*]**|Grava os logs de rastreamento de diagnóstico no arquivo especificado.|
|**/ResultsDirectory:[*caminho*]**|O diretório de resultados de teste será criado no caminho especificado, se não existir.<br />Exemplo: `/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*IDProcessoPai*]**|ID do Processo Pai responsável por iniciar o processo atual.|
|**/Port:[*porta*]**|A porta para a conexão de soquete e recebimento das mensagens do evento.|
|**/Collect:[*NomeAmigável ColetorDados*]**|Habilita o coletor de dados para a execução de teste. [Mais informações](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md).|

> [!TIP]
> As opções e os valores não diferenciam maiúsculas de minúsculas.

## <a name="examples"></a>Exemplos

A sintaxe para executar o *vstest.console.exe* é:

`vstest.console.exe [TestFileNames] [Options]`

O comando a seguir executa *vstest.console.exe* para a biblioteca de teste *myTestProject.dll*:

```cmd
vstest.console.exe myTestProject.dll
```

O comando a seguir executa *vstest.console.exe* com vários arquivos de teste. Separe os nomes de arquivo de teste com espaços:

```cmd
vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

O comando a seguir executa *vstest.console.exe* com várias opções. Ele executa os testes no arquivo *myTestFile.dll* em um processo isolado e usa as configurações especificadas no arquivo *Local.RunSettings*. Além disso, ele apenas executa os testes marcados como "Prioridade=1" e registra em log os resultados em um arquivo *.trx*.

```cmd
vstest.console.exe myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```

O comando a seguir executa *vstest.console.exe* com a `/blame` opção para a biblioteca de teste *myTestProject.dll*:

```cmd
vstest.console.exe myTestFile.dll /blame
```

Se uma falha de host de teste ocorreu, o arquivo de *sequence.xml* é gerado. O arquivo contém nomes totalmente qualificados dos testes em sua sequência de execução até e incluindo o teste específico que estava sendo executado no momento da falha.

Se não houver falha no host de teste, o arquivo de *sequence.xml* não será gerado.

Exemplo de um arquivo de *sequence.xml* gerado: 

```xml
<?xml version="1.0"?>
<TestSequence>
  <Test Name="TestProject.UnitTest1.TestMethodB" Source="D:\repos\TestProject\TestProject\bin\Debug\TestProject.dll" />
  <Test Name="TestProject.UnitTest1.TestMethodA" Source="D:\repos\TestProject\TestProject\bin\Debug\TestProject.dll" />
</TestSequence>
```
