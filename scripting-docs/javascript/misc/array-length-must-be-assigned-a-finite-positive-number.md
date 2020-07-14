---
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
ms.openlocfilehash: 30e02f4f90300e2c05076553419cda5f8c353ab0
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817678"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>O tamanho da matriz deve receber um número finito e positivo
Ao definir a propriedade **Length** de um objeto de **matriz** existente, você especificou um comprimento de matriz que não era um número positivo ou zero. Esse erro ocorre quando você atribui um valor à propriedade **Length** de um `Array` objeto que é negativo ou não é um número ( `NaN` ). Observe que o [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] converte automaticamente números fracionários para inteiros inteiros.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Atribua um número inteiro positivo à propriedade Length. Não há nenhum limite superior para o tamanho de uma matriz, a não ser o valor inteiro máximo (aproximadamente 4.000.000.000). O exemplo a seguir demonstra a maneira correta de definir a propriedade **Length** de um objeto de **matriz** .  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>Veja também  
 [Usando matrizes](../../javascript/advanced/using-arrays-javascript.md)