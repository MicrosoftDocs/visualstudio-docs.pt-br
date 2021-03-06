---
description: Essa estrutura é usada para definir as informações de JustMyCode para um módulo.
title: JMC_CODE_SPEC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- JMC_CODE_SPEC
helpviewer_keywords:
- JMC_CODE_SPEC structure
ms.assetid: d89498f1-4234-46d9-b4e2-abbcbca5068a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6c862a2897b45d89f95963ce7adfe2da8d4d350f
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225559"
---
# <a name="jmc_code_spec"></a>JMC_CODE_SPEC
Essa estrutura é usada para definir as informações de JustMyCode para um módulo.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _JMC_CODE_SPEC {
    BOOL fIsUserCode;
    BSTR bstrModuleName;
} JMC_CODE_SPEC;
```

```csharp
public struct JMC_CODE_SPEC {
    public int    fIsUserCode;
    public string bstrModuleName;
};
```

## <a name="members"></a>Membros
`fIsUserCode`\
Diferente de zero ( `TRUE` ) se o módulo for considerado código de usuário; caso contrário, será zero ( `FALSE` ) se o módulo for tratado como código externo e não deve ser depurado.

`bstrModuleName`\
Nome do módulo em questão.

## <a name="remarks"></a>Comentários
Essa estrutura é passada como uma lista de tais estruturas para o método [SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: msdbg. h

Namespace: Microsoft. VisualStudio. Debugger. Interop

Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)
