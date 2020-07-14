---
title: Como o MSBuild compila projetos
ms.date: 05/18/2020
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, build process overview
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3c1cdc4738f60301435932b3700f14377f12172
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290071"
---
# <a name="how-msbuild-builds-projects"></a>Como o MSBuild compila projetos

Como o MSBuild realmente funciona? Neste artigo, você aprenderá como o MSBuild processa seus arquivos de projeto, sejam chamados do Visual Studio ou de uma linha de comando ou script. Saber como o MSBuild funciona pode ajudá-lo a diagnosticar melhor os problemas e a personalizar melhor o processo de compilação. Este artigo descreve o processo de compilação e é amplamente aplicável a todos os tipos de projeto.

O processo de compilação completo consiste na [inicialização inicial](#startup), na [avaliação](#evaluation-phase)e na [execução](#execution-phase) dos destinos e das tarefas que criam o projeto. Além dessas entradas, as importações externas definem os detalhes do processo de compilação, incluindo as [importações padrão](#standard-imports) , como *Microsoft. Common. targets* e [importações configuráveis pelo usuário](#user-configurable-imports) no nível da solução ou do projeto.

## <a name="startup"></a>Inicialização

O MSBuild pode ser invocado do Visual Studio por meio do modelo de objeto do MSBuild no *Microsoft.Build.dll*ou invocando o executável diretamente na linha de comando ou em um script, como em sistemas de CI. Em ambos os casos, as entradas que afetam o processo de compilação incluem o arquivo de projeto (ou o objeto de projeto interno ao Visual Studio), possivelmente um arquivo de solução, variáveis de ambiente e opções de linha de comando ou seus equivalentes de modelo de objeto. Durante a fase de inicialização, as opções de linha de comando ou equivalentes de modelo de objeto são usadas para definir as configurações do MSBuild, como a configuração de agentes. As propriedades definidas na linha de comando usando `-property` a `-p` opção ou são definidas como propriedades globais, que substituem os valores que seriam definidos nos arquivos de projeto, mesmo que os arquivos de projeto sejam lidos posteriormente.

As próximas seções são sobre os arquivos de entrada, como arquivos de solução ou arquivos de projeto.

### <a name="solutions-and-projects"></a>Soluções e projetos

As instâncias do MSBuild podem consistir em um projeto ou em vários projetos como parte de uma solução. O arquivo de solução não é um arquivo XML do MSBuild, mas o MSBuild o interpreta para saber todos os projetos que precisam ser compilados para as configurações de plataforma e configuração especificadas. Quando o MSBuild processa essa entrada XML, ele é conhecido como a compilação da solução. Ele tem alguns pontos extensíveis que permitem executar algo em cada Build de solução, mas como essa compilação é uma execução separada do Build de projeto individual, nenhuma configuração de propriedades ou definições de destino da compilação da solução é relevante para cada compilação do projeto.

Você pode descobrir como estender o Build da solução em [Personalizar o Build da solução](customize-your-build.md#customize-the-solution-build).

### <a name="visual-studio-builds-vs-msbuildexe-builds"></a>Builds do Visual Studio vs. MSBuild.exe

Há algumas diferenças significativas entre o desenvolvimento de projetos no Visual Studio vs. quando você invoca o MSBuild diretamente, por meio do executável do MSBuild ou ao usar o modelo de objeto do MSBuild para iniciar uma compilação. O Visual Studio gerencia a ordem de compilação do projeto para compilações do Visual Studio; Ele chama apenas o MSBuild no nível de projeto individual e, quando ele faz isso, são definidas algumas propriedades booleanas ( `BuildingInsideVisualStudio` , `BuildProjectReferences` ) que afetam significativamente o que o MSBuild faz. Dentro de cada projeto, a execução ocorre da mesma forma que quando invocado por meio do MSBuild, mas a diferença surge com projetos referenciados. No MSBuild, quando projetos referenciados são necessários, uma compilação realmente ocorre; ou seja, ele executa tarefas e ferramentas e gera a saída. Quando um Build do Visual Studio encontra um projeto referenciado, o MSBuild retorna apenas as saídas esperadas do projeto referenciado; Ele permite que o Visual Studio controle a construção desses outros projetos. O Visual Studio determina a ordem de compilação e chama o MSBuild separadamente (conforme necessário), totalmente sob o controle do Visual Studio.

Outra diferença surge quando o MSBuild é invocado com um arquivo de solução, o MSBuild analisa o arquivo de solução, cria um arquivo de entrada XML padrão, avalia-o e o executa como um projeto. A compilação da solução é executada antes de qualquer projeto. Ao compilar a partir do Visual Studio, nada disso acontece; O MSBuild nunca vê o arquivo da solução. Como consequência, a criação da solução cria a personalização (usando *antes. SolutionName. sln. targets* e *After. SolutionName. sln. targets*) só se aplica a MSBuild.exe ou orientado a modelos de objeto, não a compilações do Visual Studio.

### <a name="project-sdks"></a>SDKs do projeto

O recurso SDK para arquivos de projeto do MSBuild é relativamente novo. Antes dessa alteração, os arquivos de projeto importaram explicitamente os arquivos *. targets* e *. props* que definiam o processo de compilação para um tipo de projeto específico.

Os projetos do .NET Core importam a versão do SDK do .NET apropriada para eles. Consulte a visão geral, [SDKs do projeto do .NET Core](/dotnet/core/project-sdk/overview)e a referência às [Propriedades](/dotnet/core/project-sdk/msbuild-props).

## <a name="evaluation-phase"></a>Fase de avaliação

Esta seção discute como esses arquivos de entrada são processados e analisados para produzir objetos na memória que determinam o que será criado.

A finalidade da fase de avaliação é criar as estruturas de objeto na memória com base nos arquivos XML de entrada e no ambiente local. A fase de avaliação consiste em cinco passagens que processam os arquivos de entrada, como os arquivos XML do projeto ou, e os arquivos XML importados, geralmente chamados de arquivos *. props* ou *. targets* , dependendo se eles definem principalmente as propriedades ou definem destinos de compilação. Cada passagem cria uma parte dos objetos na memória que são usados posteriormente na fase de execução para compilar os projetos, mas nenhuma ação de compilação real ocorre durante a fase de avaliação. Em cada passagem, os elementos são processados na ordem em que aparecem.

Os passos na fase de avaliação são os seguintes:

- Avaliar variáveis de ambiente
- Avaliar importações e propriedades
- Avaliar definições de item
- Avaliar itens
- Avaliar elementos [UsingTask](usingtask-element-msbuild.md)
- Avaliar destinos

A ordem desses passos tem implicações significativas e é importante saber ao personalizar o arquivo do projeto. Consulte [ordem de avaliação de propriedade e item](comparing-properties-and-items.md#property-and-item-evaluation-order).

### <a name="evaluate-environment-variables"></a>Avaliar variáveis de ambiente

Nesta fase, as variáveis de ambiente são usadas para definir propriedades equivalentes. Por exemplo, a variável de ambiente PATH é disponibilizada como uma propriedade `$(PATH)` . Quando executado a partir da linha de comando ou de um script, o ambiente de comando é usado como normal e, quando executado no Visual Studio, o ambiente em vigor quando o Visual Studio é iniciado é usado.

### <a name="evaluate-imports-and-properties"></a>Avaliar importações e propriedades

Nesta fase, o XML de entrada inteiro é lido no, incluindo os arquivos de projeto e toda a cadeia de importações. O MSBuild cria uma estrutura XML na memória que representa o XML do projeto e todos os arquivos importados. Neste momento, as propriedades que não estão nos destinos são avaliadas e definidas.

Como consequência do MSBuild lendo todos os arquivos de entrada XML no início em seu processo, as alterações feitas nessas entradas durante o processo de compilação não afetam a compilação atual.

As propriedades fora de qualquer destino são tratadas de forma diferente das propriedades dentro de destinos. Nesta fase, somente as propriedades definidas fora de qualquer destino são avaliadas.

Como as propriedades são processadas na ordem das propriedades, uma propriedade em qualquer ponto na entrada pode acessar os valores de propriedade que aparecem anteriormente na entrada, mas não as propriedades que aparecem mais tarde.

Como as propriedades são processadas antes de os itens serem avaliados, você não pode acessar o valor de qualquer item durante qualquer parte da passagem de propriedades. 

### <a name="evaluate-item-definitions"></a>Avaliar definições de item

Nessa fase, as [definições de item](item-definitions.md) são interpretadas e uma representação na memória dessas definições é criada.

### <a name="evaluate-items"></a>Avaliar itens

Os itens definidos dentro de um destino são tratados de forma diferente dos itens fora de qualquer destino. Nesta fase, os itens fora de qualquer destino e seus metadados associados são processados.  Os metadados definidos por definições de item são substituídos pela configuração de metadados nos itens. Como os itens são processados na ordem em que aparecem, você pode fazer referência a itens que foram definidos anteriormente, mas não aqueles que aparecem mais tarde. Como a passagem de itens é posterior à passagem das propriedades, os itens podem acessar qualquer propriedade, se definido fora de qualquer destino, independentemente de a definição da propriedade aparecer posteriormente.

### <a name="evaluate-usingtask-elements"></a>Avaliar `UsingTask` elementos

Nesta fase, os elementos [UsingTask](usingtask-element-msbuild.md) são lidos e as tarefas são declaradas para uso posterior durante a fase de execução.

### <a name="evaluate-targets"></a>Avaliar destinos

Nesta fase, todas as estruturas de objeto de destino são criadas na memória, na preparação para execução. Não ocorre nenhuma execução real. 

## <a name="execution-phase"></a>Fase de execução

Na fase de execução, os destinos são ordenados e executados e todas as tarefas são executadas. Mas, primeiro, as propriedades e os itens definidos nos destinos são avaliados juntos em uma única fase na ordem em que aparecem. A ordem de processamento é notavelmente diferente de como as propriedades e os itens que não estão em um destino são processados: todas as propriedades primeiro e, em seguida, todos os itens, em passagens separadas. As alterações nas propriedades e nos itens de um destino podem ser observadas após o destino em que foram alteradas.

### <a name="target-build-order"></a>Ordem de build de destino

Em um único projeto, os destinos são executados em série. O problema central é como determinar em qual ordem criar tudo, para que as dependências sejam usadas para criar os destinos na ordem correta.  

A ordem de compilação de destino é determinada pelo uso dos `BeforeTargets` `DependsOnTargets` atributos, e `AfterTargets` em cada destino. A ordem dos destinos posteriores pode ser influenciada durante a execução de um destino anterior, se o destino anterior modificar uma propriedade referenciada nesses atributos.

As regras de ordenação são descritas em [determinar a ordem de compilação de destino](target-build-order.md#determine-the-target-build-order). O processo é determinado por uma estrutura de pilha que contém destinos a serem compilados. O destino na parte superior dessa tarefa inicia a execução e, se ela depender de qualquer outra coisa, esses destinos serão enviados para o topo da pilha e começarão a ser executados.  Quando há um destino sem nenhuma dependência, ele é executado para conclusão e seu destino pai é retomado.

### <a name="project-references"></a>Referências de Projeto

Há dois caminhos de código que o MSBuild pode executar, o normal, descrito aqui e a opção de grafo descrita na próxima seção.

Projetos individuais especificam sua dependência em outros projetos por meio de `ProjectReference` itens. Quando um projeto na parte superior da pilha começa a Compilar, ele atinge o ponto em que o `ResolveProjectReferences` destino é executado, um destino padrão definido nos arquivos de destino comuns.

`ResolveProjectReferences`Invoca a tarefa do MSBuild com entradas dos `ProjectReference` itens para obter as saídas. Os `ProjectReference` itens são transformados em itens locais, como `Reference` . A fase de execução do MSBuild para o projeto atual pausa enquanto a fase de execução começa a processar o projeto referenciado (a fase de avaliação é feita primeiro, conforme necessário). O projeto referenciado só é criado depois que você começa a criar o projeto dependente e, portanto, cria uma árvore de compilação de projetos.

O Visual Studio permite a criação de dependências de projeto em arquivos de solução (. sln). As dependências são especificadas no arquivo de solução e só são respeitadas ao criar uma solução ou ao compilar dentro do Visual Studio. Se você criar um único projeto, esse tipo de dependência será ignorado. As referências de solução são transformadas pelo MSBuild em `ProjectReference` itens e, depois disso, são tratadas da mesma maneira.

### <a name="graph-option"></a>Opção de grafo

Se você especificar a opção de compilação do grafo ( `-graphBuild` ou `-graph` ), o `ProjectReference` se tornará um conceito de primeira classe usado pelo MSBuild. O MSBuild analisará todos os projetos e construirá o grafo de ordem de compilação, um grafo de dependência real de projetos, que é então atravessado para determinar a ordem de compilação. Assim como acontece com os destinos em projetos individuais, o MSBuild garante que os projetos referenciados sejam criados após os projetos de que dependem.

## <a name="parallel-execution"></a>Execução paralela

Se você estiver usando suporte a multiprocessador ( `-maxCpuCount` ou `-m` switch), o MSBuild criará nós, que são processos do MSBuild que usam os núcleos de CPU disponíveis. Cada projeto é enviado para um nó disponível. Dentro de um nó, compilações de projeto individuais são executadas em série.

As tarefas podem ser habilitadas para execução paralela definindo uma variável booliana <xref:Microsoft.Build.Tasks.MSBuild.BuildInParallel%2A> , que é definida de acordo com o valor da `$(BuildInParallel)` propriedade no MSBuild. Para tarefas habilitadas para execução paralela, um Agendador de trabalho gerencia nós e atribui trabalho a nós.

Consulte [criando vários projetos em paralelo com o MSBuild](building-multiple-projects-in-parallel-with-msbuild.md)

## <a name="standard-imports"></a>Importações padrão

*Microsoft. Common. props* e *Microsoft. Common. targets* são importados por arquivos de projeto do .net (explícita ou implicitamente em projetos em estilo SDK) e estão localizados na pasta *MSBuild\Current\bin* em uma instalação do Visual Studio. Projetos do C++ têm sua própria hierarquia de importações; consulte [elementos internos do MSBuild para projetos C++](/cpp/build/reference/msbuild-visual-cpp-overview).

O arquivo *Microsoft. Common. props* define os padrões que podem ser substituídos. Ele é importado (explicitamente ou implicitamente) no início de um arquivo de projeto. Dessa forma, as configurações do projeto aparecem após os padrões, para que sejam substituídas.

O arquivo *Microsoft. Common. targets* e os arquivos de destino que ele importa definem o processo de compilação padrão para projetos .net. Ele também fornece pontos de extensão que você pode usar para personalizar a compilação.

Na implementação, *Microsoft. Common. targets* é um wrapper fino que importa *Microsoft. Common. CurrentVersion. targets*. Esse arquivo contém configurações para propriedades padrão e define os destinos reais que definem o processo de compilação. O `Build` destino é definido aqui, mas está, na verdade, vazio. No entanto, o `Build` destino contém o `DependsOn` atributo que especifica os destinos individuais que compõem as etapas de compilação reais, que são `BeforeBuild` , `CoreBuild` e `AfterBuild` . O `Build` destino é definido da seguinte maneira:

```xml
  <PropertyGroup>
    <BuildDependsOn>
      BeforeBuild;
      CoreBuild;
      AfterBuild
    </BuildDependsOn>
  </PropertyGroup>

  <Target
      Name="Build"
      Condition=" '$(_InvalidConfigurationWarning)' != 'true' "
      DependsOnTargets="$(BuildDependsOn)"
      Returns="@(TargetPathWithTargetPlatformMoniker)" />
```

`BeforeBuild`e `AfterBuild` são pontos de extensão. Eles estão vazios no arquivo *Microsoft. Common. CurrentVersion. targets* , mas os projetos podem fornecer seus próprios `BeforeBuild` e `AfterBuild` destinos com tarefas que precisam ser executadas antes ou depois do processo de compilação principal. `AfterBuild`é executado antes do destino não op, `Build` , porque `AfterBuild` aparece no `DependsOn` atributo no `Build` destino, mas ocorre após `CoreBuild` .

O `CoreBuild` destino contém as chamadas para as ferramentas de compilação, da seguinte maneira:

```xml
  <PropertyGroup>
    <CoreBuildDependsOn>
      BuildOnlySettings;
      PrepareForBuild;
      PreBuildEvent;
      ResolveReferences;
      PrepareResources;
      ResolveKeySource;
      Compile;
      ExportWindowsMDFile;
      UnmanagedUnregistration;
      GenerateSerializationAssemblies;
      CreateSatelliteAssemblies;
      GenerateManifests;
      GetTargetPath;
      PrepareForRun;
      UnmanagedRegistration;
      IncrementalClean;
      PostBuildEvent
    </CoreBuildDependsOn>
  </PropertyGroup>
  <Target
      Name="CoreBuild"
      DependsOnTargets="$(CoreBuildDependsOn)">

    <OnError ExecuteTargets="_TimeStampAfterCompile;PostBuildEvent" Condition="'$(RunPostBuildEvent)'=='Always' or '$(RunPostBuildEvent)'=='OnOutputUpdated'"/>
    <OnError ExecuteTargets="_CleanRecordFileWrites"/>

  </Target>
```

A tabela a seguir descreve esses destinos; alguns destinos são aplicáveis somente a determinados tipos de projeto.

| Destino | Descrição |
|--------|-------------|
| BuildOnlySettings | Configurações apenas para compilações reais, não para quando o MSBuild é invocado na carga do projeto pelo Visual Studio. |
| PrepareForBuild | Preparar os pré-requisitos para a criação |
| PreBuildEvent | Ponto de extensão para projetos para definir tarefas a serem executadas antes da compilação |
| ResolveProjectReferences | Analisar dependências do projeto e criar projetos referenciados |
| ResolveAssemblyReferences| Localize assemblies referenciados. |
| ResolveReferences | Consiste em `ResolveProjectReferences` e `ResolveAssemblyReferences` para localizar todas as dependências |
| PrepareResources | Processar arquivos de recursos |
| ResolveKeySource| Resolva a chave de nome forte usada para assinar o assembly e o certificado usado para assinar os manifestos [ClickOnce](../deployment/clickonce-security-and-deployment.md) . |
| Compilar | Invoca o compilador |
| ExportWindowsMDFile | Gere um arquivo [WinMD](/uwp/winrt-cref/winmd-files) a partir dos arquivos WinMDModule gerados pelo compilador. |
| UnmanagedUnregistration | Remover/limpar as entradas do registro de [interoperabilidade com](/dotnet/standard/native-interop/cominterop) de uma compilação anterior |
| GenerateSerializationAssemblies | Gere um assembly de serialização XML usando [sgen.exe](/dotnet/standard/serialization/xml-serializer-generator-tool-sgen-exe).|
| CreateSatelliteAssemblies | Crie um assembly satélite para cada cultura exclusiva nos recursos. |
| Gerar manifestos | Gera manifestos de implantação e aplicativo [ClickOnce](../deployment/clickonce-security-and-deployment.md) ou um manifesto nativo. |
| GetTargetPath | Retornar um item que contém o produto de compilação (executável ou assembly) para este projeto, com metadados. |
| PrepareForRun | Copie as saídas de Build para o diretório final se elas tiverem mudado. |
| UnmanagedRegistration | Definir entradas do registro para [interoperabilidade com](/dotnet/standard/native-interop/cominterop) |
| IncrementalClean | Remova os arquivos que foram produzidos em uma compilação anterior, mas que não foram produzidos na compilação atual. Isso é necessário para fazer o `Clean` trabalho em compilações incrementais. |
| PostBuildEvent | Ponto de extensão para projetos para definir tarefas a serem executadas após a compilação |

Muitos dos destinos na tabela anterior são encontrados em importações específicas de idioma, como *Microsoft. CSharp. targets*. Esse arquivo define as etapas no processo de compilação padrão específico para projetos .NET do C#. Por exemplo, ele contém o `Compile` destino que realmente chama o compilador C#.

## <a name="user-configurable-imports"></a>Importações configuráveis pelo usuário

Além das importações padrão, há várias importações que você pode adicionar para personalizar o processo de compilação.

- *Directory. Build. props*
- *Directory.Build.targets*

Esses arquivos são lidos pelas importações padrão para todos os projetos em qualquer subpasta sob eles. Isso é comumente no nível da solução para configurações para controlar todos os projetos na solução, mas também pode ser mais alto no sistema de arquivos, até a raiz da unidade.

O arquivo *Directory. Build. props* é importado por *Microsoft. Common. props*, portanto, as propriedades definidas aqui estão disponíveis no arquivo de projeto. Eles podem ser redefinidos no arquivo de projeto para personalizar os valores em uma base por projeto. O arquivo *Directory. Build. targets* é lido no após o arquivo de projeto. Normalmente, ele contém destinos, mas aqui você também pode definir propriedades que não deseja que projetos individuais redefinam.

## <a name="customizations-in-a-project-file"></a>Personalizações em um arquivo de projeto

O Visual Studio atualiza os arquivos de projeto conforme você faz alterações no **Gerenciador de soluções**, na janela **Propriedades** ou nas **Propriedades do projeto**, mas também pode fazer suas próprias alterações editando diretamente o arquivo do projeto.

Muitos comportamentos de compilação podem ser configurados definindo propriedades do MSBuild, no arquivo de projeto para configurações locais para um projeto ou conforme mencionado na seção anterior, criando um arquivo *Directory. Build. props* para definir propriedades globalmente para pastas inteiras de projetos e soluções. Para compilações ad hoc na linha de comando, ou scripts, você também pode usar a `/p` opção na linha de comando para definir propriedades para uma invocação específica do MSBuild. Consulte [Propriedades comuns do projeto MSBuild](common-msbuild-project-properties.md) para obter informações sobre as propriedades que podem ser definidas.

## <a name="next-steps"></a>Próximas etapas

O processo do MSBuild tem vários outros pontos de extensão diferentes daqueles descritos aqui. Consulte [personalizar sua compilação](customize-your-build.md). e [como estender o processo de compilação do Visual Studio](how-to-extend-the-visual-studio-build-process.md).

## <a name="see-also"></a>Veja também

[MSBuild](msbuild.md)