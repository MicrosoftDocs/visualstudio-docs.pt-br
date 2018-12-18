---
title: Tarefa VCMessage | Microsoft Docs
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
- vc.task.vcmessage
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- VCMessage task (MSBuild (Visual C++))
- MSBuild (Visual C++), VCMessage task
ms.assetid: 956675fd-05dc-40b4-856f-616145103498
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f592160aae4fc1382b36c7331175eb6ab20d3fdc
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49243926"
---
# <a name="vcmessage-task"></a>Tarefa VCMessage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Registra mensagens de aviso e erro durante o build.  
  
## <a name="remarks"></a>Comentários  
 Essa tarefa ajuda a implementar o MSBuild para o Visual C++ e não se destina a ser chamada pelo usuário. Para obter mais informações, consulte <xref:Microsoft.Build.Utilities.TaskLoggingHelper>.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **VCMessage**.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**Argumentos**|Parâmetro **String** opcional.<br /><br /> Uma lista delimitada por ponto e vírgula de mensagens a serem exibidas.|  
|**Código**|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Um número de erro que qualifica a mensagem.|  
|**Tipo**|Parâmetro **String** opcional.<br /><br /> Especifica o tipo de mensagem a ser emitida. Especifique `"Warning"` para emitir uma mensagem de aviso ou `"Error"` para emitir uma mensagem de erro.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



