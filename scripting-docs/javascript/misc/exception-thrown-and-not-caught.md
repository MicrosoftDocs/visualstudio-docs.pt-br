---
title: Exceção lançada e não detectada | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5022
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b5235490-a8e7-42e3-804e-d85235bc6f05
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 44f207d2e32a7ca79ee0d5851a80261c5da9743d
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814584"
---
# <a name="exception-thrown-and-not-caught"></a>Exceção lançada, mas não capturada
Você incluiu uma `throw` instrução em seu código, mas ela não estava colocada dentro de um bloco **try** ou não havia nenhum bloco **Catch** associado para interceptar o erro. As exceções são geradas de dentro do bloco **try** usando a instrução **throw** e detectadas fora do bloco **try** com uma instrução **Catch** .  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Coloque o código que pode gerar uma exceção em um bloco **try** e garantir que haja um bloco **Catch** correspondente.  
  
- Verifique se sua instrução Catch espera a forma correta de exceção.  
  
- Se a exceção for relançada, verifique se há outra instrução Catch correspondente.  
  
## <a name="see-also"></a>Veja também  
 [Objeto de erro](../../javascript/reference/error-object-javascript.md)   
 [Instrução Throw](../../javascript/reference/throw-statement-javascript.md)   
 [tentar... capturar... Instrução Finally](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)