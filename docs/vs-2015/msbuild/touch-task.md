---
title: Tarefa Touch | Microsoft Docs
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
- http://schemas.microsoft.com/developer/msbuild/2003#Touch
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Touch task
- Touch task [MSBuild]
ms.assetid: 8a978645-1393-4904-ae69-42afabd8c109
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ac0614a8496d932f733d7e8bbd2d2b954329dd05
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49302037"
---
# <a name="touch-task"></a>Tarefa Touch
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Define os horários de modificação e acesso aos arquivos.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `Touch`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AlwaysCreate`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, cria todos os arquivos que ainda não existem.|  
|`Files`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem>`[]` obrigatório.<br /><br /> Especifica a coleção de arquivos a serem tocados.|  
|`ForceTouch`|Parâmetro `Boolean` opcional.<br /><br /> Se `true`, força um toque de arquivo, mesmo que os arquivos sejam somente leitura.|  
|`Time`|Parâmetro `String` opcional.<br /><br /> Especifica uma hora diferente da atual. O formato deve ser um formato aceitável para o método <xref:System.DateTime.Parse%2A>.|  
|`TouchedFiles`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem>`[]` opcional.<br /><br /> Contém a coleção de itens que foram tocados com êxito.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `Touch` para alterar os horários de acesso e modificação dos arquivos especificados na coleção de itens `Files` e coloca a lista de arquivos tocados com êxito na coleção de itens `FilesTouched`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
<ItemGroup>  
    <Files Include="File1.cs;File2.cs;File3.cs" />  
</ItemGroup>  
  
    <Target Name="TouchFiles">  
        <Touch  
            Files="@(Files)">  
            <Output  
                TaskParameter="TouchedFiles"  
                ItemName="FilesTouched"/>  
    </Touch>  
</Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



