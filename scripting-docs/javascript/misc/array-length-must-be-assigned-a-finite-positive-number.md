---
title: O tamanho da matriz deve ser atribuído um número finito e positivo | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: c51c66a4-a543-4e95-b18d-2cfbcb3d1fdd
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 63a9d714173334192028b9096de41968befa85ef
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825494"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>O tamanho da matriz deve receber um número finito e positivo
Ao definir a **comprimento** propriedade de existente **matriz** objeto, que você especificou um tamanho da matriz que não era um número positivo ou zero. Esse erro ocorre quando você atribui um valor para o **comprimento** propriedade de um `Array` objeto que é negativo ou não é um número (`NaN`). Observe que [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] automaticamente converte números fracionários em inteiros.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Atribua um número inteiro positivo para a propriedade de comprimento. Não há nenhum limite superior para o tamanho de uma matriz, que não seja o máximo valor inteiro (aproximadamente 4 bilhões). O exemplo a seguir demonstra a maneira correta para definir a **comprimento** propriedade de um **matriz** objeto.  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Usando matrizes](../../javascript/advanced/using-arrays-javascript.md)