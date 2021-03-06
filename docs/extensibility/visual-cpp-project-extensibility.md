---
description: O sistema de projeto Visual C++ é usado para arquivos. vcxproj.
title: Extensibilidade do projeto Visual C++
ms.date: 04/23/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fc538402ae39753f14a3bccd8bcd17ddb0081078
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221230"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Integração de extensibilidade e conjunto de ferramentas do sistema de projeto do Visual Studio C++

O sistema de projeto Visual C++ é usado para arquivos. vcxproj. Ele é baseado no [CPS (sistema de projeto comum) do Visual Studio](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md) e fornece pontos de extensibilidade específicos do C++ para uma fácil integração de novos conjuntos de ferramentas, arquiteturas de compilação e plataformas de destino.

## <a name="c-msbuild-targets-structure"></a>Estrutura de destinos do MSBuild do C++

Todos os arquivos. vcxproj importam estes arquivos:

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

Esses arquivos definem pequenos por conta própria. Em vez disso, eles importam outros arquivos com base nesses valores de propriedade:

- `$(ApplicationType)`

   Exemplos: Windows Store, Android, Linux

- `$(ApplicationTypeRevision)`

   Essa deve ser uma cadeia de caracteres de versão válida, do formato Major. minor [. Build [. revision]].

   Exemplos: 1,0, 10.0.0.0

- `$(Platform)`

   A arquitetura de compilação, chamada "plataforma", por motivos históricos.

   Exemplos: Win32, x86, x64, ARM

- `$(PlatformToolset)`

   Exemplos: v140, v141, v141_xp, LLVM

Esses valores de propriedade especificam nomes de pasta na `$(VCTargetsPath)` pasta raiz:

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*Tipo de aplicativo*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Compatíveis*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*Compatíveis*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

A `$(VCTargetsPath)` \\ pasta *plataformas* \\ é usada quando o `$(ApplicationType)` está vazio, para projetos da área de trabalho do Windows.

### <a name="add-a-new-platform-toolset"></a>Adicionar um novo conjunto de ferramentas de plataforma

Para adicionar um novo conjunto de ferramentas, por exemplo, "mytoolset" para a plataforma Win32 existente, crie uma pasta *mytoolset* em `$(VCTargetsPath)` *\\ plataformas \\ Win32 \\ PlatformToolsets \\* e crie arquivos de conjunto de ferramentas *. props* e *Toolset. targets* nele.

Cada nome de pasta em *PlatformToolsets* é exibido na caixa de diálogo **Propriedades do projeto** como um conjunto de ferramentas de **plataforma** disponível para a plataforma especificada, como mostrado aqui:

![A propriedade do conjunto de ferramentas da plataforma na caixa de diálogo páginas de propriedades do projeto](media/vc-project-extensibility-platform-toolset-property.png "A propriedade do conjunto de ferramentas da plataforma na caixa de diálogo páginas de propriedades do projeto")

Crie pastas *Mytoolset* semelhantes e o conjunto de ferramentas *. props* e os arquivos *Toolset. targets* em cada pasta de plataforma existente com suporte neste conjunto de ferramentas.

### <a name="add-a-new-platform"></a>Adicionar uma nova plataforma

Para adicionar uma nova plataforma, por exemplo, "myplatform", crie uma pasta *myplatform* em `$(VCTargetsPath)` *\\ plataformas \\* e crie a *plataforma. default. props*, *Platform. props* e os *arquivos Platform. targets* nela. Além disso, crie uma `$(VCTargetsPath)` pasta *\\ \\ Platforms**\\ PlatformToolsets \\* da <strong><em>plataforma</em></strong>e crie pelo menos um conjunto de ferramentas nela.

Todos os nomes de pasta na pasta *plataformas* de `$(ApplicationType)` cada `$(ApplicationTypeRevision)` um e aparecem no IDE como opções de **plataforma** disponíveis para um projeto.

![A nova opção de plataforma na caixa de diálogo nova plataforma de projeto](media/vc-project-extensibility-new-project-platform.png "A nova opção de plataforma na caixa de diálogo nova plataforma de projeto")

### <a name="add-a-new-application-type"></a>Adicionar um novo tipo de aplicativo

Para adicionar um novo tipo de aplicativo, crie uma pasta *myapplicationtype* em `$(VCTargetsPath)` *\\ tipo \\ de aplicativo* e crie um arquivo *padrão. props* nela. Pelo menos uma revisão é necessária para um tipo de aplicativo, portanto, também crie uma `$(VCTargetsPath)` pasta do *\\ tipo de aplicativo \\ myapplicationtype \\ 1,0* e crie um arquivo *padrão. props* nela. Você também deve criar uma `$(VCTargetsPath)` pasta de *\\ plataformas ApplicationType \\ myapplicationtype \\ \\ 1,0* e criar pelo menos uma plataforma nela.

`$(ApplicationType)``$(ApplicationTypeRevision)`as propriedades e não são visíveis na interface do usuário. Eles são definidos nos modelos de projeto e não podem ser alterados após a criação do projeto.

## <a name="the-vcxproj-import-tree"></a>A árvore de importação. vcxproj

Uma árvore simplificada de importações para os arquivos de propriedades e destinos do Microsoft C++ é semelhante a:

> `$(VCTargetsPath)`\\*Microsoft. cpp. default. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft. Common. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\ *Padrão* \\ \* . *props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ Tipo `$(ApplicationType)` de \\ aplicativo *Padrão. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ Tipo `$(ApplicationType)` \\ de `$(ApplicationTypeRevision)` aplicativo \\ *Padrão. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ Tipo `$(ApplicationType)` \\ de `$(ApplicationTypeRevision)` aplicativo \\  \\ `$(Platform)` Plataformas \\ *Platform. padrão. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\ *Padrão* \\ \* . *props*

Projetos da área de trabalho do Windows não definem `$(ApplicationType)` , portanto, eles só importam

> `$(VCTargetsPath)`\\*Microsoft. cpp. default. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft. Common. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\ *Padrão* \\ \* . *props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ `$(Platform)` Plataformas \\ *Platform. padrão. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\ *Padrão* \\ \* . *props*

Usaremos a `$(_PlatformFolder)` propriedade para manter os locais da `$(Platform)` pasta da plataforma. Essa propriedade é

> `$(VCTargetsPath)`\\*Compatíveis*\\`$(Platform)`

para aplicativos da área de trabalho do Windows e

> `$(VCTargetsPath)`\\ \\ Tipo `$(ApplicationType)` \\ de `$(ApplicationTypeRevision)` aplicativo \\ *Plataformas*\\`$(Platform)`

para todo o resto.

Os arquivos props são importados nesta ordem:

> `$(VCTargetsPath)`\\*Microsoft. cpp. props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform. props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft. cpp. Platform. props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* . *props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\ \\ `$(PlatformToolset)` PlatformToolsets \\ *Conjunto de ferramentas. props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* . *props*

Os arquivos de destino são importados nesta ordem:

> `$(VCTargetsPath)`\\*Microsoft. cpp. targets* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft. cpp. Current. targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform. targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft. cpp. Platform. targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* . *destinos* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\ \\ `$(PlatformToolset)` PlatformToolsets \\ *Conjunto de ferramentas. Target* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* . *destinos*

Se você precisar definir algumas propriedades padrão para o conjunto de ferramentas, poderá adicionar arquivos às pastas ImportBefore e ImportAfter apropriadas.

## <a name="author-toolsetprops-and-toolsettargets-files"></a>Criar arquivos de conjunto de ferramentas. props e Toolset. targets

Os arquivos *Toolset. props* e *Toolset. targets* têm controle total sobre o que acontece durante uma compilação quando esse conjunto de ferramentas é usado. Eles também podem controlar os depuradores disponíveis, parte da interface do usuário do IDE, como o conteúdo na caixa de diálogo **páginas de propriedades** e alguns outros aspectos do comportamento do projeto.

Embora um conjunto de ferramentas possa substituir todo o processo de compilação, normalmente você apenas deseja que o conjunto de ferramentas modifique ou adicione algumas etapas de compilação, ou use ferramentas de compilação diferentes, como parte de um processo de compilação existente. Para atingir esse objetivo, há vários arquivos comuns de props e de destinos que seu conjunto de ferramentas pode importar. Dependendo do que você deseja que seu conjunto de ferramentas faça, esses arquivos podem ser úteis para serem usados como importações ou como exemplos:

- `$(VCTargetsPath)`\\*Microsoft. CppCommon. targets*

  Esse arquivo define as principais partes do processo de compilação nativo e também importa:

  - `$(VCTargetsPath)`\\*Microsoft. CppBuild. targets*

  - `$(VCTargetsPath)`\\*Microsoft. BuildSteps. targets*

  - `$(MSBuildToolsPath)`\\*Microsoft. Common. targets*

- `$(VCTargetsPath)`\\*Microsoft. cpp. Common. props*

   Define padrões para conjuntos de ferramentas que usam os compiladores da Microsoft e as janelas de destino.

- `$(VCTargetsPath)`\\*Microsoft. cpp. WindowsSDK. props*

   Esse arquivo determina o local do SDK do Windows e define algumas propriedades importantes para aplicativos direcionados para o Windows.

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>Integrar destinos específicos do conjunto de ferramentas com o processo de compilação padrão do C++

O processo de compilação padrão do C++ é definido em *Microsoft. CppCommon. targets*. Os destinos não chamam nenhuma ferramenta de Build específica; Eles especificam as principais etapas de compilação, sua ordem e dependências.

A compilação C++ tem três etapas principais, que são representadas pelos seguintes destinos:

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

Como cada etapa de compilação pode ser executada de forma independente, os destinos em execução em uma etapa não podem contar com os grupos de itens e as propriedades definidas nos destinos executados como parte de uma etapa diferente. Essa divisão permite determinadas otimizações de desempenho de compilação. Embora ele não seja usado por padrão, você ainda é incentivado a honrar essa separação.

Os destinos que são executados dentro de cada etapa são controlados por essas propriedades:

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

Cada etapa também tem as propriedades before e After.

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

Consulte o arquivo *Microsoft. CppBuild. targets* para obter exemplos dos destinos que estão incluídos em cada etapa:

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

Se você observar os destinos, como `_ClCompile` , você verá que eles não fazem nada diretamente, mas dependem de outros destinos, incluindo `ClCompile` :

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` e outros destinos específicos da ferramenta de compilação são definidos como destinos vazios em *Microsoft. CppBuild. targets*:

```xml
<Target Name="ClCompile"/>
```

Como o `ClCompile` destino está vazio, a menos que seja substituído por um conjunto de ferramentas, nenhuma ação de Build real é executada. Os destinos do conjunto de ferramentas podem substituir o `ClCompile` destino, ou seja, eles podem conter outra `ClCompile` definição depois de importar *Microsoft. CppBuild. targets*:

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

Apesar de seu nome, que foi criado antes do Visual Studio implementar o suporte de plataforma cruzada, o `ClCompile` destino não precisa chamar CL.exe. Ele também pode chamar Clang, gcc ou outros compiladores usando as tarefas apropriadas do MSBuild.

O `ClCompile` destino não deve ter nenhuma dependência, exceto o `SelectClCompile` destino, que é necessário para que o comando de compilação de arquivo único funcione no IDE.

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>Tarefas do MSBuild a serem usadas em destinos do conjunto de ferramentas

Para invocar uma ferramenta de compilação real, o destino precisa chamar uma tarefa do MSBuild. Há uma [tarefa Exec](../msbuild/exec-task.md) básica que permite especificar uma linha de comando a ser executada. No entanto, as ferramentas de compilação geralmente têm muitas opções, entradas. e saídas para rastrear compilações incrementais, de modo que faz mais sentido ter tarefas especiais para elas. Por exemplo, a `CL` tarefa converte as propriedades do MSBuild em CL.exe opções, grava-as em um arquivo de resposta e chama CL.exe. Ele também controla todos os arquivos de entrada e saída para compilações incrementais posteriores. Para obter mais informações, consulte [compilações incrementais e verificações atualizadas](#incremental-builds-and-up-to-date-checks).

O Microsoft.Cpp.Common.Tasks.dll implementa estas tarefas:

- `BSCMake`

- `CL`

- `ClangCompile` (Clang-opções de gcc)

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (como exec, mas com acompanhamento de entrada e saída)

- `SetEnv`

- `GetOutOfDateItems`

Se você tiver uma ferramenta que execute a mesma ação que uma ferramenta existente e que tenha opções de linha de comando semelhantes (como Clang e CL do), você poderá usar a mesma tarefa para ambas.

Se você precisar criar uma nova tarefa para uma ferramenta de compilação, poderá escolher entre as seguintes opções:

1. Se você usar essa tarefa raramente ou se alguns segundos não forem importantes para sua compilação, você poderá usar tarefas ' embutidas ' do MSBuild:

   - Tarefa XAML (uma regra de compilação personalizada)

     Para obter um exemplo de uma declaração de tarefa XAML, consulte `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml* e, para seu uso, consulte `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *MASM. targets*.

   - [Tarefa de código](../msbuild/msbuild-inline-tasks.md)

1. Se você quiser um melhor desempenho de tarefas ou precisar apenas de uma funcionalidade mais complexa, use o processo de [gravação de tarefa](../msbuild/task-writing.md) regular do MSBuild.

   Se nem todas as entradas e saídas da ferramenta estiverem listadas na linha de comando da ferramenta, como `CL` nos `MIDL` casos, e `RC` , se você quiser o rastreamento de arquivo de entrada e saída automático e a criação do arquivo. tlog, derive a tarefa da `Microsoft.Build.CPPTasks.TrackedVCToolTask` classe. No momento, embora haja documentação para a classe base [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) , não há exemplos ou documentação para os detalhes da `TrackedVCToolTask` classe. Se isso for de interesse particular, adicione sua voz a uma solicitação na [comunidade de desenvolvedores](https://aka.ms/feedback/suggest?space=62).

## <a name="incremental-builds-and-up-to-date-checks"></a>Compilações incrementais e verificações atualizadas

Os destinos de compilação incremental do MSBuild padrão usam `Inputs` `Outputs` atributos e. Se você especificá-los, o MSBuild chamará o destino somente se qualquer uma das entradas tiver um carimbo de data/hora mais recente do que todas as saídas. Como os arquivos de origem geralmente incluem ou importam outros arquivos, e as ferramentas de compilação produzem saídas diferentes dependendo das opções da ferramenta, é difícil especificar todas as entradas e saídas possíveis em destinos do MSBuild.

Para gerenciar esse problema, a compilação C++ usa uma técnica diferente para dar suporte a compilações incrementais. A maioria dos destinos não especifica entradas e saídas e, como resultado, sempre é executada durante a compilação. As tarefas chamadas por destinos gravam informações sobre todas as entradas e saídas em arquivos *tlog* que têm uma extensão. tlog. Os arquivos. tlog são usados por compilações posteriores para verificar o que mudou e precisa ser recriado e o que está atualizado. Os arquivos. tlog também são a única fonte para a verificação padrão da compilação atual no IDE.

Para determinar todas as entradas e saídas, as tarefas de ferramentas nativas usam tracker.exe e a classe [Filetrackr](/dotnet/api/microsoft.build.utilities.filetracker) fornecida pelo MSBuild.

Microsoft.Build.CPPTasks.Common.dll define a `TrackedVCToolTask` classe base abstrata pública. A maioria das tarefas de ferramentas nativas é derivada dessa classe.

A partir do Visual Studio 2017 atualização 15,8, você pode usar a `GetOutOfDateItems` tarefa implementada em Microsoft.Cpp.Common.Tasks.dll para produzir arquivos. tlog para destinos personalizados com entradas e saídas conhecidas.
Como alternativa, você pode criá-los usando a `WriteLinesToFile` tarefa. Consulte o `_WriteMasmTlogs` destino em `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *MASM. targets* como exemplo.

## <a name="tlog-files"></a>arquivos. tlog

Há três tipos de arquivos. tlog: *leitura*, *gravação* e *linha de comando*. Ler e gravar arquivos. tlog são usados por compilações incrementais e pela verificação atualizada no IDE. Os arquivos de linha de comando. tlog são usados apenas em compilações incrementais.

O MSBuild fornece essas classes auxiliares para ler e gravar arquivos. tlog:

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

A classe [FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata) pode ser usada para acessar arquivos Read e Write. tlog e identificar entradas que são mais novas do que saídas, ou se uma saída estiver ausente. Ele é usado na verificação atualizada.

Os arquivos de linha de comando. tlog contêm informações sobre linhas de comando usadas na compilação. Eles são usados apenas para compilações incrementais, não para verificações atualizadas, portanto, o formato interno é determinado pela tarefa do MSBuild que os produz.

### <a name="read-tlog-format"></a>Ler o formato. tlog

*Ler* arquivos. tlog ( \* . Read. \* . tlog) contêm informações sobre arquivos de origem e suas dependências.

Um acento circunflexo ( **^** ) no início de uma linha indica uma ou mais fontes. As fontes que compartilham as mesmas dependências são separadas por uma barra vertical ( **\|** ).

Os arquivos de dependência são listados após as fontes, cada um em sua própria linha. Todos os nomes de arquivo são caminhos completos.

Por exemplo, suponha que suas fontes de projeto sejam encontradas em *F: \\ test \\ ConsoleApplication1 \\ ConsoleApplication1*. Se o arquivo de origem, *Class1. cpp*, tiver esses incluem,

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

em seguida, o arquivo *CL. Read. 1. tlog* contém o arquivo de origem seguido por suas duas dependências:

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

Não é necessário escrever nomes de arquivo em letras maiúsculas, mas é uma conveniência para algumas ferramentas.

### <a name="write-tlog-format"></a>Formato Write. tlog

*Write* . tlog ( \* . Write. \* . tlog) os arquivos conectam fontes e saídas.

Um acento circunflexo ( **^** ) no início de uma linha indica uma ou mais fontes. Várias fontes são separadas por uma barra vertical ( **\|** ).

Os arquivos de saída criados a partir das fontes devem ser listados após as fontes, cada um em sua própria linha. Todos os nomes de arquivo devem ser caminhos completos.

Por exemplo, para um projeto ConsoleApplication simples que tem um arquivo de origem adicional *Class1. cpp*, o arquivo *link. Write. 1. tlog* pode conter:

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>Compilação em tempo de design

No IDE, os projetos. vcxproj usam um conjunto de destinos do MSBuild para obter informações adicionais do projeto e para gerar novamente os arquivos de saída. Alguns desses destinos são usados apenas em compilações de tempo de design, mas muitos deles são usados tanto em compilações regulares quanto em compilações de tempo de design.

Para obter informações gerais sobre compilações de tempo de design, consulte a documentação do CPS para [compilações de tempo de design](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md). Esta documentação é apenas parte aplicável a Visual C++ projetos.

Os `CompileDesignTime` `Compile` destinos e mencionados na documentação de builds de tempo de design nunca são executados para projetos. vcxproj. Os projetos Visual C++. vcxproj usam destinos de tempo de design diferentes para obter informações do IntelliSense.

### <a name="design-time-targets-for-intellisense-information"></a>Destinos de tempo de design para informações do IntelliSense

Os destinos de tempo de design usados em projetos. vcxproj são definidos em `$(VCTargetsPath)` \\ *Microsoft. cpp. designtime. targets*.

O `GetClCommandLines` destino coleta opções de compilador para o IntelliSense:

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` – destinos somente de tempo de design, necessários para a inicialização de compilação em tempo de design. Entre outras coisas, esses destinos desabilitam algumas funcionalidades de compilação regulares para melhorar o desempenho.

- `ComputeCompileInputsTargets` – um conjunto de destinos que modifica opções e itens de compilador. Esses destinos são executados em compilações regulares e em tempo de design.

O destino chama a `CLCommandLine` tarefa para criar a linha de comando a ser usada para o IntelliSense. Novamente, apesar de seu nome, ele pode manipular não apenas as opções de CL, mas também as opções Clang e gcc. O tipo das opções do compilador é controlado pela `ClangMode` propriedade.

Atualmente, a linha de comando produzida pela `CLCommandLine` tarefa sempre usa as opções de CL (mesmo no modo Clang) porque elas são mais fáceis para o mecanismo IntelliSense analisar.

Se você estiver adicionando um destino que é executado antes da compilação, seja regular ou em tempo de design, certifique-se de que ele não interrompa as compilações de tempo de design ou afete o desempenho. A maneira mais simples de testar seu destino é abrir um prompt de comando do desenvolvedor e executar este comando:

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

Esse comando produz um log de compilação detalhado, *MSBuild. log*, que tem um resumo de desempenho para os destinos e as tarefas no final.

Certifique-se de usar `Condition ="'$(DesignTimeBuild)' != 'true'"` em todas as operações que fazem sentido apenas para compilações regulares e não para compilações de tempo de design.

### <a name="design-time-targets-that-generate-sources"></a>Destinos de tempo de design que geram fontes

*Esse recurso está desabilitado por padrão para projetos nativos de desktop e não tem suporte atualmente em projetos em cache*.

Se os `GeneratorTarget` metadados forem definidos para um item de projeto, o destino será executado automaticamente quando o projeto for carregado e quando o arquivo de origem for alterado.

::: moniker range="vs-2017"

Por exemplo, para gerar automaticamente arquivos. cpp ou. h de arquivos. XAML, os `$(VSInstallDir)` \\ arquivos *MSBuild* \\ *Microsoft* \\ *WindowsXaml* \\ *v 15.0* \\ \* \\ *Microsoft. Windows. UI. XAML. cpp. targets* definem estas entidades:

::: moniker-end

::: moniker range=">=vs-2019"

Por exemplo, para gerar automaticamente arquivos. cpp ou. h de arquivos. XAML, os `$(VSInstallDir)` \\ arquivos *MSBuild* \\ *Microsoft* \\ *WindowsXaml* \\ *v 16.0* \\ \* \\ *Microsoft. Windows. UI. XAML. cpp. targets* definem estas entidades:

::: moniker-end

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

Para usar `Task.HostObject` o para obter o conteúdo não salvo de arquivos de origem, os destinos e a tarefa devem ser registrados como [MsbuildHostObjects](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017&preserve-view=true) para os projetos fornecidos em um pkgdef:

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Visual C++ a extensibilidade do projeto no IDE do Visual Studio

O sistema de projeto Visual C++ é baseado no [sistema do vs Project](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)e usa seus pontos de extensibilidade. No entanto, a implementação da hierarquia do projeto é específica para Visual C++ e não com base no CPS, portanto, a extensibilidade da hierarquia é limitada aos itens do projeto.

### <a name="project-property-pages"></a>Página de propriedades do projeto

Para obter informações gerais de design, consulte [estrutura multiplataforma para projetos do vc + +](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/).

Em termos simples, as páginas de propriedades que você vê na caixa de diálogo **Propriedades do projeto** de um projeto C++ são definidas por arquivos de *regras* . Um arquivo de regra especifica um conjunto de propriedades para mostrar em uma página de propriedades e como e onde eles devem ser salvos no arquivo de projeto. Arquivos de regras são arquivos. XML que usam o formato XAML. Os tipos usados para serializar eles são descritos em [Microsoft. Build. Framework. XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes). Para obter mais informações sobre o uso de arquivos de regras em projetos, consulte [Property Page XML Rule files](/cpp/build/reference/property-page-xml-files).

Os arquivos de regra devem ser adicionados ao `PropertyPageSchema` grupo de itens:

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` os metadados limitam a visibilidade da regra, que também é controlada pelo tipo de regra, e pode ter um destes valores:

`Project` | `File` | `PropertySheet`

O CPS dá suporte a outros valores para o tipo de contexto, mas eles não são usados em projetos Visual C++.

Se a regra estiver visível em mais de um contexto, use ponto-e-vírgula (**;**) para separar os valores de contexto, conforme mostrado aqui:

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>Formato de regra e tipos principais

O formato da regra é simples, portanto, esta seção descreve apenas os atributos que afetam a aparência da regra na interface do usuário.

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

O `PageTemplate` atributo define como a regra é exibida na caixa de diálogo **páginas de propriedades** . O atributo pode ter um destes valores:

| Atributo | Descrição |
|------------| - |
| `generic` | Todas as propriedades são mostradas em uma página em títulos de categoria<br/>A regra pode ser visível para `Project` e `PropertySheet` contextos, mas não para `File` .<br/><br/> Exemplo: `$(VCTargetsPath)` \\ *1033* \\ *general.xml* |
| `tool` | As categorias são mostradas como subpáginas.<br/>A regra pode ser visível em todos os contextos `Project` : `PropertySheet` e `File` .<br/>A regra estará visível nas propriedades do projeto somente se o projeto tiver itens com o `ItemType` definido em `Rule.DataSource` , a menos que o nome da regra esteja incluído no `ProjectTools` grupo de itens.<br/><br/>Exemplo: `$(VCTargetsPath)` \\ *1033* \\ *clang.xml* |
| `debugger` | A página é mostrada como parte da página de depuração.<br/>As categorias são ignoradas no momento.<br/>O nome da regra deve corresponder ao atributo do objeto MEF do inicializador de depuração `ExportDebugger` .<br/><br/>Exemplo: `$(VCTargetsPath)` \\  \\ *\_ \_windows.xmldo depurador local* do 1033 |
| *Personalizar* | Modelo personalizado. O nome do modelo deve corresponder ao `ExportPropertyPageUIFactoryProvider` atributo do `PropertyPageUIFactoryProvider` objeto MEF. Consulte **Microsoft. VisualStudio. ProjectSystem. designers. Properties. IPropertyPageUIFactoryProvider**.<br/><br/> Exemplo: `$(VCTargetsPath)` \\ *1033* \\ *userMacros.xml* |

Se a regra usar um dos modelos baseados em grade de propriedade, ela poderá usar esses pontos de extensibilidade para suas propriedades:

- [Editores de valor de propriedade](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [Provedor de valores de enumeração dinâmica](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>Estender uma regra

Se você quiser usar uma regra existente, mas precisar adicionar ou remover (ou seja, ocultar) apenas algumas propriedades, poderá criar uma [regra de extensão](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md).

#### <a name="override-a-rule"></a>Substituir uma regra

Talvez você queira que o conjunto de ferramentas use a maioria das regras padrão do projeto, mas substitua apenas uma ou algumas delas. Por exemplo, digamos que você queira apenas alterar a regra C/C++ para mostrar diferentes opções de compilador. Você pode fornecer uma nova regra com o mesmo nome e nome de exibição que a regra existente e incluí-la no `PropertyPageSchema` grupo de itens após a importação de destinos de CPP padrão. Somente uma regra com um determinado nome é usada no projeto e a última incluída no `PropertyPageSchema` grupo de itens vence.

#### <a name="project-items"></a>Itens do projeto

O arquivo de *ProjectItemsSchema.xml* define `ContentType` os `ItemType` valores e para os itens que são tratados como itens de projeto e define os `FileExtension` elementos para determinar a qual grupo de itens um novo arquivo será adicionado.

O arquivo ProjectItemsSchema padrão é encontrado em `$(VCTargetsPath)` \\ *1033* \\ *ProjectItemsSchema.xml*. Para estendê-lo, você deve criar um arquivo de esquema com um novo nome, como *MyProjectItemsSchema.xml*:

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

Em seguida, no arquivo de destino, adicione:

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

Exemplo: `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml*

### <a name="debuggers"></a>Depuradores

O serviço de depuração no Visual Studio dá suporte à extensibilidade para o mecanismo de depuração. Para obter mais informações, consulte estes exemplos:

- [MIEngine, projeto de código-fonte aberto que dá suporte à depuração de lldb](https://github.com/Microsoft/MIEngine)

- [Exemplo de mecanismo de depuração do Visual Studio](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

Para especificar os mecanismos de depuração e outras propriedades para a sessão de depuração, você deve implementar um componente MEF do [inicializador de depuração](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md) e adicionar uma `debugger` regra. Para obter um exemplo, consulte o `$(VCTargetsPath)` \\ \\ \_ arquivowindows.xml do depurador local do 1033 \_ .

### <a name="deploy"></a>Implantar

os projetos. vcxproj usam a extensibilidade do sistema de projetos do Visual Studio para [implantar provedores](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md).

### <a name="build-up-to-date-check"></a>Verificação atualizada de compilação

Por padrão, a verificação atualizada de compilação requer que arquivos Read. tlog e Write. tlog sejam criados na `$(TlogLocation)` pasta durante a compilação para todas as entradas e saídas de compilação.

Para usar uma verificação personalizada atualizada:

1. Desabilite a verificação padrão atualizada adicionando a `NoVCDefaultBuildUpToDateCheckProvider` funcionalidade no arquivo *Toolset. targets* :

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. Implemente seu próprio [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md).

## <a name="project-upgrade"></a>Atualização do projeto

### <a name="default-vcxproj-project-upgrader"></a>O Atualizador de projeto padrão. vcxproj

O Atualizador de projeto default. vcxproj altera o `PlatformToolset` , o `ApplicationTypeRevision` MSBuild Toolset versão e o .NET Framework. Os dois últimos são sempre alterados para os padrões de versão do Visual Studio, mas `PlatformToolset` e `ApplicationTypeRevision` podem ser controlados por propriedades especiais do MSBuild.

O atualizador usa esses critérios para decidir se um projeto pode ser atualizado ou não:

1. Para projetos que definem `ApplicationType` e `ApplicationTypeRevision` , há uma pasta com um número de revisão maior do que a atual.

1. A propriedade `_UpgradePlatformToolsetFor_<safe_toolset_name>` é definida para o conjunto de ferramentas atual e seu valor não é igual ao conjunto de ferramentas atual.

   Nesses nomes de propriedade, *\<safe_toolset_name>* representa o nome do conjunto de ferramentas com todos os caracteres não alfanuméricos substituídos por um sublinhado ( **\_** ).

Quando um projeto pode ser atualizado, ele participa da *solução redirecionando*. Para obter mais informações, consulte [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2).

Se você quiser adornar nomes de projeto em **Gerenciador de soluções** quando os projetos usarem um conjunto de ferramentas específico, defina uma `_PlatformToolsetShortNameFor_<safe_toolset_name>` propriedade.

Para obter exemplos `_UpgradePlatformToolsetFor_<safe_toolset_name>` de `_PlatformToolsetShortNameFor_<safe_toolset_name>` definições de propriedade e, consulte o arquivo *Microsoft. cpp. default. props* . Para obter exemplos de uso, consulte o `$(VCTargetPath)` \\ arquivo *Microsoft. cpp. Platform. targets* .

### <a name="custom-project-upgrader"></a>Atualizador de projeto personalizado

Para usar um objeto personalizado de atualização de projeto, implemente um componente MEF, como mostrado aqui:

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

Seu código pode importar e chamar o objeto de atualização padrão. vcxproj:

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` é definido em *Microsoft.VisualStudio.ProjectSystem.VS.dll* e é semelhante a `IVsRetargetProjectAsync` .

Defina a `VCProjectUpgraderObjectName` propriedade para instruir o sistema de projeto a usar o objeto de atualização personalizado:

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>Desabilitar a atualização do projeto

Para desabilitar as atualizações do projeto, use um `NoUpgrade` valor:

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>Cache e extensibilidade do projeto

Para melhorar o desempenho ao trabalhar com grandes soluções C++ no Visual Studio 2017, o [cache do projeto](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/) foi introduzido. Ela é implementada como um banco de dados do SQLite populado com dado do projeto e, em seguida, usada para carregar projetos sem carregar projetos do MSBuild ou do CPS na memória.

Como não há objetos do CPS presentes para projetos. vcxproj carregados do cache, os componentes do MEF da extensão que importam `UnconfiguredProject` ou `ConfiguredProject` não podem ser criados. Para dar suporte à extensibilidade, o cache do projeto não é usado quando o Visual Studio detecta se um projeto usa (ou provavelmente usar) extensões do MEF.

Esses tipos de projeto sempre são totalmente carregados e têm objetos do CPS na memória, de modo que todas as extensões de MEF são criadas para eles:

- Projetos de inicialização

- Projetos que têm um atualizador de projeto personalizado, ou seja, eles definem uma `VCProjectUpgraderObjectName` Propriedade

- Projetos que não destinam as janelas de área de trabalho, ou seja, definem uma `ApplicationType` Propriedade

- Projetos de itens compartilhados (. vcxitems) e quaisquer projetos que fazem referência a eles por importação de projetos. vcxitems.

Se nenhuma dessas condições for detectada, um cache de projeto será criado. O cache inclui todos os dados do projeto MSBuild necessários para responder a `get` consultas em `VCProjectEngine` interfaces. Isso significa que todas as modificações no nível do arquivo de destinos e das propriedades do MSBuild feitas por uma extensão devem funcionar apenas em projetos carregados do cache.

## <a name="shipping-your-extension"></a>Enviando sua extensão

Para obter informações sobre como criar arquivos VSIX, consulte [enviando extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md). Para obter informações sobre como adicionar arquivos a locais de instalação especiais, por exemplo, para adicionar arquivos em `$(VCTargetsPath)` , consulte [instalando fora da pasta extensões](../extensibility/set-install-root.md).

## <a name="additional-resources"></a>Recursos adicionais

O sistema Microsoft Build ([MSBuild](../msbuild/msbuild.md)) fornece o mecanismo de compilação e o formato baseado em XML extensível para arquivos de projeto. Você deve estar familiarizado com os [conceitos](../msbuild/msbuild-concepts.md) básicos do MSBuild e com o modo como o [MSBuild para Visual C++](/cpp/build/reference/msbuild-visual-cpp-overview) funciona para estender o sistema de projeto Visual C++.

O Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) fornece as APIs de extensão que são usadas pelo CPS e o sistema de projeto Visual C++. Para obter uma visão geral de como o MEF é usado pelo CPS, consulte [CPS e MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) na [visão geral do VSProjectSystem do MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md).

Você pode personalizar o sistema de compilação existente para adicionar etapas de compilação ou novos tipos de arquivo. Para obter mais informações, consulte [visão geral do MSBuild (Visual C++)](/cpp/build/reference/msbuild-visual-cpp-overview) e [trabalhando com propriedades do projeto](/cpp/build/working-with-project-properties).
