---
title: Função esperada | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5002
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f62ade94-9f6f-4832-9b9b-49a06a385bbe
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f177bf81a43c45dcff4cef3040c64425ed544057
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816963"
---
# <a name="function-expected"></a>Função esperada
Você tentou invocar um dos métodos de **protótipo de função** em um objeto que não era um `Function` objeto ou usou um objeto em um contexto de chamada de função. Por exemplo, o código a seguir produz esse erro porque o **exemplo** não é uma função.  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Só chame métodos de **protótipo de função** em `Function` objetos.  
  
- Certifique-se de usar o operador de chamada de função `()` para chamar apenas funções.  
  
## <a name="see-also"></a>Veja também  
 [Objeto de função](../../javascript/reference/function-object-javascript.md)   
 [Propriedade prototype (Object)](../../javascript/reference/prototype-property-object-javascript.md)