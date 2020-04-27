---
title: Tarefa Vbc | Microsoft Docs
ms.date: 04/12/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Vbc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Vbc task [MSBuild]
- MSBuild, Vbc task
ms.assetid: 595278b1-2782-4577-b1ba-b4b5ab5625a3
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30f1a45c384495ccd02c624ea42f91a4379226df
ms.sourcegitcommit: 93859158465eab3423a0c0435f06490f0a456a57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82167443"
---
# <a name="vbc-task"></a>tarefa Vbc

Encapsula o *Vbc. exe*, que produz executáveis (*. exe*), bibliotecas de vínculo dinâmico (*. dll*) ou módulos de código (*. netmodule*). Para obter mais informações sobre o *Vbc. exe*, consulte [Visual Basic compilador de linha de comando](/dotnet/visual-basic/reference/command-line-compiler/index).

## <a name="parameters"></a>Parâmetros

 A tabela a seguir descreve os parâmetros da tarefa `Vbc`.

| Parâmetro | Descrição |
|------------------------------| - |
| `AdditionalLibPaths` | Parâmetro `String[]` opcional.<br /><br /> Especifica as pastas adicionais nas quais procurar por assemblies especificados no atributo References. |
| `AddModules` | Parâmetro `String[]` opcional.<br /><br /> Faz com que o compilador verifique todos os tipos de informações de arquivos especificados disponíveis para o projeto que você está compilando. Esse parâmetro corresponde à opção [-addmodule](/dotnet/visual-basic/reference/command-line-compiler/addmodule) do compilador *Vbc. exe* . |
| `BaseAddress` | Parâmetro `String` opcional.<br /><br /> Especifica o endereço básico do DLL. Esse parâmetro corresponde à opção [-BaseAddress](/dotnet/visual-basic/reference/command-line-compiler/baseaddress) do compilador *Vbc. exe* . |
| `CodePage` | Parâmetro `Int32` opcional.<br /><br /> Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Esse parâmetro corresponde à opção [-CodePage](/dotnet/visual-basic/reference/command-line-compiler/codepage) do compilador *Vbc. exe* . |
| `DebugType` | Parâmetro `String[]` opcional.<br /><br /> Faz com que o compilador gere informações de depuração. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> O valor padrão é `full`, que permite anexar um depurador ao programa em execução. Um valor de `pdbonly` permite a depuração de código-fonte quando o programa é iniciado no depurador, mas exibe o código de linguagem assembly somente quando o programa em execução está anexado ao depurador. Para obter mais informações, consulte [-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug). |
| `DefineConstants` | Parâmetro `String[]` opcional.<br /><br /> Define as constantes de compilador condicional. Os pares de símbolo/valor são separados por ponto e vírgula e são especificados usando a sintaxe a seguir:<br /><br /> *symbol1* `=` *value1* `;` *symbol2* `=` *value2*<br /><br /> Esse parâmetro corresponde à opção [-define](/dotnet/visual-basic/reference/command-line-compiler/define) do compilador *Vbc. exe* . |
| `DelaySign` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa colocará a chave pública no assembly. Se `false`, a tarefa assina totalmente o assembly. O valor padrão é `false`. Esse parâmetro não tem nenhum efeito a menos que usado com o parâmetro `KeyFile` ou `KeyContainer`. Esse parâmetro corresponde à opção [-delaysign](/dotnet/visual-basic/reference/command-line-compiler/delaysign) do compilador *Vbc. exe* . |
| `Deterministic` | Parâmetro `Boolean` opcional.<br/><br/> Se ele for `true`, fará com que o compilador gere um assembly cujo conteúdo binário é idêntico entre compilações caso as entradas sejam idênticas.<br/><br/>Para obter mais informações, confira [-deterministic](/dotnet/visual-basic/reference/command-line-compiler/deterministic). |
| `DisabledWarnings` | Parâmetro `String` opcional.<br /><br /> Suprime os avisos especificados. Você só precisa especificar a parte numérica do identificador de aviso. Vários avisos são separados por ponto e vírgula. Esse parâmetro corresponde à opção [-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) do compilador *Vbc. exe* . |
| `DocumentationFile` | Parâmetro `String` opcional.<br /><br /> Processa os comentários de documentação para o arquivo XML especificado. Esse parâmetro substitui o atributo `GenerateDocumentation`. Para obter mais informações, consulte [-Doc](/dotnet/visual-basic/reference/command-line-compiler/doc). |
| `EmitDebugInformation` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa gerará informações de depuração e a colocará em um arquivo *. pdb* . Para obter mais informações, consulte [-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug). |
| `ErrorReport` | Parâmetro `String` opcional.<br /><br /> Especifica como a tarefa deve relatar erros do compilador interno. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> Se `prompt` estiver especificado e ocorrer um erro interno do compilador, será exibida uma opção ao usuário para enviar os dados de erros à Microsoft.<br /><br /> Se `send` for especificado e ocorrer um erro interno do compilador, a tarefa enviará os dados de erros à Microsoft.<br /><br /> O valor padrão é `none`, que reporta os erros somente na saída de texto.<br /><br /> Esse parâmetro corresponde à opção [-errorreport](/dotnet/visual-basic/reference/command-line-compiler/errorreport) do compilador *Vbc. exe* . |
| `FileAlignment` | Parâmetro `Int32` opcional.<br /><br /> Especifica, em bytes, onde alinhar as seções do arquivo de saída. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> Esse parâmetro corresponde à opção [-filealign](/dotnet/visual-basic/reference/command-line-compiler/filealign) do compilador *Vbc. exe* . |
| `GenerateDocumentation` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, serão geradas informações sobre a documentação, que serão colocadas em um arquivo XML com o nome do arquivo executável ou da biblioteca que a tarefa está criando. Para obter mais informações, consulte [-Doc](/dotnet/visual-basic/reference/command-line-compiler/doc). |
| `Imports` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Importa namespaces de coleções do item especificado. Esse parâmetro corresponde à opção [-Imports](/dotnet/visual-basic/reference/command-line-compiler/imports) do compilador *Vbc. exe* . |
| `KeyContainer` | Parâmetro `String` opcional.<br /><br /> Especifica o nome do contêiner da chave de criptografia. Esse parâmetro corresponde à opção [-keycontainer](/dotnet/visual-basic/reference/command-line-compiler/keycontainer) do compilador *vbc.exe*. |
| `KeyFile` | Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo que contém a chave de criptografia. Para obter mais informações, consulte [-keyfile](/dotnet/visual-basic/reference/command-line-compiler/keyfile). |
| `LangVersion` | Parâmetro <xref:System.String?displayProperty=fullName> opcional.<br /><br /> Especifica a [versão da linguagem](/dotnet/visual-basic/language-reference/configure-language-version), como "15.5". |
| `LinkResources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Cria um link para um recurso do .NET Framework no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída. Esse parâmetro corresponde à opção [-linkresource](/dotnet/visual-basic/reference/command-line-compiler/linkresource) do compilador *Vbc. exe* . |
| `MainEntryPoint` | Parâmetro `String` opcional.<br /><br /> Especifica a classe ou o módulo que contém o procedimento `Sub Main`. Esse parâmetro corresponde à opção [-main](/dotnet/visual-basic/reference/command-line-compiler/main) do compilador *vbc.exe*. |
| `ModuleAssemblyName` | Parâmetro `String` opcional.<br /><br /> Especifica o assembly do qual esse módulo faz parte. |
| `NoConfig` | Parâmetro `Boolean` opcional.<br /><br /> Especifica que o compilador não deve usar o arquivo *Vbc. rsp* . Esse parâmetro corresponde ao parâmetro [-noconfig](/dotnet/visual-basic/reference/command-line-compiler/noconfig) do compilador *Vbc. exe* . |
| `NoLogo` | Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, suprimirá a exibição de informações da barra de notificação do compilador. Esse parâmetro corresponde à opção [-nologomarca](/dotnet/visual-basic/reference/command-line-compiler/nologo) do compilador *Vbc. exe* . |
| `NoStandardLib` | Parâmetro `Boolean` opcional.<br /><br /> Faz com que o compilador não referencie as bibliotecas padrão. Esse parâmetro corresponde à opção [-nostdlib](/dotnet/visual-basic/reference/command-line-compiler/nostdlib) do compilador *Vbc. exe* . |
| `NoVBRuntimeReference` | Parâmetro `Boolean` opcional.<br /><br /> Somente para uso interno. Se for true, impedirá a referência automática para *Microsoft. VisualBasic. dll*. |
| `NoWarnings` | Parâmetro `Boolean` opcional.<br /><br /> Se ele for `true`, a tarefa suprimirá todos os avisos. Para obter mais informações, consulte [-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn). |
| `Optimize` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, habilita as otimizações do compilador. Esse parâmetro corresponde à opção [-Optimize](/dotnet/visual-basic/reference/command-line-compiler/optimize) do compilador *Vbc. exe* . |
| `OptionCompare` | Parâmetro `String` opcional.<br /><br /> Especifica como são feitas comparações de cadeia de caracteres. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `binary`<br />-   `text`<br /><br /> O valor `binary` especifica que a tarefa usa comparações de cadeia de caracteres binária. O valor `text` especifica que a tarefa usa comparações de cadeia de caracteres de texto. O valor padrão desse parâmetro é `binary`. Esse parâmetro corresponde à opção [-optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare) do compilador *Vbc. exe* . |
| `OptionExplicit` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a declaração explícita de variáveis é necessária. Esse parâmetro corresponde à opção [-optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit) do compilador *Vbc. exe* . |
| `OptionInfer` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, permite a inferência de tipos de variáveis. |
| `OptionStrict` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa impõe semântica de tipo estrito para restringir conversões de tipo implícito. Esse parâmetro corresponde à opção [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) do compilador *Vbc. exe* . |
| `OptionStrictType` | Parâmetro `String` opcional.<br /><br /> Especifica qual semântica de tipo estrito gera um aviso. Atualmente, há suporte para apenas "custom". Esse parâmetro corresponde à opção [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) do compilador *Vbc. exe* . |
| `OutputAssembly` | Parâmetro de saída `String` opcional.<br /><br /> Especifica o nome do arquivo de saída. Esse parâmetro corresponde à opção [-out](/dotnet/visual-basic/reference/command-line-compiler/out) do compilador *Vbc. exe* . |
| `Platform` | Parâmetro `String` opcional.<br /><br /> Especifica a plataforma do processador a ser direcionada pelo arquivo de saída. Esse parâmetro pode ter um valor igual a `x86`, `x64``Itanium` ou `anycpu`. O padrão é `anycpu`. Esse parâmetro corresponde à opção [-platform](/dotnet/visual-basic/reference/command-line-compiler/platform) do compilador *vbc.exe*. |
| `References` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Faz com que a tarefa importe informações de tipo público dos itens especificados para o projeto atual. Esse parâmetro corresponde à opção [-Reference](/dotnet/visual-basic/reference/command-line-compiler/reference) do compilador *Vbc. exe* . |
| `RemoveIntegerChecks` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, desabilita a verificação de erro de estouro de inteiro. O valor padrão é `false`. Esse parâmetro corresponde à opção [-removeintchecks](/dotnet/visual-basic/reference/command-line-compiler/removeintchecks) do compilador *vbc.exe*. |
| `Resources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Insere um recurso do .NET Framework no arquivo de saída. Esse parâmetro corresponde à opção [-resource](/dotnet/visual-basic/reference/command-line-compiler/resource) do compilador *vbc.exe*. |
| `ResponseFiles` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica o arquivo de resposta que contém comandos para essa tarefa. Esse parâmetro corresponde à opção [@ (especificar arquivo de resposta)](/dotnet/visual-basic/reference/command-line-compiler/specify-response-file) do compilador *Vbc. exe* . |
| `RootNamespace` | Parâmetro `String` opcional.<br /><br /> Especifica o namespace raiz para todas as declarações de tipo. Esse parâmetro corresponde à opção [-RootNamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace) do compilador *Vbc. exe* . |
| `SdkPath` | Parâmetro `String` opcional.<br /><br /> Especifica o local de *mscorlib. dll* e *Microsoft. VisualBasic. dll*. Esse parâmetro corresponde à opção [-sdkpath](/dotnet/visual-basic/reference/command-line-compiler/sdkpath) do compilador *vbc.exe*. |
| `Sources` | Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica um ou mais arquivos de origem do Visual Basic. |
| `TargetCompactFramework` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa se destina ao .NET Compact Framework. Essa opção corresponde à opção [-netcf](/dotnet/visual-basic/reference/command-line-compiler/netcf) do compilador *Vbc. exe* . |
| `TargetType` | Parâmetro `String` opcional.<br /><br /> Especifica o formato do arquivo de saída. Esse parâmetro pode ter um valor igual a `library`, que cria uma biblioteca de códigos, `exe`, que cria um aplicativo de console, `module`, que cria um módulo ou `winexe`, que cria um programa do Windows. O padrão é `library`. Esse parâmetro corresponde à opção [-target](/dotnet/visual-basic/reference/command-line-compiler/target) do compilador *Vbc. exe* . |
| `Timeout` | Parâmetro `Int32` opcional.<br /><br /> Especifica a quantidade de tempo em milissegundos após o qual o executável da tarefa é encerrado. O valor padrão é `Int.MaxValue`, indicando que não há período de tempo limite. |
| `ToolPath` | Parâmetro `String` opcional.<br /><br /> Especifica o local de onde a tarefa carregará o arquivo executável subjacente (*Vbc. exe*). Se esse parâmetro não for especificado, a tarefa usará o caminho de instalação do SDK correspondente à versão do Framework que está executando o MSBuild. |
| `TreatWarningsAsErrors` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, todos os avisos são tratados como erros. Para obter mais informações, consulte [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror). |
| `UseHostCompilerIfAvailable` | Parâmetro `Boolean` opcional.<br /><br /> Instrui a tarefa a usar o objeto do compilador em processo, se disponível. Usado somente pelo Visual Studio. |
| `Utf8Output` | Parâmetro `Boolean` opcional.<br /><br /> Registra a saída do compilador usando a codificação UTF-8. Esse parâmetro corresponde à opção [-utf8output](/dotnet/visual-basic/reference/command-line-compiler/utf8output) do compilador *Vbc. exe* . |
| `Verbosity` | Parâmetro `String` opcional.<br /><br /> Especifica o nível de detalhes da saída do compilador. Os detalhes podem ser `Quiet`, `Normal` (o padrão) ou `Verbose`. |
| `WarningsAsErrors` | Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos a serem tratados como erros. Para obter mais informações, consulte [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror).<br /><br /> Esse parâmetro substitui o parâmetro `TreatWarningsAsErrors`. |
| `WarningsNotAsErrors` | Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos que não são tratados como erros. Para obter mais informações, consulte [-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror).<br /><br /> Esse parâmetro será útil apenas se o parâmetro `TreatWarningsAsErrors` for definido como `true`. |
| `Win32Icon` | Parâmetro `String` opcional.<br /><br /> Insere um arquivo *. ico* no assembly, que dá ao arquivo de saída a aparência desejada no **Explorador de arquivos**. Esse parâmetro corresponde à opção [-win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon) do compilador *Vbc. exe* . |
| `Win32Resources` | Parâmetro `String` opcional.<br /><br /> Insere um arquivo de recurso do Win32 (*. res*) no arquivo de saída. Esse parâmetro corresponde à opção [-Win32Resource](/dotnet/visual-basic/reference/command-line-compiler/win32resource) do compilador *Vbc. exe* . |

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="example"></a>Exemplo

 O exemplo a seguir compila um projeto do Visual Basic.

```xml
<VBC
   Sources="@(sources)"
   Resources="strings.resources"
   Optimize="true"
   OutputAssembly="out.exe"/>
```

## <a name="see-also"></a>Confira também

- [Compilador de linha de comando Visual Basic](/dotnet/visual-basic/reference/command-line-compiler/index)
- [Tarefas](../msbuild/msbuild-tasks.md)
- [Referência de tarefa](../msbuild/msbuild-task-reference.md)
