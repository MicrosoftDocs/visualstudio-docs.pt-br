---
title: Tarefa Csc | Microsoft Docs
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
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 657535e73294508ac59330cd379c1c6bd192a0b2
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49237374"
---
# <a name="csc-task"></a>Tarefa Csc
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula CSC.exe e produz executáveis (arquivos .exe), bibliotecas de vínculo dinâmico (arquivos .dll) ou módulos de código (arquivos .netmodule). Para obter mais informações sobre o CSC.exe, consulte [Opções do compilador C#](http://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `Csc`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AdditionalLibPaths`|Parâmetro `String[]` opcional.<br /><br /> Especifica diretórios adicionais para pesquisar referências. Para obter mais informações, consulte [/lib (opções do compilador C#)](http://msdn.microsoft.com/library/b0efcc88-e8aa-4df4-a00b-8bdef70b7673).|  
|`AddModules`|Parâmetro `String` opcional.<br /><br /> Especifica um ou mais módulos a fazerem parte do assembly. Para obter mais informações, consulte [/addmodule (opções do compilador C#)](http://msdn.microsoft.com/library/ed604546-0dc2-4bd4-9a3e-610a8d973e58).|  
|`AllowUnsafeBlocks`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, compilará o código que usa a palavra-chave [unsafe](http://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0). Para obter mais informações, consulte [/unsafe (opções do compilador C#)](http://msdn.microsoft.com/library/fdb77ed9-da03-45bd-bb7f-250704da1bcc).|  
|`ApplicationConfiguration`|Parâmetro `String` opcional.<br /><br /> Especifica um arquivo de configuração de aplicativo que contém configurações de associação de assembly.|  
|`BaseAddress`|Parâmetro `String` opcional.<br /><br /> Especifica o endereço básico preferencial no qual uma DLL será carregada. O endereço básico padrão para uma DLL é definido pelo Common Language Runtime de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Para obter mais informações, consulte [/baseaddress (opções do compilador C#)](http://msdn.microsoft.com/library/ce13c965-dfe4-4433-94f5-63b476e3a608).|  
|`CheckForOverflowUnderflow`|Parâmetro `Boolean` opcional.<br /><br /> Especifica se o aritmético inteiro que estoura os limites do tipo de dados causa uma exceção em tempo de execução. Para obter mais informações, consulte [/checked (opções do compilador C#)](http://msdn.microsoft.com/library/fb7475d3-e6a6-4e6d-b86c-69e7a74c854b).|  
|`CodePage`|Parâmetro `Int32` opcional.<br /><br /> Especifica a página de código a ser usada para todos os arquivos de código-fonte na compilação. Para obter mais informações, consulte [/codepage (opções do compilador C#)](http://msdn.microsoft.com/library/75942989-b69a-4308-90a0-840c73d2c478).|  
|`DebugType`|Parâmetro `String` opcional.<br /><br /> Especifica o tipo de depuração. `DebugType` pode ser `full` ou `pdbonly`. O padrão é `full`, o que permite que um depurador seja anexado a um programa em execução. Especificar `pdbonly` habilita a depuração de código-fonte quando o programa é iniciado no depurador, mas apenas exibe o assembler quando o programa em execução está anexado ao depurador.<br /><br /> Esse parâmetro substitui o parâmetro `EmitDebugInformation`.<br /><br /> Para obter mais informações, consulte [/debug (opções do compilador C#)](http://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969).|  
|`DefineConstants`|Parâmetro `String` opcional.<br /><br /> Define símbolos do pré-processador. Para obter mais informações, consulte [/define (opções do compilador C#)](http://msdn.microsoft.com/library/f17d7b4d-82d0-4133-8563-68cced1cac6e).|  
|`DelaySign`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, especificará que você deseja um assembly totalmente com sinal. Se for `false`, especificará que você apenas deseja colocar a chave pública no assembly.<br /><br /> Esse parâmetro não terá nenhum efeito a menos que seja usado com o parâmetro `KeyFile` ou `KeyContainer`.<br /><br /> Para obter mais informações, consulte [/delaysign (opções do compilador C#)](http://msdn.microsoft.com/library/bcb058eb-2933-4e7f-b356-5c941db4de75).|  
|`DisabledWarnings`|Parâmetro `String` opcional.<br /><br /> Especifica a lista de avisos a ser desabilitada. Para obter mais informações, consulte [/nowarn (opções do compilador C#)](http://msdn.microsoft.com/library/6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4).|  
|`DocumentationFile`|Parâmetro `String` opcional.<br /><br /> Processa comentários de documentação para um arquivo XML. Para obter mais informações, consulte [/doc (opções do compilador C#)](http://msdn.microsoft.com/library/849eea59-c936-4311-bad8-d07404480f2a).|  
|`EmitDebugInformation`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, a tarefa gerará informações de depuração e as colocará em um arquivo de banco de dados do programa (.pdb). Se for `false`, a tarefa não emitirá nenhuma informação de depuração. O padrão é `false`. Para obter mais informações, consulte [/debug (opções do compilador C#)](http://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969).|  
|`ErrorReport`|Parâmetro `String` opcional.<br /><br /> Fornece uma maneira conveniente de relatar um erro interno do C# à Microsoft. Esse parâmetro pode ter um valor igual a `prompt`, `send` ou `none`. Se o parâmetro for definido como `prompt`, você receberá um prompt quando ocorrer um erro interno do compilador. O prompt permite enviar um relatório de bugs eletronicamente à Microsoft. Se o parâmetro for definido como `send`, um relatório de bugs será enviado automaticamente. Se o parâmetro for definido como `none`, o erro será relatado apenas na saída de texto do compilador. O padrão é `none`. Para obter mais informações, consulte [/errorreport (opções do compilador C#)](http://msdn.microsoft.com/library/bd0e7493-b79d-4369-9c3f-ba26ebdfbedf).|  
|`FileAlignment`|Parâmetro `Int32` opcional.<br /><br /> Especifica o tamanho das seções no arquivo de saída. Para obter mais informações, consulte [/filealign (opções do compilador C#)](http://msdn.microsoft.com/library/15cf1c98-3798-4ced-9f08-60619308a073).|  
|`GenerateFullPaths`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, especificará o caminho absoluto para o arquivo na saída do compilador. Se for `false`, especificará o nome do arquivo. O padrão é `false`. Para obter mais informações, consulte [/fullpaths (opções do compilador C#)](http://msdn.microsoft.com/library/d2a5f857-cbb2-430b-879c-d648aaf0b8c4).|  
|`KeyContainer`|Parâmetro `String` opcional.<br /><br /> Especifica o nome do contêiner da chave de criptografia. Para obter mais informações, consulte [/keycontainer (opções do compilador C#)](http://msdn.microsoft.com/library/b3982b6d-2382-4f7e-bebd-ce98eaa30763).|  
|`KeyFile`|Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo que contém a chave de criptografia. Para obter mais informações, consulte [/keyfile (opções do compilador C#)](http://msdn.microsoft.com/library/0815f9de-ace4-4e98-b4c6-13c55dea40c2).|  
|`LangVersion`|Parâmetro `String` opcional.<br /><br /> Especifica a versão da linguagem a ser usada. Para obter mais informações, consulte [/langversion (opções do compilador C#)](http://msdn.microsoft.com/library/3fb00b05-a0ff-4782-b313-13a4c0f62d94).|  
|`LinkResources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Cria um link para um recurso [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída.<br /><br /> Os itens passados para esse parâmetro podem ter entradas de metadados opcionais chamadas `LogicalName` e `Access`. `LogicalName` corresponde ao parâmetro `identifier` da opção `/linkresource` e `Access` corresponde ao parâmetro `accessibility-modifier`. Para obter mais informações, consulte [/linkresource (opções do compilador C#)](http://msdn.microsoft.com/library/440c26c2-77c1-4811-a0a3-57cce3f5fc96).|  
|`MainEntryPoint`|Parâmetro `String` opcional.<br /><br /> Especifica o local do método `Main`. Para obter mais informações, consulte [/main (opções do compilador C#)](http://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049).|  
|`ModuleAssemblyName`|Parâmetro `String` opcional.<br /><br /> Especifica o nome do assembly do qual esse módulo fará parte.|  
|`NoConfig`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, informará ao compilador que ele não deve compilar com o arquivo csc.rsp. Para obter mais informações, consulte [/noconfig (opções do compilador C#)](http://msdn.microsoft.com/library/cd26967e-e494-4c8c-b5c9-af13b2f78b2e).|  
|`NoLogo`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, suprimirá a exibição de informações da barra de notificação do compilador. Para obter mais informações, consulte [/nologo (opções do compilador C#)](http://msdn.microsoft.com/library/426afb36-a8fb-469d-9c45-a35d9512557c).|  
|`NoStandardLib`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, impedirá a importação de mscorlib.dll, que define todo o namespace System. Use esse parâmetro se desejar definir ou criar seus próprios objetos e namespace System. Para obter mais informações, consulte [/nostdlib (opções do compilador C#)](http://msdn.microsoft.com/library/ec197989-fa49-4725-a455-e06b551eb65f).|  
|`NoWin32Manifest`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, não inclua o manifesto Win32 padrão.|  
|`Optimize`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, habilitará as otimizações. Se for `false`, desabilitará as otimizações. Para obter mais informações, consulte [/optimize (opções do compilador C#)](http://msdn.microsoft.com/library/6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0).|  
|`OutputAssembly`|Parâmetro de saída `String` opcional.<br /><br /> Especifica o nome do arquivo de saída. Para obter mais informações, consulte [/out (opções do compilador C#)](http://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5).|  
|`PdbFile`|Parâmetro `String` opcional.<br /><br /> Especifica o nome de arquivo de informações de depuração. O nome padrão é o nome do arquivo de saída com uma extensão .pdb.|  
|`Platform`|Parâmetro `String` opcional.<br /><br /> Especifica a plataforma do processador a ser direcionada pelo arquivo de saída. Esse parâmetro pode ter um valor igual a `x86`, `x64` ou `anycpu`. O padrão é `anycpu`. Para obter mais informações, consulte [/platform (opções do compilador C#)](http://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04).|  
|`References`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Faz com que a tarefa importe informações de tipo público dos itens especificados para o projeto atual. Para obter mais informações, consulte [/reference (opções do compilador C#)](http://msdn.microsoft.com/library/8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4).<br /><br /> Você pode especificar um alias de referência [!INCLUDE[csprcs](../includes/csprcs-md.md)] em um arquivo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] adicionando os metadados `Aliases` ao item original da “Referência”. Por exemplo, para definir o alias “LS1” na seguinte linha de comando CSC:<br /><br /> `csc /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> você usará:<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>`|  
|`Resources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Insere um recurso [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] no arquivo de saída.<br /><br /> Os itens passados para esse parâmetro podem ter entradas de metadados opcionais chamadas `LogicalName` e `Access`. `LogicalName` corresponde ao parâmetro `identifier` da opção `/resource` e `Access` corresponde ao parâmetro `accessibility-modifier`. Para obter mais informações, consulte [/resource (opções do compilador C#)](http://msdn.microsoft.com/library/5212666e-98ab-47e4-a497-b5545ab15c7f).|  
|`ResponseFiles`|Parâmetro `String` opcional.<br /><br /> Especifica o arquivo de resposta que contém comandos para essa tarefa. Para obter mais informações, confira [@ (Especificar de arquivo de resposta)](http://msdn.microsoft.com/library/dda4fa9f-a02c-400f-8b6a-d58834e13d7f).|  
|`Sources`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica um ou mais arquivos de origem [!INCLUDE[csprcs](../includes/csprcs-md.md)].|  
|`TargetType`|Parâmetro `String` opcional.<br /><br /> Especifica o formato do arquivo de saída. Esse parâmetro pode ter um valor igual a `library`, que cria uma biblioteca de códigos, `exe`, que cria um aplicativo de console, `module`, que cria um módulo ou `winexe`, que cria um programa do Windows. O valor padrão é `library`. Para obter mais informações, consulte [/target (opções do compilador C#)](http://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f).|  
|`TreatWarningsAsErrors`|Parâmetro `Boolean` opcional.<br /><br /> Se for `true`, tratará todos os avisos como erros. Para obter mais informações, consulte [/warnaserror (opções do compilador C#)](http://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c).|  
|`UseHostCompilerIfAvailable`|Parâmetro `Boolean` opcional.<br /><br /> Instrui a tarefa a usar o objeto do compilador em processo, se disponível. Usado somente por [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].|  
|`Utf8Output`|Parâmetro `Boolean` opcional.<br /><br /> Registra a saída do compilador usando a codificação UTF-8. Para obter mais informações, consulte [/utf8output (opções do compilador C#)](http://msdn.microsoft.com/library/27ff7381-c281-45d7-b2eb-1ad644b1354e).|  
|`WarningLevel`|Parâmetro `Int32` opcional.<br /><br /> Especifica o nível de aviso a ser exibido pelo compilador. Para obter mais informações, consulte [/warn (opções do compilador C#)](http://msdn.microsoft.com/library/5f80ff59-4991-4382-9f9a-77da18446e71).|  
|`WarningsAsErrors`|Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos a serem tratados como erros. Para obter mais informações, consulte [/warnaserror (opções do compilador C#)](http://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c).<br /><br /> Esse parâmetro substitui o parâmetro `TreatWarningsAsErrors`.|  
|`WarningsNotAsErrors`|Parâmetro `String` opcional.<br /><br /> Especifica uma lista de avisos que não são tratados como erros. Para obter mais informações, consulte [/warnaserror (opções do compilador C#)](http://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c).<br /><br /> Esse parâmetro será útil apenas se o parâmetro `TreatWarningsAsErrors` for definido como `true`.|  
|`Win32Icon`|Parâmetro `String` opcional.<br /><br /> Insere um arquivo .ico no assembly, que fornece ao arquivo de saída a aparência desejada no Explorador de Arquivos. Para obter mais informações, consulte [/win32icon (opções do compilador C#)](http://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138).|  
|`Win32Manifest`|Parâmetro `String` opcional.<br /><br /> Especifica o manifesto Win32 a ser incluído.|  
|`Win32Resource`|Parâmetro `String` opcional.<br /><br /> Insere um arquivo de recurso Win32 (.res) no arquivo de saída. Para obter mais informações, consulte [/win32res (opções do compilador C#)](http://msdn.microsoft.com/library/3c33f750-6948-4c7e-a27e-bef98f77255b).|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe `Microsoft.Build.Tasks.ManagedCompiler`, que herda da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `Csc` para compilar um executável com base nos arquivos de origem da coleção de itens `Compile`.  
  
```  
<CSC  
    Sources="@(Compile)"  
    OutputAssembly="$(AppName).exe"  
    EmitDebugInformation="true" />  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



