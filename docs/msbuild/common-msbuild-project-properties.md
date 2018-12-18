---
title: Propriedades de projeto comuns do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2018
ms.technology: msbuild
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
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fe2c39fc08528886e143bd51eb1f33219b386807
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921711"
---
# <a name="common-msbuild-project-properties"></a>Propriedades de projeto comuns do MSBuild
A tabela a seguir lista as propriedades usadas com frequência que são definidas nos arquivos de projeto do Visual Studio ou incluídas nos arquivos *.targets* fornecidos pelo MSBuild.  
  
 Os arquivos de projeto no Visual Studio (*.csproj*, *.vbproj*, *.vcxproj* e outros) contêm o código XML do MSBuild que é executado quando você cria um projeto usando o IDE. Normalmente, os projetos importam um ou mais arquivos *.targets* para definir o processo de build. Para obter mais informações, confira [Arquivos .targets do MSBuild](../msbuild/msbuild-dot-targets-files.md).  
  
## <a name="list-of-common-properties-and-parameters"></a>Lista de propriedades e parâmetros comuns  
  
| Nome da propriedade ou do parâmetro | Descrição |
|------------------------------------| - |
| AdditionalLibPaths | Especifica as pastas adicionais nas quais os compiladores devem procurar assemblies de referência. |
| AddModules | Faz com que o compilador verifique todos os tipos de informações de arquivos disponíveis para o projeto que você está compilando. Essa propriedade é equivalente à opção do compilador `/addModules`. |
| ALToolPath | O caminho no qual o *AL.exe* pode ser encontrado. Essa propriedade substitui a versão atual do *AL.exe* para habilitar o uso de outra versão. |
| ApplicationIcon | O arquivo de ícone *.ico* a ser passado para o compilador para inseri-lo como um ícone do Win32. A propriedade é equivalente à opção do compilador `/win32icon`. |
| ApplicationManifest | Especifica o caminho do arquivo que é usado para gerar informações de manifesto de UAC (Controle de Conta de Usuário) externo. Aplica-se somente a projetos do Visual Studio que direcionam [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)].<br /><br /> Na maioria dos casos, o manifesto é incorporado. No entanto, se você usar o COM de registro livre ou a implantação [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], o manifesto poderá ser um arquivo externo que é instalado junto com seus assemblies de aplicativo. Para obter mais informações, consulte a propriedade NoWin32Manifest neste tópico. |
| AssemblyOriginatorKeyFile | Especifica o arquivo que é usado para assinar o assembly (*.snk* ou *.pfx*) e que é passado para a [tarefa ResolveKeySource](../msbuild/resolvekeysource-task.md) para gerar a chave real usada para assinar o assembly. |
| AssemblySearchPaths | Uma lista de locais para pesquisa durante a resolução de assembly da referência de tempo de build. A ordem na qual os caminhos aparecem nesta lista é significativa porque os caminhos listados anteriormente têm precedência sobre as entradas mais recentes. |
| AssemblyName | O nome do assembly de saída final depois que o projeto é criado. |
| BaseAddress | Especifica o endereço básico do assembly de saída principal. Essa propriedade é equivalente à opção do compilador `/baseaddress`. |
| BaseOutputPath | Especifica o caminho básico para o arquivo de saída. Se estiver definido, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] usará `OutputPath = $(BaseOutputPath)\$(Configuration)\`. Sintaxe de exemplo: `<BaseOutputPath>c:\xyz\bin\</BaseOutputPath>` |
| BaseIntermediateOutputPath | A pasta de nível superior na qual todas as pastas de saída intermediárias específicas da configuração são criadas. O valor padrão é `obj\`. O código a seguir é um exemplo: `<BaseIntermediateOutputPath>c:\xyz\obj\</BaseIntermediateOutputPath>` |
| BuildInParallel | Um valor booliano que indica se as referências de projeto são criadas ou limpas em paralelo quando Multi-Proc [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] for usado. O valor padrão é `true`, que significa que projetos serão compilados em paralelo se o sistema tiver vários processadores ou núcleos. |
| BuildProjectReferences | Um valor booliano que indica se as referências do projeto são criadas por [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Defina automaticamente como `false` se você estiver compilando seu projeto no IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], caso contrário, use `true`. `-p:BuildProjectReferences=false` pode ser especificado na linha de comando para evitar a verificação de atualização dos projetos referenciados. |
| CleanFile | O nome do arquivo que será usado como o "cache limpo". O cache limpo é uma lista dos arquivos gerados que serão excluídos durante a operação de limpeza. O arquivo é colocado no caminho de saída intermediária pelo processo de build.<br /><br /> Esta propriedade especifica apenas os nomes de arquivo que não têm informações de caminho. |
| CodePage | Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Essa propriedade é equivalente à opção do compilador `/codepage`. |
| CompilerResponseFile | Um arquivo de resposta opcional que pode ser passado para as tarefas do compilador. |
| Configuração | A configuração que você está criando, "Depurar" ou "Versão". |
| CscToolPath | O caminho do *csc.exe*, o compilador [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]. |
| CustomBeforeMicrosoftCommonTargets | O nome de um arquivo de projeto ou arquivo de destino a ser importado automaticamente antes da importação de destinos comuns. |
| DebugSymbols | Um valor booliano que indica se os símbolos são gerados pelo build.<br /><br /> A configuração de **-p:DebugSymbols=false** na linha de comando desabilita a geração de arquivos de símbolo do banco de dados de programa (*.pdb*). |
| DefineConstants | Define as constantes de compilador condicional. Os pares de símbolo/valor são separados por ponto e vírgula e são especificados usando a sintaxe a seguir:<br /><br /> *symbol1 = value1 ; symbol2 = value2*<br /><br /> A propriedade é equivalente à opção do compilador `/define`. |
| DefineDebug | Um valor booliano que indica se você deseja que a constante DEBUG seja definida. |
| DefineTrace | Um valor booliano que indica se você deseja que a constante TRACE seja definida. |
| DebugType | Define o nível de informações de depuração que você deseja que seja gerado. Os valores válidos são "full," "pdbonly" e "none". |
| DelaySign | Um valor booliano que indica se você deseja atrasar a assinatura do assembly em vez de fazer a assinatura completa. |
| Determinista | Um valor booliano que indica se o compilador deve gerar assemblies idênticos para entradas idênticas. Esse parâmetro corresponde à opção `/deterministic` dos compiladores *vbc.exe* e *csc.exe*. |
| DisabledWarnings | Suprime os avisos especificados. Somente a parte numérica do identificador de aviso deve ser especificada. Vários avisos são separados por ponto e vírgula. Esse parâmetro corresponde à opção `/nowarn` do compilador *vbc.exe*. |
| DisableFastUpToDateCheck | Um valor booliano que se aplica apenas a [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. O gerenciador de build [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] usa um processo chamado FastUpToDateCheck para determinar se um projeto deve ser reconstruído para ser atualizado. Esse processo é mais rápido que usar [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para determinar isso. Configurar a propriedade DisableFastUpToDateCheck para `true` permite ignorar o gerenciador de build [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e forçá-lo a usar [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] para determinar se o projeto está atualizado. |
| DocumentationFile | O nome do arquivo que é gerado como o arquivo de documentação XML. Esse nome inclui o nome de arquivo e não tem nenhuma informação de caminho. |
| ErrorReport | Especifica como a tarefa de compilador deve relatar erros do compilador interno. Os valores válidos são "prompt," "send" ou "none". Essa propriedade é equivalente à opção do compilador `/errorreport`. |
| ExcludeDeploymentUrl | A [tarefa GenerateDeploymentManifest](../msbuild/generatedeploymentmanifest-task.md) adiciona uma marca deploymentProvider ao manifesto de implantação se o arquivo de projeto inclui um dos seguintes elementos:<br /><br /> -   UpdateUrl<br />-   InstallUrl<br />-   PublishUrl<br /><br /> Entretanto, ao usar ExcludeDeploymentUrl, você poderá impedir que a marca deploymentProvider seja adicionada ao manifesto de implantação, mesmo se qualquer uma das URLs acima for especificada. Para fazer isso, adicione a propriedade a seguir ao arquivo de projeto:<br /><br /> `<ExcludeDeploymentUrl>true</ExcludeDeploymentUrl>` <br /><br />**Observação:** ExcludeDeploymentUrl não é exposta no IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e pode ser definida apenas com a edição manual do arquivo de projeto. A configuração dessa propriedade não afeta a publicação em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]; ou seja, a marca deploymentProvider ainda será adicionada à URL especificada pelo PublishUrl. |
| FileAlignment | Especifica, em bytes, onde alinhar as seções do arquivo de saída. Os valores válidos são 512, 1024, 2048, 4096, 8192. Essa propriedade é equivalente à opção do compilador `/filealignment`. |
| FrameworkPathOverride | Especifica o local de *mscorlib.dll* e *microsoft.visualbasic.dll*. Esse parâmetro é equivalente à opção `/sdkpath` do compilador *vbc.exe*. |
| GenerateDocumentation | (somente Visual Basic) Um parâmetro booliano que indica se a documentação é gerada pelo build. Se ele for `true`, o build gerará informações sobre a documentação e as colocará em um arquivo *.xml* junto com o nome do arquivo executável ou a biblioteca criada pela tarefa de build. |
| IntermediateOutputPath | O caminho de saída completo intermediário conforme derivado de `BaseIntermediateOutputPath`, se nenhum caminho for especificado. Por exemplo, *\obj\debug\\*. |
| KeyContainerName | O nome do contêiner de chave de nome forte. |
| KeyOriginatorFile | O nome do arquivo de chave de nome forte. |
| MSBuildProjectExtensionsPath | Especifica o caminho em que se encontram as extensões de projeto. Por padrão, isso leva o mesmo valor que `BaseIntermediateOutputPath`. |
| ModuleAssemblyName | O nome do assembly ao qual o módulo compilado será incorporado. A propriedade é equivalente à opção do compilador `/moduleassemblyname`. |
| NoLogo | Um valor booliano que indica se você deseja que o logotipo do compilador seja desligado. Essa propriedade é equivalente à opção do compilador `/nologo`. |
| NoStdLib | Um valor booliano que indica se é necessário evitar a referência à biblioteca padrão (*mscorlib.dll*). O valor padrão é `false`. |
| NoVBRuntimeReference | Um valor booliano que indica se o tempo de execução [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] (*Microsoft.VisualBasic.dll*) deve ser incluído como uma referência no projeto. |
| NoWin32Manifest | Um valor booliano que indica se as informações do manifesto do UAC (Controle de Conta de Usuário) serão inseridas no executável do aplicativo. Aplica-se somente a projetos do Visual Studio que direcionam [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)]. Em projetos implantados usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] e COM sem registro, esse elemento será ignorado. `False` (o valor padrão) especifica se as informações do manifesto do UAC (Controle de Conta de Usuário) serão inseridas no executável do aplicativo. `True` especifica se as informações de manifesto de UAC não serão inseridas.<br /><br /> Essa propriedade é aplicável somente a projetos [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que direcionam [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)]. Em projetos implantados usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] e COM sem registro, essa propriedade será ignorada.<br /><br /> Você deverá adicionar NoWin32Manifest somente se não quiser que [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] insira qualquer manifesto no executável do aplicativo. Esse processo é chamado *virtualização*. Para usar a virtualização, defina `<ApplicationManifest>` em conjunto com `<NoWin32Manifest>` da seguinte maneira:<br /><br /> -   Para projetos [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], remova o nó `<ApplicationManifest>`. (Em projetos [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], `<NoWin32Manifest>` é ignorado quando um nó `<ApplicationManifest>` existe.)<br />-   Para projetos [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)], defina `<ApplicationManifest>` como `False` e `<NoWin32Manifest>` como `True`. (Em projetos [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)], `<ApplicationManifest>` substitui `<NoWin32Manifest>`.)<br /> Essa propriedade é equivalente à opção `/nowin32manifest` do compilador *vbc.exe*. |
| Otimizar | Um valor booliano que, quando definido como `true`, permite otimizações do compilador. Essa propriedade é equivalente à opção do compilador `/optimize`. |
| OptionCompare | Especifica como são feitas comparações de cadeia de caracteres. Os valores válidos são "binary" ou "text". Essa propriedade é equivalente à opção `/optioncompare` do compilador *vbc.exe*. |
| OptionExplicit | Um valor booliano que, quando definido como `true`, exige a declaração explícita de variáveis no código-fonte. Essa propriedade é equivalente à opção do compilador `/optionexplicit`. |
| OptionInfer | Um valor booliano que, quando definido como `true`, habilita a inferência de tipos de variáveis. Essa propriedade é equivalente à opção do compilador `/optioninfer`. |
| OptionStrict | Um valor booliano que, quando definido como `true`, faz com que a tarefa de build para impor a semântica de tipo estrito restrinja conversões de tipo implícito. Essa propriedade é equivalente à opção `/optionstrict` do compilador *vbc.exe*. |
| OutputPath | Especifica o caminho para o diretório de saída, relativo ao diretório do projeto, por exemplo, *bin\Debug*. |
| OutputType | Especifica o formato do arquivo de saída. Esse parâmetro pode ter um dos seguintes valores:<br /><br /> -   Library. Cria uma biblioteca de códigos. (Valor padrão.)<br />-   Exe. Crie um aplicativo de console.<br />-   Module. Cria um módulo.<br />-   Winexe. Cria um programa baseado em Windows.<br /><br /> Essa propriedade é equivalente à opção `/target` do compilador *vbc.exe*. |
| OverwriteReadOnlyFiles | Um valor booliano que indica se você deseja habilitar o build para substituir arquivos somente leitura ou disparar um erro. |
| PdbFile | O nome do arquivo *.pdb* que está sendo emitido. Essa propriedade é equivalente à opção `/pdb` do compilador *csc.exe*. |
| Plataforma | O sistema operacional que você está compilando. Os valores válidos são "Any CPU", "x86" e "x64". |
| ProduceReferenceAssembly | Um valor booliano que, quando definido como `true`, permite a produção de [assemblies de referência](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) para o assembly atual. `Deterministic` deve ser `true` ao usar esse recurso. Essa propriedade corresponde à opção `/refout` dos compiladores *vbc.exe* e *csc.exe*. |
| RemoveIntegerChecks | Um valor booliano que indica se é necessário desabilitar a verificação de erro de estouro de inteiro. O valor padrão é `false`. Essa propriedade é equivalente à opção `/removeintchecks` do compilador *vbc.exe*. |
| SGenUseProxyTypes | Um valor booliano que indica se os tipos de proxy devem ser gerados por *SGen.exe*.<br /><br /> O destino SGen usa essa propriedade para definir o sinalizador UseProxyTypes. Essa propriedade assume true como padrão e não há nenhuma interface do usuário para alterar isso. Para gerar o assembly de serialização para tipos não serviço Web, adicione essa propriedade ao arquivo de projeto e defina-a como falso antes de importar o *Microsoft.Common.Targets* ou o *C#/VB.targets*. |
| SGenToolPath | Um caminho de ferramenta opcional que indica o local no qual obter *SGen.exe* quando a versão atual de *SGen.exe* é substituída. |
| StartupObject | Especifica a classe ou o módulo que contém o método Main ou procedimento Sub Main. Essa propriedade é equivalente à opção do compilador `/main`. |
| ProcessorArchitecture | A arquitetura do processador que é usada quando as referências de assembly são resolvidas. Os valores válidos são "msil," "x86," "amd64" ou "ia64". |
| RootNamespace | O namespace raiz para usar ao nomear um recurso inserido. Este namespace é parte do nome do manifesto do recurso inserido. |
| Satellite_AlgorithmId | A ID do algoritmo de hash do *AL.exe* a ser usada quando os assemblies satélites forem criados. |
| Satellite_BaseAddress | O endereço básico para usar quando assemblies satélites específicos da cultura forem criados usando o destino `CreateSatelliteAssemblies`. |
| Satellite_CompanyName | O nome da empresa a ser passado para o *AL.exe* durante a geração de assembly satélite. |
| Satellite_Configuration | O nome da configuração a ser passado para o *AL.exe* durante a geração de assembly satélite. |
| Satellite_Description | O texto de descrição a ser passado para o *AL.exe* durante a geração de assembly satélite. |
| Satellite_EvidenceFile | Insere o arquivo especificado no assembly satélite que tem o nome do recurso "Security.Evidence". |
| Satellite_FileVersion | Especifica uma cadeia de caracteres para o campo Versão do Arquivo no assembly satélite. |
| Satellite_Flags | Especifica um valor para o campo Sinalizadores no assembly satélite. |
| Satellite_GenerateFullPaths | Faz com que a tarefa de build use o caminho absoluto para todos os arquivos reportados em uma mensagem de erro. |
| Satellite_LinkResource | Vincula os arquivos de recurso especificados a um assembly satélite. |
| Satellite_MainEntryPoint | Especifica o nome totalmente qualificado (ou seja, class.method) do método a ser usado como um ponto de entrada durante a conversão de um módulo em um arquivo executável durante a geração do assembly satélite. |
| Satellite_ProductName | Especifica uma cadeia de caracteres para o campo Produto no assembly satélite. |
| Satellite_ProductVersion | Especifica uma cadeia de caracteres para o campo ProductVersion no assembly satélite. |
| Satellite_TargetType | Especifica o formato de arquivo do arquivo de saída do assembly satélite como "library," "exe," ou "win". O valor padrão é "library". |
| Satellite_Title | Especifica uma cadeia de caracteres para o campo Título no assembly satélite. |
| Satellite_Trademark | Especifica uma cadeia de caracteres para o campo Marca registrada no assembly satélite. |
| Satellite_Version | Especifica as informações de versão do assembly satélite. |
| Satellite_Win32Icon | Insere um arquivo de ícone *.ico* no assembly satélite. |
| Satellite_Win32Resource | Insere um recurso do Win32 (arquivo *.res*) no assembly satélite. |
| SubsystemVersion | Especifica a versão mínima do subsistema que o arquivo executável gerado pode usar. Essa propriedade é equivalente à opção do compilador `/subsystemversion`. Para obter informações sobre o valor padrão dessa propriedade, confira [/subsystemversion (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/subsystemversion) ou [/subsystemversion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/subsystemversion-compiler-option). |
| TargetCompactFramework | A versão do .NET Compact Framework que é necessária para executar o aplicativo que você está compilando. Especificar isso permite fazer referência a determinados assemblies de estrutura que pode não ser possível fazer referência de outra forma. |
| TargetFrameworkVersion | A versão do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] que é necessária para executar o aplicativo que você está compilando. Especificar isso permite fazer referência a determinados assemblies de estrutura que pode não ser possível fazer referência de outra forma. |
| TreatWarningsAsErrors | Um parâmetro booliano que, se `true`, faz com que todos os avisos sejam tratados como erros. Esse parâmetro é equivalente à opção do compilador `/nowarn`. |
| UseHostCompilerIfAvailable | Um parâmetro booliano que, se `true`, faz com que a tarefa de build use o objeto do compilador em processo, se ele estiver disponível. Este parâmetro será usado apenas por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| Utf8Output | Um parâmetro booliano que, se `true`, registra a saída do compilador usando a codificação UTF-8. Esse parâmetro é equivalente à opção do compilador `/utf8Output`. |
| VbcToolPath | Um caminho opcional que indica outro local para *vbc.exe* quando a versão atual de *vbc.exe* é substituída. |
| VbcVerbosity | Especifica o nível de detalhes da saída do compilador [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]. Os valores válidos são "Quiet," "Normal" (o valor padrão) ou "Verbose". |
| VisualStudioVersion | Especifica a versão do Visual Studio sob a qual este projeto deve ser considerado para estar em execução. Se esta propriedade não for especificada, o MSBuild a definirá como um valor padrão razoável.<br /><br /> Essa propriedade é usada em vários tipos de projeto para especificar o conjunto de destinos que são usados para o build. Se `ToolsVersion` é definido como 4.0 ou superior para um projeto, `VisualStudioVersion` é usado para especificar o subconjunto de ferramentas que será usado. Para obter mais informações, consulte [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md). |
| WarningsAsErrors | Especifica uma lista de avisos a serem tratados como erros. Esse parâmetro é equivalente à opção do compilador `/warnaserror`. |
| WarningsNotAsErrors | Especifica uma lista de avisos que não são tratados como erros. Esse parâmetro é equivalente à opção do compilador `/warnaserror`. |
| Win32Manifest | O nome do arquivo de manifesto deve ser inserido no assembly final. Esse parâmetro é equivalente à opção do compilador `/win32Manifest`. |
| Win32Resource | O nome do arquivo do recurso do Win32 a ser inserido no assembly final. Esse parâmetro é equivalente à opção do compilador `/win32resource`. |
  
## <a name="see-also"></a>Consulte também  
 [Itens de projeto comuns do MSBuild](../msbuild/common-msbuild-project-items.md)
