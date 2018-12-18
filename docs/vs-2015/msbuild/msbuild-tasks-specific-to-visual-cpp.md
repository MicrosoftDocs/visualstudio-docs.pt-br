---
title: Tarefas específicas do MSBuild para o Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to Visual C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1da9bdb5c181c9fd935987d629f08af1505f0501
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49246137"
---
# <a name="msbuild-tasks-specific-to-visual-c"></a>Tarefas do MSBuild específicas ao Visual C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Tarefas fornecem o código que é executado durante o processo de compilação. Quando o Visual C++ é instalado, as tarefas a seguir estão disponíveis, além das que são instaladas com o [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Para obter mais informações, confira [visão geral do MSBuild (Visual C++)](http://msdn.microsoft.com/library/dd258f6f-ab51-48d9-b274-f7ba911d05ca).  
  
 Além dos parâmetros para cada tarefa, todas as tarefas também têm os seguintes parâmetros.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`Condition`|Parâmetro `String` opcional.<br /><br /> A expressão `Boolean` que o mecanismo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] usa para determinar se essa tarefa será executada. Para obter informações sobre as condições que são suportadas pelo [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], confira [Condições](../msbuild/msbuild-conditions.md).|  
|`ContinueOnError`|Parâmetro opcional. Pode conter um dos seguintes valores:<br /><br /> -   **WarnAndContinue** ou **verdadeiro**. Quando uma tarefa falha, as tarefas subsequentes no elemento de [Destino](../msbuild/target-element-msbuild.md) e a compilação continuam em execução, e todos os erros da tarefa são tratados como avisos<br />-   **ErrorAndContinue**. Quando uma tarefa falha, as tarefas subsequentes no elemento de `Target` e o build continuam em execução e todos os erros da tarefa são tratados como erros.<br />-   **ErrorAndStop** ou **falso** (padrão). Quando uma tarefa falha, as tarefas restantes do elemento de `Target` e o build não são executadas e todo o elemento `Target` e a compilação são considerados como com falha.<br /><br /> As versões do .NET Framework antes da 4.5 ofereciam suporte somente aos valores `true` e `false`.<br /><br /> Para obter mais informações, confira [Como: ignorar erros em tarefas](../msbuild/how-to-ignore-errors-in-tasks.md).|  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Tarefa BscMake](../msbuild/bscmake-task.md)|Encapsula a ferramenta do utilitário de manutenção de informações de procura da Microsoft (bscmake.exe).|  
|[Tarefa CL](../msbuild/cl-task.md)|Encapsula a ferramenta do compilador do Visual C++ (cl.exe).|  
|[Tarefa CPPClean](../msbuild/cppclean-task.md)|Exclui os arquivos temporários que o MSBuild cria quando um projeto Visual C++ é criado.|  
|[Tarefa LIB](../msbuild/lib-task.md)|Encapsula a ferramenta gerenciador de biblioteca de 32 bits da Microsoft (lib.exe).|  
|[Tarefa Link](../msbuild/link-task.md)|Encapsula a ferramenta do vinculador do Visual C++ (link.exe).|  
|[Tarefa MIDL](../msbuild/midl-task.md)|Encapsula a ferramenta do compilador da linguagem IDL da Microsoft (MIDL) (midl.exe).|  
|[Tarefa MT](../msbuild/mt-task.md)|Encapsula a Ferramenta de manifesto da Microsoft (mt.exe).|  
|[Tarefa RC](../msbuild/rc-task.md)|Encapsula a ferramenta do compilador de recurso do Microsoft Windows (rc.exe).|  
|[Tarefa SetEnv](../msbuild/setenv-task.md)|Define ou exclui o valor de uma variável de ambiente especificada.|  
|[Tarefa VCMessage](../msbuild/vcmessage-task.md)|Logs de mensagens de erro e mensagens de aviso durante uma compilação.|  
|[Tarefa XDCMake](../msbuild/xdcmake-task.md)|Encerra a ferramenta de documentação XML (xdcmake.exe), que mescla os arquivos de comentários do documento XML (.xdc) em um arquivo .xml.|  
|[Tarefa XSD](../msbuild/xsd-task.md)|Encapsula a ferramenta de definição de esquema XML (xsd.exe), a qual gera arquivos de classe ou de esquema com base em uma origem.|  
|[Referência do MSBuild](../msbuild/msbuild-reference.md)|Descreve os elementos do sistema MSBuild.|  
|[Tarefas](../msbuild/msbuild-tasks.md)|Descreve tarefas que são unidades de código que podem ser combinadas para produzirem uma compilação.|  
|[Escrevendo tarefas](../msbuild/task-writing.md)|Descreve como criar uma tarefa.|



