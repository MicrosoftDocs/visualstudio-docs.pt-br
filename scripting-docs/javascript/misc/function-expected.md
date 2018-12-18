---
title: Função esperada | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5002
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f62ade94-9f6f-4832-9b9b-49a06a385bbe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aa2db3e95d4baece288c9f984a7a9cf7a82c9d1d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928926"
---
# <a name="function-expected"></a>Função esperada
Ou você tentou invocar uma da **protótipo de função** métodos em um objeto que não era um `Function` objeto, ou você utilizou um objeto em um contexto de chamada de função. Por exemplo, o código a seguir gera este erro porque **exemplo** não é uma função.  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Apenas chame **protótipo de função** métodos em `Function` objetos.  
  
-   Certifique-se de que você use o operador de chamada de função `()` para chamar funções apenas.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de função](../../javascript/reference/function-object-javascript.md)   
 [Propriedade prototype (Object)](../../javascript/reference/prototype-property-object-javascript.md)