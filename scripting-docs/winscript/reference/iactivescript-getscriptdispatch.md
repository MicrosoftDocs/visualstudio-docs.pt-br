---
title: IActiveScript::GetScriptDispatch | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptDispatch
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptDispatch
ms.assetid: 2092ccd4-1f4c-493a-b5b7-077a70ce95ca
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5b2f09934cf6d2bb28f7dae93d0bf49c8dc7437d
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641426"
---
# <a name="iactivescriptgetscriptdispatch"></a>IActiveScript::GetScriptDispatch
Recupera o `IDispatch` interface para os métodos e propriedades associadas com o script em execução no momento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetScriptDispatch(  
    LPCOLESTR pstrItemName  // address of item name  
    IDispatch **ppdisp      // receives IDispatch pointer  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrItemName`  
 [in] Endereço de um buffer que contém o nome do item para o qual o chamador precisa o objeto de expedição associado. Se esse parâmetro for `NULL`, contém o objeto de expedição como seus membros de todas as propriedades e métodos globais definidas pelo script. Por meio de `IDispatch` interface e associado `ITypeInfo` interface, o host pode invocar métodos de script ou exibir e modificar variáveis de script.  
  
 `ppdisp`  
 [out] Endereço de uma variável que recebe um ponteiro para o objeto associado com propriedades e métodos globais do script. Se o mecanismo de script não dá suporte a tipo de objeto, `NULL` será retornado.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
|`S_FALSE`|O mecanismo de script não dá suporte a um objeto de expedição; o `ppdisp` parâmetro for definido como NULL.|  
  
## <a name="remarks"></a>Comentários  
 Porque os métodos e propriedades que podem ser adicionadas ao chamar o [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md) interface, o `IDispatch` retornado por esse método de interface dinamicamente pode dar suporte a novos métodos e propriedades. Da mesma forma, o `IDispatch::GetTypeInfo` método deve retornar um novo, exclusivo `ITypeInfo` interface quando os métodos e propriedades são adicionadas. No entanto, observe que os mecanismos de linguagem não devem alterar o `IDispatch` interface em uma maneira que é incompatível com qualquer anterior `ITypeInfo` interface retornado. Por exemplo, que implica que DISPIDs nunca seja reutilizados.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)