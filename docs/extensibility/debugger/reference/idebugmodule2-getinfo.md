---
description: Obtém informações sobre este módulo.
title: 'IDebugModule2:: GetInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::GetInfo
helpviewer_keywords:
- GetInfo method
- IDebugModule2::GetInfo method
ms.assetid: de337e66-294f-4ac9-b21e-71fac7418e36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69286a7bf50c32aa3aa720deff78ee957f53fc65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065652"
---
# <a name="idebugmodule2getinfo"></a>IDebugModule2::GetInfo
Obtém informações sobre este módulo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetInfo( 
   MODULE_INFO_FIELDS dwFields,
   MODULE_INFO*       pInfo
);
```

```cpp
int GetInfo( 
   enum_MODULE_INFO_FIELDS dwFields,
   MODULE_INFO[]           pInfo
);
```

## <a name="parameters"></a>Parâmetros
`dwFields`\
no Uma combinação de sinalizadores da enumeração [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) que especifica quais campos do `pInfo` devem ser preenchidos.

`pInfo`\
[entrada, saída] Uma estrutura de [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) que é preenchida com uma descrição do módulo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A estrutura de [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) contém o nome do módulo que é exibido na janela **módulos** .

## <a name="see-also"></a>Confira também
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
