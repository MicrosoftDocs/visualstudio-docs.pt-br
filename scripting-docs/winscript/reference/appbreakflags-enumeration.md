---
title: Enumeração APPBREAKFLAGS | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- APPBREAKFLAGS
apilocation:
- scrobj.dll
helpviewer_keywords:
- APPBREAKFLAGS constants
ms.assetid: ea8ed80f-2ddb-4800-bb3b-52b76ba6c7a0
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 126dcd704a60b591b71913f2e8e739de35c14636
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641676"
---
# <a name="appbreakflags-enumeration"></a>Enumeração APPBREAKFLAGS
Indica o estado atual da depuração para aplicativos e threads.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum enum_APPBREAKFLAGS{APPBREAKFLAG_DEBUGGER_BLOCK= 0x00000001,APPBREAKFLAG_DEBUGGER_HALT= 0x00000002,APPBREAKFLAG_STEP= 0x00010000,APPBREAKFLAG_NESTED= 0x00020000,APPBREAKFLAG_STEPTYPE_SOURCE= 0x00000000,APPBREAKFLAG_STEPTYPE_BYTECODE= 0x00100000,APPBREAKFLAG_STEPTYPE_MACHINE= 0x00200000,APPBREAKFLAG_STEPTYPE_MASK= 0x00F00000,APPBREAKFLAG_IN_BREAKPOINT= 0x80000000};  
```  
  
## <a name="members"></a>Membros  
  
|Membro|Valor|Descrição|  
|------------|-----------|-----------------|  
|APPBREAKFLAG_DEBUGGER_BLOCK|0x00000001|Mecanismo de linguagem deve interromper imediatamente em todos os threads com BREAKREASON_DEBUGGER_BLOCK.|  
|APPBREAKFLAG_DEBUGGER_HALT|0x00000002|Mecanismo de linguagem deve interromper imediatamente com BREAKREASON_DEBUGGER_HALT.|  
|APPBREAKFLAG_STEP|0x00010000|Mecanismo de linguagem deve interromper imediatamente no thread de revisão com BREAKREASON_STEP.|  
|APPBREAKFLAG_NESTED|0x00020000|O aplicativo está em execução aninhada em um ponto de interrupção.|  
|APPBREAKFLAG_STEPTYPE_SOURCE|0x00000000|O depurador está entrando no nível de fonte.|  
|APPBREAKFLAG_STEPTYPE_BYTECODE|0x00100000|O depurador está entrando no nível de código de bytes.|  
|APPBREAKFLAG_STEPTYPE_MACHINE|0x00200000|O depurador está entrando no nível do computador.|  
|APPBREAKFLAG_STEPTYPE_MASK|0x00F00000|Determinando os tipos de etapa máscara.|  
|APPBREAKFLAG_IN_BREAKPOINT|0x80000000|Um ponto de interrupção está em andamento.|  
  
## <a name="remarks"></a>Comentários  
 Alguns sinalizadores de especificam que os mecanismos de idioma devem haver uma quebra na próxima oportunidade, enquanto outros sinalizadores de especificar o modo de depuração do depurador.  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas, enumerações e constantes do depurador de Script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)   
 [BREAKREASON Enumeration](../../winscript/reference/breakreason-enumeration.md)