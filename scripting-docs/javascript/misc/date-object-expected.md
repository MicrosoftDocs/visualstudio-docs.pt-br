---
title: Objeto Date esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5006
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d6ab82e6-ca64-46b4-a06c-5c6b0aa057cb
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 969f2bcb578d74ac02a7bdaa6984de5948e49e27
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817600"
---
# <a name="date-object-expected"></a>Objeto de data esperado
Você tentou invocar o método **Date. prototype. ToString** ou **Date. prototype. valueOf** em um objeto de um tipo diferente de `Date` . O objeto deste tipo de invocação deve ser do tipo `Date` . Por exemplo:  
  
```JavaScript  
var o = new Object;  
o.f = Date.prototype.toString;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Invocar apenas os métodos **Date. prototype. ToString** ou **Date. prototype. valueOf** em objetos do tipo `Date` .  
  
## <a name="see-also"></a>Veja também  
 [Objeto Date](../../javascript/reference/date-object-javascript.md)   
 [Método getDate (Date)](../../javascript/reference/getdate-method-date-javascript.md)   
 [Objetos intrínsecos](../../javascript/intrinsic-objects-javascript.md)