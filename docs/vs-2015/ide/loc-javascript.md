---
title: '&lt;Loc&gt; (JavaScript) | Microsoft Docs'
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
- <loc> JavaScript XML tag
- loc JavaScript XML tag
ms.assetid: 0d3349b6-4bdd-418f-bc11-73665305baae
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9314453b5e75e31f98d6989efa274278706bc5a4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49244004"
---
# <a name="ltlocgt-javascript"></a>&lt;Loc&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica o local e o tipo de arquivo de sidecar que fornece as informações do IntelliSense localizadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<loc filename="filename"  
    format="vsdoc|messagebundle" />  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `filename`  
 Opcional. O nome da raiz do arquivo sidecar que contém informações de localização para a cultura neutra. Quando o Visual Studio procura informações de localização, ele tenta encontrar uma versão específica de cultura desse arquivo. Por exemplo, se `filename` é jquery.xml, Visual Studio procura a pasta correta de específicas da cultura (como JA) no mesmo local que o arquivo. js que contém o `<loc>` elemento. Se ele localiza a pasta específicas da cultura, ele verifica se existe um arquivo de jquery.xml nele. Se ele não é possível localizar o arquivo correto, ele usa em vez disso, as regras de local de recurso gerenciado. O valor padrão para `filename` é o nome do arquivo atual, mas com uma extensão. XML, em vez de. js.  
  
 `format`  
 Opcional. O tipo de arquivo secundário usado para localização. Use `messagebundle` para especificar o uso de pacotes de mensagem definido por Ajax abra metadados. `messagebundle` é o formato recomendado. No entanto, esse formato não há suporte no Microsoft Ajax ou em arquivos. winmd. Use `vsdoc` para especificar o formato de localização padrão do .NET Framework que é usado pelo Microsoft Ajax e tempo de execução do Windows. Esse atributo é opcional. `vsdoc` é o formato padrão.  
  
## <a name="remarks"></a>Comentários  
 O `<loc>` elemento deve aparecer na parte superior do arquivo na mesma seção como o `<reference>` elemento. Regras de uso para o `<loc>` elemento são os mesmos que o `<reference>` elemento. Para obter mais informações, consulte a seção "Referências diretivas" [JavaScript IntelliSense](../ide/javascript-intellisense.md).  
  
 Visual Studio processa uma única `<loc>` elemento para cada arquivo. js. Se vários `<loc>` elementos estão presentes, somente uma única `<loc>` elemento é usado. Comportamento de determinação de quais `<loc>` elemento a ser usado não está definido.  
  
 Ao usar o formato de pacote de mensagem, use o `locid` atributo nos comentários da documentação XML para especificar o `name` valor do atributo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o `<loc>` elemento com o formato de messagebundle. Adicione o seguinte XML em um arquivo chamado messageFilename.xml e coloque o arquivo na pasta correta específicas da cultura, conforme especificado na descrição do `filename` parâmetro.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<messagebundle>  
  <msg name="1">A class that represents a rectangle</msg>  
  <msg name="2">The height of a rectangle</msg>  
  <msg name="3">The width of a rectangle</msg>  
</messagebundle>  
  
```  
  
 Por exemplo, messagebundle, adicione o seguinte código para um arquivo JavaScript no seu projeto. O `<loc>` elemento deve aparecer como a primeira linha no arquivo JavaScript. As descrições nesse código serão substituídas por descrições localizadas, se disponível.  
  
```javascript  
/// <loc filename="messageFilename.xml" format="messagebundle"/>  
  
function doSomething(a,b)   
{  
    /// <summary locid='1'>description</summary>  
    /// <param name='a' locid='2'>parameter a description</param>  
    /// <param name='b' locid='3'>parameter b description</param>  
}  
  
```  
  
 O exemplo a seguir usa o formato de VSDoc. Adicione o seguinte XML em um arquivo chamado scriptFilename.xml e coloque o arquivo na pasta correta específicas da cultura.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<doc>  
  <assembly>  
    <name>Lights</name>  
  </assembly>  
  <members>  
    <member name="M:illuminate">  
      <summary>Activates a light. </summary>  
      <param name='a'>The light to activate. </param>  
    </member>  
  </members>  
</doc>  
  
```  
  
 Por exemplo, VSDoc, adicione o seguinte código para um arquivo JavaScript no seu projeto. As descrições nesse código serão substituídas por descrições localizadas, se disponível.  
  
```javascript  
/// <loc filename="scriptFilename.xml" format="vsdoc" />  
  
function illuminate(a)   
{  
    /// <summary locid='M:illuminate'>description</summary>  
    /// <param name='a' type='Number'>parameter a description</param>  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comentários da documentação XML](../ide/xml-documentation-comments-javascript.md)



