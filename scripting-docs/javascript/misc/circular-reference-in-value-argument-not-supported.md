---
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
ms.openlocfilehash: 633ed9c37e8ccde0844205910a8fa2dc12d91414
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817613"
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
  
## <a name="see-also"></a>Veja também  
 [Objeto JSON](../../javascript/reference/json-object-javascript.md)   
 [Função JSON. Parse](../../javascript/reference/json-parse-function-javascript.md)   
 [Erros de tempo de execução JavaScript](../../javascript/reference/javascript-run-time-errors.md)