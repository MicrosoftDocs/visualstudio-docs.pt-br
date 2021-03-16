---
description: Você tentou atribuir um valor a um resultado de função.
title: Não é possível atribuir a um resultado de função | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5003
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ee8ffb3a-1451-4cb3-99bf-5e9cf8b77d79
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 125d2dc7d41b1b65027952e4e6cb94ff97083e6e
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571916"
---
# <a name="cannot-assign-to-a-function-result"></a>Não é possível designar a um resultado de função
Você tentou atribuir um valor a um resultado de função. O resultado de uma função pode ser atribuído a uma variável, mas não pode ser usado como uma variável. Se você quiser atribuir um novo valor à função em si, omita os parênteses (o operador de chamada de função). O exemplo a seguir demonstra uma situação em que esse erro é gerado.  
  
```js
myFunction() = 42;  // Attempting to assign the value 42 to the result of the function call.  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Não use o valor de um resultado de chamada de função como algo ao qual você possa *atribuir*. No entanto, você pode atribuir o resultado da chamada de função *a uma variável* .  
  
    ```JavaScript  
    myVar = myFunction(42);  
    ```  
  
- Como alternativa, você pode atribuir a função em si (e não seu valor de retorno) a uma variável.  
  
    ```JavaScript  
    myFunction = new Function("return 42;");  
    ```  
  
## <a name="see-also"></a>Confira também  
 [Objeto de função](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [Escrevendo código JavaScript](https://developer.mozilla.org/docs/Learn/Getting_started_with_the_web/JavaScript_basics)   
 [Funções](https://developer.mozilla.org/docs/Learn/JavaScript/Building_blocks/Functions)
