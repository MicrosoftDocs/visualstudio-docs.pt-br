---
title: Extensibilidade de projeto do Visual C++
ms.custom: ''
ms.date: 09/12/2018
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 913ad2e785fcdb2067f89d0d4de2b250db40468b
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349670"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual Studio C++ sistema extensibilidade e conjunto de ferramentas de integração do Project

O *sistema de projeto do Visual C++* é usado para arquivos. vcxproj. Ele se baseia a [Visual Studio Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) e fornece adicionais, pontos de extensibilidade específica do C++ para fácil integração de novos conjuntos de ferramentas, arquiteturas de compilação e plataformas de destino. 

## <a name="c-msbuild-targets-structure"></a>Estrutura de destinos do MSBuild C++

Todos os arquivos. vcxproj importar esses arquivos:

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

Esses arquivos definem pouco por si só. Em vez disso, eles importarem outros arquivos com base nesses valores de propriedade:

- `$(ApplicationType)`

   Exemplos: Windows Store, Android, Linux

- `$(ApplicationTypeRevision)`

   Isso deve ser uma cadeia de caracteres de versão válida, do formulário Revision]].

   Exemplos: 1.0, 10.0.0.0

- `$(Platform)`

   A arquitetura de compilação, denominado "Platform" por razões históricas.

   Exemplos: Win32, x86, x64, ARM   

- `$(PlatformToolset)`

   Exemplos: v140, v141, v141_xp, llvm

Esses valores de propriedade especificam nomes de pastas sob o `$(VCTargetsPath)` pasta raiz:

> `$(VCTargetsPath)`\\  
> &nbsp;&nbsp;&nbsp;&nbsp;*Tipo de aplicativo*\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Plataformas*\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`  
> &nbsp;&nbsp;&nbsp;&nbsp;Plataformas\\&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(usado quando `$(ApplicationType)` estiver vazio, para projetos de área de trabalho do Windows)  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`  

### <a name="add-a-new-platform-toolset"></a>Adicionar um novo conjunto de ferramentas de plataforma

Para adicionar um novo conjunto de ferramentas, por exemplo, "MyToolset" para a plataforma Win32 existente, crie uma *MyToolset* pasta sob `$(VCTargetsPath)`  *\\plataformas\\Win32\\ PlatformToolsets\\*e crie *Toolset.props* e *Toolset.targets* arquivos nela.

Cada nome de pasta sob *PlatformToolsets* aparece na **propriedades do projeto** caixa de diálogo como uma disponível **conjunto de ferramentas de plataforma** para a plataforma especificada, conforme mostrado aqui:

![A propriedade de conjunto de ferramentas de plataforma no diálogo de páginas de propriedades do projeto](media/vc-project-extensibility-platform-toolset-property.png "o conjunto de ferramentas de plataforma de propriedade na caixa de diálogo de páginas de propriedades do projeto")

Criar semelhante *MyToolset* pastas e *Toolset.props* e *Toolset.targets* dá suporte a arquivos em cada pasta de plataforma existentes esse conjunto de ferramentas.

### <a name="add-a-new-platform"></a>Adicionar uma nova plataforma

Para adicionar uma nova plataforma, por exemplo, "MyPlatform", crie uma *MyPlatform* pasta sob `$(VCTargetsPath)`  *\\plataformas\\*e crie  *Platform.default.Props*, *Platform.props*, e *Platform.targets* arquivos nela. Crie também uma `$(VCTargetsPath)`  *\\plataformas\\*<strong><em>MyPlatform</em></strong>*\\PlatformToolsets\\*  pasta e crie pelo menos um conjunto de ferramentas nele.

Todos os nomes de pastas sob o *plataformas* pasta para cada `$(ApplicationType)` e `$(ApplicationTypeRevision)` são exibidos no IDE como disponível **plataforma** escolhas para um projeto.

![A opção de plataforma de novo na caixa de diálogo nova plataforma de projeto](media/vc-project-extensibility-new-project-platform.png "a nova opção de plataforma na caixa de diálogo nova plataforma de projeto")

### <a name="add-a-new-application-type"></a>Adicionar um novo tipo de aplicativo

Para adicionar um novo tipo de aplicativo, crie uma *MyApplicationType* pasta sob `$(VCTargetsPath)` *\\tipo de aplicativo\\* e crie um *Defaults.props* arquivo nele. Pelo menos uma revisão é necessária para um tipo de aplicativo, portanto, também criar uma `$(VCTargetsPath)`  *\\tipo de aplicativo\\MyApplicationType\\1.0* pasta e criar um  *Defaults.Props* arquivo nele. Você também deve criar uma `$(VCTargetsPath)`  *\\ApplicationType\\MyApplicationType\\1.0\\plataformas* pasta e crie pelo menos uma plataforma nele.

`$(ApplicationType)` e `$(ApplicationTypeRevision)` propriedades não são visíveis na interface do usuário. Eles são definidos nos modelos de projeto e não podem ser alterados depois que o projeto é criado.


## <a name="the-vcxproj-import-tree"></a>A árvore de importação. vcxproj

Uma árvore simplificada de importações para arquivos de objetos e destinos do Microsoft C++ é semelhante a:

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*padrão*\\\*. *arquivos de propriedades*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Tipo de aplicativo*\\`$(ApplicationType)`\\*Default.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Tipo de aplicativo*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*Default.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Tipo de aplicativo*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*plataformas* \\ `$(Platform)` \\  *Platform.default.Props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*padrão*\\\*. *arquivos de propriedades*  

Projetos de área de trabalho do Windows não definem `$(ApplicationType)`, portanto, eles apenas importarem

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore*\\*padrão*\\\*. *arquivos de propriedades*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Plataformas*\\`$(Platform)`\\*Platform.default.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter*\\*padrão*\\\*. *arquivos de propriedades*  

Vamos usar o `$(_PlatformFolder)` propriedade para manter o `$(Platform)` locais de pasta da plataforma. Essa propriedade é 

> `$(VCTargetsPath)`\\*Plataformas*\\`$(Platform)`

para aplicativos da área de trabalho do Windows, e 

> `$(VCTargetsPath)`\\*Tipo de aplicativo*\\`$(ApplicationType)`\\`$(ApplicationTypeRevision)`\\*plataformas*\\`$(Platform)`

para todo o resto.

Os arquivos de objetos são importados nesta ordem:

> `$(VCTargetsPath)`\\*Props*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.Props*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*. *arquivos de propriedades*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.props*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*. *arquivos de propriedades*  

Os arquivos de destino são importados nesta ordem:

> `$(VCTargetsPath)`\\*Microsoft.Cpp.targets*  
> &nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Current.targets*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.targets*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.targets*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore*\\\*. *destinos*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets*\\`$(PlatformToolset)`\\*Toolset.target*  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter*\\\*. *destinos*  

Se você precisa definir algumas propriedades padrão para seu conjunto de ferramentas, você pode adicionar arquivos ImportBefore e ImportAfter nas pastas apropriadas.

## <a name="author-toolsetprops-and-toolsettargets-files"></a>Arquivos Toolset.props autor e Toolset.targets

*Toolset.Props* e *Toolset.targets* arquivos têm controle total sobre o que acontece durante uma compilação quando esse conjunto de ferramentas é usado. Eles também podem controlar os depuradores disponíveis, alguns da interface de usuário do IDE, como o conteúdo a **páginas de propriedade** caixa de diálogo e alguns outros aspectos do comportamento do projeto.

Embora o processo de compilação inteiro pode ser substituído por um conjunto de ferramentas, geralmente você deseja apenas a seu conjunto de ferramentas para modificar ou adicionar que algumas etapas de build ou usar ferramentas de compilação diferente, como parte de um processo de compilação existente. Para atingir essa meta, há um número de arquivos comuns de objetos e destinos de que seu conjunto de ferramentas pode importar. Dependendo do que você deseja fazer em seu conjunto de ferramentas, esses arquivos podem ser úteis para usar como importações ou exemplos:

- `$(VCTargetsPath)`\\*Microsoft.CppCommon.targets*

   Esse arquivo define as principais partes do processo de compilação nativo e também importa:

   - `$(VCTargetsPath)`\\*Microsoft.CppBuild.targets*

   - `$(VCTargetsPath)`\\*Microsoft.BuildSteps.targets*

   - `$(MSBuildToolsPath)`\\*Targets*

- `$(VCTargetsPath)`\\*Microsoft.Cpp.Common.props*

   Define padrões para conjuntos de ferramentas que usam os compiladores Microsoft e Windows de destino.

- `$(VCTargetsPath)`\\*Microsoft.Cpp.WindowsSDK.props*

   Esse arquivo determina o local do SDK do Windows e define algumas propriedades importantes para aplicativos destinados ao Windows.

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>Integrar destinos específicos do conjunto de ferramentas com o padrão no processo de compilação do C++ 

O processo de compilação de C++ de padrão é definido no *Microsoft.CppCommon.targets*. Lá, os destinos não chamam qualquer ferramenta de compilação específica; eles especificam principal criar etapas, seu pedido e dependências.

A compilação de C++ tem três etapas principais, que são representadas pelas seguintes destinos:

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

Porque cada etapa de compilação pode ser executada de forma independente, os destinos em execução em uma única etapa não podem depender de grupos de itens e propriedades definidas nos destinos que são executados como parte de uma etapa diferente. Essa divisão permite que determinados compilação otimizações de desempenho. Embora não seja usado por padrão, é incentivado ainda a honrar essa separação.

Os destinos que são executados dentro de cada etapa são controlados por essas propriedades:

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

Cada etapa também tem propriedades Before e After. 

```xml
<Target
  Name="_BuildGenerateSourcesAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildGenerateSourcesTargets);$(BuildGenerateSourcesTargets);$(AfterBuildGenerateSourcesTargets)" />

<Target
  Name="\_BuildCompileAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildCompileTargets);$(BuildCompileTargets);$(AfterBuildCompileTargets)" />

<Target
  Name="\_BuildLinkAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildLinkTargets);$(BuildLinkTargets);$(AfterBuildLinkTargets)" />
```

Consulte a *Microsoft.CppBuild.targets* arquivo para obter exemplos de destinos que estão incluídos em cada etapa:

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

Se você examinar os destinos, tais como `_ClCompile`, você verá que eles não fazem nada diretamente por si só, mas em vez disso, dependem de outros destinos, incluindo `ClCompile`:

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` e outro compilar destinos específicos de ferramenta são definidos como destinos vazios *Microsoft.CppBuild.targets*:

```xml
<Target Name="ClCompile"/>
```

Porque o `ClCompile` destino estiver vazio, a menos que seja substituído por um conjunto de ferramentas, nenhuma ação de compilação real é executada. Os destinos de conjunto de ferramentas podem substituir a `ClCompile` de destino, ou seja, eles podem conter outro `ClCompile` definição depois de importar *Microsoft.CppBuild.targets*: 

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

Apesar do nome, que foi criado antes que o Visual Studio implementou o suporte de plataforma cruzada, o `ClCompile` destino não terá que chamar CL.exe. Ele também pode chamar gcc, Clang ou com outros compiladores usando tarefas do MSBuild apropriadas.

O `ClCompile` destino não deve ter todas as dependências, exceto o `SelectClCompile` destino, que é necessário para o comando de compilação único arquivo trabalhar no IDE.

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>Tarefas do MSBuild para usar em destinos do conjunto de ferramentas

Para invocar uma ferramenta de build real, o destino precisa chamar uma tarefa do MSBuild. Há um basic [tarefa Exec](../msbuild/exec-task.md) que permite que você especifique uma linha de comando para executar. No entanto, as ferramentas de build geralmente têm muitas opções, entradas. e as saídas para acompanhar para as compilações incrementais, então, faz mais sentido ter tarefas especiais para eles. Por exemplo, o `CL` tarefa converte as propriedades do MSBuild em CL.exe comutadores, grava-os em um arquivo de resposta e chama CL.exe. Ele também acompanha todos os arquivos de entrada e saídos para mais tarde as compilações incrementais. Para obter mais informações, consulte [compilação incremental e verificação atualizada](#incremental-build-and-up-to-date-check).

O Microsoft.Cpp.Common.Tasks.dll implementa essas tarefas:

- `BSCMake`

- `CL`

- `ClangCompile` (opções do clang gcc)

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (como Exec mas com entrada e saída de rastreamento)

- `SetEnv`

Se você tiver uma ferramenta que executa a mesma ação que uma ferramenta existente e que tem opções de linha de comando similares (assim como clang-cl e CL), você pode usar a mesma tarefa para os dois.

Se você precisar criar uma nova tarefa para uma ferramenta de compilação, você pode escolher entre as seguintes opções:

1. Se você usar essa tarefa raramente, ou se alguns segundos não importam para sua compilação, você pode usar tarefas do MSBuild 'inline':

   - Tarefa de XAML (uma regra de compilação personalizada)

     Para obter um exemplo de uma declaração de tarefa de Xaml, consulte `$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.xml*e para seu uso, consulte `$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.targets*.

   - [Tarefa de código](../msbuild/msbuild-inline-tasks.md)

1. Se você deseja o melhor desempenho da tarefa ou precisa apenas a funcionalidade mais complexa, usar o MSBuild regular [gravação de tarefa](../msbuild/task-writing.md) processo.

   Se nem todas as entradas e saídas da ferramenta são listadas na linha de comando da ferramenta, como mostra a `CL`, `MIDL`, e `RC` casos e se você quiser de entrada automática e rastreamento de arquivo de saída e criação de arquivos. tlog, derivar sua tarefa da `Microsoft.Build.CPPTasks.TrackedVCToolTask`classe. No momento, enquanto há documentação para a base [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) classe, não há exemplos ou documentação para obter os detalhes de `TrackedVCToolTask` classe. Se isso fosse de interesse específico, adicione sua voz a uma solicitação na [developercommunity.visualstudio.com](https://developercommunity.visualstudio.com/spaces/62/index.html).

## <a name="incremental-builds-and-up-to-date-checks"></a>Builds incrementais e verificações atualizadas

A compilação incremental de MSBuild padrão se destina a uso `Inputs` e `Outputs` atributos. Se você especificá-los, o MSBuild chama o destino somente se qualquer uma das entradas tem um carimbo de hora mais recente que todas as saídas. Como arquivos de origem geralmente incluem ou importar outros arquivos e criar ferramentas produzir saídas diferentes, dependendo das opções de ferramenta, é difícil especificar todas as possíveis entradas e saídas de destinos do MSBuild.

Para gerenciar esse problema, a compilação de C++ usa uma técnica diferente para dar suporte a compilações incrementais. A maioria dos destinos não especificar as entradas e saídas e como resultado, sempre executar durante a compilação. As tarefas chamadas pelos destinos gravam informações sobre todas as entradas e saídas no *tlog* arquivos que têm uma extensão. tlog. Os arquivos. tlog são usados por compilações posteriores para verificar o que foi alterado e precisa ser recriado e o que é atualizado.

Para determinar todas as entradas e saídas, tarefas de ferramenta nativa usam tracker.exe e o [FileTracker](/dotnet/api/microsoft.build.utilities.filetracker) classe fornecida pelo MSBuild.

Microsoft.Build.CPPTasks.Common.dll define o `TrackedVCToolTask` classe base abstrata pública. A maioria das tarefas de ferramenta nativa é derivada dessa classe.

## <a name="tlog-files"></a>arquivos. tlog

Há três tipos de arquivos. tlog: *leia*, *escrever*, e *linha de comando*. Arquivos. tlog a leitura e gravação são usados por builds incrementais e a verificação atualizada no IDE. Arquivos. tlog de linha de comando são usados somente em compilações incrementais.

O MSBuild fornece essas classes de auxiliar para ler e gravar arquivos. tlog:

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

O [FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata) classe pode ser usada para acesso de leitura e gravar arquivos. tlog e identificar entradas que são mais recentes de saídas, ou se uma saída está ausente. Ele é usado na verificação de atualização.

Arquivos. tlog de linha de comando contêm informações sobre linhas de comando usado na compilação. Eles são usados apenas para compilações incrementais, verificações não atualizadas, para que o formato interno é determinado pela tarefa do MSBuild que produz-los.

Se os arquivos. tlog são criados por uma tarefa, é melhor usar essas classes auxiliares para criá-los. No entanto, como a verificação de atualização padrão baseia-se agora apenas nos arquivos. tlog, às vezes é mais conveniente para produzi-las em um destino sem uma tarefa. Você pode gravá-los usando o `WriteLinesToFile` tarefa. Consulte a `_WriteMasmTlogs` de destino no `$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.targets* como exemplo.

### <a name="read-tlog-format"></a>Formato. tlog de leitura

*Leia* arquivos. tlog (\*arquivos tlog. Read.\*. tlog) contém informações sobre arquivos de origem e suas dependências.

Um acento circunflexo (**^**) no início de uma linha indica uma ou mais fontes. Fontes que compartilham as mesmas dependências são separados por uma barra vertical (**\|**).

Arquivos de dependência são listados após fontes de dados, cada um em sua própria linha. Todos os nomes de arquivo são caminhos completos.

Por exemplo, suponha que as fontes do projeto são encontradas no *f:.\\testar\\ConsoleApplication1\\ConsoleApplication1*. Se seu arquivo de origem *Class1.cpp*, possui os seguintes inclui,

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

em seguida, a *CL.read.1.tlog* arquivo contém o arquivo de origem, seguido por suas duas dependências:

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

Não é necessário gravar os nomes de arquivo em letras maiusculas, mas é uma conveniência para algumas ferramentas.

### <a name="write-tlog-format"></a>Escrever formato. tlog

*Gravar* . tlog (\*Write.\*. arquivos tlog) se conectar a fontes e saídas.

Um acento circunflexo (**^**) no início de uma linha indica uma ou mais fontes. Várias fontes são separados por uma barra vertical (**\|**).

Os arquivos de saída criados a partir de fontes de devem estar listados depois de fontes de dados, cada um em sua própria linha. Todos os nomes de arquivo devem ser caminhos completos.

Por exemplo, para um projeto ConsoleApplication simples que tem um arquivo de origem adicionais *Class1.cpp*, o *link.write.1.tlog* arquivo pode conter:

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>Compilação de tempo de design

No IDE,. vcxproj projetos usam um conjunto de destinos do MSBuild para obter informações adicionais do projeto e gerar novamente os arquivos de saída. Alguns desses destinos são usados somente em compilações de tempo de design, mas muitos deles são usados em compilações regulares e compilações de tempo de design.

Para obter informações gerais sobre compilações de tempo de design, consulte a documentação do CPS [builds de tempo de Design](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md). Esta documentação é apenas parcialmente aplicável aos projetos do Visual C++.

O `CompileDesignTime` e `Compile` destinos mencionados no tempo de design se baseia em documentação nunca executada para projetos. vcxproj. Projetos do Visual C++. vcxproj usam diferentes destinos de tempo de design para obter informações do IntelliSense.

### <a name="design-time-targets-for-intellisense-information"></a>Metas de tempo de design para as informações do IntelliSense

As metas de tempo de design usadas em projetos. vcxproj são definidas no `$(VCTargetsPath)` \\ *Microsoft.Cpp.DesignTime.targets*.

O `GetClCommandLines` destino coleta opções do compilador para IntelliSense:

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` – somente a inicialização de build de destinos, necessários para o tempo de design de tempo de design. Entre outras coisas, esses destinos desabilite algumas das funcionalidades de build normal para melhorar o desempenho.

- `ComputeCompileInputsTargets` – um conjunto de destinos que modifica as opções do compilador e itens. Esses destinos são executados em builds de tempo de design e regulares.

As chamadas de destino a `CLCommandLine` tarefas para criar a linha de comando a serem usados para IntelliSense. Novamente, apesar do nome, ele pode manipular não apenas opções CL, mas as opções Clang e o gcc. O tipo de comutadores de compilador é controlado pelo `ClangMode` propriedade.

Atualmente, a linha de comando produzido pelo `CLCommandLine` tarefa sempre usa opções CL (mesmo no modo de Clang) porque eles são mais fácil para o mecanismo IntelliSense ao analisar.

Se você estiver adicionando um destino que é executado antes da compilação, regular ou tempo de design, verifique se ele não interromperá o tempo de design se baseia ou afetar o desempenho. A maneira mais simples para testar seu destino é abrir um prompt de comando do desenvolvedor e execute este comando:

> MSBuild /p:SolutionDir =*solução-directory-com-à direita-barra invertida*; Configuração = depuração; Plataforma = Win32; BuildingInsideVisualStudio = true; DesignTimebuild = /t: true\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*. vcxproj

Esse comando gera um log de compilação detalhado *MSBuild*, que tem um desempenho de resumo para os destinos e tarefas no final.

Certifique-se de usar `Condition ="'$(DesignTimeBuild)' != 'true'"` em todas as operações que só fazem sentido para compilações regulares e não para builds de tempo de design.

### <a name="design-time-targets-that-generate-sources"></a>Metas de tempo de design que geram fontes

*Esse recurso está desabilitado por padrão para projetos nativos de área de trabalho e atualmente não há suporte para projetos em cache*.

Se `GeneratorTarget` metadados é definido para um item de projeto e, em seguida, o destino é executado automaticamente, ambos quando o projeto é carregado e quando o arquivo de origem é alterado.

Por exemplo gerar automaticamente. cpp ou. h, arquivos de arquivos. XAML, o `$(VSInstallDir)` \\ *MSBuild*\\*Microsoft* \\  *WindowsXaml*\\*v15.0*\\\*\\*Microsoft.Windows.UI.Xaml.CPP.Targets* arquivos definem-los entidades:

```xml
<ItemDefinitionGroup>
  <Page>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </Page>
  <ApplicationDefinition>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </ApplicationDefinition>
</ItemDefinitionGroup>
<Target Name="DesignTimeMarkupCompilation">
  <!-- BuildingProject is used in Managed builds (always true in Native) -->
  <!-- DesignTimeBuild is used in Native builds (always false in Managed) -->
  <CallTarget Condition="'$(BuildingProject)' != 'true' Or $(DesignTimeBuild) == 'true'" Targets="DesignTimeMarkupCompilationCT" />
</Target>
```

Para usar `Task.HostObject` para obter o conteúdo não salvo arquivos de origem, os destinos e tarefas devem ser registrados como [MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017) para os projetos de determinado em um pkgdef:

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Extensibilidade de projeto do Visual C++ no IDE do Visual Studio

O sistema de projeto do Visual C++ se baseia a [sistema de projeto do VS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)e usa seus pontos de extensibilidade. No entanto, a implementação da hierarquia de projeto é específica para o Visual C++ e não baseado no CPS, extensibilidade de hierarquia é limitada aos itens de projeto.

### <a name="project-property-pages"></a>Páginas de propriedades do projeto

Para obter informações gerais de design, consulte [extensibilidade da plataforma - parte 1](https://blogs.msdn.microsoft.com/vsproject/2009/06/09/platform-extensibility-part-1/) e [extensibilidade da plataforma - parte 2](https://blogs.msdn.microsoft.com/vsproject/2009/06/18/platform-extensibility-part-2/).

Em termos simples, as páginas de propriedades que você verá na **propriedades do projeto** caixa de diálogo para um projeto C++ são definidos pela *regra* arquivos. Um arquivo de regra especifica um conjunto de propriedades para mostrar em uma página de propriedades e como e onde eles devem ser salvos no projeto de arquivos. Arquivos de regras são arquivos. XML que usam o formato Xaml. Os tipos usados para serializá-los são descritos em [xamltypes](/dotnet/api/microsoft.build.framework.xamltypes). Para obter mais informações sobre o uso de arquivos de regras em projetos, consulte [arquivos de regras do XML da página de propriedade](/cpp/ide/property-page-xml-files).

Os arquivos de regra devem ser adicionados para o `PropertyPageSchema` grupo de itens:

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` metadados limita a visibilidade de regra, que também é controlada pelo tipo de regra e pode ter um destes valores:

> `Project` | `File` | `PropertySheet`

CPS dá suporte a outros valores para o tipo de contexto, mas eles não são usados em projetos do Visual C++.

Se a regra deve estar visível em mais de um contexto, use ponto e vírgula (**;**) para separar os valores de contexto, como mostrado aqui:

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>Formato de regra e os principais tipos

O formato de regra é simples, portanto, esta seção descreve somente os atributos que afetam como a regra aparece na interface do usuário.

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

O `PageTemplate` atributo define como a regra é exibida na **páginas de propriedade** caixa de diálogo. O atributo pode ter um destes valores:


| Atributo | Descrição |
|------------| - |
| `generic` | Todas as propriedades são mostradas em uma única página nos títulos de categoria<br/>A regra pode ser visível para os `Project` e `PropertySheet` contextos, mas não `File`.<br/><br/> Exemplo: `$(VCTargetsPath)` \\ *1033*\\*arquivo General* |
| `tool` | Categorias são mostradas como subpáginas.<br/>A regra pode ser visível em todos os contextos: `Project`, `PropertySheet` e `File`.<br/>A regra está visível nas propriedades do projeto somente se o projeto tem itens com o `ItemType` definidos no `Rule.DataSource`, a menos que o nome da regra está incluído no `ProjectTools` grupo de itens.<br/><br/>Exemplo: `$(VCTargetsPath)` \\ *1033*\\*clang.xml* |
| `debugger` | A página é mostrada como parte da página de depuração.<br/>Categorias são ignoradas no momento.<br/>O nome da regra deve corresponder do objeto Debug iniciador MEF `ExportDebugger` atributo.<br/><br/>Exemplo: `$(VCTargetsPath)` \\ *1033*\\*depurador\_local\_windows.xml* |
| *custom* | Modelo personalizado. O nome do modelo deve corresponder a `ExportPropertyPageUIFactoryProvider` atributo do `PropertyPageUIFactoryProvider` objeto MEF. Ver **Microsoft.VisualStudio.ProjectSystem.Designers.Properties.IPropertyPageUIFactoryProvider**.<br/><br/> Exemplo: `$(VCTargetsPath)` \\ *1033*\\*userMacros.xml* |

Se a regra usa um dos modelos com base em grade de propriedade, ele poderá usar esses pontos de extensibilidade para suas propriedades:

- [Editores de valor de propriedade](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [Provedor de valores de enumeração dinâmica](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>Estender uma regra

Se você quiser usar uma regra existente, mas precisa adicionar ou remover (isto é, ocultar) apenas algumas propriedades, você pode criar uma [regra de extensão](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md).

#### <a name="override-a-rule"></a>Substituir uma regra

Talvez você queira seu conjunto de ferramentas para usar a maioria das regras do padrão de projeto, mas substitua apenas um ou alguns deles. Por exemplo, digamos que você deseja alterar a regra de C/C++ para mostrar as opções do compilador diferentes. Você pode fornecer uma nova regra com o mesmo nome e nome de exibição como a regra existente e incluí-lo no `PropertyPageSchema` grupo de itens após a importação de destinos de cpp padrão. Apenas uma regra com um determinado nome é usada no projeto e o último deles são incluídos na `PropertyPageSchema` wins do grupo de itens.

#### <a name="project-items"></a>Itens de projeto

O *Projectitemsschema* arquivo define as `ContentType` e `ItemType` os valores para os itens que são tratados como itens de projeto e define `FileExtension` elementos para determinar qual grupo de Item, um novo arquivo for adicionado ao.

O arquivo ProjectItemsSchema padrão for encontrado no `$(VCTargetsPath)` \\ *1033*\\*Projectitemsschema*. Para estendê-lo, você deve criar um arquivo de esquema com um novo nome, como *MyProjectItemsSchema.xml*:

```xml
<ProjectSchemaDefinitions xmlns="http://schemas.microsoft.com/build/2009/properties">

  <ItemType Name="MyItemType" DisplayName="C/C++ compiler"/>

  <ContentType
    Name="MyItems"
    DisplayName="My items"
    ItemType=" MyItemType ">
  </ContentType>

  <FileExtension Name=".abc" ContentType=" MyItems"/>

</ProjectSchemaDefinitions>
```

Em seguida, no arquivo de destinos, adicione:

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

Exemplo: `$(VCTargetsPath)` \\ *BuildCustomizations*\\*masm.xml*

### <a name="debuggers"></a>Depuradores

O serviço de depuração no Visual Studio dá suporte à extensibilidade para o mecanismo de depuração. Para obter mais informações, consulte estes exemplos:

- [MIEngine, projeto de código-fonte aberto que dá suporte à depuração lldb](https://github.com/Microsoft/MIEngine)

- [Exemplo de mecanismo de depuração do Visual Studio](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

Para especificar os mecanismos de depuração e outras propriedades para a sessão de depuração, você deve implementar uma [depurar iniciador](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md) componente MEF e adicione um `debugger` regra. Por exemplo, consulte o `$(VCTargetsPath)` \\1033\\depurador\_local\_windows.xml arquivo.

### <a name="deploy"></a>Implantar

a extensibilidade do sistema de projeto do Visual Studio para usam o projetos. vcxproj [provedores implantar](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md).

### <a name="build-up-to-date-check"></a>Construir verificação atualizada

Por padrão, a verificação de atualização de compilação exige leitura arquivos. tlog a. tlog e gravação a ser criado no `$(TlogLocation)` pasta durante a compilação para todas as entradas de compilação e saídas.

Para usar uma verificação de atualização personalizada:

1. Desabilitar a verificação de atualização padrão adicionando os `NoVCDefaultBuildUpToDateCheckProvider` funcionalidade na *Toolset.targets* arquivo:

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. Implementar seu próprio [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md).

## <a name="project-upgrade"></a>Atualização do projeto

### <a name="default-vcxproj-project-upgrader"></a>Atualizador de projeto. vcxproj padrão

As alterações de atualizador do projeto. vcxproj padrão a `PlatformToolset`, `ApplicationTypeRevision`, conjunto de ferramentas MSBuild versão e o .net framework. As duas últimas sempre são alteradas para os padrões de versão do Visual Studio, mas `PlatformToolset` e `ApplicationTypeRevision` pode ser controlado por propriedades especiais do MSBuild.

O atualizador usa esses critérios para decidir se um projeto pode ser atualizado ou não:

1. Para projetos que definem `ApplicationType` e `ApplicationTypeRevision`, há uma pasta com um número de revisão maior que o atual.

1. A propriedade `_UpgradePlatformToolsetFor_<safe_toolset_name>` está definido para o conjunto de ferramentas atual, e seu valor não é igual ao conjunto de ferramentas atual.

   Esses nomes de propriedade,  *\<safe_toolset_name >* representa o nome do conjunto de ferramentas com todos os caracteres não alfanuméricos substituídos por um sublinhado (**\_**).

Quando um projeto pode ser atualizado, ele participa *solução de redirecionamento*. Para obter mais informações, consulte [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2).

Se você quiser Adornar os nomes de projeto em **Gerenciador de soluções** quando projetos usam um conjunto de ferramentas específico, defina um `_PlatformToolsetShortNameFor_<safe_toolset_name>` propriedade.

Para obter exemplos de `_UpgradePlatformToolsetFor_<safe_toolset_name>` e `_PlatformToolsetShortNameFor_<safe_toolset_name>` definições de propriedade, consulte o *Microsoft.Cpp.Default.props* arquivo. Para obter exemplos de uso, consulte o `$(VCTargetPath)` \\ *Microsoft.Cpp.Platform.targets* arquivo.

### <a name="custom-project-upgrader"></a>Atualizador de projeto personalizado

Para usar um objeto de projeto personalizado do atualizador, implemente um componente MEF, conforme mostrado aqui:

```csharp
/// </summary>
[Export("MyProjectUpgrader", typeof(IProjectRetargetHandler))]
[Export(typeof(IProjectRetargetHandler))]
[ExportMetadata("Name", "MyProjectUpgrader")]
[OrderPrecedence(20)]
[PartMetadata(ProjectCapabilities.Requires, ProjectCapabilities.VisualC)]

internal class MyProjectUpgrader: IProjectRetargetHandler
{
    // ...
}
```

Seu código pode importar e chamar o objeto de atualizador. vcxproj padrão:

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` é definido em *Microsoft.VisualStudio.ProjectSystem.VS.dll* e é semelhante ao `IVsRetargetProjectAsync`.

Definir o `VCProjectUpgraderObjectName` propriedade informar ao sistema de projeto para usar o objeto do atualizador:

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>Desabilitar a atualização do projeto

Para desabilitar atualizações de projeto, use um `NoUpgrade` valor:

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>Cache do projeto e extensibilidade

Para melhorar o desempenho ao trabalhar com soluções grandes do C++ no Visual Studio 2017, o [cache de projeto](https://blogs.msdn.microsoft.com/vcblog/2016/10/05/faster-c-solution-load-with-vs-15/) foi introduzido. Ele é implementado como um banco de dados SQLite preenchido com dados do projeto e, em seguida, usado para carregar projetos sem carregar os projetos do MSBuild ou o CPS em memória.

Como não há nenhum presente para projetos. vcxproj carregados do cache de objetos de CPS, componentes do MEF da extensão que importe `UnconfiguredProject` ou `ConfiguredProject` não pode ser criado. Para dar suporte à extensibilidade, o cache do projeto não é usado quando o Visual Studio detecta se um projeto usa (ou provavelmente usará) extensões MEF.

Esses tipos de projeto são sempre totalmente carregados e têm objetos CPS na memória, portanto, todas as extensões do MEF são criadas para eles:

- Projetos de inicialização

- Projetos que têm um atualizador de projeto personalizado, ou seja, elas definem um `VCProjectUpgraderObjectName` propriedade

- Projetos que não se destinam Windows de área de trabalho, ou seja, elas definem um `ApplicationType` propriedade

- Itens de projeto (.vcxitems) e todos os projetos compartilhados que referenciam-las por importar projetos .vcxitems.

Se nenhuma dessas condições for detectada, um cache de projeto é criado. O cache inclui todos os dados do projeto MSBuild necessários para responder `get` as consultas em `VCProjectEngine` interfaces. Isso significa que todas as modificações nos objetos do MSBuild e feito por uma extensão de nível de arquivo de destinos deve funcionar em projetos carregados do cache.

## <a name="shipping-your-extension"></a>Sua extensão de envio

Para obter informações sobre como criar arquivos VSIX, consulte [envio extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md). Para obter informações sobre como adicionar arquivos para locais de instalação especial, por exemplo, para adicionar arquivos sob `$(VCTargetsPath)`, consulte [instalando fora da pasta de extensões](../extensibility/set-install-root.md).

## <a name="additional-resources"></a>Recursos adicionais

O sistema de compilação da Microsoft ([MSBuild](../msbuild/msbuild.md)) fornece o mecanismo de compilação e o formato extensível baseado em XML para arquivos de projeto. Você deve estar familiarizado com o basic [conceitos do MSBuild](../msbuild/msbuild-concepts.md) e com a forma [MSBuild para o Visual C++](/cpp/build/msbuild-visual-cpp-overview) funciona para estender o Visual C++ de sistema de projeto.

O Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) fornece a extensão de APIs que são usadas por CPS e o sistema de projeto do Visual C++. Para uma visão geral de como o MEF é usado pelo CPS, consulte [CPS e MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) na [VSProjectSystem visão de geral de MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md).

Você pode personalizar o sistema de compilação existente para adicionar etapas de compilação ou novos tipos de arquivo. Para obter mais informações, consulte [visão geral do MSBuild (Visual C++)](/cpp/build/msbuild-visual-cpp-overview) e [trabalhando com propriedades do projeto](/cpp/ide/working-with-project-properties).
