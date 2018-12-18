---
title: Perguntas frequentes sobre o Live Unit Testing
ms.date: 2017-10-03
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio ALM
- Live Unit Testing FAQ
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
ms.openlocfilehash: 2c0c81bc8413b9d1698e2ad7c21d0d9f397834ea
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849067"
---
# <a name="live-unit-testing-frequently-asked-questions"></a>Perguntas frequentes sobre o Live Unit Testing

## <a name="latest-features"></a>Recursos mais recentes
**O Live Unit Testing é aprimorado e aperfeiçoado regularmente. Como faço para encontrar informações sobre os novos recursos e as melhorias mais recentes?**

Para saber mais sobre as novas funcionalidades e melhorias feitas no Live Unit Testing começando pelo Visual Studio 2017 versão 15,3, veja [What's new in Live Unit Testing](live-unit-testing-whats-new.md) (Novidades no Live Unit Testing).

## <a name="supported-frameworks-and-versions"></a>Versões e estruturas compatíveis
**Quais são as estruturas de teste compatíveis com o Live Unit Testing e quais são as versões mínimas compatíveis?**

O Live Unit Testing funciona com as três estruturas de teste de unidade populares listadas na tabela a seguir. A versão mínima com suporte de seus adaptadores e suas estruturas também é listada na tabela. As estruturas de teste de unidade estão disponíveis em NuGet.org.

<table>
<tr>
   <th>Estrutura de teste</th>
   <th>Versão mínima do Adaptador do Visual Studio</th>
   <th>Versão mínima da Estrutura</th>
</tr>
<tr>
   <td>xUnit.net</td>
   <td> xunit.runner.visualstudio versão 2.2.0-beta3-build1187</td>
   <td>xunit 1.9.2</td>
</tr>
<tr>
   <td>NUnit</td>
   <td>NUnit3TestAdapter versão 3.5.1</td>
   <td>NUnit versão 3.5.0</td>
</tr>
<tr>
   <td>MSTest</td>
   <td>MSTest.TestAdapter 1.1.4-preview</td>
   <td>MSTest.TestFramework 1.0.5-preview</td>
</tr>
</table>

Se você tiver projetos de teste mais antigos baseados no MSTest que fazem referência a `Microsoft.VisualStudio.QualityTools.UnitTestFramework` e não desejar mudar para os pacotes NuGet do MSTest mais recentes, atualize para o Visual Studio 2017 versão 15.4.

Em alguns casos, talvez seja necessário restaurar explicitamente os pacotes NuGet referenciados pelos projetos na solução para que o Live Unit Testing funcione. É possível restaurar os pacotes fazendo uma compilação explícita da solução (selecione **Compilar**, **Recompilar Solução** no menu superior do Visual Studio) ou clicando com o botão direito do mouse na solução e selecionando **Restaurar Pacotes NuGet** antes de habilitar o Live Unit Testing.

## <a name="net-core-support"></a>Suporte do .NET Core
**O Live Unit Testing funciona com o .NET Core?**

Sim. O Live Unit Testing funciona com o .NET Core e .NET Framework. O suporte ao .NET Core foi adicionado recentemente ao Visual Studio 2017 versão 15.3. Faça o upgrade para essa versão do Visual Studio se quiser suporte para o Live Unit Testing para .NET Core.

## <a name="configuration"></a>Configuração
**Por que o Live Unit Testing não funciona ao ser ligado?**

A **Janela de Saída** (quando o menu suspenso Live Unit Testing está selecionado) deve informar por que o Live Unit Testing não funciona. O Live Unit Testing poderá não funcionar por um dos seguintes motivos:

- Se os pacotes NuGet referenciados pelos projetos na solução não tiverem sido restaurados, o Live Unit Testing não funcionará. Fazer uma compilação explícita da solução ou restaurar os pacotes NuGet na solução antes de ativar o Live Unit Testing deverá resolver esse problema.

- Se estiver usando testes baseados no MSTest nos projetos, lembre-se de remover a referência a `Microsoft.VisualStudio.QualityTools.UnitTestFramework` e adicionar referências aos últimos pacotes NuGet do MSTest: `MSTest.TestAdapter` (uma versão mínima de 1.1.11 é necessária) e `MSTest.TestFramework` (uma versão mínima de 1.1.11 é necessária). Para obter mais informações, consulte a seção “Estruturas de teste com suporte” do artigo [Usar o Live Unit Testing no Visual Studio 2017 Enterprise Edition](live-unit-testing.md#supported-test-frameworks).

- No mínimo, um projeto na solução deve ter uma referência ao NuGet ou uma referência direta à estrutura de teste do xUnit, NUnit ou MSTest. Esse projeto também deve referenciar um pacote NuGet de adaptadores de teste do Visual Studio correspondente. O adaptador de teste do Visual Studio também pode ser referenciado por meio de um arquivo *.runsettings*. O arquivo *.runsettings* precisa ter uma entrada como o seguinte exemplo:

```xml
<RunSettings>
    <RunConfiguration>
          <TestAdaptersPaths>path-to-your-test-adapter</TestAdaptersPaths>
     </RunConfiguration>
</RunSettings>
```

## <a name="incorrect-coverage-after-upgrade"></a>Cobertura incorreta após a atualização
**Por que o Live Unit Testing mostra uma cobertura incorreta depois de atualizar o adaptador de teste referenciado nos Projetos do Visual Studio para a versão compatível?**

- Se vários projetos na solução referenciarem o pacote do adaptador de teste NuGet, cada um deles deverá ser atualizado para a versão com suporte.

- Verifique também se o arquivo *.props* do MSBuild importado do pacote do adaptador de teste foi atualizado corretamente. Verifique a versão e o caminho da importação do pacote NuGet, que geralmente podem ser encontrados próximo à parte superior do arquivo de projeto, da seguinte forma:

   ```xml
    <Import Project="..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props" Condition="Exists('..\packages\xunit.runner.visualstudio.2.2.0\build\net20\xunit.runner.visualstudio.props')" />
   ```

## <a name="customize-builds"></a>Builds personalizados
**Posso personalizar meus builds do Live Unit Testing?**

Se a solução exigir etapas personalizadas de build para instrumentação (Live Unit Testing) que não são necessárias para o build não instrumentado "normal", você poderá adicionar o código ao projeto ou arquivos *.targets* que verificam a propriedade `BuildingForLiveUnitTesting` e executam etapas de pré/pós-build personalizadas. Também é possível optar por remover algumas etapas de build (como publicar ou gerar pacotes) ou adicionar etapas de build (como copiar pré-requisitos) a um build do Live Unit Testing baseado na propriedade desse projeto. A personalização do build com base nessa propriedade não altera o build normal de nenhum modo e só afeta os builds do Live Unit Testing.

Por exemplo, pode haver um destino que produz pacotes NuGet durante um build normal. Provavelmente, você não desejará que os pacotes NuGet sejam gerados após cada edição feita. Portanto, é possível desabilitar esse destino no build do Live Unit Testing fazendo algo semelhante ao seguinte:  

```xml
<Target Name="GenerateNuGetPackages" BeforeTargets="AfterBuild" Condition="'$(BuildingForLiveUnitTesting)' != 'true'">
    <Exec Command='"$(MSBuildThisFileDirectory)..\tools\GenPac" '/>
</Target>
```

## <a name="error-messages-with-ltoutputpathgt-or-ltoutdirgt"></a>Mensagens de erro com &lt;OutputPath&gt; ou &lt;OutDir&gt;
**Por que recebo este erro quando o Live Unit Testing tenta criar minha solução: “... parece definir `<OutputPath>` ou `<OutDir>` incondicionalmente. O Live Unit Testing não executará testes do assembly de saída”?**

Você pode receber esse erro se o processo de build da solução substitui `<OutputPath>` ou `<OutDir>` incondicionalmente e, portanto, ele não é um subdiretório de `<BaseOutputPath>`. Nesses casos, o Live Unit Testing não funcionará, pois ele também substitui esses valores, a fim de garantir que os artefatos de build sejam soltos em uma pasta em `<BaseOutputPath>`. Se precisar substituir a localização em que você deseja que os artefatos de build sejam soltos em um build normal, substitua o `<OutputPath>` condicionalmente com base em `<BaseOutputPath>`.

Por exemplo, se o build substituir o `<OutputPath>`, conforme mostrado abaixo:

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

## <a name="set-the-location-of-build-artifacts"></a>Definir o local dos artefatos do build
**Quero que os artefatos de um build do Live Unit Testing sejam encaminhados para uma localização específica em vez da localização padrão na pasta *.vs*. Como fazer para alterar isso?**

Defina a variável de ambiente em nível de usuário `LiveUnitTesting_BuildRoot` com o caminho no qual você deseja que os artefatos de build do Live Unit Testing sejam soltos. 

## <a name="test-explorer-vs-live-unit-testing-test-runs"></a>Execuções de teste do Gerenciador de Testes vs. Live Unit Testing 
**Qual a diferença entre a execução de testes na janela do Gerenciador de Testes e no Live Unit Testing?**

Há várias diferenças:

- A execução ou a depuração de testes na janela **Gerenciador de Testes** executa binários regulares, enquanto o Live Unit Testing executa binários instrumentados. Se você desejar depurar binários instrumentados, a adição de uma chamada de método [Debugger.Launch](xref:System.Diagnostics.Debugger.Launch) ao método de teste faz com que o depurador seja iniciado sempre que o método é executado (incluindo quando ele é executado pelo Live Unit Testing). Em seguida, é possível anexar e depurar o binário instrumentado. No entanto, esperamos que a instrumentação seja transparente para você na maioria dos cenários de usuário e que você não precise depurar binários instrumentados.

- O Live Unit Testing não cria um domínio do aplicativo para executar testes, mas os testes executados por meio da janela **Gerenciador de Testes** criam um domínio do aplicativo.

- O Live Unit Testing executa testes em cada assembly de teste sequencialmente, ao passo que se você executar vários testes na janela **Gerenciador de Testes** e selecionar o botão **Executar Testes em Paralelo**, eles serão executados em paralelo.

- A descoberta e a execução de testes no Live Unit Testing usam a versão 2 do `TestPlatform`, enquanto a janela **Gerenciador de Testes** usa a versão 1. No entanto, você não observará nenhuma diferença na maioria dos casos.

- Atualmente, o **Gerenciador de Testes** executa testes em um STA (Single-Threaded Apartment) por padrão, enquanto o Live Unit Testing executa testes em um MTA (Multi-Threaded Apartment). Para executar testes do MSTest no STA no Live Unit Testing, decore o método de teste ou a classe recipiente com o atributo `<STATestMethod>` ou `<STATestClass>` que pode ser encontrado no pacote NuGet `MSTest.STAExtensions 1.0.3-beta`. Para o NUnit, decore o método de teste com o atributo `<RequiresThread(ApartmentState.STA)>` e para o xUnit, com o atributo `<STAFact>`.

## <a name="exclude-tests"></a>Excluir testes
**Como faço para excluir testes de participação do Live Unit Testing?**

Confira a seção "Incluir e excluir projetos e métodos de teste" do artigo [Usar o Live Unit Testing no Visual Studio 2017 Enterprise Edition](live-unit-testing.md#include-and-exclude-test-projects-and-test-methods) para obter a configuração específica do usuário. É útil incluir ou excluir testes quando você deseja executar um conjunto específico de testes em uma sessão de edição específica ou para persistir suas próprias preferências pessoais.
 
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

## <a name="win32-pe-headers"></a>Cabeçalhos do Win32 PE
**Por que os cabeçalhos do Win32 PE são diferentes em assemblies instrumentados compilados pelo Live Unit Testing?**

Esse problema foi corrigido e não consta no Visual Studio 2017 versão 15.3. Faça upgrade para essa versão do Visual Studio.

Para versões mais antigas do Visual Studio 2017, há um bug conhecido que pode resultar na falha dos builds do Live Unit Testing em inserir os seguintes dados de Cabeçalho do Win32 PE:

- Versão de Arquivo (especificada por @System.Reflection.AssemblyFileVersionAttribute no código).

- Ícone do Win32 (especificado por `/win32icon:` na linha de comando).

- Manifesto do Win32 (especificado por `/win32manifest:` na linha de comando).

Os testes que dependem desses valores poderão falhar quando executados pelo Live Unit Testing.

## <a name="continuous-builds"></a>Builds contínuos
**Por que o Live Unit Testing continua compilando minha solução o tempo inteiro, mesmo quando não estou fazendo edições?**

A solução poderá ser compilada mesmo que você não esteja fazendo edições se o processo de build da solução gerar um código-fonte que faz parte da própria solução e os arquivos de destino do build não tiverem entradas e saídas apropriadas especificadas. Os destinos devem receber uma lista de entradas e saídas para que o MSBuild possa executar as verificações atualizadas apropriadas e determinar se um novo build é necessário.

O Live Unit Testing inicia um build sempre que detecta uma alteração nos arquivos de origem. Como o build da solução gera arquivos de origem, o Live Unit Testing entrará em um loop infinito de build. Se, no entanto, as entradas e as saídas do destino forem verificadas quando o Live Unit Testing iniciar o segundo build (depois de detectar os arquivos de origem recém-gerados do build anterior), ele interromperá o loop de build, pois as verificações de entradas e saídas indicarão que tudo está atualizado.  

## <a name="lightweight-solution-load"></a>Carga de solução leve
**Como o Live Unit Testing funciona com o recurso Carga de Solução Leve?**

No momento, o Live Unit Testing não funciona bem com o recurso de carga de solução leve. Ele funciona somente depois que pelo menos um dos projetos de teste é carregado. Até lá, ele não funcionará, porque o Live Unit Testing depende de que, pelo menos, um dos projetos de teste que referenciam um adaptador de teste (MSTest, xUnit ou NUnit) seja carregado.

> [!NOTE]
> A carga de solução leve não está mais disponível no Visual Studio 2017 versão 15.5 e posterior. No Visual Studio 2017 versão 15.5 e posteriores, grandes soluções que contêm código gerenciado são carregadas mais rápido do que anteriormente, mesmo sem carga de solução leve.

## <a name="new-process-coverage"></a>Nova cobertura de processo
**Por que o Live Unit Testing não captura a cobertura de um novo processo criado por um teste?**

Esse é um problema conhecido e deverá ser corrigido em uma próxima atualização do Visual Studio 2017.

## <a name="including-or-excluding-tests-not-working"></a>Como incluir ou excluir testes que não funcionam
**Por que nada acontece depois de incluir ou excluir testes do conjunto de Teste Dinâmico?**

Esse problema foi corrigido e não consta no Visual Studio 2017 versão 15.3. Faça upgrade para essa versão do Visual Studio.

Para versões anteriores do Visual Studio de 2017, esse é um problema conhecido. Para solucionar esse problema, você precisará fazer uma edição em qualquer arquivo depois de incluir ou excluir os testes. 

## <a name="editor-icons"></a>Ícones do editor
**Por que não consigo ver nenhum ícone no editor, embora o Live Unit Testing pareça estar executando os testes de acordo com as mensagens na janela de Saída?**

Talvez você não veja ícones no editor se os assemblies que o Live Unit Testing está operando não estão instrumentados por algum motivo. Por exemplo, o Live Unit Testing não é compatível com projetos que definem `<UseHostCompilerIfAvailable>false</UseHostCompilerIfAvailable>`. Nesse caso, o processo de build precisa ser atualizado para remover essa configuração ou alterá-la para `true`, a fim de que o Live Unit Testing funcione. 

## <a name="capture-logs"></a>Coletar logs
**Como faço para coletar logs mais detalhados de relatórios de registros de bugs?**

É possível fazer várias coisas para coletar logs mais detalhados:

- Acesse **Ferramentas** > **Opções** > **Live Unit Testing** e altere a opção de log para **Detalhado**. O log detalhado faz com que logs mais detalhados sejam mostrados na janela de **Saída**.

- Defina a variável de ambiente do usuário `LiveUnitTesting_BuildLog` com o nome do arquivo que você deseja usar para capturar o log do MSBuild. Em seguida, as mensagens de log detalhado do MSBuild de builds do Live Unit Testing podem ser recuperadas desse arquivo.

- Defina a variável de ambiente de usuário `LiveUnitTesting_TestPlatformLog` como `1` para capturar o log da Plataforma de Teste. Em seguida, as mensagens de log da Plataforma de Teste das execuções do Live Unit Testing poderão ser recuperadas de `[Solution Root]\.vs\[Solution Name]\log\[VisualStudio Process ID]`.

- Crie uma variável de ambiente em nível de usuário chamada `VS_UTE_DIAGNOSTICS` e defina-a como 1 (ou qualquer valor) e reinicie o Visual Studio. Agora você verá muitos logs na guia **Saída – Testes** do Visual Studio.

## <a name="see-also"></a>Consulte também

- [Teste de Unidade Dinâmica](live-unit-testing.md)
