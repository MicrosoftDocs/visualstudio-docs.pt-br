---
description: Cria uma instância de um mecanismo de depuração no servidor.
title: 'IDebugCoreServer3:: CreateInstanceInServer | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc3a24e28c378bda34034822aedf4d35e5a6313e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154672"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
Cria uma instância de um mecanismo de depuração no servidor.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreateInstanceInServer(
   LPCWSTR  szDll,
   WORD     wLangId,
   REFCLSID clsidObject,
   REFIID   riid,
   void**   ppvObject
);
```

```csharp
int CreateInstanceInServer(
   string     szDll,
   ushort     wLangID,
   ref Guid   clsidObject,
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>Parâmetros
`szDll`\
no Caminho para a DLL que implementa o CLSID especificado no `clsidObject` parâmetro. Se for `NULL` , a função de com `CoCreateInstance` será chamada.

`wLangId`\
no Localidade do mecanismo de depuração. Isso pode ser 0 se o método [Setlocaling](../../../extensibility/debugger/reference/idebugengine2-setlocale.md) não deve ser chamado.

`clsidObject`\
no CLSID do mecanismo de depuração a ser criado.

`riid`\
no ID da interface específica a ser recuperada do objeto de classe.

`ppvObject`\
[fora] `IUnknown` interface do objeto instanciado. Converta ou realize marshaling deste objeto para a interface desejada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)
