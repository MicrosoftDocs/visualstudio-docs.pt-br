---
description: Cria um enumerador para os campos do contêiner.
title: 'IDebugContainerField:: EnumFields | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63ce34fc9eddec84326982cf7d30fda919817040
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077922"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
Cria um enumerador para os campos do contêiner.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumFields( 
   FIELD_KIND         dwKindFilter,
   FIELD_MODIFIERS    dwModifiersFilter,
   LPCOLESTR          pszNameFilter,
   NAME_MATCH         nameMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumFields(
   enum_ FIELD_KIND      dwKindFilter,
   enum_ FIELD_MODIFIERS dwModifiersFilter,
   string                pszNameFilter,
   NAME_MATCH            nameMatch,
   out IEnumDebugFields  ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`dwKindFilter`\
no Uma combinação de [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) constantes que selecionam os campos a serem enumerados. Os tipos de campo podem descrever os tipos de armazenamento, como classe ou primitivo, ou informações específicas, como ponteiro local, parâmetro ou "This".

`dwModifiersFilter`\
no Uma combinação de [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) constantes que selecionam os campos a serem enumerados. Os modificadores de campo podem ser permissões de acesso, como pública ou privada, ou informações de armazenamento, como virtual, estática ou final.

`pszNameFilter`\
no O nome do campo a ser enumerado. Isso pode ser um valor nulo se todos os campos forem retornados.

`nameMatch`\
no Um valor da enumeração [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) que controla se a pesquisa diferencia maiúsculas de minúsculas ou não.

`ppEnum`\
fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de campos. Retorna um valor nulo se não houver campos.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou S_FALSE se não houver campos. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Os `dwKindFilter` `dwModifiersFilter` parâmetros,, e `pszNameFilter` podem ser combinados, por exemplo, para selecionar todos os métodos virtuais públicos chamados "meumetodo".

## <a name="see-also"></a>Confira também
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
