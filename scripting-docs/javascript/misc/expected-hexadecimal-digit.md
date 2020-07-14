---
title: Dígito hexadecimal esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 67a86df7-49f9-43cb-99c6-99b1a427827a
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c0797d44115fb5b44cb0c670153e8476356bd533
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816560"
---
# <a name="expected-hexadecimal-digit"></a>Dígito hexadecimal esperado
Você criou uma sequência de escape Unicode incorreta. As seqüências de escape Unicode começam com \u, seguida de exatamente quatro dígitos hexadecimais (não mais e não menos). Os dígitos hexadecimais Unicode podem conter apenas os números 0-9, as letras maiúsculas a-F e as letras minúsculas a-f. O exemplo a seguir demonstra uma sequência de escape Unicode formada corretamente.  
  
```JavaScript  
z = "\u1A5F";  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se os dígitos hexadecimais Unicode começam com \u, contém apenas os números 0-9, as letras maiúsculas a-F, as letras minúsculas a-f; e são agrupados em quatro dígitos.  
  
    > [!NOTE]
    > Se você quiser usar o texto literal \u em uma cadeia de caracteres, use duas barras invertidas-( \\ \u)-uma para escapar da primeira barra invertida.  
  
## <a name="see-also"></a>Veja também  
 [Tipos de dados](../../javascript/data-types-javascript.md)