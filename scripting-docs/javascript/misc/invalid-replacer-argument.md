---
description: Foi feita uma tentativa de invocar JSON. stringify com um argumento que não é válido.
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
ms.openlocfilehash: 95a73d6fcbcf1350eece52e2cd58693646617a28
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570889"
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
  
## <a name="see-also"></a>Confira também  
 [Objeto JSON](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON)   
 [Função JSON. Parse](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)   
 [Erros de tempo de execução JavaScript](/microsoft-edge/devtools-guide/console/error-and-status-codes#javascript-run-time-errors)
