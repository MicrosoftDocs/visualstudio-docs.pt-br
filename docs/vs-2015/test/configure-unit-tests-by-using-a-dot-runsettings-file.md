---
title: Configurar testes de unidade usando um arquivo .runsettings | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7e9e4a2-5d01-4f78-b408-5be3892bd162
caps.latest.revision: 28
ms.author: gewarren
manager: douge
ms.openlocfilehash: 806c19b7132a4541ff97c253700a5e5e980ef556
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49817971"
---
# <a name="configure-unit-tests-by-using-a-runsettings-file"></a>Configurar testes de unidade usando um arquivo .runsettings
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os testes de unidade no Visual Studio podem ser configurados com um arquivo *.runsettings. (O nome do arquivo não importa, contanto que você use a extensão ‘.runsettings.’) Por exemplo, é possível alterar o .NET Framework em que os testes serão executados, o diretório no qual os resultados de teste são enviados e os dados coletados durante uma execução de teste.  
  
 Se não desejar adicionar nenhuma configuração especial, não é preciso ter um arquivo *.runsettings. O uso mais frequente é para personalizar a [Cobertura de Código](../test/customizing-code-coverage-analysis.md).  
  
> [!NOTE]
>  **.runsettings e .testsettings**  
>   
>  Há dois tipos de arquivo para a configuração de testes. *.runsettings são usados para testes de unidade. E \*.testsettings para [testes de ambiente de laboratório](http://msdn.microsoft.com/library/0c15317e-80c6-4317-aed3-82b8e15e3901), testes de carga e desempenho da Web e para personalizar alguns tipos de adaptadores de dados de diagnóstico, como adaptadores de log de evento e IntelliTrace.  
>   
>  Em edições anteriores do Visual Studio até 2010, os testes de unidade também eram personalizados com arquivos *.testsettings. Ainda é possível fazer isso, mas os testes serão executados mais lentamente do que usando as configurações equivalentes em um arquivo \*.runsettings.  
  
## <a name="customizing-tests-with-a-runsettings-file"></a>Personalizando testes com um arquivo .runsettings  
  
1. Adicione um arquivo XML à solução Visual Studio e renomeie-o para test.runsettings. (O nome do arquivo não importa, mas a extensão deve ser .runsettings.)  
  
2. Substitua o conteúdo do arquivo pelo [exemplo](#example).  
  
    Edite-o conforme suas necessidades.  
  
3. No menu **Testar**, escolha **Configurações de Teste**, **Selecionar Arquivo de Configurações de Teste**.  
  
   É possível criar mais de um arquivo \*.runsettings em sua solução e habilitá-los ou desabilitá-los em momentos diferentes com o menu **Configurações de Teste**.  
  
   ![Habilitando um arquivo de configurações de execução](../test/media/runsettings-1.png "RunSettings-1")  
  
##  <a name="example"></a> Copiar este exemplo de arquivo .runsettings  
 Veja um arquivo *.runsettings típico. Cada elemento do arquivo é opcional, porque cada valor possui um padrão.  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<RunSettings>  
  <!-- Configurations that affect the Test Framework -->  
  <RunConfiguration>  
    <MaxCpuCount>1</MaxCpuCount>  
    <!-- Path relative to solution directory -->  
    <ResultsDirectory>.\TestResults</ResultsDirectory>  
  
    <!-- [x86] | x64    
      - You can also change it from menu Test, Test Settings, Default Processor Architecture -->  
    <TargetPlatform>x86</TargetPlatform>  
  
    <!-- Framework35 | [Framework40] | Framework45 -->  
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>  
  
    <!-- Path to Test Adapters -->  
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>  
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
  
    </DataCollectors>  
  </DataCollectionRunSettings>  
  
  <!-- Parameters used by tests at runtime -->  
  <TestRunParameters>  
    <Parameter name="webAppUrl" value="http://localhost" />  
    <Parameter name="webAppUserName" value="Admin" />  
    <Parameter name="webAppPassword" value="Password" />  
  </TestRunParameters>  
  
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
  
 O arquivo .runsettings também é usado para configurar a [Cobertura de Código](../test/customizing-code-coverage-analysis.md).  
  
 O restante deste tópico descreve o conteúdo do arquivo.  
  
## <a name="edit-your-runsettings-file"></a>Editar o arquivo .runsettings  
 O arquivo .runsettings possui os elementos a seguir.  
  
### <a name="test-run-configuration"></a>Configuração de execução de teste  
  
|Nó|Padrão|Valores|  
|----------|-------------|------------|  
|`ResultsDirectory`||O diretório no qual os resultados do teste serão colocados.|  
|`TargetFrameworkVersion`|Framework40|Framework35, Framework40, Framework45<br /><br /> Isso especifica qual versão do framework de testes de unidade é usada para descobrir e executar os testes. Pode ser diferente da versão da plataforma .NET especificada nas propriedades de compilação do projeto de teste de unidade.|  
|`TargetPlatform`|x86|x86, x64|  
|`TreatTestAdapterErrorsAsWarnings`|false|false, true|  
|`TestAdaptersPaths`||Um ou vários caminhos para o diretório em que os TestAdapters estão localizados|  
|`MaxCpuCount`|1|Isso controla o grau de execução de teste paralela ao executar testes de unidade usando os núcleos disponíveis no computador.  O mecanismo de execução de testes inicia como um processo distinto em cada núcleo disponível e fornece um contêiner para cada núcleo com testes a serem executados, como um assembly, DLL ou artefato relevante.  O contêiner do teste está agendando a unidade.  Em cada contêiner, os testes são executados de acordo com a estrutura de teste.  Se houver muitos contêineres, à medida que os processos terminarem de executar os testes em um contêiner, eles passarão para o próximo contêiner disponível.<br /><br /> MaxCpuCount pode ser:<br /><br /> n,em que 1 <= n <= número de núcleos: até n processos serão iniciados<br /><br /> n, em que n = qualquer outro valor: o número de processos iniciados será até a quantidade de núcleos disponíveis no computador|  
  
### <a name="diagnostic-data-adapters-data-collectors"></a>Adaptadores de dados de diagnóstico (coletores de dados)  
 O elemento `DataCollectors` especifica configurações de adaptadores de dados de diagnóstico. Os adaptadores de dados de diagnóstico são usados para coletar informações adicionais sobre o ambiente e o aplicativo em teste. Cada adaptador tem configurações padrão, e você só precisará fornecer configurações caso não deseje usar os padrões.  
  
#### <a name="code-coverage-adapter"></a>Adaptador de cobertura de código  
 O coletor de dados de cobertura de código cria um log das partes do código do aplicativo que foram utilizadas no teste. Para obter mais informações sobre como personalizar as configurações de cobertura de código, consulte [Personalizando análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
#### <a name="other-diagnostic-data-adapters"></a>Outros adaptadores de dados de diagnóstico  
 O adaptador de cobertura de código é atualmente o único adaptador que pode ser personalizado usando o arquivo de configurações de execução.  
  
 Para personalizar qualquer outro tipo de adaptador de dados de diagnóstico, você deve usar um arquivo de configurações de teste. Para obter mais informações, consulte [Especificando configurações de teste do Visual Studio](http://msdn.microsoft.com/library/0c15317e-80c6-4317-aed3-82b8e15e3901).  
  
#### <a name="testrunparameters"></a>TestRunParameters  
 TestRunParameters fornece uma maneira de definir variáveis e valores disponíveis para os testes em tempo de execução.  
  
### <a name="mstest-run-settings"></a>Configurações de execução do MSTest  
 Essas configurações são específicas para o adaptador de teste que executa os métodos de teste que têm o atributo `[TestMethod]`.  
  
|Configuração|Padrão|Valores|  
|-------------------|-------------|------------|  
|ForcedLegacyMode|false|No Visual Studio 2012, o adaptador MSTest foi otimizado para torná-lo mais rápido e mais escalonável. Alguns comportamentos, como a ordem em que os testes são executados, não podem ser exatamente iguais aos de edições anteriores do Visual Studio. Defina esse valor como `true` para usar o adaptador mais antigo de teste.<br /><br /> Por exemplo, você poderá usar isso se tiver um arquivo app.config especificado para um teste de unidade.<br /><br /> Recomendamos que você considere refatorar seus testes para permitir o uso do adaptador mais recente.|  
|IgnoreTestImpact|false|O recurso de impacto de teste prioriza os testes que são afetados pelas alterações recentes, quando executados no MSTest ou no Microsoft Test Manager. Essa configuração desativa o recurso. Para obter mais informações, consulte [Como coletar dados para verificar quais testes devem ser executados após alterações feitas no código](http://msdn.microsoft.com/library/2f921ea1-9bb0-4870-a30f-0521fc22cb47).|  
|SettingsFile||Você pode especificar uma arquivo de configurações de teste para usar com o adaptador MSTest aqui. Também é possível especificar um arquivo de configurações de teste usando o menu **Testar**, **Configurações de Teste**, **Selecionar Arquivo de Configurações de Teste**.<br /><br /> Se você especificar esse valor, também será necessário definir o **ForcedlegacyMode** como **true**.<br /><br /> `<RunSettings>   <MSTest>     <SettingsFile>my.testsettings</SettingsFile>      <ForcedLegacyMode>true</ForcedLegacyMode>    </MSTest> </RunSettings>`|  
|KeepExecutorAliveAfterLegacyRun|false|Após a execução do teste ser concluída, o MSTest será fechado. Qualquer processo iniciado como parte do teste também será destruído nesse momento. Se você quiser manter o executor de teste ativo, transforme essa configuração em true.<br /><br /> Por exemplo, você pode usar isso para manter o navegador em execução entre os testes de IU codificados.|  
|DeploymentEnabled|true|Se você definir isso como false, os itens de implantação especificados em seu método de teste não serão copiados para o diretório de implantação.|  
|CaptureTraceOutput|true|Você pode gravar no rastreamento de depuração do método de teste usando Trace.WriteLine. Usando essa configuração, você pode desativar esses rastreamentos de depuração.|  
|DeleteDeploymentDirectoryAfterTestRunIsComplete|true|Você pode manter o Diretório de Implantação após um teste configurando esse valor para false.|  
|MapInconclusiveToFailed|false|Se um teste retornar com um status inconclusivo, ele geralmente será mapeado para o status Ignorado no Gerenciador de Testes. Se você quiser que os testes Inconclusivos sejam mostrados como Falha, use esta configuração.|  
|InProcMode|false|Se você quiser que os testes sejam executados no mesmo processo do adaptador MSTest, defina esse valor como true. Essa configuração fornece um ganho menor de desempenho. Mas se um teste fechar com uma exceção, os outros testes não continuarão.|  
|AssemblyResolution|false|É possível especificar caminhos para outros assemblies ao localizar e executar testes de unidade.  Por exemplo, use esses caminhos para assemblies de dependência que não residem no mesmo diretório que o assembly de teste.  Para especificar um caminho, use um elemento de “Caminho do diretório”.  Os caminhos podem conter variáveis de ambiente.<br /><br /> `<AssemblyResolution>  <Directory Path>"D:\myfolder\bin\" includeSubDirectories="false"/> </AssemblyResolution>`|  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando análise de cobertura de código](../test/customizing-code-coverage-analysis.md)   
 [Especificando configurações de teste para testes do Visual Studio](http://msdn.microsoft.com/library/0c15317e-80c6-4317-aed3-82b8e15e3901)



