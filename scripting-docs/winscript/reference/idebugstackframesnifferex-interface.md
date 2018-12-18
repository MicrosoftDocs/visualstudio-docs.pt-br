---
title: Interface IDebugStackFrameSnifferEx | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugStackFrameSnifferEx interface
ms.assetid: fd6cf744-dee7-45f2-9a90-355b90372923
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 56d6e63c41db274634b2593989800ea0392b93a6
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726756"
---
# <a name="idebugstackframesnifferex-interface"></a>Interface IDebugStackFrameSnifferEx
Fornece uma maneira para enumerar os quadros de pilha lógico conhecidos por um componente. Mecanismos de script geralmente implementam essa interface. O processo depuração manager usa essa interface para localizar todos os quadros de pilha associado a um determinado thread.  
  
> [!NOTE]
>  Essa interface é chamada de segmento de interesse. A implementação de interface deve identificar o thread atual e retorna um enumerador apropriado.  
  
 Além dos métodos herdados de `IDebugStackFrameSniffer`, o `IDebugStackFrameSnifferEx` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugStackFrameSnifferEx::EnumStackFramesEx](../../winscript/reference/idebugstackframesnifferex-enumstackframesex.md)|Retorna um enumerador de quadros de pilha do thread atual.|