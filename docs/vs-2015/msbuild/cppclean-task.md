---
title: Tarefa CPPClean | Microsoft Docs
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
- vc.task.cppclean
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), CPPClean task
- CPPClean task (MSBuild (Visual C++))
ms.assetid: b62a482e-8fb5-4999-b50b-6605a078e291
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a96571cbc4de4281daddd42f4b1d53b60b300e53
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49826941"
---
# <a name="cppclean-task"></a>Tarefa CPPClean
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


Exclui os arquivos temporários criados pelo MSBuild quando projeto do Visual C++ é compilado. O processo de exclusão de arquivos de build é conhecido como *limpeza*.  

## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **CPPClean**.  


|            Parâmetro            |                                                                                                Descrição                                                                                                 |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **DeletedFiles**         |                               Parâmetro de saída `ITaskItem[]` opcional.<br /><br /> Define uma matriz de itens de arquivo de saída do MSBuild que pode ser consumida e emitida por tarefas.                                |
|          **DoDelete**           |                                                            Parâmetro **Boolean** opcional.<br /><br /> Se `true`, limpará arquivos de build temporários.                                                             |
| **FilePatternsToDeleteOnClean** |                                            Parâmetro `String` obrigatório.<br /><br /> Especifica uma lista delimitada por ponto e vírgula de extensões de arquivo dos arquivos a serem limpos.                                             |
|   **FilesExcludedFromClean**    |                                                    Parâmetro `String` opcional.<br /><br /> Especifica uma lista delimitada por ponto e vírgula de arquivos que não serão limpos.                                                    |
|       **FoldersToClean**        | Parâmetro `String` obrigatório.<br /><br /> Especifica uma lista delimitada por ponto e vírgula de diretórios a serem limpos. Você pode especificar uma completa ou um caminho relativo e o caminho pode conter o símbolo curinga (**\\**\*). |

## <a name="remarks"></a>Comentários  

## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



