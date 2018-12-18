---
title: Tarefa WriteLinesToFile | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#WriteLinesToFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- WriteLinesToFile task [MSBuild]
- MSBuild, WriteLinesToFile task
ms.assetid: 9c8862ac-8da5-4437-9430-ecc30421f1c9
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4af63679437e0b128472d084a55f1ef24a93bc4f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49301841"
---
# <a name="writelinestofile-task"></a>Tarefa WriteLinesToFile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Grava os caminhos dos itens especificados no arquivo de texto especificado.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `WriteLinestoFile`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`File`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> obrigatório.<br /><br /> Especifica o arquivo no qual os itens serão gravados.|  
|`Lines`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Especifica os itens a serem gravados no arquivo.|  
|`Overwrite`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, a tarefa substituirá todo o conteúdo existente no arquivo.|  
|`Encoding`|Parâmetro `String` opcional.<br /><br /> Seleciona a codificação de caracteres, por exemplo, "Unicode".  Confira também <xref:System.Text.Encoding>.|  
  
## <a name="remarks"></a>Comentários  
 Se `Overwrite` for `true`, criará um novo arquivo, gravará os conteúdos nele e o fechará. Se o arquivo de destino já existir, ele será substituído. Se `Overwrite` for `false`, acrescentará os conteúdos ao arquivo, criando um arquivo de destino, caso ele ainda não exista.  
  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `WriteLinesToFile` para gravar os caminhos dos itens na coleção de itens `MyItems` no arquivo especificado pela coleção de itens `MyTextFile`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MyTextFile Include="Items.txt"/>  
        <MyItems Include="*.cs"/>  
    </ItemGroup>  
  
    <Target Name="WriteToFile">  
        <WriteLinesToFile  
            File="@(MyTextFile)"  
            Lines="@(MyItems)"  
            Overwrite="true"  
            Encoding="Unicode"/>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



