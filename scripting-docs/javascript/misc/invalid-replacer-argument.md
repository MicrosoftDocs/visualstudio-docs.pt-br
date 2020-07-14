---
title: Argumento de realocador inválido | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4727186f-facd-4aa6-9447-bbefbae83f07
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 452af60c37e4a56996438cc2957e9b69ccee98ef
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816820"
---
# <a name="invalid-replacer-argument"></a>Argumento substituto inválido
Foi feita uma tentativa de invocar `JSON.stringify` com um argumento que não é válido. O `replacer` argumento deve ser uma função ou uma matriz.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Altere o `replacer` argumento para uma função ou uma matriz.  
  
## <a name="example"></a>Exemplo  
 O código neste exemplo causa um erro de tempo de execução porque `memberfilter` é um objeto em vez de uma função ou matriz.  
  
```JavaScript  
var contact = new Object();  
contact.firstname = "Jesper";  
contact.surname = "Aaberg";  
contact.phone = ["555-0100", "555-0120"];  
  
var memberfilter = new Object();  
  
// This line will cause a runtime error.  
var jsontext = JSON.stringify(contact, memberfilter, "\t");  
```  
  
## <a name="see-also"></a>Veja também  
 [Objeto JSON](../../javascript/reference/json-object-javascript.md)   
 [Função JSON. Parse](../../javascript/reference/json-parse-function-javascript.md)   
 [Erros de tempo de execução JavaScript](../../javascript/reference/javascript-run-time-errors.md)