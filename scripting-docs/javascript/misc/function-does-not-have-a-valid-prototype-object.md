---
title: A função não tem um objeto de protótipo válido | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ca6f13620bb486cf1663bd5bef9a9a93b2c8a480
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817353"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>A função não tem um objeto de protótipo válido
Você tentou usar o **instanceof** para determinar se um objeto foi derivado de uma classe de função específica, mas redefiniu a propriedade do objeto `prototype` como `null` ou um tipo de objeto externo (não objetos válidos [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] ). Um objeto externo pode ser um objeto do modelo de objeto de host (por exemplo, o documento ou o objeto de janela do Internet Explorer) ou um objeto COM externo.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Verifique se a propriedade da função `prototype` se refere a um [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] objeto válido.  
  
## <a name="see-also"></a>Veja também  
 [Objeto de função](../../javascript/reference/function-object-javascript.md)   
 [Propriedade prototype (Object)](../../javascript/reference/prototype-property-object-javascript.md)