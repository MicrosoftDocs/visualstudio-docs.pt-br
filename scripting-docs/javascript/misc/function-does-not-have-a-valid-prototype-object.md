---
title: Função não tem um objeto de protótipo válido | Microsoft Docs
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
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a4e2cbf198a452cd61f1355682ea3041436d2a27
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24633006"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>A função não tem um objeto de protótipo válido
Você tentou usar **instanceof** para determinar se um objeto foi derivado de uma classe de função específica, mas você redefiniu o objeto `prototype` propriedade como `null`, ou um tipo de objeto externo (ambos não válido [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] objetos). Um objeto externo pode ser um objeto do modelo de objeto de host (por exemplo, o documento do Internet Explorer ou o objeto de janela) ou um objeto COM externo.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Verifique se a função `prototype` propriedade se refere a uma opção válida [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de função](../../javascript/reference/function-object-javascript.md)   
 [Propriedade prototype (Object)](../../javascript/reference/prototype-property-object-javascript.md)