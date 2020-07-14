---
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
ms.openlocfilehash: 09ab257e6c473e2747a24559200e7b1f432d5687
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815273"
---
# <a name="vbarray-expected"></a>VBArray esperado
Você forneceu um objeto que não era um Visual Basic safeArray, quando um era esperado.  
  
```js
new VBArray(safeArray);  
```  
  
 VBArrays são somente leitura e não podem ser criados diretamente. O argumento safeArray é um valor VBArray e deve ter obtido um valor VBArray antes de ser passado para o `VBArray` Construtor. Isso só pode ser feito recuperando o valor de um ActiveX existente ou outro objeto.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Certifique-se de que você passe somente objetos **VBArray** para o construtor **VBArray** .  
  
## <a name="see-also"></a>Veja também  
 [Objeto VBArray](../../javascript/reference/vbarray-object-javascript.md)   
 [Usando matrizes](../../javascript/advanced/using-arrays-javascript.md)