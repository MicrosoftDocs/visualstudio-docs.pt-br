---
title: IDebugBeforeSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 26a8d7b28528a79a925207e1ee3794fcbb4ca1d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423511"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

O mecanismo de depuração (DE) envia essa interface para o SDM (Gerenciador de depuração de sessão) para definir a mensagem da barra de status durante cargas de símbolo.  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugBeforeSymbolSearchEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Notas para implementadores  
 O DE implementa essa interface quando ela deve definir a mensagem da barra de status durante cargas de símbolo. Essa interface é implementada somente por mecanismos de depuração que funcionam com o ou fazem parte de intérpretes de script. A interface [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) deve ser implementada no mesmo objeto que essa interface (o SDM usa **QueryInterface** para acessar a interface **IDebugEvent2** ).  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 O DE cria e envia esse objeto DE evento quando ele deve definir a mensagem da barra de status durante cargas de símbolo. O evento é enviado usando a função de retorno de chamada [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) fornecida pelo SDM quando ele é anexado ao programa que está sendo depurado.  
  
## <a name="methods"></a>Métodos  
 A tabela a seguir mostra os métodos de `IDebugBeforeSymbolSearchEvent2` .  
  
|Método|Descrição|  
|------------|-----------------|  
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|Recupera o nome do módulo que está sendo depurado no momento.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: Msdbg. h  
  
 Namespace: Microsoft. VisualStudio. Debugger. Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
