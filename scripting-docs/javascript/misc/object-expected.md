---
title: Objeto esperado | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5007
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d88c93d-e5b5-4b11-9bb5-bf1a5e41ccc3
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6add25325653627d23eb699ab53c0f2799c8322f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24632806"
---
# <a name="object-expected"></a>Objeto esperado
Você tentou invocar um método ou propriedade em um objeto de um tipo diferente de `Object`, ou passou um argumento de um tipo diferente de `Object` quando um `Object` era necessário.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Invoque apenas o método ou propriedade em objetos do tipo `Object`.  
  
-   Se o erro ocorrer para um argumento não objeto, passe um objeto do tipo `Object`.  
  
-   Verifique se uma referência indefinida ou nula está sendo invocada em vez de um objeto do tipo `Object`.  
  
     Por exemplo, se você receber esse erro em myVar no código a seguir:  
  
    ```JavaScript  
    var str = myVar.toString();  
    ```  
  
     você pode usar esse código:  
  
    ```JavaScript  
    if (myVar) {  
        var str = myVar.toString();  
    }  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Object](../../javascript/reference/object-object-javascript.md)   
 [Objetos e matrizes](../../javascript/objects-and-arrays-javascript.md)