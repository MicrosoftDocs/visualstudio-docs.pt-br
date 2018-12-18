---
title: Objeto de data esperado | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- javascript
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.WebClient.Help.SCRIPT5006
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d6ab82e6-ca64-46b4-a06c-5c6b0aa057cb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 05e27b822f933ade811084552f6f0379257ae82e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49947635"
---
# <a name="date-object-expected"></a>Objeto de data esperado
Você tentou invocar o **Date.prototype.toString** ou **Date.prototype.valueOf** método em um objeto de um tipo diferente de `Date`. O objeto desse tipo de invocação deve ser do tipo `Date`. Por exemplo:  
  
```JavaScript  
var o = new Object;  
o.f = Date.prototype.toString;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Invoque apenas o **Date.prototype.toString** ou **Date.prototype.valueOf** métodos em objetos do tipo `Date`.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Date](../../javascript/reference/date-object-javascript.md)   
 [Método getDate (Date)](../../javascript/reference/getdate-method-date-javascript.md)   
 [Objetos intrínsecos](../../javascript/intrinsic-objects-javascript.md)