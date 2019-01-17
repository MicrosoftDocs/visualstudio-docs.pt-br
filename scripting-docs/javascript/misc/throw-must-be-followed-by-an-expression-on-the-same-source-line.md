---
title: Throw deve ser seguido por uma expressão na mesma linha de origem | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT1035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b03b7747-01a1-40c6-af80-a1dd70bc5781
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7179a22d2713c9ddc894618bd6921f3f873f2ad8
ms.sourcegitcommit: 8bf9e51c77a5a602fab9513b9187e59e57dfebad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54345416"
---
# <a name="throw-must-be-followed-by-an-expression-on-the-same-source-line"></a>O lançamento deve ser seguido por uma expressão na mesma linha de origem
Você usou o `throw` palavra-chave, mas não seguiu-lo com uma expressão na mesma linha de código-fonte. Um `throw` instrução consiste em duas partes: o `throw` palavra-chave, seguido pela expressão seja lançada. Por exemplo:  
  
```JavaScript  
if (denominator == 0) {  
 throw new DivideByZeroException();  
}  
```  
  
 Não é possível dividir esses dois componentes.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Certifique-se de que o `throw` palavra-chave e a expressão a ser gerada aparece na mesma linha.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Error](../../javascript/reference/error-object-javascript.md)   
 [Instrução throw](../../javascript/reference/throw-statement-javascript.md)   
 [Instrução try...catch...finally](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)