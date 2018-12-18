---
title: IPerPropertyBrowsing2::GetDisplayString | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2.GetDisplayString
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2::GetDisplayString
ms.assetid: 8f75c6a9-86a9-4e2d-8cb4-74e7b1c0a524
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: be88a76ce22dfd863e680fcc1a6794065ecaf76f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836873"
---
# <a name="iperpropertybrowsing2getdisplaystring"></a>IPerPropertyBrowsing2::GetDisplayString
Obtém uma cadeia de caracteres para exibir tipos que não são inerentemente visíveis o texto retornado é um nome que descreve a propriedade e pode ser exibida na interface do usuário do chamador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetDisplayString(  
   DISPID  dispid,  
   BSTR*  pBstr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dispid`  
 [in] Despache o identificador da propriedade cujo nome de exibição é solicitado.  
  
 `pBstr`  
 [out] Ponteiro para o `BSTR` que contém o nome de exibição para a propriedade identificada por `dispID`.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um válidas `HRESULT`, normalmente `S_OK`.  
  
## <a name="remarks"></a>Comentários  
 A cadeia de caracteres retornada não é um valor válido da propriedade. Ele é apenas uma exibição de cadeia de caracteres da propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Interface 1 IPerPropertyBrowsing2](../../winscript/reference/iperpropertybrowsing2-interface-1.md)