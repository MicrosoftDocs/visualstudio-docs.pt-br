---
title: Configurar testes de unidade com um arquivo .runsettings
description: Saiba como usar o arquivo. RunSettings no Visual Studio para configurar testes de unidade que são executados a partir da linha de comando, do IDE ou em um fluxo de trabalho de compilação.
ms.custom: SEO-VS-2020
ms.date: 07/15/2020
ms.topic: conceptual
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 9d6b4dd8bd21da7fcfc4d7cde54e5f5a7926472e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165716"
---
# <a name="configure-unit-tests-by-using-a-runsettings-file"></a>Configurar testes de unidade usando um arquivo *. RunSettings*

Os testes de unidade no Visual Studio podem ser configurados usando um arquivo *. RunSettings* . Por exemplo, é possível alterar a versão do .NET na qual os testes são executados, o diretório para os resultados de teste ou os dados coletados durante uma execução de teste. Um uso comum de um arquivo *.runsettings* é personalizar a [análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

Arquivos de configurações de execução podem ser usados para configurar testes que são executados a partir da [linha de comando](vstest-console-options.md), do IDE ou em um fluxo de [trabalho de compilação](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true) usando Azure Test Plans ou Team Foundation Server (TFS).

Arquivos de configurações de execução são opcionais. Se você não precisar de nenhuma configuração especial, não precisará de um arquivo *. RunSettings* .

## <a name="create-a-run-settings-file-and-customize-it"></a>Criar um arquivo de configurações de execução e personalizá-lo

1. Adicione um arquivo de configurações de execução à sua solução. No **Gerenciador de soluções**, no menu de atalho da sua solução, escolha **Adicionar**  >  **novo item** e selecione **arquivo XML**. Salve o arquivo com um nome como *Test. RunSettings*.

   > [!TIP]
   > O nome do arquivo não é importante, desde que você use a extensão *.runsettings*.

2. Adicione o conteúdo do [arquivo de exemplo *. RunSettings](#example-runsettings-file)e, em seguida, personalize-o para suas necessidades, conforme descrito nas seções a seguir.

3. Especifique o arquivo *. RunSettings que você deseja usando um dos seguintes métodos:

   - [Visual Studio IDE](#specify-a-run-settings-file-in-the-ide)
   - [Linha de comando](#specify-a-run-settings-file-from-the-command-line)
   - [Crie um fluxo de trabalho](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true) usando Azure Test Plans ou Team Foundation Server (TFS).

4. Execute os testes de unidade para usar as configurações de execução personalizadas.

::: moniker range="vs-2017"

Se você quiser desativar e ativar as configurações personalizadas no IDE, desmarque ou selecione o arquivo no menu configurações do teste **de teste** >  .

![Menu de configurações do teste com o arquivo de configurações personalizadas no Visual Studio 2017](../test/media/codecoverage-settingsfile.png)

::: moniker-end

::: moniker range=">=vs-2019"

Se você quiser desativar e ativar as configurações personalizadas no IDE, desmarque ou selecione o arquivo no menu de **teste** .

::: moniker-end

> [!TIP]
> Crie mais de um arquivo *.runsettings* na solução e selecione um como o arquivo ativo de configurações do teste, conforme necessário.

## <a name="specify-a-run-settings-file-in-the-ide"></a>Especificar um arquivo de configurações de execução no IDE

Os métodos disponíveis dependem da sua versão do Visual Studio.

::: moniker range="vs-2017"
Para especificar um arquivo de configurações de execução no IDE, selecione **Teste** > **Configurações do Teste** > **Selecionar Arquivo de Configurações do Teste** e, em seguida, selecione o arquivo *.runsettings*.

![Selecionar o menu do arquivo de configurações do teste no Visual Studio 2017](media/select-test-settings-file.png)

O arquivo será exibido no menu de Configurações do Teste e você poderá marcá-lo ou desmarcá-lo. Quando estiver marcado, o arquivo de configurações de execução se aplicará sempre que você selecionar **Analisar Cobertura de Código**.
::: moniker-end

::: moniker range=">=vs-2019"

### <a name="visual-studio-2019-version-164-and-later"></a>Visual Studio 2019 versão 16,4 e posterior

Há três maneiras de especificar um arquivo de configurações de execução no Visual Studio 2019 versão 16,4 e posterior.

- [Detectar automaticamente as configurações de execução](#autodetect-the-run-settings-file)
- [Definir manualmente as configurações de execução](#manually-select-the-run-settings-file)
- [Definir uma propriedade de compilação](#set-a-build-property)

#### <a name="autodetect-the-run-settings-file"></a>Detectar automaticamente o arquivo de configurações de execução

Para detectar automaticamente o arquivo de configurações de execução, coloque-o na raiz da sua solução.

Se a detecção automática de arquivos de configurações de execução estiver habilitada, as configurações nesse arquivo serão aplicadas em todos os testes executados. Você pode ativar a detecção automática de arquivos RunSettings usando dois métodos:

- Selecione **ferramentas** > **Opções** > **testar** > **detectar automaticamente arquivos RunSettings**

   ![Opção de detecção automática de arquivo RunSettings no Visual Studio 2019](media/vs-2019/auto-detect-runsettings-tools-window.png)

- Selecione **testar** > **definir configurações de execução** > **detectar automaticamente arquivos RunSettings**

   ![Menu de detecção automática de arquivos do RunSettings no Visual Studio 2019](media/vs-2019/auto-detect-runsettings-menu.png)

#### <a name="manually-select-the-run-settings-file"></a>Selecionar manualmente o arquivo de configurações de execução

No IDE, selecione **testar** > **definir configurações de execução** > **Selecione arquivo de RunSettings de toda a solução** e, em seguida, selecione o arquivo *. RunSettings* .

   - Esse arquivo substitui o arquivo *. RunSettings* na raiz da solução, se houver um, e é aplicado em todos os testes executados.
   - Esta seleção de arquivo só persiste localmente.

![Selecione testar o menu arquivo de RunSettings de toda a solução no Visual Studio 2019](media/vs-2019/select-solution-settings-file.png)

#### <a name="set-a-build-property"></a>Definir uma propriedade de compilação

Adicione uma propriedade de compilação a um projeto por meio do arquivo de projeto ou um arquivo Directory. Build. props. O arquivo de configurações de execução para um projeto é especificado pela propriedade **RunSettingsFilePath**.

- Atualmente, há suporte para configurações de execução de nível de projeto em projetos C#, VB, C++ e F #.
- Um arquivo especificado para um projeto substitui qualquer outro arquivo de configurações de execução especificado na solução.
- [Essas propriedades do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md) podem ser usadas para especificar o caminho para o arquivo RunSettings.

Exemplo de especificação de um arquivo *. RunSettings* para um projeto:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <RunSettingsFilePath>$(MSBuildProjectDirectory)\example.runsettings</RunSettingsFilePath>
  </PropertyGroup>
  ...
</Project>
```

### <a name="visual-studio-2019-version-163-and-earlier"></a>Visual Studio 2019 versão 16,3 e anterior

Para especificar um arquivo de configurações de execução no IDE, selecione **testar**  >  **Selecionar arquivo de configurações**. Navegue até o arquivo *.runsettings* e selecione-o.

![Selecionar o menu do arquivo de configurações do teste no Visual Studio 2019](media/vs-2019/select-settings-file.png)

O arquivo aparece no menu teste e você pode selecioná-lo ou desselecioná-lo. Quando estiver marcado, o arquivo de configurações de execução se aplicará sempre que você selecionar **Analisar Cobertura de Código**.
::: moniker-end

## <a name="specify-a-run-settings-file-from-the-command-line"></a>Especificar um arquivo de configurações de execução na linha de comando

Para executar testes da linha de comando, use *vstest.console.exe* e especifique o arquivo de configurações usando o parâmetro **/Settings** .

1. Abra o [prompt de comando do desenvolvedor para Visual Studio](../ide/reference/command-prompt-powershell.md).

2. Insira um comando semelhante a:

   ```cmd
   vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage /Settings:CodeCoverage.runsettings
   ```

   ou

   ```cmd
   vstest.console.exe --settings:test.runsettings test.dll
   ```

Para obter mais informações, consulte [Opções de linha de comando de VSTest.Console.exe](vstest-console-options.md).

## <a name="the-runsettings-file"></a>O arquivo *. RunSettings

O arquivo *. RunSettings é um arquivo XML que contém elementos de configuração diferentes dentro do elemento **RunSettings** . As seções a seguir detalham os diferentes elementos. Para obter um exemplo completo, consulte o [arquivo de exemplo *. RunSettings](#example-runsettings-file).

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- configuration elements -->
</RunSettings>
```

Cada um dos elementos de configuração é opcional porque tem um valor padrão.

## <a name="runconfiguration-element"></a>Elemento RunConfiguration

```xml
<RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <ResultsDirectory>.\TestResults</ResultsDirectory>
    <TargetPlatform>x86</TargetPlatform>
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>
    <TestSessionTimeout>10000</TestSessionTimeout>
    <TreatNoTestsAsError>true</TreatNoTestsAsError>
</RunConfiguration>
```

O elemento **RunConfiguration** pode incluir os seguintes elementos:

|Nó|Padrão|Valores|
|-|-|-|
|**MaxCpuCount**|1|Essa configuração controla o grau de execução de teste paralela ao executar testes de unidade usando os núcleos disponíveis no computador. O mecanismo de execução de testes inicia como um processo distinto em cada núcleo disponível e fornece um contêiner para cada núcleo com testes a serem executados. Um contêiner pode ser um assembly, uma DLL ou um artefato relevante. O contêiner do teste está agendando a unidade. Em cada contêiner, os testes são executados de acordo com a estrutura de teste. Se houver muitos contêineres, à medida que os processos concluírem a execução dos testes em um contêiner, eles passarão para o próximo contêiner disponível.<br /><br />MaxCpuCount pode ser:<br /><br />n, em que 1 <= n <= número de núcleos: até n processos são iniciados<br /><br />n, em que n = qualquer outro valor: o número de processos iniciados pode ser até o número de núcleos disponíveis. Por exemplo, defina n = 0 para permitir que a plataforma decida automaticamente o número ideal de processos a serem iniciados com base no ambiente.|
|**ResultsDirectory**||O diretório no qual os resultados do teste são colocados. O caminho é relativo ao diretório que contém o arquivo. RunSettings.|
|**TargetFrameworkVersion**|Framework40|`FrameworkCore10` para fontes do .NET Core, `FrameworkUap10` para fontes baseadas no UWP, `Framework45` para o .NET Framework 4.5 e posterior, `Framework40` para o .NET Framework 4.0 e `Framework35` para o .NET Framework 3.5.<br /><br />Essa configuração especifica a versão da estrutura de teste de unidade usada para descobrir e executar os testes. Pode ser diferente da versão da plataforma .NET especificada nas propriedades de compilação do projeto de teste de unidade.<br /><br />Se você omitir o elemento `TargetFrameworkVersion` a partir do arquivo *.runsettings*, a plataforma determinará automaticamente a versão da estrutura com base nos binários compilados.|
|**TargetPlatform**|x86|x86, x64|
|**TreatTestAdapterErrorsAsWarnings**|false|false, true|
|**TestAdaptersPaths**||Um ou mais caminhos para o diretório no qual os TestAdapters estão localizados|
|**TestSessionTimeout**||Permite que os usuários finalizem uma sessão de teste quando ele exceder o tempo limite determinado. Definir um tempo limite assegura que os recursos serão restritos e as sessões de teste serão restritas a um período de tempo. Essa configuração está disponível no **Visual Studio 2017 versão 15.5** e posterior.|
|**DotnetHostPath**||Especifique um caminho personalizado para o host dotnet que é usado para executar o testhost. Isso é útil quando você está criando seu próprio dotnet, por exemplo, ao criar o repositório dotnet/tempo de execução. A especificação dessa opção irá ignorar a procura de testhost.exe e sempre usará o testhost.dll.|
|**TreatNoTestsAsError**|false| true ou false <br>Especifique um valor booliano, que define o código de saída quando nenhum teste é descoberto. Se o valor for `true` e nenhum teste for descoberto, um código de saída diferente de zero será retornado. Caso contrário, zero será retornado.|

## <a name="datacollectors-element-diagnostic-data-adapters"></a>Elemento datacoletores (adaptadores de dados de diagnóstico)

O elemento **DataCollectors** especifica as configurações de adaptadores de dados de diagnóstico. Os adaptadores de dados de diagnóstico coletam informações adicionais sobre o ambiente e o aplicativo em teste. Cada adaptador tem configurações padrão e você só precisará fornecer configurações caso não deseje usar os padrões.

```xml
<DataCollectionRunSettings>
  <DataCollectors>
    <!-- data collectors -->
  </DataCollectors>
</DataCollectionRunSettings>
```

### <a name="codecoverage-data-collector"></a>Coletor de dados do CodeCoverage

O coletor de dados de cobertura de código cria um log das partes do código do aplicativo que foram utilizadas no teste. Para obter informações detalhadas sobre como personalizar as configurações de cobertura de código, consulte [Personalizar análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

```xml
<DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
  <Configuration>
    <CodeCoverage>
      <ModulePaths>
        <Exclude>
          <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
        </Exclude>
      </ModulePaths>

      <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
      <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
      <CollectFromChildProcesses>True</CollectFromChildProcesses>
      <CollectAspDotNet>False</CollectAspDotNet>
    </CodeCoverage>
  </Configuration>
</DataCollector>
```

### <a name="videorecorder-data-collector"></a>Coletor de dados do VideoRecorder

O coletor de dados de vídeo captura uma gravação de tela quando os testes são executados. A gravação é útil para solucionar problemas de testes de interface do usuário. O coletor de dados de vídeo está disponível no **Visual Studio 2017 versão 15.5** e posterior. Para obter um exemplo de como configurar esse coletor de dados, consulte o [arquivo de exemplo *. RunSettings](#example-runsettings-file).

Para personalizar qualquer outro tipo de adaptador de dados de diagnóstico, use um [arquivo de configurações do teste](../test/collect-diagnostic-information-using-test-settings.md).

### <a name="blame-data-collector"></a>Coletor de dados de culpa

Essa opção pode ajudá-lo a isolar um teste problemático que causa uma falha no host de teste. A execução do coletor cria um arquivo de saída (*Sequence.xml*) em *TestResults*, que captura a ordem de execução do teste antes da falha.

```xml
<DataCollector friendlyName="blame" enabled="True">
</DataCollector>
```

## <a name="testrunparameters"></a>TestRunParameters

```xml
<TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="docsUrl" value="https://docs.microsoft.com" />
</TestRunParameters>
```

Os parâmetros de execução de teste fornecem uma maneira de definir variáveis e valores que estão disponíveis para os testes em tempo de execução. Acesse os parâmetros usando a <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.Properties%2A?displayProperty=nameWithType> Propriedade MSTest (ou o NUnit [TestContext](https://docs.nunit.org/articles/nunit/writing-tests/TestContext.html)):

```csharp
private string _appUrl;
public TestContext TestContext { get; set; }

[TestMethod] // [Test] for NUnit
public void HomePageTest()
{
    string _appURL = TestContext.Properties["webAppUrl"];
}
```

Para usar parâmetros de execução de teste, adicione uma <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> propriedade pública à sua classe de teste.

## <a name="loggerrunsettings-element"></a>Elemento LoggerRunSettings

A `LoggerRunSettings` seção define um ou mais agentes de log a serem usados para a execução de teste. Os agentes mais comuns são console, Visual Studio Resultados de Teste File (TRX) e HTML.

```xml
<LoggerRunSettings>
    <Loggers>
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
    </Loggers>
  </LoggerRunSettings>
```

## <a name="mstest-element"></a>Elemento MSTest

Essas configurações são específicas para o adaptador de teste que executa os métodos de teste que têm o atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>.

```xml
<MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
</MSTest>
```

|Configuração|Padrão|Valores|
|-|-|-|
|**ForcedLegacyMode**|false|No Visual Studio 2012, o adaptador MSTest foi otimizado para torná-lo mais rápido e mais escalonável. Alguns comportamentos, como a ordem em que os testes são executados, não podem ser exatamente iguais aos de edições anteriores do Visual Studio. Defina esse valor como **true** para usar o adaptador de teste mais antigo.<br /><br />Por exemplo, você poderá usar essa configuração se tiver um arquivo *app.config* especificado para um teste de unidade.<br /><br />Recomendamos que você considere refatorar seus testes para permitir o uso do adaptador mais recente.|
|**IgnoreTestImpact**|false|O recurso de impacto de teste prioriza os testes que são afetados por alterações recentes, quando executado em MSTest ou de Microsoft Test Manager (preterido no Visual Studio 2017). Essa configuração desativa o recurso. Para obter mais informações, confira [Quais testes devem ser executados desde um build anterior](/previous-versions/dd286589(v=vs.140)).|
|**SettingsFile**||Especifique um arquivo de configurações do teste para usar com o adaptador MSTest aqui. Você também pode especificar um arquivo de configurações do teste [no menu de configurações](#specify-a-run-settings-file-in-the-ide).<br /><br />Se você especificar esse valor, também será necessário definir o **ForcedlegacyMode** como **true**.<br /><br />`<ForcedLegacyMode>true</ForcedLegacyMode>`|
|**KeepExecutorAliveAfterLegacyRun**|false|Após a execução do teste ser concluída, o MSTest será fechado. Qualquer processo iniciado como parte do teste também será eliminado. Caso deseje manter o executor de teste ativo, defina o valor como **true**. Por exemplo, você pode usar essa configuração para manter o navegador em execução entre os testes de IU codificados.|
|**DeploymentEnabled**|true|Se você definir esse valor como **false**, os itens de implantação especificados no método de teste não serão copiados para o diretório de implantação.|
|**CaptureTraceOutput**|true|Grave no rastreamento de depuração por meio do método de teste usando <xref:System.Diagnostics.Trace.WriteLine%2A?displayProperty=nameWithType>.|
|**DeleteDeploymentDirectoryAfterTestRunIsComplete**|true|Para reter o diretório de implantação após uma execução de teste, defina esse valor como **false**.|
|**MapInconclusiveToFailed**|false|Se um teste for concluído com um status inconclusivo, ele será mapeado para o status Ignorado no **Gerenciador de Testes**. Caso deseje que os testes inconclusivos sejam mostrados como com falha, defina esse valor como **true**.|
|**InProcMode**|false|Caso deseje que os testes sejam executados no mesmo processo do adaptador MSTest, defina esse valor como **true**. Essa configuração fornece um ganho menor de desempenho. No entanto, se um teste for encerrado com uma exceção, os testes restantes não serão executados.|
|**AssemblyResolution**|false|É possível especificar caminhos para outros assemblies ao localizar e executar testes de unidade. Por exemplo, use esses caminhos para assemblies de dependência que não estão no mesmo diretório do assembly de teste. Para especificar um caminho, use um elemento **Caminho do Diretório**. Os caminhos podem incluir variáveis de ambiente.<br /><br />`<AssemblyResolution>  <Directory Path="D:\myfolder\bin\" includeSubDirectories="false"/> </AssemblyResolution>`|

## <a name="example-runsettings-file"></a>Arquivo *. RunSettings* de exemplo

O XML a seguir mostra o conteúdo de um arquivo *.runsettings* típico. Copie esse código e edite-o para atender às suas necessidades.

Cada elemento do arquivo é opcional, porque tem um valor padrão.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- Configurations that affect the Test Framework -->
  <RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <!-- Path relative to directory that contains .runsettings file-->
    <ResultsDirectory>.\TestResults</ResultsDirectory>

    <!-- x86 or x64 -->
    <!-- You can also change it from the Test menu; choose "Processor Architecture for AnyCPU Projects" -->
    <TargetPlatform>x86</TargetPlatform>

    <!-- Framework35 | [Framework40] | Framework45 -->
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>

    <!-- Path to Test Adapters -->
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>

    <!-- TestSessionTimeout was introduced in Visual Studio 2017 version 15.5 -->
    <!-- Specify timeout in milliseconds. A valid value should be greater than 0 -->
    <TestSessionTimeout>10000</TestSessionTimeout>

    <!-- true or false -->
    <!-- Value that specifies the exit code when no tests are discovered -->
    <TreatNoTestsAsError>true</TreatNoTestsAsError>
  </RunConfiguration>

  <!-- Configurations for data collectors -->
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
            <ModulePaths>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- We recommend you do not change the following values: -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>

      <DataCollector uri="datacollector://microsoft/VideoRecorder/1.0" assemblyQualifiedName="Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder.VideoRecorderDataCollector, Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder, Version=15.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" friendlyName="Screen and Voice Recorder">
        <!--Video data collector was introduced in Visual Studio 2017 version 15.5 -->
        <Configuration>
          <!-- Set "sendRecordedMediaForPassedTestCase" to "false" to add video attachments to failed tests only -->
          <MediaRecorder sendRecordedMediaForPassedTestCase="true"  xmlns="">           
            <ScreenCaptureVideo bitRate="512" frameRate="2" quality="20" />
          </MediaRecorder>
        </Configuration>
      </DataCollector>

      <!-- Configuration for blame data collector -->
      <DataCollector friendlyName="blame" enabled="True">
      </DataCollector>

    </DataCollectors>
  </DataCollectionRunSettings>

  <!-- Parameters used by tests at run time -->
  <TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="webAppUserName" value="Admin" />
    <Parameter name="webAppPassword" value="Password" />
  </TestRunParameters>

  <!-- Configuration for loggers -->
  <LoggerRunSettings>
    <Loggers>
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="blame" enabled="True" />
    </Loggers>
  </LoggerRunSettings>

  <!-- Adapter Specific sections -->

  <!-- MSTest adapter -->
  <MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
  </MSTest>

</RunSettings>
```

## <a name="specify-environment-variables-in-the-runsettings-file"></a>Especificar variáveis de ambiente no arquivo *. RunSettings*

As variáveis de ambiente podem ser definidas no arquivo *. RunSettings* , que pode interagir diretamente com o host de teste. A especificação de variáveis de ambiente no arquivo *. RunSettings* é necessária para dar suporte a projetos não triviais que exigem a configuração de variáveis de ambiente, como *DOTNET_ROOT*. Essas variáveis são definidas durante a geração do processo de host de teste e estão disponíveis no host.

### <a name="example"></a>Exemplo

O código a seguir é um arquivo *. RunSettings* de exemplo que passa variáveis de ambiente:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- File name extension must be .runsettings -->
<RunSettings>
  <RunConfiguration>
    <EnvironmentVariables>
      <!-- List of environment variables we want to set-->
      <DOTNET_ROOT>C:\ProgramFiles\dotnet</DOTNET_ROOT>
      <SDK_PATH>C:\Codebase\Sdk</SDK_PATH>
    </EnvironmentVariables>
  </RunConfiguration>
</RunSettings>
```

O nó **RunConfiguration** deve conter um nó **EnvironmentVariables** . Uma variável de ambiente pode ser especificada como um nome de elemento e seu valor.

> [!NOTE]
> Como essas variáveis de ambiente sempre devem ser definidas quando o host de teste é iniciado, os testes sempre devem ser executados em um processo separado. Para isso, o sinalizador */InIsolation* será definido quando houver variáveis de ambiente para que o host de teste sempre seja invocado.

## <a name="see-also"></a>Confira também

- [Configurar uma execução de teste](https://github.com/microsoft/vstest-docs/blob/master/docs/configure.md)
- [Personalizar a análise de cobertura de código](../test/customizing-code-coverage-analysis.md)
- [Tarefa de teste do Visual Studio (Azure Test Plans)](/azure/devops/pipelines/tasks/test/vstest?view=vsts&preserve-view=true)
