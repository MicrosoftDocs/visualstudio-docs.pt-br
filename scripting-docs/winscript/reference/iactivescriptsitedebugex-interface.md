---
title: Interface IActiveScriptSiteDebugEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSiteDebugEx Interface
ms.assetid: 76869378-1a7b-47bd-8cd0-acc31f91d58d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2cf5849ff1fca282bace97774c6b7ac9e4510226
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725036"
---
# <a name="iactivescriptsitedebugex-interface"></a>Interface IActiveScriptSiteDebugEx
Implementar essa interface junto com o `IActiveScriptSiteDebug` se você estiver escrevendo um host que deve receber uma notificação de um erro de tempo de execução em um aplicativo e opcionalmente anexar ao aplicativo para depuração de interface. O Gerenciador de depuração do processo fornece notificação por meio de `IActiveScriptDebug` se o depurador de script de um Just-In-Time foi encontrado no computador. Se o depurador de script sem Just-In-Time é encontrado, o PDM fornece notificação por meio de `IActiveScriptDebugEx` em vez disso.  
  
 Para obter uma notificação de um erro de tempo de execução, o host deve tratar [ActiveScriptSiteDebug::OnScriptErrorDebug](http://msdn.microsoft.com/en-us/cf7639f9-a699-4571-9f3a-82ef52c0b5f4). Com base em uma ação do usuário, você pode, em seguida, decidir se anexar o depurador interno e o retorno ou retornar a partir do depurador no OnScriptErrorDebug `pfEnterDebugger` parâmetro.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug](../../winscript/reference/iactivescriptsitedebugex-oncannotjitscripterrordebug.md)|Informa o host sobre um erro de tempo de execução do script quando o processo de depurar Gerenciador não encontrar um depurador apenas tempo externo.|