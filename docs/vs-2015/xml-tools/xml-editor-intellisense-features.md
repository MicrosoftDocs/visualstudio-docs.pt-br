---
title: Recursos de IntelliSense do Editor de XML | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2b26f214-cc3a-46bf-b260-14eb8e599182
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9c691eea7417e882ee3b73e9f2adc538714b486a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158565"
---
# <a name="xml-editor-intellisense-features"></a>Recursos do IntelliSense o editor XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O editor XML fornece os recursos do IntelliSense comparáveis a outros editores de linguagem fornecidos no Visual Studio. Esta seção explica como você pode usar o IntelliSense com a linguagem de definição de esquema XML (XSD) e documentos XSLT.  
  
## <a name="intellisense-in-an-xsd-document"></a>O IntelliSense em um documento XSD  
 Depois que um esquema está associado com seu documento, você obtém uma lista suspensa de elementos esperados quando você digita `"<"` ou clique em de **exibir uma lista de membros do objeto** na barra de ferramentas do editor XML. Para obter informações sobre como associar esquemas com documentos XML, consulte [validação de documento XML](../xml-tools/xml-document-validation.md).  
  
 Quando você digita o ESPAÇO de dentro de uma marca inicial, você também obtém uma lista suspensa que mostra todos os atributos que podem ser adicionados ao elemento atual.  
  
 Quando você digita `"="` para um valor de atributo, ou as aspas de abertura para o valor, você também obtém a lista de valores possíveis para esse atributo. Os valores são fornecidos apenas se o esquema fornece valores enumerados através de facetas de `xsd:enumeration` , ou se o atributo é um tipo de `Boolean` . Uma lista do IntelliSense de códigos de idioma conhecido também é fornecida para `xml:lang` ou qualquer `simpleType` que deriva de `xsd:language`. Uma lista do IntelliSense de valores conhecidos de `targetNamespace` é fornecida para declarações de namespace.  
  
 Uma lista do IntelliSense de valores possíveis é fornecida também quando você digita `">"` para fechar uma tag de início se o elemento é `simpleType`. O comportamento de elementos é semelhante ao comportamento dos atributos descritos no parágrafo anterior.  
  
 Dicas de ferramenta também aparece nessas IntelliSense listas com base em `xsd:annotation` e informações de `xsd:documentation` encontrado no esquema associado.  
  
## <a name="intellisense-in-an-xslt-document"></a>O IntelliSense em um documento XSLT  
 Após adicionar um modelo nomeado ou um atributo para o documento de fonte, você pode usar o IntelliSense para inserir o seguinte:  
  
- Nomes definidos de atributo.  
  
- Modos do modelo.  
  
- Nomes de modelo.  
  
- Nomes de parâmetro para um modo determinado.  
  
- Nomes de parâmetro para um modelo chamado determinado.  
  
  Para obter mais informações, confira [Passo a passo: Usando XSLT IntelliSense](../xml-tools/walkthrough-using-xslt-intellisense.md) tópico.  
  
## <a name="auto-completion"></a>Preenchimento automático  
 O editor XML também facilita editando XML preenchendo na sintaxe XML necessário para você. Por exemplo, se você digitar a seguinte marcação inicial:  
  
 `<book>`  
  
 O editor XML preenche a marca de fim e posicionar o cursor após a marca inicial. A seguir está um exemplo disso (o "&#124;" observa a posição do cursor):  
  
 `<book>`&#124;`</book>`  
  
 Porque valores de atributo devem sempre ter aspas, o editor XML preenche as aspas para você. Por exemplo, se você digitar o seguinte:  
  
 `<book title=`  
  
 O editor XML adiciona as aspas e posicionar o cursor entre aspas:  
  
 `<book title="`&#124;`"`  
  
 Da mesma forma, o editor XML também insere a seguinte sintaxe XML automaticamente para você:  
  
- Termina uma instrução de processamento:  `?>`  
  
- Finalizar um bloco CDATA: `]]>`  
  
- Termine um comentário: `-->`  
  
- Termina uma declaração de DTD: `>`  
  
  O editor XML também tem a capacidade de inserir uma declaração de namespace se você selecionar um elemento qualificado namespace ou o atributo de uma lista do IntelliSense e de namespace para esse elemento ou atributo ainda não está no escopo.  
  
  Por exemplo, se você selecionar o elemento de `e:Book` de lista do IntelliSense onde o prefixo é associado ao namespace de `http://books` que não foi declarada no documento, o editor XML insere a declaração de namespace necessário para você. O seguinte é o texto resultante XML:  
  
  `<e:Book xmlns:e="http://books"`  
  
## <a name="brace-matching"></a>Correspondência de chave  
 O editor XML fornece a chave realçando para fornecer feedback imediato em elementos que apenas se você tiver fechado. Você também pode usar o atalho de teclado (CTRL) para ignorar uma chave da chave correspondente.  
  
 O editor XML faz isso para os seguintes itens:  
  
- Início correspondente e marcas de fim.  
  
- Qualquer par de "\<" ou ">" colchetes angulares.  
  
- Início e fim de comentários.  
  
- Início e final de instrução de processamento.  
  
- Início e fim de blocos CDATA.  
  
- Início e fim de declarações de DTD.  
  
- Abrindo e fechando aspas em atributos.  
  
## <a name="modifying-the-intellisense-options"></a>Alterando as opções do IntelliSense  
 Os recursos do IntelliSense e de preenchimento automático são ativados por padrão. No entanto, você pode alterar isso modificando suas configurações de opções de ferramentas.  
  
 O **AutoInserção** seção o **diversos** página controla o comportamento a seguir:  
  
|Nome|Descrição|  
|----------|-----------------|  
|Fechar marcas|Insere fechar marcas para novos elementos.|  
|Aspas de atributo|O valor do atributo das inserções que quando você digite um novo nome de atributo.|  
|Outra marcação|Comentários, CDATA termina, DOCTYPE, instruções de processamento, e outras declarações de marcação.|  
  
#### <a name="to-change-the-auto-completion-behavior"></a>Para alterar o comportamento de preenchimento automático  
  
1. Selecione **Opções** no menu **Ferramentas**.  
  
2. Expandir **Editor de texto**, expanda **XML**e selecione **diversos**.  
  
3. Fazer alterações para o **AutoInserção** seção e clique em **Okey**.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)   
 [Usando o IntelliSense](../ide/using-intellisense.md)   
 [Passo a passo: usando XSLT IntelliSense](../xml-tools/walkthrough-using-xslt-intellisense.md)
