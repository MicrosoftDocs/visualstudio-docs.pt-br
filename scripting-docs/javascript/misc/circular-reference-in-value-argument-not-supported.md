---
title: Referência circular no argumento de valor não tem suportada | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5034
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d06f0fa-86f5-49d1-8d50-af1759990f43
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d25489065ceece41108a75c9d3763a95e4adb924
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949416"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>Referência circular no argumento de valor não é compatível
Foi feita uma tentativa para invocar `JSON.stringify` com um valor que não é válido. O `value` argumento, uma matriz ou objeto, contém uma referência circular.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Remova a referência circular no argumento.  
  
## <a name="example"></a>Exemplo  
 O código neste exemplo causa um erro de tempo de execução porque `john` tem uma referência a `mary` e `mary` tem uma referência a `john`. Para remover a referência circular, remover ou desproteger a propriedade `brother` do `mary` objeto ou o `sister` propriedade do `john` objeto.  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto JSON](../../javascript/reference/json-object-javascript.md)   
 [Função JSON. Parse](../../javascript/reference/json-parse-function-javascript.md)   
 [Erros de tempo de execução JavaScript](../../javascript/reference/javascript-run-time-errors.md)