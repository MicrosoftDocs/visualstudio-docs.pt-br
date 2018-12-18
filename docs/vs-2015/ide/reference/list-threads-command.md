---
title: Comando Listar Threads | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- debug.listthreads
helpviewer_keywords:
- ListThreads command
- list threads command
- Debug.ListThreads command
ms.assetid: 34b665c0-d46f-4c1a-a066-b678eba5ac54
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7ffad16bc121582b4f8a8ec4c58ac44aa2449617
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49286657"
---
# <a name="list-threads-command"></a>Comando Listar Threads
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Exibe uma lista dos threads no programa atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Debug.ListThreads [index]  
```  
  
## <a name="arguments"></a>Arguments  
 `index`  
 Opcional. Seleciona um thread pelo seu índice para o thread atual.  
  
## <a name="remarks"></a>Comentários  
 Quando especificado, o argumento `index` marca o thread indicado como o thread atual. Um asterisco (*) é exibido na lista ao lado do thread atual.  
  
## <a name="example"></a>Exemplo  
  
```  
>Debug.ListThreads   
```  
  
## <a name="see-also"></a>Consulte também  
 [Comando List Call Stack](../../ide/reference/list-call-stack-command.md)   
 [Comando Listar Desmontagem](../../ide/reference/list-disassembly-command.md)   
 [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)   
 [Janela Comando](../../ide/reference/command-window.md)   
 [Caixa Localizar/Comando](../../ide/find-command-box.md)   
 [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)



