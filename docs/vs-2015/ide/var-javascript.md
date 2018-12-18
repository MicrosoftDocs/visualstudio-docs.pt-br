---
title: '&lt;var&gt; (JavaScript) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- <var> JavaScript XML tag
- var JavaScript XML tag
ms.assetid: 34ff9023-c81c-46d1-85b6-0022f0962e66
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 04f592bab7679ed3e8fe8791872ce2280d05359a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49881970"
---
# <a name="ltvargt-javascript"></a>&lt;var&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica informações sobre a documentação para uma variável.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<var type="ValueType" integer="true|false"  
    domElement="true|false" mayBeNull="true|false"  
    elementType="ArrayElementType" elementInteger="true|false"  
    elementDomElement="true|false" elementMayBeNull="true|false"  
    helpKeyword="keyword" locid="descriptionID">description  
</var>   
```  
  
#### <a name="parameters"></a>Parâmetros  
 `type`  
 Opcional. O tipo de dados da variável. O tipo pode ser um dos seguintes:  
  
- Um tipo de linguagem ECMAScript que está na especificação do ECMAScript 5, tais como `Number` e `Object`.  
  
- Objeto de um DOM, como `HTMLElement`, `Window`, e `Document`.  
  
- Uma função de construtor do JavaScript.  
  
  `integer`  
  Opcional. Se `type` é `Number`, especifica se a variável é um inteiro. Definido como `true` para indicar que a variável é um inteiro; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `domElement`  
  Opcional. Esse atributo está preterido; o `type` atributo tem precedência sobre esse atributo. Esse atributo especifica se a variável documentada é um elemento DOM. Definido como `true` para especificar que a variável é um elemento DOM; caso contrário, defina como `false`. Se o `type` atributo não for definido e `domElement` é definido como `true`, IntelliSense trata a variável documentada como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `mayBeNull`  
  Opcional. Especifica se a variável documentada pode ser definida como null. Definido como `true` para indicar que a variável pode ser definida como nula; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementType`  
  Opcional. Se `type` é `Array`, esse atributo especifica o tipo dos elementos na matriz.  
  
  `elementInteger`  
  Opcional. Se `type` está `Array` e `elementType` é `Number`, este atributo especifica se os elementos na matriz são inteiros. Definido como `true` para indicar que os elementos na matriz são inteiros; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementDomElement`  
  Opcional. Esse atributo está preterido; o `elementType` atributo tem precedência sobre esse atributo. Se `type` é `Array`, este atributo especifica se os elementos na matriz são elementos DOM. Definido como `true` para especificar que os elementos são elementos DOM; caso contrário, defina como `false`. Se o `elementType` atributo não for definido e `elementDomElement` é definido como `true`, IntelliSense trata cada elemento na matriz como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `elementMayBeNull`  
  Opcional. Se `type` é `Array`, especifica se os elementos na matriz podem ser definidos como null. Definido como `true` para indicar que os elementos na matriz podem ser definidos como nula; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `helpKeyword`  
  Opcional. A palavra-chave para ajuda de F1.  
  
  `locid`  
  Opcional. O identificador de informações de localização sobre a variável. O identificador é um membro ID ou ele corresponde ao `name` valor em um pacote de mensagem definido pelos metadados OpenAjax do atributo. O tipo de identificador depende do formato especificado na [ \<loc >](../ide/loc-javascript.md) marca.  
  
  `description`  
  Opcional. Uma descrição da variável.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como usar o `<var>` elemento.  
  
```javascript  
/// <var>A rectangle that has a width of 5.</var>  
var Rectangle = {  
    /// <field type = 'Number'>The width of the rectangle.</field>  
    wid: 5,  
    /// <field type = 'Number'>The length of the rectangle.</field>  
    len: 0,  
    /// <field type='Number'>Returns the area of the rectangle.</field>  
    getArea: function (wid, len) {  
        return len * wid;  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)



