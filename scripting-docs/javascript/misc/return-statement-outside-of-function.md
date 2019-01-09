---
title: instrução ' return' fora função | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT1018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 03568f9f-5f4f-4a10-a738-9a73f3832b9e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 82ba1488692f8e8b59063b8f9a52b0682d27e7f8
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54096441"
---
# <a name="return-statement-outside-of-function"></a>Instrução 'return' fora de função
Você usou um `return` instrução no escopo global do seu código. O `return` instrução deve aparecer apenas dentro do corpo de uma função.  
  
 Invocação de uma função com o `()` operador é uma expressão. Todas as expressões têm valores; o `return` instrução é usada para especificar o valor retornado por uma função. O formato geral é:  
  
```js
  
return [ expression ];  
```  
  
 Quando o `return` instrução é executada, *expressão* é avaliado e retornado como o valor da função. Se não houver nenhuma expressão **indefinido** é retornado.  
  
 A execução da função é interrompido quando o `return` instrução é executada, mesmo se houver outras instruções ainda resta no corpo da função. A exceção a essa regra é se o **retornar** instrução ocorre dentro de uma **tente** bloco, e há um correspondente **finalmente** bloco, o código no  **Por fim** bloco serão executadas antes da função retorna.  
  
 Se uma função retornar porque ela atinge o final do corpo da função sem executar uma `return` instrução, o valor retornado é o **indefinido** valor (Isso significa que o resultado da função não pode ser usado como parte de uma expressão maior ).  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Remover o `return` instrução do corpo principal do seu código (o escopo global).  
  
## <a name="see-also"></a>Consulte também  
 [Instrução return](../../javascript/reference/return-statement-javascript.md)   
 [Objeto de função](../../javascript/reference/function-object-javascript.md)   
 [Propriedade caller (Function)](../../javascript/reference/caller-property-function-javascript.md)