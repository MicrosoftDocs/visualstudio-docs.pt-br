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
ms.openlocfilehash: bfca799111c83f29924c997218c42f09bff5568a
ms.sourcegitcommit: b4e0cc76d94fe8cf6d238c4cc09512d17131a195
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81224453"
---
# <a name="vstestconsoleexe-command-line-options"></a>Opções da linha de comando de VSTest.Console.exe

O *VSTest.Console.exe* é a ferramenta de linha de comando para execução de testes. É possível especificar várias opções em qualquer ordem na linha de comando. Essas opções são listadas em [Opções gerais de linha de comando](#general-command-line-options).

> [!NOTE]
> O adaptador MSTest no Visual Studio também funciona no modo herdado (equivalente à execução de testes com *mstest.exe*) para compatibilidade. No modo herdado, ele não pode aproveitar o recurso TestCaseFilter. O adaptador pode alternar para o modo herdado quando um arquivo *testsettings* é especificado, **forcelegacymode** é definido como **true** em um arquivo *runsettings* ou usando atributos como **HostType**.
>
> Para executar testes automatizados em um computador baseado na arquitetura ARM, use o *VSTest.Console.exe*.

Abra um [Prompt de comando do desenvolvedor](/dotnet/framework/tools/developer-command-prompt-for-vs) para usar a ferramenta de linha de comando, ou você pode encontrar a ferramenta em *%Program Files(x86)%\Microsoft Visual Studio\\<\> \\ versão<edição\>\common7\ide\CommonExtensions\\<Platform | Microsoft>*.

## <a name="general-command-line-options"></a>Opções gerais de linha de comando

A tabela a seguir lista todas as opções para o *VSTest.Console.exe*, além de breves descrições sobre elas. É possível ver um resumo semelhante digitando `VSTest.Console/?` na linha de comando.

| Opção | Descrição |
|---|---|
|**[*nomes dos arquivos de teste*]**|Executa testes dos arquivos especificados. Separa vários nomes de arquivo de teste com espaços.<br />Exemplos: `mytestproject.dll`, `mytestproject.dll myothertestproject.exe`|
|**/Settings:[*nome do arquivo*]**|Execute testes com configurações adicionais, como coletores de dados.<br />Exemplo: `/Settings:Local.RunSettings`|
|**/Tests:[*nome do teste*]**|Executa testes com nomes que contêm os valores fornecidos. Para fornecer vários valores, separe-os por vírgulas.<br />Exemplo: `/Tests:TestMethod1,testMethod2`<br />A opção de linha de comando **/Tests** não pode ser usada com a opção de linha de comando **/TestCaseFilter**.|
|**/Paralelo**|Especifica que os testes sejam executados em paralelo. Por padrão, todos os núcleos disponíveis no computador podem ser usados. Você pode configurar o número de núcleos a serem usados em um arquivo de configurações.|
|**/Enablecodecoverage**|Permite o adaptador de diagnóstico de dados CodeCoverage na execução de teste.<br />As configurações padrão serão usadas se não forem especificadas usando o arquivo de configurações.|
|**/InIsolation**|Executa os testes em um processo isolado.<br />Esse isolamento torna o processo *vstest.console.exe* menos suscetível a ser interrompido acidentalmente nos testes. Entretanto, os testes podem ser executados mais lentamente.|
|**/UseVsixExtensions**|Essa opção faz com que o processo *vstest.console.exe* use ou ignore as extensões VSIX instaladas (se houver) na execução de teste.<br />Essa opção foi preterida. A partir da próxima versão principal do Visual Studio, essa opção poderá ser removida. A migração para o consumo de extensões foi disponibilizada como um pacote NuGet.<br />Exemplo: `/UseVsixExtensions:true`|
|**/TestAdapterPath:[*caminho*]**|Força o processo *vstest.console.exe* a usar adaptadores de teste personalizados de um caminho especificado (se houver) na execução de teste.<br />Exemplo: `/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[*tipo de plataforma*]**|Arquitetura da plataforma de destino a ser usada para a execução de teste.<br />Os valores válidos são x86, x64 e ARM.|
|**/Framework: [*versão do framework*]**|Versão do .NET de destino a ser usada na execução do teste.<br />Exemplos de valores são `Framework35`, `Framework40`, `Framework45`, `FrameworkUap10` e `.NETCoreApp,Version=v1.1`.<br />Se a estrutura de destino for especificada como **Framework35**, os testes serão executados no "modo de compatibilidade" do CLR 4.0.<br />Exemplo: `/Framework:framework40`|
|**/TestCaseFilter:[*expressão*]**|Execute testes que correspondam à expressão fornecida.<br /><Expressão\> é do formato <propriedade\>=<valor\>[\|<Expressão\>].<br />Exemplo: `/TestCaseFilter:"Priority=1"`<br />Exemplo: `/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />A opção de linha de comando **/TestCaseFilter** não pode ser usada com a opção de linha de comando **/Tests**. <br />Para obter informações sobre como criar e usar expressões, confira [Filtro TestCase](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md).|
|**/?**|Exibe informações de uso.|
|**/Logger:[*uri/nome_amigável*]**|Especificar um agente para resultados do teste.<br />Exemplo: Para registrar resultados em um Arquivo de Resultados de Teste do Estúdio Visual (TRX), use<br />**/Logger:trx**<br />**[; LogFileName=\<Padrão para nome de arquivo exclusivo>]**|
|**/ListTests:[*nome do arquivo*]**|Lista testes descobertos do contêiner de teste fornecido.|
|**/ListDiscoverers**|Lista detectores de testes instalados.|
|**/ListExecutors**|Lista executores de testes instalados.|
|**/ListLoggers**|Lista agentes de testes instalados.|
|**/ListSettingsProviders**|Lista provedores de configurações de teste instalados.|
|**/Blame**|Acompanha os testes durante sua execução e, em caso de falha do processo de host de teste, emite os nomes de testes em sua sequência de execução até e incluindo o teste específico que estava em execução no momento da falha. Essa saída facilita o isolamento do teste incorreto e o diagnóstico adicional. [Mais informações.](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md)|
|**/Diag:[*nome do arquivo*]**|Grava os logs de rastreamento de diagnóstico no arquivo especificado.|
|**/ResultsDirectory:[*caminho*]**|O diretório de resultados de teste será criado no caminho especificado, se não existir.<br />Exemplo: `/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*IDProcessoPai*]**|ID do Processo Pai responsável por iniciar o processo atual.|
|**/Port:[*porta*]**|A porta para a conexão de soquete e recebimento das mensagens do evento.|
|**/Collect:[*NomeAmigável ColetorDados*]**|Habilita o coletor de dados para a execução de teste. [Mais informações.](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md)|

> [!TIP]
> As opções e os valores não diferenciam maiúsculas de minúsculas.

## <a name="examples"></a>Exemplos

A sintaxe para execução do *VSTest.Console.exe* é:

`Vstest.console.exe [TestFileNames] [Options]`

O seguinte comando executa o *VSTest.Console.exe* para a biblioteca de testes **myTestProject.dll**:

```cmd
vstest.console.exe myTestProject.dll
```

O comando a seguir executa o *VSTest.Console.exe* com vários arquivos de teste. Separe os nomes de arquivo de teste com espaços:

```cmd
Vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

O comando a seguir executa o *VSTest.Console.exe* com várias opções. Ele executa os testes no arquivo *myTestFile.dll* em um processo isolado e usa as configurações especificadas no arquivo *Local.RunSettings*. Além disso, ele apenas executa os testes marcados como "Prioridade=1" e registra em log os resultados em um arquivo *.trx*.

```cmd
vstest.console.exe  myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```
