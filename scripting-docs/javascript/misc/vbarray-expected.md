---
description: Você forneceu um objeto que não era um Visual Basic safeArray, quando um era esperado.
title: VBArray esperado | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5013
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f2998d7d-13a4-4bbe-b872-3ff3316551e4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e344e24b3fbef7b7f119a36513c222e085328072
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572072"
---
# <a name="vbarray-expected"></a>VBArray esperado
Você forneceu um objeto que não era um Visual Basic safeArray, quando um era esperado.  
  
```js
new VBArray(safeArray);  
```  
  
 VBArrays são somente leitura e não podem ser criados diretamente. O argumento safeArray é um valor VBArray e deve ter obtido um valor VBArray antes de ser passado para o `VBArray` Construtor. Isso só pode ser feito recuperando o valor de um ActiveX existente ou outro objeto.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Certifique-se de que você passe somente objetos **VBArray** para o construtor **VBArray** .  
  
## <a name="see-also"></a>Confira também  
 [Objeto VBArray](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/VBArray)   
 [Usando matrizes](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/Arrays)
