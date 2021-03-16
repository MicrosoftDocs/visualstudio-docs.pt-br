---
description: Foi feita uma tentativa de invocar JSON. stringify com um valor que não é válido.
title: Não há suporte para referência circular em argumento de valor | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 88e4ead99f8c59a1300d018bff9d3e81b0874b51
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571136"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>Referência circular no argumento de valor não é compatível
Foi feita uma tentativa de invocar `JSON.stringify` com um valor que não é válido. O `value` argumento, uma matriz ou um objeto, contém uma referência circular.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Remova a referência circular do argumento.  
  
## <a name="example"></a>Exemplo  
 O código neste exemplo causa um erro de tempo de execução porque `john` tem uma referência a `mary` e `mary` tem uma referência a `john` . para remover a referência circular, remova ou desmarque a propriedade do objeto `brother` `mary` ou da `sister` Propriedade do `john` objeto.  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>Confira também  
 [Objeto JSON](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON)   
 [Função JSON. Parse](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)   
 [Erros de tempo de execução JavaScript](/microsoft-edge/devtools-guide/console/error-and-status-codes#javascript-run-time-errors)
