---
title: Exceção lançada, mas não capturada | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5022
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b5235490-a8e7-42e3-804e-d85235bc6f05
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 839ff08da4d26406b508a206c809b0813d2b32e1
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24633116"
---
# <a name="exception-thrown-and-not-caught"></a>Exceção lançada, mas não capturada
Você incluído um `throw` instrução no seu código, mas não foi incluída dentro de um **tente** bloco, ou não associados **catch** bloco para interceptar o erro. As exceções são geradas no **tente** bloquear usando o **gerar** instrução e capturada fora o **tente** bloco com um **catch** instrução.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Coloque o código que pode gerar uma exceção em um **tente** bloquear e verifique se há um correspondente **catch** bloco.  
  
-   Certifique-se de que sua instrução catch esperava o formato correto de exceção.  
  
-   Se a exceção é lançada novamente, verifique se que há outra instrução catch correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Error](../../javascript/reference/error-object-javascript.md)   
 [Instrução throw](../../javascript/reference/throw-statement-javascript.md)   
 [Instrução try...catch...finally](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)