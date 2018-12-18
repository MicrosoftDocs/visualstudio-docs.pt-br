---
title: 'Método: Readnullterminatedstring | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.ReadNullTerminatedString
apilocation:
- jscript9diag.dll
ms.assetid: 64683b39-6fc2-40c4-82ae-2a6f58d392d5
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 94cb90b8b44aa5dab13a2e916dec22ae950e77ef
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729496"
---
# <a name="ijsdebugdatatargetreadnullterminatedstring-method"></a>Método IJsDebugDataTarget::ReadNullTerminatedString
Lê o número especificado de caracteres de destino.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT ReadNullTerminatedString(  
   UINT64 address,  
   UINT16 characterSize,  
   UINT32 maxCharacters,  
   BSTR *pString  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `address`  
 [in] O endereço para ler.  
  
 `characterSize`  
 [in] o tamanho de cada caractere na cadeia de caracteres  
  
 `maxCharacters`  
 [in] O número máximo de caracteres a serem lidos. maxCharacters devem ser razoável. Qualquer solicitação para mais de 128MB de memória falhará.  Se a cadeia de caracteres for maior que maxCharacters, a cadeia de caracteres de resultado será truncada após maxCharacters.  
  
 `pString`  
 [out] BSTR de leitura do destino.  
  
## <a name="return-value"></a>Valor de retorno  
  
## <a name="remarks"></a>Comentários  
 Retornará S_FALSE se truncado.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** jscript9diag.h  
  
## <a name="see-also"></a>Consulte também  
 [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)