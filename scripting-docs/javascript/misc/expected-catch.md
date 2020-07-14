---
title: "' Catch ' esperado | Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1033
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f1cd947f-eba2-411e-8e84-8ca86f608643
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1d9950573e7bbeefe3594d77df2ae41c12f77ed3
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816677"
---
# <a name="expected-catch"></a>'catch' esperado
Você usou o bloco **try** de tratamento de exceção, mas não gravou a instrução **Catch** associada. O mecanismo de tratamento de exceção requer que o código que pode falhar, juntamente com o código que não deve ser executado se ocorrer uma exceção, seja encapsulado dentro de um bloco **try** . As exceções são geradas de dentro do bloco **try** usando a instrução **throw** e capturadas fora do bloco **try** com uma ou mais instruções **Catch** .  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione o bloco **Catch** associado.  
  
- Tente usar um bloco **finally** em vez de um bloco **Catch** .  
  
## <a name="see-also"></a>Veja também  
 [tentar... capturar... Instrução Finally](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)   
 [Objeto de erro](../../javascript/reference/error-object-javascript.md)