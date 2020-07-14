---
title: Objeto esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5007
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d88c93d-e5b5-4b11-9bb5-bf1a5e41ccc3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 28eec125914f0207fbdf79a39ea2140dd74d6d0d
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816222"
---
# <a name="object-expected"></a>Objeto esperado
Você tentou invocar um método ou propriedade em um objeto de um tipo diferente de `Object`, ou passou um argumento de um tipo diferente de `Object` quando um `Object` era necessário.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Invoque apenas o método ou propriedade em objetos do tipo `Object`.  
  
- Se o erro ocorrer para um argumento não objeto, passe um objeto do tipo `Object`.  
  
- Verifique se uma referência indefinida ou nula está sendo invocada em vez de um objeto do tipo `Object`.  
  
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
  
## <a name="see-also"></a>Veja também  
 [Objeto Object](../../javascript/reference/object-object-javascript.md)   
 [Objetos e matrizes](../../javascript/objects-and-arrays-javascript.md)