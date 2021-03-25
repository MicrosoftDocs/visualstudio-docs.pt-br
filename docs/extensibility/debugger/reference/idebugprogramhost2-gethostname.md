---
description: Obtém o título, nome amigável ou nome de arquivo do processo de hospedagem deste programa.
title: 'IDebugProgramHost2:: GetHostName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53b4d69be1ea24f5c240b6247539f499c9fb00fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084006"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
Obtém o título, nome amigável ou nome de arquivo do processo de hospedagem deste programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetHostName( 
   DWORD dwType,
   BSTR* pbstrHostName
);
```

```csharp
int GetHostName( 
   uint dwType,
   out string pbstrHostName
);
```

## <a name="parameters"></a>Parâmetros
`dwType`\
no Um valor da enumeração de [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md) .

`pbstrHostName`\
fora Retorna o nome solicitado do processo de hospedagem.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Em uma implementação típica desse método, o `dwType` parâmetro é ignorado e um nome amigável do computador host é retornado. Outra implementação possível é passar o `dwType` parâmetro para uma chamada para o método [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) para obter o nome.

## <a name="see-also"></a>Confira também
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
