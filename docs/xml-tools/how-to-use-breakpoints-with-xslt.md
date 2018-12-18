---
title: 'Como: Use pontos de interrupção com XSLT'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 430b7f14f35506b45fe73be47d056cdd7b6a9c95
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34548347"
---
# <a name="how-to-use-breakpoints-with-xslt"></a>Como: usar pontos de interrupção com XSLT

Você pode definir pontos de interrupção em uma folha de estilos XSLT ou no documento de código-fonte XML. Se você definir um ponto de interrupção em uma marca, quando a execução iniciar o ponto de interrupção se transportará para a instrução que tem a seguinte linha de código informações.

Para obter mais informações, consulte [Noções básicas de depuração: pontos de interrupção](../debugger/using-breakpoints.md).

## <a name="set-a-breakpoint-in-a-style-sheet"></a>Definir um ponto de interrupção em uma folha de estilo

Os pontos de interrupção podem ser definidos em marcas inicial, em marcas de fim, e em nós de texto de uma folha de estilos XSLT. Os pontos de interrupção também podem ser definidos no código em um bloco de script.

### <a name="to-set-a-breakpoint-in-a-style-sheet"></a>Para definir um ponto de interrupção em uma folha de estilos

1.  Abra uma folha de estilos no editor XML.

2.  Posicione o cursor no local de ponto de interrupção, clique com botão direito, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.

3.  Clique no botão Procurar (**...** ) sobre o **entrada** campo da janela de propriedades do documento.

4.  Localize o documento XML de origem e clique em **abrir**.

     Isso define o arquivo de documento de origem que é usado para a transformação XSLT.

5.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.

## <a name="set-a-breakpoint-in-an-xml-source-document"></a>Definir um ponto de interrupção em um documento de origem XML

Os pontos de interrupção podem ser definidas em elementos, atributos, no nó de namespace, nos comentários, na instrução de processamento, e os nós de texto de um documento-fonte XML. Você não pode definir um ponto de interrupção no nó do documento, ou em um nó de namespace que é herdada de elemento pai.

### <a name="to-set-a-breakpoint-in-an-xml-source-document"></a>Para definir um ponto de interrupção em um documento-fonte XML

1.  Abra o documento XML no editor XML.

2.  Posicione o cursor no local de ponto de interrupção, clique com botão direito, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.

3.  Clique no botão Procurar (**...** ) sobre o **estilos** campo da janela de propriedades do documento.

4.  Localize o documento XML de origem e clique em **abrir**.

     Isso define o arquivo de documento de origem que é usado para a transformação XSLT.

5.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Depurar uma folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)