---
title: '&lt;preterido&gt; (JavaScript) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf33d371-59da-4310-95ee-d7524fd9d58c
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4c643afe786366c7c470e74d02a5145a600a6b87
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49269263"
---
# <a name="ltdeprecatedgt-javascript"></a>&lt;preterido&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica um método ou função preterida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<deprecated  
    type="deprecate|remove"  
    locid="descriptionID">description  
</deprecated>  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `type`  
 Opcional. Especifica se a função ou método será removido em uma versão futura, ou se a função ou método já foi removido e que seu uso pode resultar em um erro. Definido como `deprecate` para especificar que a função ou método será removido em uma versão futura. Definido como `remove` para especificar que a função ou método já foi removido.  
  
 `locid`  
 Opcional. O identificador de informações de localização sobre o método ou função. O identificador é um membro ID ou ele corresponde ao `name` valor em um pacote de mensagem definido pelos metadados OpenAjax do atributo. O tipo de identificador depende do formato especificado na [ \<loc >](../ide/loc-javascript.md) elemento.  
  
 `description`  
 Opcional. Uma descrição da função ou método que está sendo preterido.  
  
## <a name="remarks"></a>Comentários  
 Os elementos usados para anotar as funções, que incluem `<deprecated>`, devem ser colocados no corpo da função antes que as instruções. Quando você marca uma função como preteridos, recomendamos que você substitua sua [ \<resumo >](../ide/summary-javascript.md) elemento com o `<deprecated>` elemento.  
  
## <a name="example"></a>Exemplo  
 O código a seguir mostra como usar o `<deprecated>` elemento.  
  
```javascript  
function areaFunction(radiusParam) {  
    /// <deprecated type="deprecate" >Determines the area of a circle when supplied a radius parameter.</deprecated>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)



