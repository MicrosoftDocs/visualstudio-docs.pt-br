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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60e551829a1f424a9bb7f89642f1d692db8d8032
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075972"
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
