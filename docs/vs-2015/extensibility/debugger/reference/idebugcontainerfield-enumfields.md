---
title: IDebugContainerField::EnumFields | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 485de4bdc9ff5b17c056c0db4e2930f5c6986fe7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205303"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Cria um enumerador para os campos do contêiner.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
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
  
#### <a name="parameters"></a>Parâmetros  
 `dwKindFilter`  
 [in] Uma combinação de [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) constantes que selecione os campos a serem enumerados. Tipos de campo podem descrever os tipos de armazenamento, como classe ou informações primitivas ou específicas, como local, parâmetro ou ponteiro "this".  
  
 `dwModifiersFilter`  
 [in] Uma combinação de [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) constantes que selecione os campos a serem enumerados. Modificadores de campo podem ser permissões de acesso, como público ou privado ou informações de armazenamento, como virtual, estático ou final.  
  
 `pszNameFilter`  
 [in] O nome do campo a ser enumerado. Isso pode ser um valor nulo se todos os campos devem ser retornados.  
  
 `nameMatch`  
 [in] Um valor a partir de [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) enumeração que controla se a pesquisa diferencia maiusculas de minúsculas ou não.  
  
 `ppEnum`  
 [out] Retorna um [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) objeto que representa a lista de campos. Retorna um valor nulo se não houver nenhum campo.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, Retorna S_OK ou S_FALSE se não houver nenhum campo. Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O `dwKindFilter`, `dwModifiersFilter`, e `pszNameFilter` parâmetros podem ser combinados, por exemplo, para selecionar todos os métodos virtuais públicos denominados "MyMethod".  
  
## <a name="see-also"></a>Consulte também  
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)   
 [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)   
 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
