---
description: Você tentou invocar o método Date. prototype. toString ou Date. prototype. valueOf em um objeto de um tipo diferente de Date.
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
ms.openlocfilehash: 171514ae180c2e9b24e8aee56a23c47a909bd152
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571084"
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
  
## <a name="see-also"></a>Confira também  
 [Objeto Date](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)   
 [Método getDate (Date)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date/getdate)   
 [Objetos intrínsecos](https://developer.mozilla.org/docs/Learn/JavaScript/Objects)
