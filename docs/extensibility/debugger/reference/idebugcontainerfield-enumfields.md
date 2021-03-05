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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 68ec12cd97318fc41b97c5a7701dff2346524101
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143162"
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
