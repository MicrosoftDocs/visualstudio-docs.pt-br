---
title: IPerPropertyBrowsing2::GetPredefinedStrings | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2.GetPredefinedStrings
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2::GetPredefinedStrings
ms.assetid: d2fa30f7-a566-4dbd-8b47-ffdc00419771
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5a5f71ba91c65a8d99d831c777fc47fe9233fc18
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58157796"
---
# <a name="iperpropertybrowsing2getpredefinedstrings"></a>IPerPropertyBrowsing2::GetPredefinedStrings
Permite que o chamador preencher uma caixa de listagem com uma matriz contada de ponteiros de cadeia de caracteres que representam os valores possíveis para essa propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetPredefinedStrings(  
   DISPID  dispid,  
   CALPOLESTR*  pCaStrings,  
   CADWORD*  pCaCookies  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dispid`  
 [in] Identificador de expedição da propriedade para o qual o chamador está solicitando a lista de cadeia de caracteres.  
  
 `pCaStrings`  
 [out] Ponteiro para uma estrutura de matriz alocada pelo chamador, contado que contém a contagem de elemento e o endereço de uma matriz alocada pelo método de ponteiros de cadeia de caracteres. Se o método falhar, nenhuma memória é alocada, e o conteúdo da estrutura é indefinido.  
  
 `pCaCookies`  
 [out] Ponteiro para a estrutura de matriz alocada pelo chamador, contado que contém a contagem de elemento e o endereço de uma matriz alocada pelo método de DWORDs. Se o método falhar, nenhuma memória é alocada, e o conteúdo da estrutura é indefinido.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um válidas `HRESULT`, normalmente `S_OK`.  
  
## <a name="see-also"></a>Consulte também  
 [Interface 1 IPerPropertyBrowsing2](../../winscript/reference/iperpropertybrowsing2-interface-1.md)