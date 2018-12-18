---
title: Tarefa CreateItem | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#CreateItem
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateItem task [MSBuild]
- MSBuild, CreateItem task
ms.assetid: c4311f38-979e-4324-b524-9e8c1cbdc41a
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7db76f3ec603c493cef38536b6fb54b74ac6c43b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49180895"
---
# <a name="createitem-task"></a>Tarefa CreateItem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Popula as coleções de itens com os itens de entrada. Isso permite que os itens sejam copiados de uma lista para outra.  
  
> [!NOTE]
>  Essa tarefa foi preterida. Do .NET Framework 3.5 em diante, grupos de itens podem ser colocados dentro de elementos [Target](../msbuild/target-element-msbuild.md). Para obter mais informações, consulte [Itens](../msbuild/msbuild-items.md).  
  
## <a name="attributes"></a>Atributos  
 A tabela a seguir descreve os parâmetros da tarefa `CreateItem`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AdditionalMetadata`|Parâmetro de matriz `String` opcional.<br /><br /> Especifica os metadados adicionais para anexar aos itens de saída.  Especifique o nome de metadados e o valor do item com a seguinte sintaxe:<br /><br /> *MetadataName* `=` *MetadataValue*<br /><br /> Vários pares de nome/valor de metadados devem ser separados por ponto e vírgula. Se o nome ou o valor contiver um ponto e vírgula ou outros caracteres especiais, eles devem ser escapados. Para obter mais informações, confira [Como: usar caracteres especiais no MSBuild](../msbuild/how-to-escape-special-characters-in-msbuild.md).|  
|`Exclude`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Especifica os itens a serem excluídos da coleção de itens de saída. Esse parâmetro pode conter especificações de curinga. Para mais informações, consulte [Itens](../msbuild/msbuild-items.md) e [Como excluir arquivos do build](../msbuild/how-to-exclude-files-from-the-build.md).|  
|`Include`|<xref:Microsoft.Build.Framework.ITaskItem>`[]`Parâmetro obrigatório.<br /><br /> Especifica os itens a serem incluídos na coleção de itens de saída. Esse parâmetro pode conter especificações de curinga.|  
|`PreserveExistingMetadata`|Parâmetro `Boolean` opcional.<br /><br /> Se `True`, somente os metadados adicionais se aplicarão, se eles ainda não existirem.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir cria um novo item denominado `MySourceItemsWithMetadata` da coleção de itens `MySourceItems`. A tarefa `CreateItem` popula a nova coleção de itens com os itens no item `MySourceItems`. Em seguida, ela adiciona uma entrada de metadados adicionais chamada `MyMetadata` com um valor de `Hello` para cada item na nova coleção.  
  
 Depois que a tarefa é executada, a coleção de itens `MySourceItemsWithMetadata` contém os itens `file1.resx` e `file2.resx`, ambos com entradas de metadados para `MyMetadata`. A coleta do item `MySourceItems` permanece inalterada.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MySourceItems Include="file1.resx;file2.resx" />  
    </ItemGroup>  
  
    <Target Name="NewItems">  
        <CreateItem  
            Include="@(MySourceItems)"  
            AdditionalMetadata="MyMetadata=Hello">  
           <Output  
               TaskParameter="Include"  
               ItemName="MySourceItemsWithMetadata"/>  
        </CreateItem>  
  
    </Target>  
  
</Project>  
```  
  
 A tabela a seguir descreve o valor do item de saída após a execução da tarefa. Os metadados de item são mostrados entre parênteses após o item.  
  
|Coleta de itens|Conteúdo|  
|---------------------|--------------|  
|`MySourceItemsWithMetadata`|`file1.resx` (`MyMetadata="Hello"`)<br /><br /> `file2.resx` (`MyMetadata="Hello"`)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



