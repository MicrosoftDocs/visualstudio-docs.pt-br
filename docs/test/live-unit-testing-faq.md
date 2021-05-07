---
title: Perguntas frequentes sobre o Live Unit Testing
description: Revise essas Live Unit Testing frequentes, incluindo estruturas, configuração e personalização com suporte.
ms.custom: SEO-VS-2020
ms.date: 10/03/2017
ms.topic: conceptual
helpviewer_keywords:
- Live Unit Testing FAQ
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
ms.openlocfilehash: bb2c9a4cae25b388d5817b04ff54f6e6443b2f44
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800468"
---
# <a name="live-unit-testing-frequently-asked-questions"></a>Perguntas frequentes sobre o Live Unit Testing

## <a name="supported-frameworks"></a>Estruturas com suporte

**Quais estruturas de teste são compatíveis com o Live Unit Testing e quais são as versões mínimas compatíveis?**

O Live Unit Testing funciona com as três estruturas de teste de unidade populares listadas na tabela a seguir. A versão mínima com suporte de seus adaptadores e suas estruturas também é listada na tabela. As estruturas de teste de unidade estão disponíveis em NuGet.org.

|Estrutura de teste  |Versão mínima do Adaptador do Visual Studio  |Versão mínima da Estrutura  |
|---------|---------|---------|
|xUnit.net |xunit.runner.visualstudio versão 2.2.0-beta3-build1187 |xunit 1.9.2 |
|NUnit |NUnit3TestAdapter versão 3.7.0 |NUnit versão 3.5.0 |
|MSTest |MSTest.TestAdapter 1.1.4-preview |MSTest.TestFramework 1.0.5-preview |

Se você tiver projetos de teste baseados no MSTest mais antigos que referenciam e não desejar mover para os pacotes NuGet do MSTest mais novos, atualize para o `Microsoft.VisualStudio.QualityTools.UnitTestFramework` Visual Studio 2019 ou Visual Studio 2017.

Em alguns casos, talvez seja necessário restaurar explicitamente os pacotes NuGet referenciados pelos projetos na solução para que o Live Unit Testing funcione. Você pode restaurar os pacotes fazendo um build explícito da solução (selecione Criar Solução de Recomposição no menu Visual Studio de nível superior) ou clicando com o botão direito do mouse na solução e selecionando Restaurar Pacotes  >   **NuGet** antes de habilenciar o Teste de Unidade Vivo.

## <a name="net-core-support"></a>Suporte do .NET Core

**O Live Unit Testing funciona com o .NET Core?**

Sim. O Live Unit Testing funciona com o .NET Core e .NET Framework.

## <a name="configuration"></a>Configuração

**Por que o Live Unit Testing não funciona ao ser ligado?**

A janela Saída (quando Live Unit Testing lista Live Unit Testing lista listada está selecionada) deve dizer por que Live Unit Testing está funcionando. O Live Unit Testing poderá não funcionar por um dos seguintes motivos:

- Se os pacotes NuGet referenciados pelos projetos na solução não tiverem sido restaurados, o Live Unit Testing não funcionará. Fazer uma compilação explícita da solução ou restaurar os pacotes NuGet na solução antes de ativar o Live Unit Testing deverá resolver esse problema.

- Se estiver usando testes baseados no MSTest nos projetos, lembre-se de remover a referência a `Microsoft.VisualStudio.QualityTools.UnitTestFramework` e adicionar referências aos últimos pacotes NuGet do MSTest: `MSTest.TestAdapter` (uma versão mínima de 1.1.11 é necessária) e `MSTest.TestFramework` (uma versão mínima de 1.1.11 é necessária). Para obter mais informações, confira a seção "Estruturas de teste compatíveis" do artigo [Usar o Live Unit Testing no Visual Studio](live-unit-testing.md#supported-test-frameworks).

- No mínimo, um projeto na solução deve ter uma referência ao NuGet ou uma referência direta à estrutura de teste do xUnit, NUnit ou MSTest. Esse projeto também deve referenciar um pacote NuGet de adaptadores de teste do Visual Studio correspondente. O adaptador de teste do Visual Studio também pode ser referenciado por meio de um arquivo *.runsettings*. O arquivo *.runsettings* precisa ter uma entrada como o seguinte exemplo:

```xml
<RunSettings>
    <RunConfiguration>
          <TestAdaptersPaths>path-to-your-test-adapter</TestAdaptersPaths>
     </RunConfiguration>
</RunSettings>
```

## <a name="incorrect-coverage-after-upgrade"></a>Cobertura incorreta após a atualização

**Por que o Live Unit Testing mostra uma cobertura incorreta depois de atualizar o adaptador de teste referenciado nos Projetos do Visual Studio para a versão com suporte?**

- Se vários projetos na solução referenciarem o pacote do adaptador de teste NuGet, cada um deles deverá ser atualizado para a versão com suporte.

- Certifique-se de que o arquivo *.props* do MSBuild importado do pacote do adaptador de teste também seja atualizado corretamente. Verifique a versão e o caminho da importação do pacote NuGet, que geralmente podem ser encontrados próximo à parte superior do arquivo de projeto, da seguinte forma:

   ```xml
    <Import Project="..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props" Condition="Exists('..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props')" />
   ```

## <a name="customize-builds"></a>Builds personalizados

**Posso personalizar meus builds do Live Unit Testing?**

Se sua solução exigir etapas personalizadas para criar para instrumentação (Live Unit Testing) que não são necessárias para o build "regular" não instrumentado, você poderá adicionar código ao seu projeto ou arquivos *.targets* que verificam a propriedade e executam etapas personalizadas de build `BuildingForLiveUnitTesting` pré/pós-build. Também é possível optar por remover algumas etapas de build (como publicar ou gerar pacotes) ou adicionar etapas de build (como copiar pré-requisitos) a um build do Live Unit Testing baseado na propriedade desse projeto. A personalização do build com base nessa propriedade não altera o build normal de nenhum modo e só afeta os builds do Live Unit Testing.

Por exemplo, pode haver um destino que produz pacotes NuGet durante um build normal. Provavelmente, você não desejará que os pacotes NuGet sejam gerados após cada edição feita. Portanto, é possível desabilitar esse destino no build do Live Unit Testing fazendo algo semelhante ao seguinte:  

```xml
<Target Name="GenerateNuGetPackages" BeforeTargets="AfterBuild" Condition="'$(BuildingForLiveUnitTesting)' != 'true'">
    <Exec Command='"$(MSBuildThisFileDirectory)..\tools\GenPac" '/>
</Target>
```

## <a name="error-messages-with-outputpath-outdir-or-intermediateoutputpath"></a>Mensagens de erro \<OutputPath> com ou \<OutDir>\<IntermediateOutputPath>

**Por que eu vejo o seguinte erro quando Live Unit Testing tenta criar minha solução: "... parece definir incondicionalmente `<OutputPath>` ou `<OutDir>` . Live Unit Testing executará testes do assembly de saída"?**

Você poderá obter esse erro se o processo de build da solução tiver uma lógica personalizada que especifica onde os binários devem ser gerados. Por padrão, o local de seus binários depende `<OutputPath>` de ou , bem como ou `<OutDir>` `<IntermediateOutputPath>` `<BaseOutputPath>` `<BaseIntermediateOutputPath>` .

Live Unit Testing substitui essas variáveis para garantir que os artefatos de build sejam descartados para uma pasta Live Unit Testing artefatos e falhará se o processo de build também substituir essas variáveis.

Há duas abordagens principais para criar Live Unit Testing build com êxito. Para configurações de build mais fáceis, você pode basear seus caminhos de saída em `<BaseIntermediateOutputPath>` . Para configurações mais complexas, você pode basear seus caminhos de saída `<LiveUnitTestingBuildRootPath>` .

### <a name="overriding-outputpathintermediateoutputpath-conditionally-based-on-baseoutputpath-baseintermediateoutputpath"></a>Substituindo `<OutputPath>` / `<IntermediateOutputPath>` condicionalmente com base em `<BaseOutputPath>` / `<BaseIntermediateOutputPath>` .

> [!NOTE]
> Para usar essa abordagem, cada projeto precisa ser capaz de criar de forma independente uma da outra. Não têm um artefato de referência de projeto de outro projeto durante a compilação. Não há um projeto carregar dinamicamente assemblies de outro projeto durante o tempo de execução (por exemplo, chamada `Assembly.Loadfile("..\..\Project2\Release\Project2.dll")` ).

Durante a compilação, Live Unit Testing substitui automaticamente as `<BaseOutputPath>` / `<BaseIntermediateOutputPath>` variáveis para direcionar a pasta Live Unit Testing artefatos.

Por exemplo, se o build substituir o <OutputPath>, conforme mostrado abaixo:

```xml
<Project>
  <PropertyGroup>
    <OutputPath>$(SolutionDir)Artifacts\$(Configuration)\bin\$(MSBuildProjectName)</OutputPath>
  </PropertyGroup>
</Project>
```

em seguida, substitua-o pelo seguinte XML:

```xml
<Project>
  <PropertyGroup>
    <BaseOutputPath Condition="'$(BaseOutputPath)' == ''">$(SolutionDir)Artifacts\$(Configuration)\bin\$(MSBuildProjectName)\</BaseOutputPath>
    <OutputPath Condition="'$(OutputPath)' == ''">$(BaseOutputPath)</OutputPath>
  </PropertyGroup>
</Project>
```

Isso garante que `<OutputPath>` reside na pasta `<BaseOutputPath>`.

Não substitua `<OutDir>` diretamente no processo de build; em vez disso, substitua `<OutputPath>` para soltar os artefatos de build em uma localização específica.

### <a name="overriding-your-properties-based-on-the-liveunittestingbuildrootpath-property"></a>Substituindo suas propriedades com base na `<LiveUnitTestingBuildRootPath>` propriedade.

> [!NOTE]
> Nessa abordagem, você precisa ter cuidado com os arquivos adicionados na pasta de artefatos que não são gerados durante a compilação. O exemplo a seguir mostra o que fazer ao colocar a pasta pacotes em artefatos. Como o conteúdo dessa pasta não é gerado durante a compilação, a Propriedade MSBuild **não deve ser alterada**.

Durante uma Live Unit Testing compilação, a `<LiveUnitTestingBuildRootPath>` propriedade é definida como o local da pasta Live Unit Testing artefatos.

Por exemplo, suponha que seu projeto tenha a estrutura mostrada aqui.

```
.vs\...\lut\0\b
artifacts\{binlog,obj,bin,nupkg,testresults,packages}
src\{proj1,proj2,proj3}
tests\{testproj1,testproj2}
Solution.sln
```
Durante a compilação Live Unit Testing, a `<LiveUnitTestingBuildRootPath>` propriedade é definida como o caminho completo de `.vs\...\lut\0\b` . Se o projeto definir a `<ArtifactsRoot>` propriedade que é mapeada para o dir da solução, você poderá atualizar o projeto do MSBuild da seguinte maneira:

```xml
<Project>
    <PropertyGroup Condition="'$(LiveUnitTestingBuildRootPath)' == ''">
        <SolutionDir>$([MSBuild]::GetDirectoryNameOfFileAbove(`$(MSBuildProjectDirectory)`, `YOUR_SOLUTION_NAME.sln`))\</SolutionDir>

        <ArtifactsRoot>Artifacts\</ArtifactsRoot>
        <ArtifactsRoot Condition="'$(LiveUnitTestingBuildRootPath)' != ''">$(LiveUnitTestingBuildRootPath)</ArtifactsRoot>
    </PropertyGroup>

    <PropertyGroup>
        <BinLogPath>$(ArtifactsRoot)\BinLog</BinLogPath>
        <ObjPath>$(ArtifactsRoot)\Obj</ObjPath>
        <BinPath>$(ArtifactsRoot)\Bin</BinPath>
        <NupkgPath>$(ArtifactsRoot)\Nupkg</NupkgPath>
        <TestResultsPath>$(ArtifactsRoot)\TestResults</TestResultsPath>

        <!-- Note: Given that a build doesn't generate packages, the path should be relative to the solution dir, rather than artifacts root, which will change during a Live Unit Testing build. -->
        <PackagesPath>$(SolutionDir)\artifacts\packages</PackagesPath>
    </PropertyGroup>
</Project>
```

## <a name="build-artifact-location"></a>Localização do artefato de compilação

**Quero que os artefatos de um Live Unit Testing Build vá para um local específico em vez do local padrão na pasta *. vs* . Como posso alterar isso?**

Defina a variável de ambiente em nível de usuário `LiveUnitTesting_BuildRoot` com o caminho no qual você deseja que os artefatos de build do Live Unit Testing sejam soltos. 

## <a name="test-explorer-versus-live-unit-testing"></a>Gerenciador de testes versus Live Unit Testing

**Qual a diferença entre a execução de testes na janela Gerenciador de Testes e a execução de testes no Live Unit Testing?**

Há várias diferenças:

- Executar ou depurar testes da janela **Gerenciador de testes** executa binários regulares, enquanto Live Unit Testing executa binários instrumentados. Se você desejar depurar binários instrumentados, a adição de uma chamada de método [Debugger.Launch](xref:System.Diagnostics.Debugger.Launch) ao método de teste faz com que o depurador seja iniciado sempre que o método é executado (incluindo quando ele é executado pelo Live Unit Testing). Em seguida, é possível anexar e depurar o binário instrumentado. No entanto, esperamos que a instrumentação seja transparente para você na maioria dos cenários de usuário e que você não precise depurar binários instrumentados.

- Live Unit Testing não cria um novo domínio de aplicativo para executar testes, mas os testes são executados na janela **Gerenciador de testes** , crie um novo domínio de aplicativo.

- O Live Unit Testing executa testes em cada assembly de teste sequencialmente. No **Gerenciador de testes**, você pode optar por executar vários testes em paralelo.

- **O Test Explorer** executa testes em um STA (single-threaded apartment) por padrão, enquanto Live Unit Testing executa testes em um MTA (apartment multi-threaded). Para executar testes do MSTest no STA no Live Unit Testing, decore o método de teste ou a classe recipiente com o atributo `<STATestMethod>` ou `<STATestClass>` que pode ser encontrado no pacote NuGet `MSTest.STAExtensions 1.0.3-beta`. Para o NUnit, decore o método de teste com o atributo `<RequiresThread(ApartmentState.STA)>` e para o xUnit, com o atributo `<STAFact>`.

## <a name="exclude-tests"></a>Excluir testes

**Como fazer para excluir testes de fazer parte do Live Unit Testing?**

Confira a seção "Incluir e excluir projetos e métodos de teste" do artigo [Usar o Live Unit Testing no Visual Studio](live-unit-testing.md#include-and-exclude-test-projects-and-test-methods) para obter a configuração específica do usuário. É útil incluir ou excluir testes quando você deseja executar um conjunto específico de testes em uma sessão de edição específica ou para persistir suas próprias preferências pessoais.

Para configurações específicas da solução, você pode aplicar o atributo <xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute?displayProperty=fullName> programaticamente para excluir métodos, propriedades, classes ou estruturas de serem instrumentados pelo by Live Unit Testing. Além disso, também é possível definir a propriedade `<ExcludeFromCodeCoverage>` como `true` no arquivo de projeto para excluir todo o projeto de ser instrumentado. O Live Unit Testing ainda executará os testes que não foram instrumentados, mas sua cobertura não será visualizada.

Verifique também se `Microsoft.CodeAnalysis.LiveUnitTesting.Runtime` foi carregado no domínio do aplicativo atual e desabilite testes com base no motivo. Por exemplo, você pode fazer algo semelhante ao seguinte com o xUnit:

```csharp
[ExcludeFromCodeCoverage]
public class SkipLiveFactAttribute : FactAttribute
{
   private static bool s_lutRuntimeLoaded = AppDomain.CurrentDomain.GetAssemblies().Any(a => a.GetName().Name ==
                                            "Microsoft.CodeAnalysis.LiveUnitTesting.Runtime");
   public override string Skip => s_lutRuntimeLoaded ? "Test excluded from Live Unit Testing" : "";
}

public class Class1
{
   [SkipLiveFact]
   public void F()
   {
      Assert.True(true);
   }
}
```

::: moniker range="vs-2017"

## <a name="win32-pe-headers"></a>Cabeçalhos do Win32 PE

**Por que os cabeçalhos do Win32 PE são diferentes em assemblies instrumentados compilados pelo Live Unit Testing?**

Esse problema foi corrigido e não existe no Visual Studio 2017 versão 15.3 e posterior.

Para versões mais antigas do Visual Studio 2017, há um bug conhecido que pode resultar na falha dos builds do Live Unit Testing em inserir os seguintes dados de Cabeçalho do Win32 PE:

- Versão de Arquivo (especificada por @System.Reflection.AssemblyFileVersionAttribute no código).

- Ícone do Win32 (especificado por `/win32icon:` na linha de comando).

- Manifesto do Win32 (especificado por `/win32manifest:` na linha de comando).

Os testes que dependem desses valores poderão falhar quando executados pelo Live Unit Testing.

::: moniker-end

## <a name="continuous-builds"></a>Builds contínuos

**Por que o Live Unit Testing continua compilando minha solução em todos os momentos, mesmo quando não estou fazendo nenhuma edição?**

Sua solução poderá ser construída mesmo se você não estiver fazendo edições se o processo de build gerar o código-fonte que faz parte da própria solução e os arquivos de destino de build não têm entradas e saídas apropriadas especificadas. Os destinos devem receber uma lista de entradas e saídas para que o MSBuild possa executar as verificações atualizadas apropriadas e determinar se um novo build é necessário.

O Live Unit Testing inicia um build sempre que detecta uma alteração nos arquivos de origem. Como o build da solução gera arquivos de origem, Live Unit Testing entra em um loop de build infinito. No entanto, se as entradas e saídas do destino são verificadas quando o Live Unit Testing inicia o segundo build (depois de detectar os arquivos de origem recém-gerados do build anterior), ele interrompe o loop de build porque as verificações de entradas e saídas indicam que tudo está atualizado.

## <a name="editor-icons"></a>Ícones do editor

**Por que não vejo nenhum ícone no editor, embora Live Unit Testing pareça estar executando os testes com base nas mensagens na janela Saída?**

Talvez você não veja ícones no editor se os assemblies que o Live Unit Testing está operando não estão instrumentados por algum motivo. Por exemplo, o Live Unit Testing não é compatível com projetos que definem `<UseHostCompilerIfAvailable>false</UseHostCompilerIfAvailable>`. Nesse caso, o processo de build precisa ser atualizado para remover essa configuração ou alterá-la para `true`, a fim de que o Live Unit Testing funcione. 

## <a name="capture-logs"></a>Coletar logs

**Como fazer para coletar logs mais detalhados de relatórios de bugs de arquivo?**

É possível fazer várias coisas para coletar logs mais detalhados:

- Vá para **Ferramentas**  >  **Opções**  >  **Live Unit Testing** e altere a opção de registro em log para **Detalhado.** O log detalhado faz com que logs mais detalhados sejam mostrados na janela de **Saída**.

- Defina a variável de ambiente do usuário `LiveUnitTesting_BuildLog` com o nome do arquivo que você deseja usar para capturar o log do MSBuild. Em seguida, as mensagens de log detalhado do MSBuild de builds do Live Unit Testing podem ser recuperadas desse arquivo.

- Defina a variável de ambiente de usuário `LiveUnitTesting_TestPlatformLog` como `1` para capturar o log da Plataforma de Teste. Em seguida, as mensagens de log da Plataforma de Teste das execuções do Live Unit Testing poderão ser recuperadas de `[Solution Root]\.vs\[Solution Name]\log\[VisualStudio Process ID]`.

- Crie uma variável de ambiente em nível de usuário chamada `VS_UTE_DIAGNOSTICS` e defina-a como 1 (ou qualquer valor) e reinicie o Visual Studio. Agora você deve ver muito registro em log na **guia Saída – Testes** no Visual Studio.

## <a name="see-also"></a>Confira também

- [Live Unit Testing](live-unit-testing.md)
