---
title: IDebugProgram2::EnumModules | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumModules
helpviewer_keywords:
- IDebugProgram2::EnumModules
ms.assetid: 876ac9da-3b7c-4156-b79a-8f340e9fcea6
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e8de1f98cb6953ba713796e1dbd74de849a0aaf7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917299"
---
# <a name="idebugprogram2enummodules"></a>IDebugProgram2::EnumModules
Recupera uma lista dos módulos que este programa foi carregado e está em execução.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumModules( 
   IEnumDebugModules2** ppEnum
);
```

```csharp
int EnumModules( 
   out IEnumDebugModules2 ppEnum
);
```

#### <a name="parameters"></a>Parâmetros
 `ppEnum`

 [out] Retorna um [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) objeto que contém uma lista dos módulos.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Um módulo é uma DLL ou um assembly e normalmente é listado na **módulos** janela de depuração.

## <a name="see-also"></a>Consulte também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)