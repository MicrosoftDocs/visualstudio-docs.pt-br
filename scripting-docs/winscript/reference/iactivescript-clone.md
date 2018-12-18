---
title: IActiveScript::Clone | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.Clone
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_Clone
ms.assetid: aa000b2a-7085-448d-a422-f7adac7851cb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4b0b83bcf86bcc56701d11f22640df966334697b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641586"
---
# <a name="iactivescriptclone"></a>IActiveScript::Clone
Clona o mecanismo de script atual (menos qualquer estado de execução atual), retornando um mecanismo de script carregado que não tem nenhum site no thread atual. As propriedades desse novo mecanismo de script será idênticas para as propriedades que do mecanismo de script original estaria em se foram uma transição para o estado inicializado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Clone(  
    IActiveScript **ppscript  // receives pointer to IActiveScript  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppscript`  
 [out] Endereço de uma variável que recebe um ponteiro para o [IActiveScript](../../winscript/reference/iactivescript.md) interface do mecanismo de script clonado. O host deve criar um site e a chamada a [IActiveScript::SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md) método sobre o novo mecanismo de script antes de ele estar no estado inicializado e, portanto, utilizável.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_NOTIMPL`|Não há suporte para o método.|  
|`E_POINTER`|Um ponteiro inválido foi especificado.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
  
## <a name="remarks"></a>Comentários  
 O `IActiveScript::Clone` método é uma otimização de `IPersist*::Save`, `CoCreateInstance`, e `IPersist*::Load`, portanto, o estado do mecanismo de script novo deve ser o mesmo que o estado do mecanismo de script original foram salvos e carregado em um novo mecanismo de script. Itens nomeados são duplicados no mecanismo de script clonado, mas ponteiros para objetos específicos para cada item são esquecidos e são obtidos com o [IActiveScriptSite::GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md) método. Isso permite que um modelo de objeto idênticas com pontos de entrada por thread (um modelo de apartment) a ser usado.  
  
 Esse método é usado para hosts de servidor multi-threaded que podem executar várias instâncias do mesmo script. O mecanismo de script pode retornar `E_NOTIMPL`, caso em que o host pode alcançar o mesmo resultado duplicando o estado persistente e criando uma nova instância do mecanismo de script com um `IPersist*` interface.  
  
 Esse método pode ser chamado de threads não base sem resultando em um texto explicativo de base não a objetos de host ou para o [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)