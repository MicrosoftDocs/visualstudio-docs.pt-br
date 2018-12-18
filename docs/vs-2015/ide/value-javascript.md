---
title: '&lt;valor&gt; (JavaScript) | Microsoft Docs'
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
- <value> JavaScript XML tag
- value JavaScript XML tag
ms.assetid: 983e31de-cb1d-411e-b60d-eea6698a26f6
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f88f3ae2e7442549004d2331b4517eb7fa2b5509
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914327"
---
# <a name="ltvaluegt-javascript"></a>&lt;valor&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica informações sobre a documentação para `get` e `set` funções para as propriedades do ECMAScript 3.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<value type="ValueType" integer="true|false"  
    domElement="true|false" mayBeNull="true|false"  
    elementType="ArrayElementType" elementInteger="true|false"  
    elementDomElement="true|false" elementMayBeNull="true|false"  
    locid="descriptionID">description  
</value>  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `type`  
 Opcional. O tipo de dados da propriedade. O tipo pode ser um dos seguintes:  
  
- Um tipo de linguagem ECMAScript que está na especificação do ECMAScript 5, tais como `Number` e `Object`.  
  
- Objeto de um DOM, como `HTMLElement`, `Window`, e `Document`.  
  
- Uma função de construtor do JavaScript.  
  
  `integer`  
  Opcional. Se `type` é `Number`, especifica se a propriedade é um inteiro. Definido como `true` para indicar que a propriedade é um inteiro; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `domElement`  
  Opcional. Esse atributo está preterido; o `type` atributo tem precedência sobre esse atributo. Esse atributo especifica se a propriedade documentada é um elemento DOM. Definido como `true` para especificar que a propriedade é um elemento DOM; caso contrário, defina como `false`. Se o `type` atributo não for definido e `domElement` é definido como `true`, IntelliSense trata a propriedade documentada como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `mayBeNull`  
  Opcional. Especifica se a propriedade documentada pode ser definida como null. Definido como `true` para indicar que a propriedade pode ser definida como nula; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementType`  
  Opcional. Se `type` é `Array`, esse atributo especifica o tipo dos elementos na matriz.  
  
  `elementInteger`  
  Opcional. Se `type` está `Array` e `elementType` é `Number`, este atributo especifica se os elementos na matriz são inteiros. Definido como `true` para indicar que os elementos na matriz são inteiros; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementDomElement`  
  Opcional. Esse atributo está preterido; o `elementType` atributo tem precedência sobre esse atributo. Se `type` é `Array`, este atributo especifica se os elementos na matriz são elementos DOM. Definido como `true` para especificar que os elementos são elementos DOM; caso contrário, defina como `false`. Se o `elementType` atributo não for definido e `elementDomElement` é definido como `true`, IntelliSense trata cada elemento na matriz como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `elementMayBeNull`  
  Opcional. Se `type` é `Array`, especifica se os elementos na matriz podem ser definidos como null. Definido como `true` para indicar que os elementos na matriz podem ser definidos como nula; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `locid`  
  Opcional. O identificador para obter informações sobre a propriedade de localização. O identificador é um membro ID ou ele corresponde ao `name` valor em um pacote de mensagem definido pelos metadados OpenAjax do atributo. O tipo de identificador depende do formato especificado na [ \<loc >](../ide/loc-javascript.md) elemento.  
  
  `description`  
  Opcional. Uma descrição da propriedade.  
  
## <a name="remarks"></a>Comentários  
 Uso de propriedades do ECMAScript 5 a [ \<resumo >](../ide/summary-javascript.md) elemento.  
  
 Use o `<value>` elemento imediatamente antes do `get` ou `set` função.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como usar o `<value>` elemento em um `get` função.  
  
```javascript  
function Sys$CancelEventArgs$get_cancel() {  
    /// <value type="Boolean" locid="P:J#Sys.CancelEventArgs.cancel"></value>  
    if (arguments.length !== 0) throw Error.parameterCount();  
    return this._cancel();  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)



