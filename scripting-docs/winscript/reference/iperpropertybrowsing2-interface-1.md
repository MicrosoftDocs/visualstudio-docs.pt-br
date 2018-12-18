---
title: Interface IPerPropertyBrowsing2 1 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IPerPropertyBrowsing2
apilocation:
- scrobj.dll
helpviewer_keywords:
- IPerPropertyBrowsing2 interface
ms.assetid: 1e50b3f7-cc1c-495a-93c7-3ee03aea0b8a
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 75a0a7ef30bca2205789a63ea577808c11582791
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728386"
---
# <a name="iperpropertybrowsing2-interface-1"></a>Interface IPerPropertyBrowsing2 1
Acessa as informações nas páginas de propriedade oferecidos por um objeto.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|`GetDisplayString`|Retorna uma cadeia de caracteres de texto que descreve a propriedade especificada.|  
|`MapPropertyToPage`|Retorna o CLSID da página de propriedades que permite a manipulação da propriedade especificada.|  
|`GetPredefinedStrings`|Retorna uma matriz de cadeias de caracteres de contado (`LPOLESTR` ponteiros) listando as descrições dos valores permitidos que pode aceitar a propriedade especificada.|  
|`SetPredefinedValue`|Define o valor da propriedade para o valor predefinido identificado pelo token`dwCookie.`|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: dbgprop.h