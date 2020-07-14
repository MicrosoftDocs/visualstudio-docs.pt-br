---
title: Comentário não finalizado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1016
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d4286315-814b-4966-b4c4-1ee19d796eff
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 16f675cb62c0c3fd5f3aba7ba6190427fe101353
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814796"
---
# <a name="unterminated-comment"></a>Comentário não finalizado
Você iniciou um bloco de comentário de várias linhas, mas não o terminou corretamente. Os comentários de várias linhas começam com uma combinação "/*" e terminam com a \* combinação "/" inversa. Veja um exemplo a seguir:  
  
```JavaScript  
/* This is a comment  
This is another part of the same comment.*/  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Não se esqueça de terminar comentários de várias linhas com "*/".  
  
## <a name="see-also"></a>Veja também  
 [Instruções Comment](../../javascript/reference/comment-statements-javascript.md)