---
title: Não é possível ter ' break ' fora do loop | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 11d02172-2a78-4705-a730-d21111db5f42
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0959bad452d3b24ca1475b66e37fbdab1e9c3e7f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817652"
---
# <a name="cant-have-break-outside-of-loop"></a>Não é possível ter 'break' fora do loop
Você tentou usar a palavra-chave **Break** fora de um loop. A palavra-chave **Break** é usada para encerrar um loop ou uma `switch` instrução. Ele deve ser inserido no corpo de um loop ou `switch` instrução. No entanto, um **rótulo** pode seguir a palavra-chave break.  
  
```js
break labelname;  
```  
  
 Você só precisa da forma rotulada da palavra-chave **Break** quando estiver usando loops aninhados ou `switch` instruções e precisar interromper um loop que não seja o mais interno.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a palavra-chave **Break** aparece dentro de um loop delimitador ou instrução switch.  
  
## <a name="see-also"></a>Veja também  
 [Instrução break](../../javascript/reference/break-statement-javascript.md)   
 [Controlando o fluxo do programa](../../javascript/controlling-program-flow-javascript.md)   
 [Solucionar problemas com scripts](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)