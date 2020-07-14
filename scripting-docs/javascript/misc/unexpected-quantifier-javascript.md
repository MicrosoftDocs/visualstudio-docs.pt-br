---
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
ms.openlocfilehash: da4ff08ae667b868670364c7ad6b9a6b69ae6ad3
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815325"
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
  
## <a name="see-also"></a>Veja também  
 [Objeto de expressão regular](../../javascript/reference/regular-expression-object-javascript.md)   
 [Sintaxe de expressão regular (JavaScript)](https://msdn.microsoft.com/library/1400241x)