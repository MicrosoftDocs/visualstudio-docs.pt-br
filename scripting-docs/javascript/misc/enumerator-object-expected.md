---
description: Você tentou invocar o método enumerador. prototype. atEnd, Enumerator. prototype. Item, enumerador. prototype. moveFirst ou enumerador. prototype. moveNext em um objeto de um tipo diferente de enumerador.
title: Objeto enumerador esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5015
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: dc6e32c1-a6e6-4e12-ac99-e3f65f91c8d7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9fc48ca3e0f17d97af3d538033c2319538afc079
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571045"
---
# <a name="enumerator-object-expected"></a>Objeto enumerador esperado
Você tentou invocar o método **enumerador. prototype. atEnd, Enumerator. prototype. Item, enumerador. prototype. MoveFirst** ou **enumerador. prototype. MoveNext** em um objeto de um tipo diferente de `Enumerator` . O objeto deste tipo de invocação deve ser do tipo `Enumerator` . Aqui está um exemplo de código que interrompe esta regra:  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Invoque somente os métodos **Enumerator. prototype. atEnd**, **enumerador. prototype. Item**, **enumerador. prototype. MoveFirst** ou **enumerador. prototype. MoveNext** em objetos do tipo `Enumerator` . Para descobrir se o objeto é um `Enumerator` objeto, use:  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>Confira também  
 [Objeto Enumerator](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/Enumerator)
