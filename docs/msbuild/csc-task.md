---
title: Tarefa Csc | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Csc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Csc task [MSBuild]
- MSBuild, Csc task
ms.assetid: d8c19b36-f5ca-484b-afa6-8ff3b90e103a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bd360a34c70d3208211b861dae064bd4c5a01595
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832348"
---
# <a name="csc-task"></a>tarefa Csc
Encapsula *csc.exe* e produz executáveis (arquivos *.exe*), bibliotecas de vínculo dinâmico (arquivos *.dll*) ou módulos de código (arquivos *.netmodule*). Para obter mais informações sobre o *csc.exe*, confira [Opções do compilador C#](/dotnet/csharp/language-reference/compiler-options/index).  

## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `Csc`.  


| Parâmetro | Descrição |
|------------------------------| - |
| `AdditionalLibPaths` | Parâmetro `String[]` opcional.<br /><br /> Especifica diretórios adicionais para pesquisar referências. Para obter mais informações, confira [-lib (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/lib-compiler-option). |
| `AddModules` | Parâmetro `String` opcional.<br /><br /> Especifica um ou mais módulos a fazerem parte do assembly. Para obter mais informações, confira [-addmodule (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/addmodule-compiler-option). |
| `AllowUnsafeBlocks` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, compilará o código que usa a palavra-chave [unsafe](/dotnet/csharp/language-reference/keywords/unsafe). Para obter mais informações, confira [-unsafe (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/unsafe-compiler-option). |
| `ApplicationConfiguration` | Parâmetro `String` opcional.<br /><br /> Especifica um arquivo de configuração de aplicativo que contém configurações de associação de assembly. |
| `BaseAddress` | Parâmetro `String` opcional.<br /><br /> Especifica o endereço básico preferencial no qual uma DLL será carregada. O endereço básico padrão para uma DLL é definido pelo Common Language Runtime de [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. Para obter mais informações, confira [-baseaddress (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option). |
| `CheckForOverflowUnderflow` | Parâmetro `Boolean` opcional.<br /><br /> Especifica se o aritmético inteiro que estoura os limites do tipo de dados causa uma exceção em tempo de execução. Para obter mais informações, confira [-checked (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option). |
| `CodePage` | Parâmetro `Int32` opcional.<br /><br /> Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Para obter mais informações, confira [-codepage (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/codepage-compiler-option). |
| `DebugType` | Parâmetro `String` opcional.<br /><br /> Especifica o tipo de depuração. `DebugType` pode ser `full` ou `pdbonly`. O padrão é `full`, o que permite que um depurador seja anexado a um programa em execução. Especificar `pdbonly` habilita a depuração de código-fonte quando o programa é iniciado no depurador, mas apenas exibe o assembler quando o programa em execução está anexado ao depurador.<br /><br /> Esse parâmetro substitui o parâmetro `EmitDebugInformation`.<br /><br /> Para obter mais informações, confira [-debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option). |
| `DefineConstants` | Parâmetro `String` opcional.<br /><br /> Define símbolos do pré-processador. Para obter mais informações, confira [-define (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/define-compiler-option). |
| `DelaySign` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, especificará que você deseja um assembly totalmente com sinal. Se for `false`, especificará que você apenas deseja colocar a chave pública no assembly.<br /><br /> Esse parâmetro não terá nenhum efeito a menos que seja usado com o parâmetro `KeyFile` ou `KeyContainer`.<br /><br /> Para obter mais informações, confira [-delaysign (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/delaysign-compiler-option). |
| `Deterministic` | Parâmetro `Boolean` opcional.<br/><br/> Se ele for `true`, fará com que o compilador gere um assembly cujo conteúdo binário é idêntico entre compilações caso as entradas sejam idênticas.<br/><br/>Para obter mais informações, confira [-deterministic (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option). |
| `DisabledWarnings` | Parâmetro `String` opcional.<br /><br /> Especifica a lista de avisos a ser desabilitada. Para obter mais informações, confira [-nowarn (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nowarn-compiler-option). |
| `DocumentationFile` | Parâmetro `String` opcional.<br /><br /> Processa comentários de documentação para um arquivo XML. Para obter mais informações, confira [-doc (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/doc-compiler-option). |
| `EmitDebugInformation` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, a tarefa gerará informações de depuração e as colocará em um arquivo de banco de dados do programa (.pdb). Se for `false`, a tarefa não emitirá nenhuma informação de depuração. O padrão é `false`. Para obter mais informações, confira [-debug (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option). |
| `ErrorReport` | Parâmetro `String` opcional.<br /><br /> Fornece uma maneira conveniente de relatar um erro interno do C# à Microsoft. Esse parâmetro pode ter um valor igual a `prompt`, `send` ou `none`. Se o parâmetro for definido como `prompt`, você receberá um prompt quando ocorrer um erro interno do compilador. O prompt permite enviar um relatório de bugs eletronicamente à Microsoft. Se o parâmetro for definido como `send`, um relatório de bugs será enviado automaticamente. Se o parâmetro for definido como `none`, o erro será relatado apenas na saída de texto do compilador. O padrão é `none`. Para obter mais informações, confira [-errorreport (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option). |
| `FileAlignment` | Parâmetro `Int32` opcional.<br /><br /> Especifica o tamanho das seções no arquivo de saída. Para obter mais informações, confira [-filealign (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option). |
| `GenerateFullPaths` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, especificará o caminho absoluto para o arquivo na saída do compilador. Se for `false`, especificará o nome do arquivo. O padrão é `false`. Para obter mais informações, confira [-fullpaths (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/fullpaths-compiler-option). |
| `KeyContainer` | Parâmetro `String` opcional.<br /><br /> Especifica o nome do contêiner da chave de criptografia. Para obter mais informações, confira [-keycontainer (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/keycontainer-compiler-option). |
| `KeyFile` | Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo que contém a chave de criptografia. Para obter mais informações, confira [-keyfile (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/keyfile-compiler-option). |
| `LangVersion` | Parâmetro `String` opcional.<br /><br /> Especifica a versão da linguagem a ser usada. Para obter mais informações, confira [-langversion (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option). |
| `LinkResources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Cria um link para um recurso [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída.<br /><br /> Os itens passados para esse parâmetro podem ter entradas de metadados opcionais chamadas `LogicalName` e `Access`. `LogicalName` corresponde ao parâmetro `identifier` da opção `/linkresource` e `Access` corresponde ao parâmetro `accessibility-modifier`. Para obter mais informações, confira [-linkresource (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/linkresource-compiler-option). |
| `MainEntryPoint` | Parâmetro `String` opcional.<br /><br /> Especifica o local do método `Main`. Para obter mais informações, confira [-main (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/main-compiler-option). |
| `ModuleAssemblyName` | Parâmetro `String` opcional.<br /><br /> Especifica o nome do assembly do qual esse módulo fará parte. |
| `NoConfig` | Parâmetro `Boolean` opcional.<br /><br /> Se ele for `true`, instruirá o compilador a não compilar com o arquivo *csc.rsp*. Para obter mais informações, confira [-noconfig (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/noconfig-compiler-option). |
| `NoLogo` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, suprimirá a exibição de informações da barra de notificação do compilador. Para obter mais informações, confira [-nologo (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nologo-compiler-option). |
| `NoStandardLib` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, impedirá a importação de *mscorlib.dll*, que define todo o namespace System. Use esse parâmetro se desejar definir ou criar seus próprios objetos e namespace System. Para obter mais informações, confira [-nostdlib (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option). |
| `NoWin32Manifest` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, não inclua o manifesto Win32 padrão. |
| `Optimize` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, habilitará as otimizações. Se for `false`, desabilitará as otimizações. Para obter mais informações, confira [-optimize (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/optimize-compiler-option). |
| `OutputAssembly` | Parâmetro de saída `String` opcional.<br /><br /> Especifica o nome do arquivo de saída. Para obter mais informações, confira [-out (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/out-compiler-option). |
| `OutputRefAssembly` | Parâmetro `String` opcional.<br /><br /> Especifica o nome do arquivo do assembly de referência de saída. Para obter mais informações, confira [-refout (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/refout-compiler-option). |
| `PdbFile` | Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo de informações de depuração. O nome padrão é o nome do arquivo de saída com uma extensão *.pdb*. |
| `Platform` | Parâmetro `String` opcional.<br /><br /> Especifica a plataforma do processador a ser direcionada pelo arquivo de saída. Esse parâmetro pode ter um valor igual a `x86`, `x64` ou `anycpu`. O padrão é `anycpu`. Para obter mais informações, confira [-platform (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option). |
| `References` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Faz com que a tarefa importe informações de tipo público dos itens especificados para o projeto atual. Para obter mais informações, confira [-reference (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/reference-compiler-option).<br /><br /> Você pode especificar um alias de referência [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] em um arquivo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] adicionando os metadados `Aliases` ao item original da “Referência”. Por exemplo, para definir o alias "LS1" na seguinte linha de comando Csc:<br /><br /> `CSC /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> você usará:<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>` |
| `Resources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Insere um recurso [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] no arquivo de saída.<br /><br /> Os itens passados para esse parâmetro podem ter entradas de metadados opcionais chamadas `LogicalName` e `Access`. `LogicalName` corresponde ao parâmetro `identifier` da opção `/resource` e `Access` corresponde ao parâmetro `accessibility-modifier`. Para obter mais informações, confira [-resource (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/resource-compiler-option). |
| `ResponseFiles` | Parâmetro `String` opcional.<br /><br /> Especifica o arquivo de resposta que contém comandos para essa tarefa. Para obter mais informações, confira [@ (Especificar arquivo de resposta)](/dotnet/csharp/language-reference/compiler-options/response-file-compiler-option). |
| `Sources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica um ou mais arquivos de origem [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]. |
| `TargetType` | Parâmetro `String` opcional.<br /><br /> Especifica o formato do arquivo de saída. Esse parâmetro pode ter um valor igual a `library`, que cria uma biblioteca de códigos, `exe`, que cria um aplicativo de console, `module`, que cria um módulo ou `winexe`, que cria um programa do Windows. O valor padrão é `library`. Para obter mais informações, confira [-target (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/target-compiler-option). |
| `TreatWarningsAsErrors` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, tratará todos os avisos como erros. Para obter mais informações, confira [-warnaserror (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option). |
| `UseHostCompilerIfAvailable` | Parâmetro `Boolean` opcional.<br /><br /> Instrui a tarefa a usar o objeto do compilador em processo, se disponível. Usado somente por [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| `Utf8Output` | Parâmetro `Boolean` opcional.<br /><br /> Registra a saída do compilador usando a codificação UTF-8. Para obter mais informações, confira [-utf8output (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/utf8output-compiler-option). |
| `WarningLevel` | Parâmetro `Int32` opcional.<br /><br /> Especifica o nível de aviso a ser exibido pelo compilador. Para obter mais informações, confira [-warn (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warn-compiler-option). |
| `WarningsAsErrors` | Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos a serem tratados como erros. Para obter mais informações, confira [-warnaserror (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option).<br /><br /> Esse parâmetro substitui o parâmetro `TreatWarningsAsErrors`. |
| `WarningsNotAsErrors` | Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos que não são tratados como erros. Para obter mais informações, confira [-warnaserror (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option).<br /><br /> Esse parâmetro será útil apenas se o parâmetro `TreatWarningsAsErrors` for definido como `true`. |
| `Win32Icon` | Parâmetro `String` opcional.<br /><br /> Insere um arquivo *.ico* no assembly, que fornece ao arquivo de saída a aparência desejada no **Explorador de Arquivos**. Para obter mais informações, confira [-win32icon (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option). |
| `Win32Manifest` | Parâmetro `String` opcional.<br /><br /> Especifica o manifesto Win32 a ser incluído. |
| `Win32Resource` | Parâmetro `String` opcional.<br /><br /> Insere um arquivo (*.res*) do recurso do Win32 no arquivo de saída. Para obter mais informações, confira [-win32res (opções do compilador C#)](/dotnet/csharp/language-reference/compiler-options/win32res-compiler-option). |

## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe `Microsoft.Build.Tasks.ManagedCompiler`, que herda da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  

## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `Csc` para compilar um executável com base nos arquivos de origem da coleção de itens `Compile`.  

```xml  
<CSC  
    Sources="@(Compile)"  
    OutputAssembly="$(AppName).exe"  
    EmitDebugInformation="true" />  
```  

## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)
