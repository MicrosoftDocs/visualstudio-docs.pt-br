---
description: Você usou o bloco try de tratamento de exceção, mas não gravou a instrução Catch associada.
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
ms.openlocfilehash: b5cf6087ff5a299c575ac4f2cd5eb8a3e206b7e0
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571032"
---
# <a name="expected-catch"></a>'catch' esperado
Você usou o bloco **try** de tratamento de exceção, mas não gravou a instrução **Catch** associada. O mecanismo de tratamento de exceção requer que o código que pode falhar, juntamente com o código que não deve ser executado se ocorrer uma exceção, seja encapsulado dentro de um bloco **try** . As exceções são geradas de dentro do bloco **try** usando a instrução **throw** e capturadas fora do bloco **try** com uma ou mais instruções **Catch** .  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione o bloco **Catch** associado.  
  
- Tente usar um bloco **finally** em vez de um bloco **Catch** .  
  
## <a name="see-also"></a>Confira também  
 [tentar... capturar... Instrução Finally](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)   
 [Objeto Error](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)
