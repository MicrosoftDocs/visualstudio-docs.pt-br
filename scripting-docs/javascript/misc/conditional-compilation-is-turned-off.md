---
title: A compilação condicional está desativada | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 56621d6f7fcc195a4ece7654adeafd1096c37e8b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572934"
---
# <a name="conditional-compilation-is-turned-off"></a>Compilação condicional está desativada
Você tentou usar uma variável de compilação condicional sem primeiro ativar a compilação condicional. A ativação da compilação condicional diz ao compilador de [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] para interpretar identificadores começando com @ como variáveis de compilação condicional. Você faz isso iniciando o código condicional com a instrução:  
  
```js
/*@cc_on @*/  
```  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Adicione a seguinte instrução ao início do seu código condicional:  
  
    ```JavaScript  
    /*@cc_on @*/  
    ```  
  
## <a name="see-also"></a>Consulte também  
 @No__t_1 de [compilação condicional](../../javascript/advanced/conditional-compilation-javascript.md)  
 [Variáveis de compilação condicional](../../javascript/advanced/conditional-compilation-variables-javascript.md)    
 [instrução de @cc_on](../../javascript/reference/at-cc-on-statement-javascript.md)    
 [instrução de @if](../../javascript/reference/at-if-statement-javascript.md)    
 [Instrução @set](../../javascript/reference/at-set-statement-javascript.md)