---
title: IVariantChangeType::ChangeType | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IVariantChangeType.ChangeType
apilocation:
- scrobj.dll
helpviewer_keywords:
- IVariantChangeType::ChangeType
ms.assetid: 52374764-c42e-49af-a219-ee00c535a118
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d742d1bd57c85aa75c9ccd60479d08c1a559fb37
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734196"
---
# <a name="ivariantchangetypechangetype"></a>IVariantChangeType::ChangeType
Usa um valor variant e cria uma nova variante com um tipo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ChangeType(  
   VARIANT*  pvarDst,  
   VARIANT*  pvarSrc,  
   LCID  lcid,  
   VARTYPE  vtNew  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pvarDst`  
 [out no] Um tipo variant para conter o valor representado pelo `pvarSrc`, mas com o tipo especificado pelo `vtNew`.  
  
 `pvarSrc`  
 [in] Um valor variant para alterar para um novo tipo.  
  
 `lcid`  
 [in] O contexto de localidade a ser usada ao converter os argumentos de ou cadeias de caracteres.  
  
 `vtNew`  
 [in] Especifica o tipo de `pvarDst` seja.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 O `pvarDst` e `pvarSrc` argumentos podem ser iguais, caso em que o valor original é substituído. Esse método passa `pvarDst` para o `VariantClear` função e, consequentemente, `pvarDst` deve ser inicializado para um valor válido.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IVariantChangeType](../../winscript/reference/ivariantchangetype-interface.md)