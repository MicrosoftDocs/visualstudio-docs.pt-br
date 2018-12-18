---
title: Usando a tarefa AspNetCompiler para pré-compilar aplicativos ASP.NET | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AspNetCompiler
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AspNetCompiler task
- AspNetCompiler task [MSBuild]
ms.assetid: f811c019-a67b-4d54-82e6-e29549496f6e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 69971e72569dcae1f02f1e2b7988ef15f881fe85
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37945163"
---
# <a name="aspnetcompiler-task"></a>Tarefa AspNetCompiler
A tarefa `AspNetCompiler` encapsula *aspnet_compiler.exe*, um utilitário para pré-compilar aplicativos [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].  
  
## <a name="task-parameters"></a>Parâmetros de tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `AspNetCompiler`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AllowPartiallyTrustedCallers`|Parâmetro `Boolean` opcional.<br /><br /> Se esse parâmetro for `true`, o assembly de nome forte permitirá chamadores parcialmente confiáveis.|  
|`Clean`|Parâmetro opcional `Boolean`<br /><br /> Se esse parâmetro for `true`, o aplicativo pré-compilado será compilado limpo. Todos os componentes compilados anteriormente serão recompilados. O valor padrão é `false`. Esse parâmetro corresponde à opção **-c** do *aspnet_compiler.exe*.|  
|`Debug`|Parâmetro `Boolean` opcional.<br /><br /> Se esse parâmetro for `true`, informações de depuração (arquivo .PDB) serão emitidas durante o build. O valor padrão é `false`. Esse parâmetro corresponde à opção **-d** do *aspnet_compiler.exe*.|  
|`DelaySign`|Parâmetro `Boolean` opcional.<br /><br /> Se esse parâmetro for `true`, o assembly não será totalmente assinado quando for criado.|  
|`FixedNames`|Parâmetro `Boolean` opcional.<br /><br /> Se esse parâmetro for `true`, os assemblies compilados receberão nomes fixos.|  
|`Force`|Parâmetro opcional `Boolean`<br /><br /> Se esse parâmetro for `true`, a tarefa substituirá o diretório de destino se ele já existir. Os conteúdos existentes serão perdidos. O valor padrão é `false`. Esse parâmetro corresponde à opção **-f** do *aspnet_compiler.exe*.|  
|`KeyContainer`|Parâmetro `String` opcional.<br /><br /> Especifica um contêiner de chave de nome forte.|  
|`KeyFile`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho físico do arquivo de chave de nome forte.|  
|`MetabasePath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho completo da metabase do IIS do aplicativo. Esse parâmetro não pode ser combinado com os parâmetros `VirtualPath` ou `PhysicalPath`. Esse parâmetro corresponde à opção **-m** do *aspnet_compiler.exe*.|  
|`PhysicalPath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho físico do aplicativo a ser compilado. Se esse parâmetro estiver ausente, a metabase do IIS será usada para localizar o aplicativo. Esse parâmetro corresponde à opção **-p** do *aspnet_compiler.exe*.|  
|`TargetFrameworkMoniker`|Parâmetro `String` opcional.<br /><br /> Especifica o TargetFrameworkMoniker que indica qual versão do .NET Framework do *aspnet_compiler.exe* deve ser usada. Aceita apenas monikers do .NET Framework.|  
|`TargetPath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho físico para o qual o aplicativo é compilado. Se não for especificado, o aplicativo será pré-compilado no local.|  
|`Updateable`|Parâmetro `Boolean` opcional.<br /><br /> Se esse parâmetro for `true`, o aplicativo pré-compilado será atualizável.  O valor padrão é `false`. Esse parâmetro corresponde à opção **-u** do *aspnet_compiler.exe*.|  
|`VirtualPath`|Parâmetro `String` opcional.<br /><br /> Especifica o caminho virtual do aplicativo a ser compilado. Se `PhysicalPath` for especificado, o caminho físico será usado para localizar o aplicativo. Caso contrário, a metabase do IIS será usada e será considerado que o aplicativo está no site padrão. Esse parâmetro corresponde à opção **-v** do *aspnet_compiler.exe*.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.ToolTaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.ToolTask>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base ToolTaskExtension](../msbuild/tooltaskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir usa a tarefa `AspNetCompiler` para pré-compilar um aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="PrecompileWeb">  
        <AspNetCompiler  
            VirtualPath="/MyWebSite"  
            PhysicalPath="c:\inetpub\wwwroot\MyWebSite\"  
            TargetPath="c:\precompiledweb\MyWebSite\"  
            Force="true"  
            Debug="true"  
        />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
