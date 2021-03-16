---
description: Você tentou criar uma expressão regular com um intervalo de conjunto de caracteres inválido.
title: Intervalo inválido no conjunto de caracteres (JavaScript) | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5021
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 971e9d5a-f88a-47a8-af94-f3c7c4aed5ab
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9441f9cfd3adf94ddd38841d522c83922c9154f1
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571669"
---
# <a name="invalid-range-in-character-set-javascript"></a>Intervalo inválido no conjunto de caracteres (JavaScript)
Você tentou criar uma expressão regular com um intervalo de conjunto de caracteres inválido. Os conjuntos de caracteres devem variar apenas de caracteres únicos, como a-z ou 0-9; Você não pode incluir classes de caracteres como \w em um conjunto de caracteres. O primeiro caractere no intervalo também deve vir antes do segundo caractere no intervalo. Por exemplo:  
  
```JavaScript  
var good = /[a-z]/;     // A valid character range - a comes before z.  
var notGood = /[z-a]/;  // An invalid character range - z does not come before a.  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Use apenas caracteres únicos para compor o conjunto de caracteres de expressão regular e verifique se eles estão na ordem correta.  
  
## <a name="see-also"></a>Confira também  
 [Objeto de expressão regular](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [Sintaxe de expressão regular (JavaScript)](/previous-versions/1400241x(v=vs.100))
