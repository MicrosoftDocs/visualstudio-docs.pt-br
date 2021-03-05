---
description: Define o valor dessa propriedade como o valor da referência fornecida.
title: 'IDebugProperty2:: SetValueAsReference | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b5b9529a4e4cd56a2b354eaa7f847db4d9d82be1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166743"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
Define o valor dessa propriedade como o valor da referência fornecida.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetValueAsReference(
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```csharp
int SetValueAsReference(
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>Parâmetros
`rgpArgs`\
no Uma matriz de argumentos para passar para o setter de propriedade de código gerenciado. Se o setter da propriedade não usar argumentos ou se esse objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) não fizer referência a tal setter de propriedade, `rgpArgs` deverá ser um valor nulo. Esse parâmetro é normalmente um valor nulo.

`dwArgCount`\
no O número de argumentos na `rgpArgs` matriz.

`pValue`\
no Uma referência, na forma de um objeto [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) , ao valor a ser usado para definir essa propriedade.

`dwTimeout`\
no Quanto tempo levar para definir o valor, em milissegundos. Um valor típico é `INFINITE` . Isso afeta o período de tempo que qualquer avaliação possível pode tomar.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro, normalmente um dos seguintes:

|Erro|Descrição|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|Não há suporte para a definição do valor de uma referência.|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|O valor não pode ser definido, pois essa propriedade se refere a um método.|
|`E_SETVALUE_VALUE_IS_READONLY`|O valor é somente leitura e não pode ser definido.|
|`E_NOTIMPL`|O método não está implementado.|

## <a name="see-also"></a>Confira também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
