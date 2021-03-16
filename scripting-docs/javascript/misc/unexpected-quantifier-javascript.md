---
description: Ao compor seu padrão de pesquisa de expressão regular, você criou um elemento pattern com um fator de repetição ilegal.
title: Quantificador inesperado (JavaScript) | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba6d34f9-2d6f-486c-a929-6cd9818be322
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9351f9306cea9e3f6346b007d6fe05c1d7bbf319
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571955"
---
# <a name="unexpected-quantifier-javascript"></a>Quantificador inesperado (JavaScript)
Ao compor seu padrão de pesquisa de expressão regular, você criou um elemento pattern com um fator de repetição ilegal. Por exemplo, o padrão  
  
```js
/^+/  
```  
  
 é inválido porque o elemento ^ (início da entrada) não pode ter um fator de repetição. A tabela a seguir lista os elementos que não podem ter fatores de repetição.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|^|Início da entrada|  
|$|Fim da entrada|  
|\b|Limite de palavra|  
|\B|Limite de não palavra|  
|*|Zero ou mais repetições|  
|+|Uma ou mais repetições|  
|?|Zero ou uma repetição|  
|p|n repetições|  
|{n,}|n ou mais repetições|  
|{n, m}|De n a m repetições, inclusivo|  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se o seu elemento de padrão de pesquisa contém apenas fatores de repetição legal.  
  
## <a name="see-also"></a>Confira também  
 [Objeto de expressão regular](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [Sintaxe de expressão regular (JavaScript)](/previous-versions/1400241x(v=vs.100))
