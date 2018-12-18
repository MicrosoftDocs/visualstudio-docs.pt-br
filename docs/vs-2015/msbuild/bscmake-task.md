---
title: Tarefa BscMake | Microsoft Docs
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
- vc.task.bscmake
- VC.Project.VCBscMakeTool.PreserveSBR
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), tasks
- BscMake task (MSBuild (Visual C++))
ms.assetid: bb98fc67-cad8-43a7-9598-60df6d734db2
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 92f346bdab454e04f7df16ea39e42668da33d451
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49243211"
---
# <a name="bscmake-task"></a>Tarefa BscMake
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
IMPORTANTE]
>  O bscmake não é usado pelo IDE do Visual Studio. Desde o Visual Studio 2008, as informações de procura são armazenadas automaticamente em um arquivo .sdf na pasta da solução.  
  
 Encapsula a ferramenta do Utilitário de Manutenção de Informações de Procura da Microsoft (bscmake.exe).  A ferramenta bscmake.exe cria um arquivo de informações de procura (.bsc) dos arquivos do navegador de origem (.sbr) que são criados durante o build. Use o **Pesquisador de Objetos** para exibir um arquivo .bsc. Para obter mais informações, consulte [referência BSCMAKE](http://msdn.microsoft.com/library/b97ad994-1355-4809-98db-6abc12c6fb13).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **BscMake**. A maioria dos parâmetros de tarefa corresponde a uma opção de linha de comando.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|**AdditionalOptions**|Parâmetro **String** opcional.<br /><br /> Uma lista de opções, conforme especificado na linha de comando. Por exemplo, "/*option1* /*option2* /*option#*". Use esse parâmetro para especificar opções não representadas por nenhum outro parâmetro da tarefa **BscMake**.<br /><br /> Para obter mais informações, consulte as opções em [Opções BSCMAKE](http://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2).|  
|**OutputFile**|Parâmetro **String** opcional.<br /><br /> Especifica um nome de arquivo que substitui o nome de arquivo de saída padrão.<br /><br /> Para obter mais informações, consulte a opção **/o** em [Opções BSCMAKE](http://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2).|  
|**PreserveSBR**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, ele forçará um build não incremental. Um build completo não incremental ocorre independentemente de existir um arquivo .bsc e impede que arquivos .sbr sejam truncados.<br /><br /> Para obter mais informações, consulte a opção **/n** em [Opções BSCMAKE](http://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2).|  
|**Sources**|Parâmetro opcional **ITaskItem[]**.<br /><br /> Define uma matriz de itens de arquivo de origem do MSBuild que pode ser consumida e emitida por tarefas.|  
|**SuppressStartupBanner**|Parâmetro **Boolean** opcional.<br /><br /> Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.<br /><br /> Para obter mais informações, consulte a opção **/NOLOGO** em [Opções BSCMAKE](http://msdn.microsoft.com/library/fa2f1e06-c684-41cf-80dd-6a554835ebd2).|  
|**TrackerLogDirectory**|Parâmetro **String** opcional.<br /><br /> Especifica o diretório do log de rastreamento.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



