---
title: Tarefa CallTarget | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CallTarget task [MSBuild]
- MSBuild, CallTarget task
ms.assetid: bb1fe2c4-4383-436f-8326-c24cc4a46150
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85ad6261dba80e56ab44f43b4c70df79d63bb509
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55001625"
---
# <a name="calltarget-task"></a>Tarefa CallTarget
Invoca os destinos especificados no arquivo de projeto.  

## <a name="task-parameters"></a>Parâmetros de tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `CallTarget`.  


| Parâmetro | Descrição |
|---------------------------| - |
| `RunEachTargetSeparately` | Parâmetro de entrada de `Boolean` opcional.<br /><br /> Se `true`, o mecanismo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] será chamado uma vez por destino. Se `false`, o mecanismo [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] será chamado para compilar todos os destinos. O valor padrão é `false`. |
| `TargetOutputs` | Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém as saídas de todos os destinos compilados. |
| `Targets` | Parâmetro `String[]` opcional.<br /><br /> Especifica o destino ou os destinos que serão compilados. |
| `UseResultsCache` | Parâmetro `Boolean` opcional.<br /><br /> Se `true`, o resultado em cache será retornado, se presente.<br /><br /> **Observação** Quando uma tarefa MSBuild for executada, a saída é armazenada em cache em um escopo (ProjectFileName, GlobalProperties)[TargetNames] como uma lista de itens de build. |

## <a name="remarks"></a>Comentários  
 Se um destino especificado em `Targets` falhar e `RunEachTargetSeparately` for `true`, a tarefa continuará a compilar os destinos restantes.  

 Caso deseje criar os destinos padrão, use a [tarefa MSBuild](../msbuild/msbuild-task.md) e defina o parâmetro `Projects` como igual a `$(MSBuildProjectFile)`.  

 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  

## <a name="example"></a>Exemplo  
 O exemplo a seguir chama `TargetA` de dentro de `CallOtherTargets`.  

```xml  
<Project DefaultTargets="CallOtherTargets"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  

    <Target Name="CallOtherTargets">  
        <CallTarget Targets="TargetA"/>  
    </Target>  

    <Target Name="TargetA">  
        <Message Text="Building TargetA..." />  
    </Target>  

</Project>  
```  

## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Destinos](../msbuild/msbuild-targets.md)