---
title: IActiveScriptSite::GetItemInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.GetItemInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_GetItemInfo
ms.assetid: f859ed3b-02c1-4924-99f8-5f5bf1bf8405
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ccb898c14571d1f1fd1fcae7cb0b9a6d322f2754
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725416"
---
# <a name="iactivescriptsitegetiteminfo"></a>IActiveScriptSite::GetItemInfo
Permite que o mecanismo de script obter informações sobre um item adicionado com o [IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetItemInfo(  
    LPCOLESTR pstrName,     // address of item name  
    DWORD dwReturnMask,     // bit mask for information retrieval  
    IUnknown **ppunkItem,   // address of pointer to item's IUnknown  
    ITypeInfo **ppTypeInfo  // address of pointer to item's ITypeInfo  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrName`  
 [in] O nome associado ao item, como especificado no [IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) método.  
  
 `dwReturnMask`  
 [in] Uma máscara de bits que especifica quais informações sobre o item devem ser retornadas. O mecanismo de script deve solicitar a quantidade mínima de informações possível porque alguns dos parâmetros de retorno (por exemplo, `ITypeInfo`) pode levar um tempo considerável para carregar ou gerar. Pode ser uma combinação dos seguintes valores:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTINFO_IUNKNOWN|Retorna o `IUnknown` interface para este item.|  
|SCRIPTINFO_ITYPEINFO|Retorna o `ITypeInfo` interface para este item.|  
  
 `ppunkItem`  
 [out] Endereço de uma variável que recebe um ponteiro para o `IUnknown` interface associada ao item determinado. O mecanismo de script pode usar o `IUnknown::QueryInterface` método para obter o `IDispatch` interface para o item. Esse parâmetro recebe NULL se `dwReturnMask` não inclui o valor SCRIPTINFO_IUNKNOWN. Além disso, ele recebe NULL se não houver nenhum objeto associado com o nome de item. Esse mecanismo é usado para criar uma classe simples quando o objeto nomeado foi adicionado com o sinalizador SCRIPTITEM_CODEONLY definido [IActiveScript::AddNamedItem](../../winscript/reference/iactivescript-addnameditem.md) método.  
  
 `ppTypeInfo`  
 [out] Endereço de uma variável que recebe um ponteiro para o `ITypeInfo` associado ao item de interface. Esse parâmetro recebe NULL se `dwReturnMask` não inclui o valor SCRIPTINFO_ITYPEINFO, ou se as informações de tipo não estão disponíveis para este item. Se as informações de tipo não estão disponíveis, o objeto não é possível fonte de eventos e associação de nome deve ser realizada com o `IDispatch::GetIDsOfNames` método. Observe que o `ITypeInfo` interface recuperado descreve coclass do item (TKIND_COCLASS) como o objeto pode dar suporte a várias interfaces e eventos. Se o item oferece suporte a `IProvideMultipleTypeInfo` interface, o `ITypeInfo` interface recuperado é o mesmo que o índice zero `ITypeInfo` que deve ser obtido usando o `IProvideMultipleTypeInfo::GetInfoOfIndex` método.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`TYPE_E_ELEMENTNOTFOUND`|Um item do nome especificado não foi encontrado.|  
  
## <a name="remarks"></a>Comentários  
 Esse método recupera apenas as informações indicadas pelo `dwReturnMask` parâmetro; Isso melhora o desempenho. Por exemplo, se um `ITypeInfo` interface não é necessária para um item, simplesmente não for especificado em `dwReturnMask`.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)