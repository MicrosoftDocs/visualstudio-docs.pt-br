---
description: Obtém o GUID do mecanismo de depuração (DE).
title: 'IDebugEngine2:: getengineid | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::GetEngineID
helpviewer_keywords:
- IDebugEngine2::GetEngineID
ms.assetid: 0d5674c8-a9b9-4b72-8211-d2d68695775a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d7a483517f89c91005f465c539d2af4b9d442a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088023"
---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
Obtém o GUID do mecanismo de depuração (DE).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetEngineID(
    GUID* pguidEngine
);
```

```csharp
int GetEngineID(
    out Guid pguidEngine
);
```

## <a name="parameters"></a>Parâmetros
`pguidEngine`\
fora Retorna o GUID do de.

## <a name="return-value"></a>Valor Retornado
Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
Alguns exemplos de GUIDs típicos são `guidScriptEng` , `guidNativeEng` ou `guidSQLEng` . Novos mecanismos de depuração criarão seu próprio GUID para identificação.

## <a name="example"></a>Exemplo
O exemplo a seguir mostra como implementar esse método para um `CEngine` objeto simples que implementa a interface [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) .

```cpp
HRESULT CEngine::GetEngineId(GUID *pguidEngine) {
    if (pguidEngine) {
        // Set pguidEngine to guidBatEng, as defined in the Batdbg.idl file.
        // Other languages would require their own guidDifferentEngine to be
        //defined in the Batdbg.idl file.
        *pguidEngine = guidBatEng;
        return NOERROR; // This is typically S_OK.
    } else {
        return E_INVALIDARG;
    }
}
```

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
