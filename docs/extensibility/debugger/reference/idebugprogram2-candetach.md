---
title: IDebugProgram2::CanDetach | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5285dce44c7aacad12fad60f255140a14d53a8d7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857530"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
Determina se um mecanismo de depuração (DES) poderá desanexar do programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CanDetach(  
   void  
);  
```  
  
```csharp  
int CanDetach();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Se desanexar retorna `S_OK`; caso contrário, retorna um código de erro. Retorna `S_FALSE` se a DE não é possível desanexar do programa.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)