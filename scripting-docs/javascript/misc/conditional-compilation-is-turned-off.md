---
title: A compilação condicional está desativada | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 59a030b0-a6c6-47f2-b90e-c0ed204d5116
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: da272529768f3227ce6e0ee3e0ebbf086140dd15
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816118"
---
# <a name="conditional-compilation-is-turned-off"></a>Compilação condicional está desativada
Você tentou usar uma variável de compilação condicional sem primeiro ativar a compilação condicional. A ativação da compilação condicional diz ao [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] compilador para interpretar identificadores começando com @ como variáveis de compilação condicional. Você faz isso iniciando o código condicional com a instrução:  
  
```js
/*@cc_on @*/  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione a seguinte instrução ao início do seu código condicional:  
  
    ```JavaScript  
    /*@cc_on @*/  
    ```  
  
## <a name="see-also"></a>Veja também  
 [Compilação condicional](../../javascript/advanced/conditional-compilation-javascript.md)   
 [Variáveis de compilação condicional](../../javascript/advanced/conditional-compilation-variables-javascript.md)   
 [@cc_onPrivacidade](../../javascript/reference/at-cc-on-statement-javascript.md)   
 [@ifPrivacidade](../../javascript/reference/at-if-statement-javascript.md)   
 [@setPrivacidade](../../javascript/reference/at-set-statement-javascript.md)