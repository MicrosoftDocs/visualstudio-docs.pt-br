---
title: Interface IDebugStackFrameSniffer | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugStackFrameSniffer interface
ms.assetid: 5669598e-a6bd-4694-9cb2-bd908be72bed
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 250c104d24f27900a6ff0eb8e8f72644f820bf5a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726796"
---
# <a name="idebugstackframesniffer-interface"></a>Interface IDebugStackFrameSniffer
Fornece uma maneira para enumerar os quadros de pilha lógico conhecidos por um componente. Mecanismos de script geralmente implementam essa interface. O processo depuração manager usa essa interface para localizar todos os quadros de pilha associado a um determinado thread.  
  
> [!NOTE]
>  O depurador chama essa interface de dentro do segmento de interesse. O mecanismo de script deve identificar o thread atual e retorna um enumerador apropriado.  
  
## <a name="methods"></a>Métodos  
 Além dos métodos herdados de `IUnknown`, o `IDebugStackFrameSniffer` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugStackFrameSniffer::EnumStackFrames](../../winscript/reference/idebugstackframesniffer-enumstackframes.md)|Retorna um enumerador de quadros de pilha do thread atual.|