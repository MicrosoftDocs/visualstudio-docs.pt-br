---
title: Tarefa Vbc | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4ed9563f4149b550e123cf74a09f19245514fe97
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281856"
---
# <a name="vbc-task"></a>Tarefa Vbc
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula vbc.exe, que produz executáveis (.exe), bibliotecas de vínculo dinâmico (.dll) ou módulos de código (.netmodule). Para obter mais informações sobre vbc.exe, consulte o [Compilador de linha de comando do Visual Basic](http://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `Vbc`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AdditionalLibPaths`|Parâmetro `String[]` opcional.<br /><br /> Especifica as pastas adicionais nas quais procurar por assemblies especificados no atributo References.|  
|`AddModules`|Parâmetro `String[]` opcional.<br /><br /> Faz com que o compilador verifique todos os tipos de informações de arquivos especificados disponíveis para o projeto que você está compilando. Esse parâmetro corresponde à opção [/addmodule](http://msdn.microsoft.com/library/fb4b89d4-4926-4f20-868d-427fa28497b2) do compilador vbc.exe.|  
|`BaseAddress`|Parâmetro `String` opcional.<br /><br /> Especifica o endereço básico do DLL. Esse parâmetro corresponde à opção [/baseaddress](http://msdn.microsoft.com/library/c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47) do compilador vbc.exe.|  
|`CodePage`|Parâmetro `Int32` opcional.<br /><br /> Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Esse parâmetro corresponde à opção [/codepage](http://msdn.microsoft.com/library/be36ec33-6800-4505-838c-4124564f5cc9) do compilador vbc.exe.|  
|`DebugType`|Parâmetro `String[]` opcional.<br /><br /> Faz com que o compilador gere informações de depuração. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> O valor padrão é `full`, que permite anexar um depurador ao programa em execução. Um valor de `pdbonly` permite a depuração de código-fonte quando o programa é iniciado no depurador, mas exibe o código de linguagem assembly somente quando o programa em execução está anexado ao depurador. Para saber mais, consulte [/debug (Visual Basic)](http://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2).|  
|`DefineConstants`|Parâmetro `String[]` opcional.<br /><br /> Define as constantes de compilador condicional. Os pares de símbolo/valor são separados por ponto e vírgula e são especificados usando a sintaxe a seguir:<br /><br /> *symbol1* `=` *value1* `;` *symbol2* `=` *value2*<br /><br /> Esse parâmetro corresponde à opção [/define](http://msdn.microsoft.com/library/f735c57d-1cf9-4f2f-a26f-0de630fd4077) do compilador vbc.exe.|  
|`DelaySign`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa colocará a chave pública no assembly. Se `false`, a tarefa assina totalmente o assembly. O valor padrão é `false`. Esse parâmetro não tem nenhum efeito a menos que usado com o parâmetro `KeyFile` ou `KeyContainer`. Esse parâmetro corresponde à opção [/delaysign](http://msdn.microsoft.com/library/c76e61a4-1884-4252-9fb2-377f99caa690) do compilador vbc.exe.|  
|`DisabledWarnings`|Parâmetro `String` opcional.<br /><br /> Suprime os avisos especificados. Você só precisa especificar a parte numérica do identificador de aviso. Vários avisos são separados por ponto e vírgula. Esse parâmetro corresponde à opção [/nowarn](http://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) do compilador vbc.exe.|  
|`DocumentationFile`|Parâmetro `String` opcional.<br /><br /> Processa os comentários de documentação para o arquivo XML especificado. Esse parâmetro substitui o atributo `GenerateDocumentation`. Para obter mais informações, consulte [/doc](http://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65).|  
|`EmitDebugInformation`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa gerará informações de depuração e as colocará em um arquivo .pdb. Para saber mais, consulte [/debug (Visual Basic)](http://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2).|  
|`ErrorReport`|Parâmetro `String` opcional.<br /><br /> Especifica como a tarefa deve relatar erros do compilador interno. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> Se `prompt` for especificado e ocorrer um erro interno do compilador, será exibida ao usuário uma opção para enviar os dados de erros à Microsoft.<br /><br /> Se `send` for especificado e ocorrer um erro interno do compilador, a tarefa enviará os dados de erros à Microsoft.<br /><br /> O valor padrão é `none`, que reporta os erros somente na saída de texto.<br /><br /> Esse parâmetro corresponde à opção [/errorreport](http://msdn.microsoft.com/library/a7fe83a2-a6d8-460c-8dad-79a8f433f501) do compilador vbc.exe.|  
|`FileAlignment`|Parâmetro `Int32` opcional.<br /><br /> Especifica, em bytes, onde alinhar as seções do arquivo de saída. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> Esse parâmetro corresponde à opção [/filealign](http://msdn.microsoft.com/library/cc61ec3d-ad38-4b28-9659-099d73cad099) do compilador vbc.exe.|  
|`GenerateDocumentation`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, serão geradas informações sobre a documentação, que serão colocadas em um arquivo XML com o nome do arquivo executável ou da biblioteca que a tarefa está criando. Para obter mais informações, consulte [/doc](http://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65).|  
|`Imports`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Importa namespaces de coleções do item especificado. Esse parâmetro corresponde à opção [/imports](http://msdn.microsoft.com/library/9a93fb53-c080-497b-bf9b-441022dbbc39) do compilador vbc.exe.|  
|`KeyContainer`|Parâmetro `String` opcional.<br /><br /> Especifica o nome do contêiner da chave de criptografia. Esse parâmetro corresponde à opção [/keycontainer](http://msdn.microsoft.com/library/6a9bc861-1752-4db1-9f64-b5252f0482cc) do compilador vbc.exe.|  
|`KeyFile`|Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo que contém a chave de criptografia. Para saber mais, consulte [/keyfile](http://msdn.microsoft.com/library/ffa82a4b-517a-4c6c-9889-5bae7b534bb8).|  
|`LangVersion`|Opcional [String] (<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Especifica a versão da linguagem, “9” ou “10”.|  
|`LinkResources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Cria um link para um recurso do .NET Framework no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída. Esse parâmetro corresponde à opção [/linkresource](http://msdn.microsoft.com/library/cf4dcad8-17b7-404c-9184-29358aa05b15) do compilador vbc.exe.|  
|`MainEntryPoint`|Parâmetro `String` opcional.<br /><br /> Especifica a classe ou o módulo que contém o procedimento `Sub Main`. Esse parâmetro corresponde à opção [/main](http://msdn.microsoft.com/library/83fc339d-6652-415d-b205-b5133319b5b0) do compilador vbc.exe.|  
|`ModuleAssemblyName`|Parâmetro `String` opcional.<br /><br /> Especifica o assembly do qual esse módulo faz parte.|  
|`NoConfig`|Parâmetro `Boolean` opcional.<br /><br /> Especifica que o compilador não deve usar o arquivo vbc.rsp. Esse parâmetro corresponde ao parâmetro [/noconfig](http://msdn.microsoft.com/library/a7405067-bd21-4171-adf4-a126fa3ad6c3) do compilador vbc.exe.|  
|`NoLogo`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, suprimirá a exibição de informações da barra de notificação do compilador. Esse parâmetro corresponde à opção [/nologo](http://msdn.microsoft.com/library/25ef54b6-d676-4639-a2d2-a747a158bc07) do compilador vbc.exe.|  
|`NoStandardLib`|Parâmetro `Boolean` opcional.<br /><br /> Faz com que o compilador não referencie as bibliotecas padrão. Esse parâmetro corresponde à opção [/nostdlib](http://msdn.microsoft.com/library/140381b8-dc96-4ad5-ae11-792c9ed0be4d) do compilador vbc.exe.|  
|`NoVBRuntimeReference`|Parâmetro `Boolean` opcional.<br /><br /> Apenas para uso interno. Se verdadeiro, impede a referência automática para Microsoft.VisualBasic.dll.|  
|`NoWarnings`|Parâmetro `Boolean` opcional.<br /><br /> Se ele for `true`, a tarefa suprimirá todos os avisos. Para obter mais informações, consulte [/nowarn](http://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83).|  
|`Optimize`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, habilita as otimizações do compilador. Esse parâmetro corresponde à opção [/optimize](http://msdn.microsoft.com/library/fcba4a97-3622-4b87-a891-0f77deab4998) do compilador vbc.exe.|  
|`OptionCompare`|Parâmetro `String` opcional.<br /><br /> Especifica como são feitas comparações de cadeia de caracteres. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `binary`<br />-   `text`<br /><br /> O valor `binary` especifica que a tarefa usa comparações de cadeia de caracteres binária. O valor `text` especifica que a tarefa usa comparações de cadeia de caracteres de texto. O valor padrão desse parâmetro é `binary`. Esse parâmetro corresponde à opção [/optioncompare](http://msdn.microsoft.com/library/7237b766-b44d-4cc5-9a3c-885348a7d9e4) do compilador vbc.exe.|  
|`OptionExplicit`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a declaração explícita de variáveis é necessária. Esse parâmetro corresponde à opção [/optionexplicit](http://msdn.microsoft.com/library/5d296ab3-bafe-4c4d-9887-78f162ed86c7) do compilador vbc.exe.|  
|`OptionInfer`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, permite a inferência de tipos de variáveis.|  
|`OptionStrict`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa impõe semântica de tipo estrito para restringir conversões de tipo implícito. Esse parâmetro corresponde à opção [/optionstrict](http://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) do compilador vbc.exe.|  
|`OptionStrictType`|Parâmetro `String` opcional.<br /><br /> Especifica qual semântica de tipo estrito gera um aviso. Atualmente, há suporte para apenas "custom". Esse parâmetro corresponde à opção [/optionstrict](http://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) do compilador vbc.exe.|  
|`OutputAssembly`|Parâmetro de saída `String` opcional.<br /><br /> Especifica o nome do arquivo de saída. Esse parâmetro corresponde à opção [/out](http://msdn.microsoft.com/library/9f148c15-0909-4cb8-a2db-777f8a8b45ae) do compilador vbc.exe.|  
|`Platform`|Parâmetro `String` opcional.<br /><br /> Especifica a plataforma do processador a ser direcionada pelo arquivo de saída. Esse parâmetro pode ter um valor igual a `x86`, `x64` `Itanium` ou `anycpu`. O padrão é `anycpu`. Esse parâmetro corresponde à opção [/platform](http://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1) do compilador vbc.exe.|  
|`References`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Faz com que a tarefa importe informações de tipo público dos itens especificados para o projeto atual. Esse parâmetro corresponde à opção [/reference](http://msdn.microsoft.com/library/66bdfced-bbf6-43d1-a554-bc0990315737) do compilador vbc.exe.|  
|`RemoveIntegerChecks`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, desabilita a verificação de erro de estouro de inteiro. O valor padrão é `false`. Esse parâmetro corresponde à opção [/removeintchecks](http://msdn.microsoft.com/library/c1835bd5-1e38-4fba-bd2f-6984774765d4) do compilador vbc.exe.|  
|`Resources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Insere um recurso do .NET Framework no arquivo de saída. Esse parâmetro corresponde à opção [/resource](http://msdn.microsoft.com/library/eee2f227-91f2-4f2b-a9d6-1c51c5320858) do compilador vbc.exe.|  
|`ResponseFiles`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica o arquivo de resposta que contém comandos para essa tarefa. Esse parâmetro corresponde à opção [@ (Especificar Arquivo de Resposta)](http://msdn.microsoft.com/library/a6847eaa-e5f9-4303-9421-45b55484b9ca) do compilador vbc.exe.|  
|`RootNamespace`|Parâmetro `String` opcional.<br /><br /> Especifica o namespace raiz para todas as declarações de tipo. Esse parâmetro corresponde à opção [/rootnamespace](http://msdn.microsoft.com/library/e9245edf-6bef-420d-a7c7-324117752783) do compilador vbc.exe.|  
|`SdkPath`|Parâmetro `String` opcional.<br /><br /> Especifica o local de mscorlib.dll e microsoft.visualbasic.dll. Esse parâmetro corresponde à opção [/sdkpath](http://msdn.microsoft.com/library/fec8a3f1-b791-4a37-8af7-344859f8212d) do compilador vbc.exe.|  
|`Sources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica um ou mais arquivos de origem [!INCLUDE[vbprvb](../includes/vbprvb-md.md)].|  
|`TargetCompactFramework`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa direciona o [!INCLUDE[Compact](../includes/compact-md.md)]. Essa opção corresponde à opção [/netcf](http://msdn.microsoft.com/library/db7cfa59-c315-401c-a59b-0daf355343d6) do compilador vbc.exe.|  
|`TargetType`|Parâmetro `String` opcional.<br /><br /> Especifica o formato do arquivo de saída. Esse parâmetro pode ter um valor igual a `library`, que cria uma biblioteca de códigos, `exe`, que cria um aplicativo de console, `module`, que cria um módulo ou `winexe`, que cria um programa do Windows. O padrão é `library`. Esse parâmetro corresponde à opção [/target](http://msdn.microsoft.com/library/e0954147-548b-461f-9c4b-a8f88845616c) do compilador vbc.exe.|  
|`Timeout`|Parâmetro `Int32` opcional.<br /><br /> Especifica a quantidade de tempo em milissegundos após o qual o executável da tarefa é encerrado. O valor padrão é `Int.MaxValue`, indicando que não há período de tempo limite.|  
|`ToolPath`|Parâmetro `String` opcional.<br /><br /> Especifica o local do qual a tarefa carregará o arquivo executável subjacente (vbc.exe). Se esse parâmetro não for especificado, a tarefa usará o caminho de instalação do SDK correspondente à versão da estrutura que está executando [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)].|  
|`TreatWarningsAsErrors`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, todos os avisos são tratados como erros. Para obter mais informações, consulte [/warnaserror (Visual Basic)](http://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1).|  
|`UseHostCompilerIfAvailable`|Parâmetro `Boolean` opcional.<br /><br /> Instrui a tarefa a usar o objeto do compilador em processo, se disponível. Usado somente por [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|`Utf8Output`|Parâmetro `Boolean` opcional.<br /><br /> Registra a saída do compilador usando a codificação UTF-8. Esse parâmetro corresponde à opção [/utf8output](http://msdn.microsoft.com/library/8ab36b1e-027a-49ac-85b4-f48997d9e4d6) do compilador vbc.exe.|  
|`Verbosity`|Parâmetro `String` opcional.<br /><br /> Especifica os detalhes da saída do compilador. Os detalhes podem ser `Quiet`, `Normal` (o padrão) ou `Verbose`.|  
|`WarningsAsErrors`|Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos a serem tratados como erros. Para obter mais informações, consulte [/warnaserror (Visual Basic)](http://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1).<br /><br /> Esse parâmetro substitui o parâmetro `TreatWarningsAsErrors`.|  
|`WarningsNotAsErrors`|Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos que não são tratados como erros. Para obter mais informações, consulte [/warnaserror (Visual Basic)](http://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1).<br /><br /> Esse parâmetro será útil apenas se o parâmetro `TreatWarningsAsErrors` for definido como `true`.|  
|`Win32Icon`|Parâmetro `String` opcional.<br /><br /> Insere um arquivo .ico no assembly, que fornece ao arquivo de saída a aparência desejada no Explorador de Arquivos. Esse parâmetro corresponde à opção [/win32icon](http://msdn.microsoft.com/library/aecaab01-9353-46c5-941c-6edabd4eff92) do compilador vbc.exe.|  
|`Win32Resources`|Parâmetro `String` opcional.<br /><br /> Insere um arquivo de recurso Win32 (.res) no arquivo de saída. Esse parâmetro corresponde à opção [/win32resource](http://msdn.microsoft.com/library/e226946d-19ce-4cc9-91f5-aed24f77aa2b) do compilador vbc.exe.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir compila um projeto [!INCLUDE[vbprvb](../includes/vbprvb-md.md)].  
  
```  
<VBC  
   Sources="@(sources)"  
   Resources="strings.resources"  
   Optimize="true"  
   OutputAssembly="out.exe"/>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Compilador de linha de comando do Visual Basic](http://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c)   
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



