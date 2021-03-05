---
description: Obtém as propriedades do programa.
title: 'IDebugProgram2:: getdebugproperty | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0114d0cf51769d6162563f6c60d51a3f031e19e2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159946"
---
# <a name="idebugprogram2getdebugproperty"></a>IDebugProgram2::GetDebugProperty
Obtém as propriedades do programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDebugProperty( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>Parâmetros
`ppProperty`\
fora Retorna um objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) que representa as propriedades do programa.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 As propriedades retornadas por esse método são específicas para o programa. Se o programa precisar retornar mais de uma propriedade, o objeto [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) retornado por esse método será um contêiner de propriedades adicionais e chamar o método [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) retornará uma lista de todas as propriedades.

 Um programa pode expor qualquer número e tipo de propriedades adicionais que podem ser descritas por meio da `IDebugProperty2` interface. Um IDE pode exibir as propriedades de programa adicionais por meio de uma interface de usuário do navegador de propriedades genérico.

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
