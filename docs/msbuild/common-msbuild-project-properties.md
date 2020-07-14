---
title: Propriedades de projeto comuns do MSBuild | Microsoft Docs
ms.date: 01/18/2018
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- msbuild, common properties
- msbuild, project file properties
- ExcludeDeploymentUrl property
- project file properties (MSBuild)
ms.assetid: 9857505d-ae15-42f1-936d-6cd7fb9dd276
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 62f372be9ffa6ae76503550616c6b3612aad6146
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770872"
---
# <a name="common-msbuild-project-properties"></a>Propriedades de projeto comuns do MSBuild

A tabela a seguir lista as propriedades usadas com frequência que são definidas nos arquivos de projeto do Visual Studio ou incluídos nos arquivos *. targets* fornecidos pelo MSBuild.

 Os arquivos de projeto no Visual Studio (*.csproj*, *.vbproj*, *.vcxproj* e outros) contêm o código XML do MSBuild que é executado quando você cria um projeto usando o IDE. Normalmente, os projetos importam um ou mais arquivos *.targets* para definir o processo de build. Para obter mais informações, confira [Arquivos .targets do MSBuild](../msbuild/msbuild-dot-targets-files.md).

## <a name="list-of-common-properties-and-parameters"></a>Lista de propriedades e parâmetros comuns

| Nome da propriedade ou do parâmetro | Tipos de projeto | Descrição |
|------------------------------------| - | - |
| AdditionalLibPaths | .NET | Especifica as pastas adicionais nas quais os compiladores devem procurar assemblies de referência. |
| AddModules | .NET | Faz com que o compilador verifique todos os tipos de informações de arquivos disponíveis para o projeto que você está compilando. Essa propriedade é equivalente à opção do compilador `/addModules`. |
| ALToolPath | .NET | O caminho onde *AL.exe* pode ser encontrado. Essa propriedade substitui a versão atual do *AL.exe* para habilitar o uso de uma versão diferente. |
| ApplicationIcon | .NET | O arquivo de ícone *. ico* para passar para o compilador para inserção como um ícone do Win32. A propriedade é equivalente à opção do compilador `/win32icon`. |
| ApplicationManifest | Todos | Especifica o caminho do arquivo que é usado para gerar informações de manifesto de UAC (Controle de Conta de Usuário) externo. Aplica-se somente a projetos do Visual Studio destinados ao Windows Vista.<br /><br /> Na maioria dos casos, o manifesto é incorporado. No entanto, se você usar a implantação gratuita de COM ou ClickOnce, o manifesto poderá ser um arquivo externo que é instalado junto com seus assemblies de aplicativo. Para obter mais informações, consulte a propriedade NoWin32Manifest neste tópico. |
| AssemblyOriginatorKeyFile | .NET | Especifica o arquivo que é usado para assinar o assembly (*. SNK* ou *. pfx*) e que é passado para a [tarefa ResolveKeySource](../msbuild/resolvekeysource-task.md) para gerar a chave real usada para assinar o assembly. |
| AssemblySearchPaths | .NET | Uma lista de locais para pesquisa durante a resolução de assembly da referência de tempo de build. A ordem na qual os caminhos aparecem nesta lista é significativa porque os caminhos listados anteriormente têm precedência sobre as entradas mais recentes. |
| AssemblyName | .NET | O nome do assembly de saída final depois que o projeto é criado. |
| BaseAddress | .NET | Especifica o endereço básico do assembly de saída principal. Essa propriedade é equivalente à opção do compilador `/baseaddress`. |
| BaseIntermediateOutputPath | Todos | A pasta de nível superior na qual todas as pastas de saída intermediárias específicas da configuração são criadas. O valor padrão é `obj\`. O código a seguir é um exemplo: `<BaseIntermediateOutputPath>c:\xyz\obj\</BaseIntermediateOutputPath>` |
| BaseOutputPath | Todos | Especifica o caminho básico para o arquivo de saída. Se estiver definido, o MSBuild usará `OutputPath = $(BaseOutputPath)\$(Configuration)\` . Sintaxe de exemplo: `<BaseOutputPath>c:\xyz\bin\</BaseOutputPath>` |
| BuildInParallel | Todos | Um valor booliano que indica se as referências do projeto são criadas ou limpas em paralelo quando o MSBuild de vários procs é usado. O valor padrão é `true`, que significa que projetos serão compilados em paralelo se o sistema tiver vários processadores ou núcleos. |
| BuildProjectReferences | Todos | Um valor booliano que indica se as referências do projeto são criadas pelo MSBuild. Definido automaticamente como `false` se você estiver criando seu projeto no IDE (ambiente de desenvolvimento integrado) do Visual Studio, `true` caso contrário. `-p:BuildProjectReferences=false` pode ser especificado na linha de comando para evitar a verificação de atualização dos projetos referenciados. |
| CleanFile | Todos | O nome do arquivo que será usado como o "cache limpo". O cache limpo é uma lista dos arquivos gerados que serão excluídos durante a operação de limpeza. O arquivo é colocado no caminho de saída intermediária pelo processo de build.<br /><br /> Esta propriedade especifica apenas os nomes de arquivo que não têm informações de caminho. |
| CodePage | .NET | Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Essa propriedade é equivalente à opção do compilador `/codepage`. |
| CompilerResponseFile | .NET | Um arquivo de resposta opcional que pode ser passado para as tarefas do compilador. |
| Configuração | Todos | A configuração que você está compilando, geralmente `Debug` ou `Release` , mas configurável nos níveis da solução e do projeto. |
| CscToolPath | C# | O caminho do *csc.exe*, o compilador C#. |
| CustomBeforeMicrosoftCommonTargets | Todos | O nome de um arquivo de projeto ou arquivo de destino a ser importado automaticamente antes da importação de destinos comuns. |
| DebugSymbols | Todos | Um valor booliano que indica se os símbolos são gerados pelo build.<br /><br /> A configuração **-p:DebugSymbols = false** na linha de comando desabilita a geração de arquivos de símbolo do banco de dados do programa (*. pdb*). |
| DebugType | Todos | Define o nível de informações de depuração que você deseja que seja gerado. Os valores válidos são "full", "pdbonly", "portable", "embedded" e "none". |
| DefineConstants | .NET | Define as constantes de compilador condicional. Os pares de símbolo/valor são separados por ponto e vírgula e são especificados usando a sintaxe a seguir:<br /><br /> *symbol1 = value1 ; symbol2 = value2*<br /><br /> A propriedade é equivalente à opção do compilador `/define`. |
| DefineDebug | Todos |  Um valor booliano que indica se você deseja que a constante DEBUG seja definida. |
| DefineTrace | Todos | Um valor booliano que indica se você deseja que a constante TRACE seja definida. |
| DelaySign | .NET | Um valor booliano que indica se você deseja atrasar a assinatura do assembly em vez de fazer a assinatura completa. |
| Determinística | .NET | Um valor booliano que indica se o compilador deve gerar assemblies idênticos para entradas idênticas. Esse parâmetro corresponde à `/deterministic` opção dos compiladores. |
| DisableFastUpToDateCheck | Todos | Um valor booliano que se aplica somente ao Visual Studio. O Gerenciador de compilação do Visual Studio usa um processo chamado FastUpToDateCheck para determinar se um projeto deve ser recriado para ser atualizado. Esse processo é mais rápido do que usar o MSBuild para determinar isso. Definir a propriedade DisableFastUpToDateCheck como `true` permite ignorar o Gerenciador de compilação do Visual Studio e forçá-lo a usar o MSBuild para determinar se o projeto está atualizado. |
| DocumentationFile | .NET | O nome do arquivo que é gerado como o arquivo de documentação XML. Esse nome inclui o nome de arquivo e não tem nenhuma informação de caminho. |
| ErrorReport | .NET | Especifica como a tarefa de compilador deve relatar erros do compilador interno. Os valores válidos são "prompt," "send" ou "none". Essa propriedade é equivalente à opção do compilador `/errorreport`. |
| ExcludeDeploymentUrl | .NET | A [tarefa GenerateDeploymentManifest](../msbuild/generatedeploymentmanifest-task.md) adiciona uma marca deploymentProvider ao manifesto de implantação se o arquivo de projeto incluir qualquer um dos seguintes elementos:<br /><br /> -   UpdateUrl<br />-   InstallUrl<br />-   PublishUrl<br /><br /> Entretanto, ao usar ExcludeDeploymentUrl, você poderá impedir que a marca deploymentProvider seja adicionada ao manifesto de implantação, mesmo se qualquer uma das URLs acima for especificada. Para fazer isso, adicione a propriedade a seguir ao arquivo de projeto:<br /><br /> `<ExcludeDeploymentUrl>true</ExcludeDeploymentUrl>` <br /><br />**Observação:**  ExcludeDeploymentUrl não é exposto no IDE do Visual Studio e só pode ser definido pela edição manual do arquivo de projeto. Definir essa propriedade não afeta a publicação no Visual Studio; ou seja, a marca deploymentProvider ainda será adicionada à URL especificada por PublishUrl. |
| FileAlignment | .NET | Especifica, em bytes, onde alinhar as seções do arquivo de saída. Os valores válidos são 512, 1024, 2048, 4096, 8192. Essa propriedade é equivalente à opção do compilador `/filealignment`. |
| FrameworkPathOverride | Visual Basic | Especifica o local de *mscorlib.dll* e *microsoft.visualbasic.dll*. Esse parâmetro é equivalente ao `/sdkpath` switch do compilador de *vbc.exe* . |
| GenerateDocumentation | .NET | Um parâmetro booliano que indica se a documentação é gerada pelo build. Se `true` , a compilação gerará informações de documentação e as colocará em um arquivo *. xml* junto com o nome do arquivo executável ou da biblioteca criada pela tarefa de compilação. |
| GenerateFullPaths | C# | Gere caminhos completos para nomes de FileNames na saída usando a opção de compilador [-fullpaths](/dotnet/csharp/language-reference/compiler-options/fullpaths-compiler-option) . |
| GenerateSerializationAssemblies | .NET | Indica se os assemblies de serialização XML devem ser gerados por *SGen.exe*, que pode ser definido como ativado, automático ou desativado. Essa propriedade é usada para assemblies destinados exclusivamente ao .NET Framework. Para gerar assemblies de serialização de XML para assemblies do .NET Standard ou .NET Core, faça referência ao pacote do NuGet *Microsoft.XmlSerializer.Generator*. |
| IntermediateOutputPath | Todos | O caminho de saída completo intermediário conforme derivado de `BaseIntermediateOutputPath`, se nenhum caminho for especificado. Por exemplo, *\obj\debug \\ *. |
| KeyContainerName | Todos | O nome do contêiner de chave de nome forte. |
| KeyOriginatorFile | Todos | O nome do arquivo de chave de nome forte. |
| ModuleAssemblyName | .NET | O nome do assembly ao qual o módulo compilado será incorporado. A propriedade é equivalente à opção do compilador `/moduleassemblyname`. |
| MSBuildProjectExtensionsPath | Todos | Especifica o caminho em que se encontram as extensões de projeto. Por padrão, isso leva o mesmo valor que `BaseIntermediateOutputPath`. |
| NoLogo | Todos | Um valor booliano que indica se você deseja que o logotipo do compilador seja desligado. Essa propriedade é equivalente à opção do compilador `/nologo`. |
| NoStdLib | .NET | Um valor booliano que indica se deve ser evitada a referência à biblioteca padrão (*mscorlib.dll*). O valor padrão é `false`. |
| NoVBRuntimeReference | Visual Basic | Um valor booliano que indica se o tempo de execução de Visual Basic (*Microsoft.VisualBasic.dll*) deve ser incluído como uma referência no projeto. |
| Nowarn | .NET | Suprime os avisos especificados. Somente a parte numérica do identificador de aviso deve ser especificada. Vários avisos são separados por ponto e vírgula. Esse parâmetro corresponde à `/nowarn` opção dos compiladores. |
| NoWin32Manifest | .NET | Um valor booliano que indica se as informações do manifesto do UAC (Controle de Conta de Usuário) serão inseridas no executável do aplicativo. Aplica-se somente a projetos do Visual Studio destinados ao Windows Vista. Em projetos implantados usando ClickOnce e COM livre de registro, esse elemento é ignorado. `False` (o valor padrão) especifica se as informações do manifesto do UAC (Controle de Conta de Usuário) serão inseridas no executável do aplicativo. `True` especifica se as informações de manifesto de UAC não serão inseridas.<br /><br /> Essa propriedade só se aplica a projetos do Visual Studio destinados ao Windows Vista. Em projetos implantados usando ClickOnce e COM livre de registro, essa propriedade é ignorada.<br /><br /> Você deve adicionar NoWin32Manifest somente se não quiser que o Visual Studio incorpore qualquer informação de manifesto no executável do aplicativo; Esse processo é chamado de *virtualização*. Para usar a virtualização, defina `<ApplicationManifest>` em conjunto com `<NoWin32Manifest>` da seguinte maneira:<br /><br /> -Para projetos Visual Basic, remova o `<ApplicationManifest>` nó. (Em projetos Visual Basic, `<NoWin32Manifest>` é ignorado quando um `<ApplicationManifest>` nó existe.)<br />-Para projetos C#, defina `<ApplicationManifest>` como `False` e `<NoWin32Manifest>` como `True` . (Em projetos C#, `<ApplicationManifest>` substituições `<NoWin32Manifest>` .)<br /> Essa propriedade é equivalente à `/nowin32manifest` opção de compilador de *vbc.exe*. |
| Otimizar | .NET | Um valor booliano que, quando definido como `true`, permite otimizações do compilador. Essa propriedade é equivalente à opção do compilador `/optimize`. |
| OptionCompare | VisualBasic | Especifica como são feitas comparações de cadeia de caracteres. Os valores válidos são "binary" ou "text". Essa propriedade é equivalente à `/optioncompare` opção de compilador de *vbc.exe*. |
| OptionExplicit | Visual Basic | Um valor booliano que, quando definido como `true`, exige a declaração explícita de variáveis no código-fonte. Essa propriedade é equivalente à opção do compilador `/optionexplicit`. |
| OptionInfer | Visual Basic | Um valor booliano que, quando definido como `true`, habilita a inferência de tipos de variáveis. Essa propriedade é equivalente à opção do compilador `/optioninfer`. |
| OptionStrict | Visual Basic | Um valor booliano que, quando definido como `true`, faz com que a tarefa de build para impor a semântica de tipo estrito restrinja conversões de tipo implícito. Essa propriedade é equivalente à `/optionstrict` opção do compilador de *vbc.exe* . |
| OutDir | Todos | Indica o local de saída final para o projeto ou solução. Ao criar uma solução, o OutDir pode ser usado para reunir várias saídas de projeto em um único local. Além disso, o OutDir está incluído em AssemblySearchPaths usado para resolver referências. Por exemplo, *bin\Debug*. |
| OutputPath | Todos | Especifica o caminho para o diretório de saída, relativo ao diretório do projeto, por exemplo, *bin\Debug*. |
| OutputType | Todos |  Especifica o formato do arquivo de saída. Esse parâmetro pode ter um dos seguintes valores:<br /><br /> -   Library. Cria uma biblioteca de códigos. (Valor padrão.)<br />-   Exe. Crie um aplicativo de console.<br />-   Module. Cria um módulo.<br />-   Winexe. Cria um programa baseado em Windows.<br /><br /> Para C# e Visual Basic, essa propriedade é equivalente à `/target` opção. |
| OverwriteReadOnlyFiles | Todos | Um valor booliano que indica se você deseja habilitar o build para substituir arquivos somente leitura ou disparar um erro. |
| PathMap | .NET | Especifica como mapear caminhos físicos para nomes de caminho de origem emitidos pelo compilador. Essa propriedade é equivalente à `/pathmap` opção dos compiladores. |
| PdbFile | .NET | O nome do arquivo *. pdb* que você está emitindo. Essa propriedade é equivalente à `/pdb` opção do compilador de *csc.exe* . |
| Plataforma | Todos | O sistema operacional que você está compilando. Exemplos de builds de .NET Framework são "qualquer CPU", "x86" e "x64". |
| ProcessorArchitecture | .NET | A arquitetura do processador que é usada quando as referências de assembly são resolvidas. Os valores válidos são "msil," "x86," "amd64" ou "ia64". |
| ProduceOnlyReferenceAssembly | .NET | Um valor booliano que instrui o compilador a emitir apenas um assembly de referência ao invés do código compilado. Não pode ser usado em conjunto com `ProduceReferenceAssembly`.  Essa propriedade corresponde à opção `/refonly` dos compiladores *vbc.exe* e *csc.exe*. |
| ProduceReferenceAssembly | .NET | Um valor booliano que, quando definido como `true`, permite a produção de [assemblies de referência](/dotnet/standard/assembly/reference-assemblies) para o assembly atual. `Deterministic` deve ser `true` ao usar esse recurso. Essa propriedade corresponde à opção `/refout` dos compiladores *vbc.exe* e *csc.exe*. |
| RemoveIntegerChecks | Visual Basic | Um valor booliano que indica se é necessário desabilitar a verificação de erro de estouro de inteiro. O valor padrão é `false`. Essa propriedade é equivalente à `/removeintchecks` opção do compilador de *vbc.exe* . |
| RootNamespace | Todos | O namespace raiz para usar ao nomear um recurso inserido. Este namespace é parte do nome do manifesto do recurso inserido. |
| Satellite_AlgorithmId | .NET | A ID do *AL.exe* algoritmo de hash a ser usado quando os assemblies satélite são criados. |
| Satellite_BaseAddress | .NET | O endereço básico para usar quando assemblies satélites específicos da cultura forem criados usando o destino `CreateSatelliteAssemblies`. |
| Satellite_CompanyName | .NET | O nome da empresa a ser passado para *AL.exe* durante a geração de assembly satélite. |
| Satellite_Configuration | .NET | O nome da configuração para passar para *AL.exe* durante a geração de assembly satélite. |
| Satellite_Description | .NET | O texto de descrição a ser passado para *AL.exe* durante a geração de assembly satélite. |
| Satellite_EvidenceFile | .NET | Insere o arquivo especificado no assembly satélite que tem o nome do recurso "Security.Evidence". |
| Satellite_FileVersion | .NET | Especifica uma cadeia de caracteres para o campo Versão do Arquivo no assembly satélite. |
| Satellite_Flags | .NET | Especifica um valor para o campo Sinalizadores no assembly satélite. |
| Satellite_GenerateFullPaths | .NET | Faz com que a tarefa de build use o caminho absoluto para todos os arquivos reportados em uma mensagem de erro. |
| Satellite_LinkResource | .NET | Vincula os arquivos de recurso especificados a um assembly satélite. |
| Satellite_MainEntryPoint | .NET | Especifica o nome totalmente qualificado (ou seja, class.method) do método a ser usado como um ponto de entrada durante a conversão de um módulo em um arquivo executável durante a geração do assembly satélite. |
| Satellite_ProductName | .NET | Especifica uma cadeia de caracteres para o campo Produto no assembly satélite. |
| Satellite_ProductVersion | .NET | Especifica uma cadeia de caracteres para o campo ProductVersion no assembly satélite. |
| Satellite_TargetType | .NET | Especifica o formato de arquivo do arquivo de saída do assembly satélite como "library," "exe," ou "win". O valor padrão é "library". |
| Satellite_Title | .NET | Especifica uma cadeia de caracteres para o campo Título no assembly satélite. |
| Satellite_Trademark | .NET | Especifica uma cadeia de caracteres para o campo Marca registrada no assembly satélite. |
| Satellite_Version | .NET | Especifica as informações de versão do assembly satélite. |
| Satellite_Win32Icon | .NET | Insere um arquivo de ícone *. ico* no assembly satélite. |
| Satellite_Win32Resource | .NET | Insere um recurso do Win32 (arquivo *. res* ) no assembly satélite. |
| SGenToolPath | .NET | Um caminho de ferramenta opcional que indica onde obter *SGen.exe* quando a versão atual do *SGen.exe* é substituída. |
| SGenUseProxyTypes | .NET | Um valor booliano que indica se os tipos de proxy devem ser gerados pelo *SGen.exe*. Isso se aplica somente quando *GenerateSerializationAssemblies* está definido como on.<br /><br /> O destino SGen usa essa propriedade para definir o sinalizador UseProxyTypes. Essa propriedade assume true como padrão e não há nenhuma interface do usuário para alterar isso. Para gerar o assembly de serialização para tipos não WebService, adicione essa propriedade ao arquivo de projeto e defina-a como false antes de importar o *Microsoft. Common. targets* ou o *C#/vb.targets*. |
| SkipInvalidConfigurations | Todos | Quando `true` , gere um aviso em combinações de plataforma e configuração inválidas, mas não falhe na compilação; quando `false` ou indefinido (o padrão), gere um erro. |
| StartupObject | .NET | Especifica a classe ou o módulo que contém o método Main ou procedimento Sub Main. Essa propriedade é equivalente à opção do compilador `/main`. |
| SubsystemVersion | .NET | Especifica a versão mínima do subsistema que o arquivo executável gerado pode usar. Essa propriedade é equivalente à opção do compilador `/subsystemversion`. Para obter informações sobre o valor padrão dessa propriedade, consulte [/SubSystemVersion (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/subsystemversion) ou [/SubSystemVersion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/subsystemversion-compiler-option). |
| TargetCompactFramework | .NET | A versão do .NET Compact Framework que é necessária para executar o aplicativo que você está compilando. Especificar isso permite fazer referência a determinados assemblies de estrutura que pode não ser possível fazer referência de outra forma. |
| TargetFrameworkVersion | .NET | A versão do .NET Framework necessária para executar o aplicativo que está sendo criado. Especificar isso permite fazer referência a determinados assemblies de estrutura que pode não ser possível fazer referência de outra forma. |
| TreatWarningsAsErrors | .NET | Um parâmetro booliano que, se `true`, faz com que todos os avisos sejam tratados como erros. Esse parâmetro é equivalente à opção do compilador `/nowarn`. |
| UseHostCompilerIfAvailable | .NET | Um parâmetro booliano que, se `true`, faz com que a tarefa de build use o objeto do compilador em processo, se ele estiver disponível. Esse parâmetro é usado somente pelo Visual Studio. |
| Utf8Output | .NET | Um parâmetro booliano que, se `true`, registra a saída do compilador usando a codificação UTF-8. Esse parâmetro é equivalente à opção do compilador `/utf8Output`. |
| VbcToolPath | Visual Basic | Um caminho opcional que indica outro local para *vbc.exe* quando a versão atual do *vbc.exe* é substituída. |
| VbcVerbosity | Visual Basic | Especifica o detalhamento da saída do compilador de Visual Basic. Os valores válidos são "Quiet," "Normal" (o valor padrão) ou "Verbose". |
| VisualStudioVersion | Todos | Especifica a versão do Visual Studio sob a qual este projeto deve ser considerado para estar em execução. Se esta propriedade não for especificada, o MSBuild a definirá como um valor padrão razoável.<br /><br /> Essa propriedade é usada em vários tipos de projeto para especificar o conjunto de destinos que são usados para o build. Se `ToolsVersion` é definido como 4.0 ou superior para um projeto, `VisualStudioVersion` é usado para especificar o subconjunto de ferramentas que será usado. Para obter mais informações, consulte [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md). |
| WarningsAsErrors | .NET | Especifica uma lista de avisos a serem tratados como erros. Esse parâmetro é equivalente à opção do compilador `/warnaserror`. |
| WarningsNotAsErrors | .NET | Especifica uma lista de avisos que não são tratados como erros. Esse parâmetro é equivalente à opção do compilador `/warnaserror`. |
| Win32Manifest | .NET | O nome do arquivo de manifesto deve ser inserido no assembly final. Esse parâmetro é equivalente à opção do compilador `/win32Manifest`. |
| Win32Resource | .NET | O nome do arquivo do recurso do Win32 a ser inserido no assembly final. Esse parâmetro é equivalente à opção do compilador `/win32resource`. |

## <a name="see-also"></a>Confira também

- [Itens de projeto comuns do MSBuild](../msbuild/common-msbuild-project-items.md)
