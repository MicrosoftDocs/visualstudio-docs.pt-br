---
title: IDebugCoreServer3::QueryIsLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::QueryIsLocal
helpviewer_keywords:
- IDebugCoreServer3::QueryIsLocal
ms.assetid: cca030de-f853-4ed7-b2fb-395f08a6b884
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26bed2a60d7412682588a5a39fd6f1301005da01
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62569070"
---
# <a name="idebugcoreserver3queryislocal"></a>IDebugCoreServer3::QueryIsLocal
Determina se o servidor é local para o chamador.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT QueryIsLocal(
   void
);
```

```csharp
int QueryIsLocal();
```

## <a name="return-value"></a>Valor de retorno
 Retorna `S_OK` para indicar que o servidor é local. Retorna `S_FALSE` se o servidor estiver em execução de uma instância do msvsmon.exe, que normalmente é usado para depuração remota.

## <a name="see-also"></a>Consulte também
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)