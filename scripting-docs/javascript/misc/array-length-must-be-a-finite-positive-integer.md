---
title: O comprimento da matriz deve ser um inteiro positivo finito | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5029
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1a467040-4702-4178-848f-418a5974e907
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa8b9a85c0c7457cb06d36fd3cd849ce48484b46
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817080"
---
# <a name="array-length-must-be-a-finite-positive-integer"></a>O tamanho da matriz deve ser um número inteiro finito e positivo
Você está chamando o construtor de **matriz** com um argumento que não é um número inteiro (números inteiros consistem em zero mais o conjunto de inteiros positivos).  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Use inteiros positivos somente ao criar um novo `Array` objeto. Se você quiser criar uma matriz com um único elemento que não seja um inteiro, faça isso em um processo de duas etapas. Primeiro, crie uma matriz com um elemento e, em seguida, coloque o valor no primeiro elemento (matriz [0]). Veja a seguir um exemplo que gera esse erro.  
  
    ```JavaScript  
    var piArray = new Array(3.14159);  
    ```  
  
     O exemplo a seguir demonstra a maneira correta de especificar uma matriz com um único elemento numérico.  
  
    ```JavaScript  
    var piArray = new Array(1);  
    piArray [0] = 3.14159;  
    ```  
  
     Não há nenhum limite superior para o tamanho de uma matriz, a não ser o valor inteiro máximo (aproximadamente 4.000.000.000).  
  
## <a name="see-also"></a>Veja também  
 [Usando matrizes](../../javascript/advanced/using-arrays-javascript.md)