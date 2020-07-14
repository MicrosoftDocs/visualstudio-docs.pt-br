---
title: Throw deve ser seguido por uma expressão na mesma linha de origem | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b03b7747-01a1-40c6-af80-a1dd70bc5781
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b7bc7ff09152cd0ce7b95c6de73ea98446529c44
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815520"
---
# <a name="throw-must-be-followed-by-an-expression-on-the-same-source-line"></a>O lançamento deve ser seguido por uma expressão na mesma linha de origem
Você usou a `throw` palavra-chave, mas não a segue com uma expressão na mesma linha de origem. Uma `throw` instrução consiste em duas partes: a `throw` palavra-chave, seguida da expressão a ser gerada. Por exemplo:  
  
```JavaScript  
if (denominator == 0) {  
 throw new DivideByZeroException();  
}  
```  
  
 Você não pode dividir esses dois componentes.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a `throw` palavra-chave e a expressão a serem geradas aparecem na mesma linha.  
  
## <a name="see-also"></a>Veja também  
 [Objeto de erro](../../javascript/reference/error-object-javascript.md)   
 [Instrução Throw](../../javascript/reference/throw-statement-javascript.md)   
 [tentar... capturar... Instrução Finally](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)