---
title: Tarefa AssignCulture | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#AssignCulture
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AssignCulture task
- AssignCulture task [MSBuild]
ms.assetid: 8f8314cc-82a6-4f16-a62d-b9f0d1d5e274
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c35d949f2d3cf3924a63ce6db0e596af1fccddbd
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49235645"
---
# <a name="assignculture-task"></a>Tarefa AssignCulture
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Essa tarefa aceita uma lista de itens que pode conter uma cadeia de caracteres de identificador de cultura .NET válida como parte do nome de arquivo e produz itens com metadados nomeados como `Culture` que contêm o identificador de cultura correspondente. Por exemplo, o nome de arquivo Form1.fr-fr.resx tem um identificador de cultura "fr-fr" inserido, assim, essa tarefa produzirá um item com o mesmo nome de arquivo e com os metadados `Culture` iguais a `fr-fr`. A tarefa também produz uma lista de nomes de arquivo com a cultura removida do nome de arquivo.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `AssignCulture`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AssignedFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém a lista de itens recebidos no parâmetro `Files`, com uma entrada de metadados `Culture` adicionada a cada item.<br /><br /> Se o item de entrada do parâmetro `Files` já contiver uma entrada de metadados `Culture`, a entrada de metadados original será utilizada.<br /><br /> A tarefá atribuirá uma entrada de metadados `Culture` somente se o nome de arquivo contiver um identificador de cultura válido. O identificador de cultura deve estar entre os dois últimos pontos no nome de arquivo.|  
|`AssignedFilesWithCulture`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém o subconjunto dos itens do parâmetro `AssignedFiles` que tem uma entrada de metadados `Culture`.|  
|`AssignedFilesWithNoCulture`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém o subconjunto dos itens do parâmetro `AssignedFiles` que não tem uma entrada de metadados `Culture`.|  
|`CultureNeutralAssignedFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém a mesma lista de itens produzida no parâmetro `AssignedFiles`, exceto aqueles com a cultura removida do nome de arquivo.<br /><br /> A tarefa removerá a cultura do nome de arquivo somente se ele for um identificador de cultura válido.|  
|`Files`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Especifica a lista de arquivos com nomes de cultura inseridos a qual a cultura será atribuída.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir executa a tarefa `AssignCulture` com a coleção de itens `ResourceFiles`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ResourceFiles Include="MyResource1.fr.resx"/>  
        <ResourceFiles Include="MyResource2.XX.resx"/>  
    </ItemGroup>  
  
    <Target Name="Culture">  
        <AssignCulture  
            Files="@(ResourceFiles)"  
            <Output TaskParameter="AssignedFiles"  
                ItemName="OutAssignedFiles"/>  
            <Output TaskParameter="AssignedFilesWithCulture"  
                ItemName="OutAssignedFilesWithCulture"/>  
            <Output TaskParameter="AssignedFilesWithNoCulture"  
                ItemName="OutAssignedFilesWithNoCulture"/>  
            <Output TaskParameter="CultureNeutralAssignedFiles"  
                ItemName="OutCultureNeutralAssignedFiles"/>  
        </AssignCulture>  
    </Target>  
</Project>  
```  
  
 A tabela a seguir descreve o valor dos itens de saída após a execução da tarefa. Os metadados de item são mostrados entre parênteses após o item.  
  
|Coleta de itens|Conteúdo|  
|---------------------|--------------|  
|`OutAssignedFiles`|`MyResource1.fr.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx` (não há metadados adicionais)|  
|`OutAssignedFilesWithCulture`|`MyResource1.fr.resx (Culture="fr")`|  
|`OutAssignedFilesWithNoCulture`|`MyResource2.XX.resx` (não há metadados adicionais)|  
|`OutCultureNeutralAssignedFiles`|`MyResource1.resx (Culture="fr")`<br /><br /> `MyResource2.XX.resx (`não há metadados adicionais)|  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



