---
title: Tarefa SetEnv | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2018
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.setenv
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), tasks
- SetEnv task (MSBuild (Visual C++))
ms.assetid: fd9e4225-68cb-4608-8b27-468b0218c936
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3024a0477193647a6949eeaa4d8d40d4d965f940
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220395"
---
# <a name="setenv-task"></a>Tarefa SetEnv
Define ou exclui o valor de uma variável de ambiente especificada.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **SetEnv**.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**Nome**|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> O nome de uma variável de ambiente.|  
|**OutputEnvironmentVariable**|Parâmetro de saída opcional **String**.<br /><br /> Contém o valor atribuído à variável de ambiente especificado pelo parâmetro **Nome**.|  
|**Prefixo**|Parâmetro `Boolean` obrigatório.<br /><br /> Se `true`, concatenará o valor do parâmetro **Valor** antes do valor da variável de ambiente especificado pelo parâmetro **Nome** e, em seguida, atribuirá o resultado à variável de ambiente. Se `false`, atribuirá somente o valor do parâmetro **Valor** à variável de ambiente.|  
|**Target**|Parâmetro **String** opcional.<br /><br /> Especifica o local em que uma variável de ambiente é armazenada. Especifique "User" ou "Machine".<br /><br /> Para saber mais, confira [Enumeração EnvironmentVariableTarget](xref:System.EnvironmentVariableTarget).|  
|**Valor**|Parâmetro **String** opcional.<br /><br /> O valor atribuído à variável de ambiente especificado pelo parâmetro **Nome**. Se **Valor** estiver vazio e a variável existir, a variável será excluída. Se a variável não existir, nenhum erro ocorrerá mesmo que a operação não possa ser executada.<br /><br /> Para saber mais, confira [Método Environment::SetEnvironmentVariable](xref:System.Environment.SetEnvironmentVariable%2A).|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)