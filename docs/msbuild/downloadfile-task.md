---
title: Tarefa DownloadFile | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.technology: msbuild
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#DownloadFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- DownloadFile task [MSBuild]
- MSBuild, DownloadFile task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: Mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 14b5daafbc4c11547515b9d77be2877eb07bcb8b
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37945338"
---
# <a name="downloadfile-task"></a>Tarefa DownloadFile
Baixa os arquivos especificados usando o protocolo HTTP.

>[!NOTE]
>A tarefa DownloadFile está disponível somente no MSBuild 15.8 e superior.
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `DownloadFile`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`DestinationFileName`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem><br /><br /> O nome a ser usado para o arquivo baixado.  Por padrão, o nome de arquivo é derivado da `SourceUrl` ou do servidor remoto.|
|`DestinationFolder`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> obrigatório.<br /><br /> Especifica a pasta de destino na qual baixar o arquivo.  Se a pasta será criada, caso ela não exista.|
|`DownloadedFile`|Parâmetro de saída <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o arquivo baixado.|
|`Retries`|Parâmetro `Int32` opcional.<br /><br /> Especifica o número de tentativas de download, se todas as tentativas anteriores falharam. Usa zero como padrão.|  
|`RetryDelayMilliseconds`|Parâmetro `Int32` opcional.<br /><br /> Especifica o atraso em milissegundos entre as repetições necessárias. Usa 5.000 como padrão.|  
|`SkipUnchangedFiles`|Parâmetro `Boolean` opcional.<br /><br /> Se ele for `true`, ignorará o download de arquivos inalterados. Assume o padrão de `true`. A tarefa `DownloadFile` considera os arquivos como inalterados se eles têm o mesmo tamanho e a mesma hora da última modificação, de acordo com o servidor remoto. <br /><br />**Observação:** nem todos os servidores HTTP indicam que a data da última modificação dos arquivos fará com que o arquivo seja baixado novamente.|
|`SourceUrl`|Parâmetro `String` obrigatório.<br /><br /> Especifica a URL a ser baixada.|
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, confira [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir baixa um arquivo e inclui-o nos itens `Content` antes de compilar o projeto.
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>  
      <MyUrl>https://raw.githubusercontent.com/Microsoft/msbuild/master/LICENSE</MyUrl>
    </PropertyGroup>  

    <Target Name="DownloadContentFiles" BeforeTargets="Build">
        <DownloadFile
            SourceUrl="$(MyUrl)"
            DestinationFolder="$(MSBuildProjectDirectory)">
        <Output TaskParameter="DownloadedFile" ItemName="Content" />
      </DownloadFile>
    </Target>

</Project>
```
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
