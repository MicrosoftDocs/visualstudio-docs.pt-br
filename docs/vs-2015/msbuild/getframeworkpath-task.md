---
title: Tarefa GetFrameworkPath | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#GetFrameworkPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFrameworkPath task [MSBuild]
- MSBuild, GetFrameworkPath task
ms.assetid: 5b7bcdd7-d4a0-442d-af29-8aadb3b10598
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dcad656c058fffaf3f075b195cb1f105079a8e5d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248593"
---
# <a name="getframeworkpath-task"></a>Tarefa GetFrameworkPath
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Recupera o caminho para os assemblies [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `GetFrameworkPath`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`FrameworkVersion11Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework versão 1.1, se estiverem presentes. Caso contrário, retornará `null`.|  
|`FrameworkVersion20Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework versão 2.0, se estiverem presentes. Caso contrário, retornará `null`.|  
|`FrameworkVersion30Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework versão 3.0, se estiverem presentes. Caso contrário, retornará `null`.|  
|`FrameworkVersion35Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework versão 3.5, se estiverem presentes. Caso contrário, retornará `null`.|  
|`FrameworkVersion40Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework versão 4.0, se estiverem presentes. Caso contrário, retornará `null`.|  
|`Path`|Parâmetro de saída `String` opcional.<br /><br /> Contém o caminho para os assemblies do framework mais recentes, se estiverem disponíveis. Caso contrário, retornará `null`.|  
  
## <a name="remarks"></a>Comentários  
 Se várias versões do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] estiverem instaladas, essa tarefa retorna a versão na qual o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] está projetado para funcionar.  
  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `GetFrameworkPath` para armazenar o caminho para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] na propriedade `FrameworkPath`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="GetPath">  
        <GetFrameworkPath>  
            <Output  
                TaskParameter="Path"  
                PropertyName="FrameworkPath" />  
        </GetFrameworkPath>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



