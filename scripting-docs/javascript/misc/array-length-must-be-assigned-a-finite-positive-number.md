---
description: Ao definir a propriedade Length de um objeto de matriz existente, você especificou um comprimento de matriz que não era um número positivo ou zero.
title: O comprimento da matriz deve ser atribuído a um número positivo finito | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: c51c66a4-a543-4e95-b18d-2cfbcb3d1fdd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3938f240580564112915ab0ba3036b63dc96cd8f
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572137"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>O tamanho da matriz deve receber um número finito e positivo
Ao definir a propriedade **Length** de um objeto de **matriz** existente, você especificou um comprimento de matriz que não era um número positivo ou zero. Esse erro ocorre quando você atribui um valor à propriedade **Length** de um `Array` objeto que é negativo ou não é um número ( `NaN` ). Observe que o [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] converte automaticamente números fracionários para inteiros inteiros.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Atribua um número inteiro positivo à propriedade Length. Não há nenhum limite superior para o tamanho de uma matriz, a não ser o valor inteiro máximo (aproximadamente 4.000.000.000). O exemplo a seguir demonstra a maneira correta de definir a propriedade **Length** de um objeto de **matriz** .  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>Confira também  
 [Usando matrizes](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/Arrays)
