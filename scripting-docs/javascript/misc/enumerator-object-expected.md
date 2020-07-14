---
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
ms.openlocfilehash: ff61894ce808cd33876e876c596e791a3347ab72
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817587"
---
# <a name="enumerator-object-expected"></a>Objeto enumerador esperado
Você tentou invocar o método **enumerador. prototype. atEnd, Enumerator. prototype. Item, enumerador. prototype. MoveFirst** ou **enumerador. prototype. MoveNext** em um objeto de um tipo diferente de `Enumerator` . O objeto deste tipo de invocação deve ser do tipo `Enumerator` . Aqui está um exemplo de código que interrompe esta regra:  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Invoque somente os métodos **Enumerator. prototype. atEnd**, **enumerador. prototype. Item**, **enumerador. prototype. MoveFirst**ou **enumerador. prototype. MoveNext** em objetos do tipo `Enumerator` . Para descobrir se o objeto é um `Enumerator` objeto, use:  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>Veja também  
 [Objeto Enumerator](../../javascript/reference/enumerator-object-javascript.md)