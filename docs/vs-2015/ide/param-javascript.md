---
title: '&lt;param&gt; (JavaScript) | Microsoft Docs'
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
- <param> JavaScript XML tag
- param JavaScript XML tag
ms.assetid: 2c4e0167-c1dd-4e54-83f1-c437856bddc1
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b1178fc6ff2cb5b4664930eaa70fd3de5ebed0f5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949065"
---
# <a name="ltparamgt-javascript"></a>&lt;param&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica informações sobre a documentação para um parâmetro em uma função ou método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<param name="parameterName" type="ParameterType"  
    integer="true|false" domElement="true|false"  
    mayBeNull="true|false" elementType="ArrayElementType"  
    elementInteger="true|false" elementDomElement="true|false"  
    elementMayBeNull="true|false" locid="descriptionID"  
    parameterArray="true|false" optional="true|false"  
    value="code">description  
</param>  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `name`  
 Necessário. O nome do parâmetro.  
  
 `type`  
 Opcional. O tipo de dados do parâmetro. O tipo pode ser um dos seguintes:  
  
- Digite uma linguagem ECMAScript na especificação do ECMAScript 5, como `Number` e `Object`.  
  
- Objeto de um DOM, como `HTMLElement`, `Window`, e `Document`.  
  
- Uma função de construtor do JavaScript.  
  
  `integer`  
  Opcional. Se `type` é `Number`, especifica se o parâmetro é um inteiro. Definido como `true` para indicar que o parâmetro é um inteiro; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `domElement`  
  Opcional. Esse atributo está preterido; o `type` atributo tem precedência sobre esse atributo. Esse atributo especifica se o parâmetro documentado é um elemento DOM. Definido como `true` para especificar que o parâmetro é um elemento DOM; caso contrário, defina como `false`. Se o `type` atributo não for definido e `domElement` é definido como `true`, IntelliSense trata o parâmetro documentado como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `mayBeNull`  
  Opcional. Especifica se o parâmetro documentado pode ser definido como null. Definido como `true` para indicar que o parâmetro pode ser definido como nulo; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementType`  
  Opcional. Se `type` é `Array`, esse atributo especifica o tipo dos elementos na matriz.  
  
  `elementInteger`  
  Opcional. Se `type` está `Array` e `elementType` é `Number`, este atributo especifica se os elementos na matriz são inteiros. Definido como `true` para indicar que os elementos na matriz são inteiros; caso contrário, defina como `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `elementDomElement`  
  Opcional. Esse atributo está preterido; o `elementType` atributo tem precedência sobre esse atributo. Se `type` é `Array`, este atributo especifica se os elementos na matriz são elementos DOM. Definido como `true` para especificar que os elementos são elementos DOM; caso contrário, defina como `false`. Se o `elementType` atributo não for definido e `elementDomElement` é definido como `true`, IntelliSense trata cada elemento na matriz como um `HTMLElement` ao executar o preenchimento de declaração.  
  
  `elementMayBeNull`  
  Opcional. Se `type` é `Array`, especifica se os elementos na matriz podem ser definidos como null. Definido como `true` para indicar que os elementos na matriz podem ser definidos como nula; caso contrário, defina `false`. O valor padrão é `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `locid`  
  Opcional. O identificador de informações de localização sobre o parâmetro. O identificador é um membro ID ou ele corresponde ao `name` valor em um pacote de mensagem definido pelos metadados OpenAjax do atributo. O tipo de identificador depende do formato especificado na [ \<loc >](../ide/loc-javascript.md) elemento.  
  
  `parameterArray`  
  Opcional. Especifica se o parâmetro documentado pode ser repetido na chamada de função, semelhante a repetição de parâmetros com suporte no `String.format` função. Definido como `true` para indicar que o parâmetro pode ser repetida; caso contrário, defina `false`. Esse atributo não é usado pelo Visual Studio para fornecer informações de IntelliSense.  
  
  `optional`  
  Opcional. Especifica se o parâmetro documentado é opcional na função de chamada. Definido como `true` para indicar que o parâmetro é opcional; caso contrário, defina `false`.  
  
  `value`  
  Opcional. Especifica o código que deve ser avaliado para uso pelo IntelliSense em vez do código de função em si. Você pode usar esse atributo é fornecer informações de tipo quando o tipo de parâmetro é indefinido. Por exemplo, você pode usar `value=’1’` para tratar o tipo de parâmetro como um número.  
  
  `description`  
  Opcional. Uma descrição do parâmetro.  
  
## <a name="remarks"></a>Comentários  
 É o único atributo obrigatório `name`. Todos os outros atributos são opcionais.  
  
 Elementos usados para anotar as funções, tais como [ \<resumo >](../ide/summary-javascript.md), [ \<param >](../ide/param-javascript.md), e [ \<retorna >](../ide/returns-javascript.md), devem ser colocados no corpo da função antes que as instruções.  
  
 Se houver vários `<param>` elementos que têm o mesmo nome, um do `<param>` elementos é usado e os elementos redundantes serão ignorados. O comportamento que determina qual elemento é usado não está definido. Se `name` refere-se a um parâmetro inexistente, o elemento é ignorado.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como usar o `<param>` elemento.  
  
```javascript  
function areaFunction(radiusParam)  
{  
    /// <summary>Determines the area of a circle when provided a radius parameter.</summary>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
// Uses of <param> with the value attribute.  
  
function calculate(a) {  
    /// <param name='a' value='1'/>  
    a.    // Completion list for a Number.  
}  
  
function calculate(a) {  
    /// <param name='a' value='{x:0,y:0}'/>  
    a.    // x and y appear in the completion list.  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)



