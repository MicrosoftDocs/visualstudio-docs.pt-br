---
title: instrução ' Return ' fora da função | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 03568f9f-5f4f-4a10-a738-9a73f3832b9e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ec17d9e421d06736a236e26dd5a1200a5564e7d
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862049"
---
# <a name="return-statement-outside-of-function"></a>Instrução 'return' fora de função
Você usou uma `return` instrução no escopo global do seu código. A `return` instrução só deve aparecer dentro do corpo de uma função.  
  
 Invocar uma função com o `()` operador é uma expressão. Todas as expressões têm valores; a `return` instrução é usada para especificar o valor retornado por uma função. A forma geral é:  
  
```js
  
return [ expression ];  
```  
  
 Quando a `return` instrução é executada, a *expressão* é avaliada e retornada como o valor da função. Se não houver nenhuma expressão, **indefinido** será retornado.  
  
 A execução da função é interrompida quando a `return` instrução é executada, mesmo se houver outras instruções ainda restantes no corpo da função. A exceção a essa regra é se a instrução **Return** ocorrer dentro de um bloco **try** e houver um bloco **finally** correspondente, o código no bloco **finally** será executado antes da função retornar.  
  
 Se uma função retornar porque atinge o final do corpo da função sem executar uma `return` instrução, o valor retornado é o valor **indefinido** (isso significa que o resultado da função não pode ser usado como parte de uma expressão maior).  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Remova a `return` instrução do corpo principal do seu código (o escopo global).  
  
## <a name="see-also"></a>Confira também  
 [Instrução de retorno](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/return)   
 [Objeto de função](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [Propriedade caller (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/caller)