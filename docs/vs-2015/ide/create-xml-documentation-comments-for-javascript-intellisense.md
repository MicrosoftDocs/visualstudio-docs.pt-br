---
title: Criar comentários de documentação XML para JavaScript IntelliSense | Microsoft Docs
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
- code comments, JavaScript IntelliSense
- XML documentation comments, JavaScript IntelliSense
- documentation comments [JavaScript]
- IntelliSense [JavaScript], XML documentation comments
ms.assetid: a27f5b50-9807-436f-a0cf-6f3137ecbaf0
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d15144a2cee70e5f6bdc496bf2c09eb8fb95c85d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49220552"
---
# <a name="create-xml-documentation-comments-for-javascript-intellisense"></a>Criar comentários de documentação XML para JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*Comentários da documentação XML* são JavaScript comentários que você adicione um script para fornecer informações sobre os elementos de código como funções, campos e variáveis. No Visual Studio, essas descrições de texto são exibidas com o IntelliSense quando você faz referência a função de script.  
  
 Este tópico fornece um tutorial básico sobre como usar os comentários da documentação XML. Para obter informações sobre o uso de outros elementos, tais como [ \<var >](../ide/var-javascript.md) e [ \<valor >](../ide/value-javascript.md)e para exemplos de código adicionais, consulte [comentários da documentação XML ](../ide/xml-documentation-comments-javascript.md). Para obter informações sobre como fornecer informações de IntelliSense para um retorno de chamada assíncrono como uma `Promise`, consulte [ \<retorna >](../ide/returns-javascript.md).  
  
> [!NOTE]
>  Os comentários da documentação XML estão disponíveis somente em assemblies, serviços e arquivos referenciados.  
  
### <a name="to-create-xml-documentation-comments-for-a-javascript-function"></a>Criar comentários da documentação XML para uma função JavaScript  
  
-   Na função, adicione [ \<resumo >](../ide/summary-javascript.md), [ \<param >](../ide/param-javascript.md), e [ \<retorna >](../ide/returns-javascript.md) elementos e preceder cada elemento com três barras (/ / /).  
  
    > [!NOTE]
    >  Cada elemento deve estar em uma única linha.  
  
     O exemplo a seguir mostra uma função de JavaScript.  
  
    ```javascript  
    function getArea(radius)  
    {  
        /// <summary>Determines the area of a circle that has the specified radius parameter.</summary>  
        /// <param name="radius" type="Number">The radius of the circle.</param>  
        /// <returns type="Number">The area.</returns>  
        var areaVal;  
        areaVal = Math.PI * radius * radius;  
        return areaVal;  
    }  
    ```  
  
-   Para exibir os comentários da documentação XML, digite o nome e o parêntese de abertura de uma função que é marcado com comentários da documentação XML, como no exemplo a seguir:  
  
    ```javascript  
    var areaVal = getArea(  
    ```  
  
     Quando você digita o parêntese de abertura da função que contém os comentários da documentação XML, o Editor de código usa o IntelliSense para exibir as informações que são definidas nos comentários da documentação XML.  
  
### <a name="to-create-xml-documentation-comments-for-a-javascript-field"></a>Criar comentários da documentação XML para um campo de JavaScript  
  
-   Em uma definição de função ou o objeto de construtor, adicione uma [ \<campo >](../ide/field-javascript.md) elemento precedidas por três barras (/ / /).  
  
     O exemplo a seguir mostra o uso do `<field>` elemento em uma função de construtor. Para obter exemplos adicionais, consulte [ \<campo >](../ide/field-javascript.md).  
  
    ```javascript  
    function Engine() {  
        /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>  
        this.HorsePower = 150;  
    }  
    ```  
  
-   Para exibir os comentários da documentação XML, crie um objeto usando o construtor de função que é marcado com comentários da documentação XML, como no exemplo a seguir.  
  
    ```javascript  
    var eng = new Engine();  
    ```  
  
-   Na próxima linha, digite o nome do objeto e um período para mostrar informações de IntelliSense para o campo.  
  
    ```javascript  
    eng.  
    ```  
  
### <a name="to-create-xml-documentation-comments-for-an-overloaded-function"></a>Criar comentários da documentação XML para uma função sobrecarregada  
  
1.  Na função, adicione uma [ \<assinatura >](../ide/signature-javascript.md) elemento para cada sobrecarga. Esses elementos, adicione outros elementos, como `<summary>`, `<param>`, e `<returns>`, precede cada elemento com três barras (/ / /).  
  
     O exemplo a seguir mostra uma função sobrecarregada do JavaScript. Neste exemplo, as sobrecargas diferem por tipo de parâmetro.  
  
    ```javascript  
    function calc(a) {  
        /// <signature>  
        /// <summary>Function summary 1.</summary>  
        /// <param name="a" type="Number">A number.</param>  
        /// <returns type="Number" />  
        /// </signature>  
        /// <signature>  
        /// <summary>Function summary 2.</summary>  
        /// <param name="a" type="String">A string.</param>  
        /// <returns type="Number" />  
        /// </signature>  
        return a;  
    }  
    ```  
  
2.  Para exibir os comentários da documentação XML, digite o nome e o parêntese de abertura da função que é marcado com comentários da documentação XML, como no exemplo a seguir:  
  
    ```javascript  
    calc(  
    ```  
  
### <a name="to-create-localized-intellisense"></a>Para criar o IntelliSense localizado  
  
1.  Crie um arquivo XML que tenha comentários de documentação no formato OpenAjax MessageBundle.  
  
    > [!IMPORTANT]
    >  MessageBundle é o formato recomendado. Esse formato não é suportado no Ajax da Microsoft ou em arquivos. winmd. Para obter informações sobre como usar a alternativa `VSDoc` de formato, consulte [ \<loc >](../ide/loc-javascript.md).  
  
     O exemplo a seguir mostra o conteúdo em um arquivo de sidecar que contém as informações do IntelliSense localizadas. Isso é um arquivo XML que está localizado em uma pasta específicas da cultura, como JA. A pasta deve estar no mesmo local que o arquivo. js que contém o `<loc>` elemento. O nome de arquivo do arquivo XML deve corresponder a `filename` parâmetro especificado no `<loc>` elemento.  
  
    ```  
    <messagebundle>  
      <msg name="1">A class that represents a rectangle</msg>  
      <msg name="2">The length of the rectangle</msg>  
      <msg name="3">The height of the rectangle</msg>  
    </messagebundle>  
  
    ```  
  
2.  Em seu arquivo. js, adicione o código a seguir. O `<loc>` elemento deve ser declarado antes de qualquer script e segue as mesmas regras de uso que o `<reference>` elemento. Para obter mais informações, consulte [JavaScript IntelliSense](../ide/javascript-intellisense.md) e [ \<loc >](../ide/loc-javascript.md).  
  
    ```javascript  
    /// <loc filename="messageFilename.xml" format="messagebundle"/>  
  
    ```  
  
3.  Em seu arquivo. js, adicione os elementos de documentação XML e as descrições padrão. Defina as `locid` valores para corresponder ao correspondente de atributo `name` valores de atributo do arquivo de sidecar. As descrições padrão serão substituídas pelas informações do IntelliSense localizadas, se ele estiver disponível.  
  
    ```javascript  
    function add(a,b)   
    {  
        /// <summary locid='1'>description</summary>  
        /// <param name='a' locid='2'>parameter a description</param>  
        /// <param name='b' locid='3'>parameter b description</param>  
    }  
  
    ```  
  
4.  Para exibir os comentários da documentação XML, digite o nome e o parêntese de abertura da função, como no exemplo a seguir:  
  
    ```javascript  
    add(  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [JavaScript IntelliSense](../ide/javascript-intellisense.md)   
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)   
 [NIB: Instruções passo a passo: IntelliSense do JavaScript no ASP.NET](http://msdn.microsoft.com/en-us/4f6e0cc2-7f48-4dbf-abb0-7fb743a2d05b)



