---
title: Tarefa UnregisterAssembly | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#UnregisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UnregisterAssembly task
- UnregisterAssembly task [MSBuild]
ms.assetid: 04f549dd-3591-4dda-9c3a-cf6ede9df2c3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d6f1712192f8d68131a9adbbc8eb6de5d85429ad
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39150529"
---
# <a name="unregisterassembly-task"></a>Tarefa UnregisterAssembly
Cancela o registro os assemblies especificados para fins de interoperabilidade COM. Executa o inverso da [tarefa RegisterAssembly](../msbuild/registerassembly-task.md).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `UnregisterAssembly`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Assemblies`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os assemblies cujo registro deverá ser cancelado.|  
|`AssemblyListFile`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Contém informações sobre o estado entre a tarefa `RegisterAssembly` e a tarefa `UnregisterAssembly`. Isso impede que a tarefa tente cancelar o registro de um assembly que falhou ao se registrar na tarefa `RegisterAssembly`.<br /><br /> Se esse parâmetro for especificado, os parâmetros `Assemblies` e `TypeLibFiles` serão ignorados.|  
|`TypeLibFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Cancela o registro da biblioteca de tipos especificada do assembly especificado. **Observação:** esse parâmetro só é necessário se o nome de arquivo de biblioteca de tipos é diferente do nome do assembly.|  
  
## <a name="remarks"></a>Comentários  
 Não é necessário que o assembly exista para que esta tarefa seja bem-sucedida. Se você tentar cancelar o registro de um assembly que não existe, a tarefa terá êxito com um aviso. Isso ocorre porque é o trabalho dessa tarefa remover o registro do assembly do Registro. Se o assembly não existir, ele não estará no Registro e, portanto, a tarefa terá sido bem-sucedida.  
  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.AppDomainIsolatedTaskExtension>, que herda da classe <xref:System.MarshalByRefObject>. A classe `MarshalByRefObject` fornece a mesma funcionalidade que a classe <xref:Microsoft.Build.Utilities.Task>, mas ela pode ser instanciada em seu próprio domínio do aplicativo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `UnregisterAssembly` para cancelar o registro do assembly no caminho especificado pelas propriedades `OutputPath` e `FileName`, se ele existir.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <OutputPath>\Output\</OutputPath>  
        <FileName>MyFile.dll</FileName>  
    </PropertyGroup>  
    <Target Name="UnregisterAssemblies">  
        <UnregisterAssembly  
            Condition="Exists('$(OutputPath)$(FileName)')"  
            Assemblies="$(OutputPath)$(FileName)" />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa RegisterAssembly](../msbuild/registerassembly-task.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)