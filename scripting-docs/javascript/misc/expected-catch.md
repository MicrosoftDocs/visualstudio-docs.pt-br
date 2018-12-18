---
title: Esperado &#39; catch &#39; | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT1033
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f1cd947f-eba2-411e-8e84-8ca86f608643
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e6cd1e57137d220ebcf3834070e36d8257e2dca7
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24633786"
---
# <a name="expected-39catch39"></a>Esperado &#39; catch &#39;
Você usou a manipulação de exceção **tente** bloquear, mas não gravou associado **catch** instrução. A mecanismo de tratamento de exceção requer que o código que pode falhar, juntamente com o código que não deve ser executado se uma exceção ocorrer, ser encapsulado dentro de um **tente** bloco. As exceções são geradas no **tente** bloquear usando o **gerar** instrução e capturada fora o **tente** bloco com um ou mais **catch**instruções.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Adicionar associado **catch** bloco.  
  
-   Tente usar um **finalmente** bloquear em vez de um **catch** bloco.  
  
## <a name="see-also"></a>Consulte também  
 [Try...... finally instrução catch](../../javascript/reference/try-dot-dot-dot-catch-dot-dot-dot-finally-statement-javascript.md)   
 [Objeto Error](../../javascript/reference/error-object-javascript.md)