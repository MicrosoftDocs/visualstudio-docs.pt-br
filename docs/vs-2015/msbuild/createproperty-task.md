---
title: Tarefa CreateProperty | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#CreateProperty
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateProperty task [MSBuild]
- MSBuild, CreateProperty task
ms.assetid: fbc31a88-62d4-43d2-b739-68ef3fac38f5
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c18288e5088871703605da4915786486e2e864b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49267651"
---
# <a name="createproperty-task"></a>Tarefa CreateProperty
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Popula as propriedades com os valores passados. Isso permite que os valores sejam copiados de uma propriedade ou cadeia de caracteres para outra.  
  
## <a name="attributes"></a>Atributos  
 A tabela a seguir descreve os parâmetros da tarefa `CreateProperty`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Value`|Parâmetro de saída `String` opcional.<br /><br /> Especifica o valor a ser copiado para a nova propriedade.|  
|`ValueSetByTask`|Parâmetro de saída `String` opcional.<br /><br /> Contém o mesmo valor que o parâmetro `Value`. Use esse parâmetro somente para evitar que a propriedade de saída seja definida por [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] quando ela ignora o destino delimitador porque as saídas estão atualizadas.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `CreateProperty` para criar a propriedade `NewFile` usando a combinação dos valores das propriedades `SourceFilename` e `SourceFileExtension`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <SourceFilename>Module1</SourceFilename>  
        <SourceFileExtension>vb</SourceFileExtension>  
    </PropertyGroup>  
  
    <Target Name="CreateProperties">  
  
        <CreateProperty  
            Value="$(SourceFilename).$(SourceFileExtension)">  
            <Output  
                TaskParameter="Value"  
                PropertyName="NewFile" />  
        </CreateProperty>  
  
    </Target>  
  
</Project>  
```  
  
 Depois de executar o projeto, o valor da propriedade `NewFile` será `Module1.vb`.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



