---
title: 'Como: usar pontos de interrupção com XSLT | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bf7bbc2c-71dc-4cac-a6fc-add6b27d92ed
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b01553075115ce953b499f722a254b5a2b9f20ee
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49233448"
---
# <a name="how-to-use-breakpoints-with-xslt"></a>Como: Use pontos de interrupção com XSLT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir pontos de interrupção em uma folha de estilos XSLT ou no documento de código-fonte XML. Se você definir um ponto de interrupção em uma marca, quando a execução iniciar o ponto de interrupção se transportará para a instrução que tem a seguinte linha de código informações.  
  
 Para obter mais informações, consulte [Noções básicas de depuração: pontos de interrupção](http://msdn.microsoft.com/en-us/752a02c2-0ac7-4c8b-aa1b-4b2b3b21152e).  
  
## <a name="set-a-breakpoint-in-a-style-sheet"></a>Definir um ponto de interrupção em uma folha de estilos  
 Os pontos de interrupção podem ser definidos em marcas inicial, em marcas de fim, e em nós de texto de uma folha de estilos XSLT. Os pontos de interrupção também podem ser definidos no código em um bloco de script.  
  
#### <a name="to-set-a-breakpoint-in-a-style-sheet"></a>Para definir um ponto de interrupção em uma folha de estilos  
  
1.  Abra uma folha de estilos no editor XML.  
  
2.  Posicione o cursor no local do ponto de interrupção, clique com botão direito, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.  
  
3.  Clique no botão Procurar no botão Procurar (**...** ) sobre o **entrada** campo da janela de propriedades do documento.  
  
4.  Localize o documento XML de origem e clique em **aberto**.  
  
     Isso define o arquivo de documento de origem que é usado para a transformação XSLT.  
  
5.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.  
  
## <a name="set-a-breakpoint-in-an-xml-source-document"></a>Definir um ponto de interrupção em um documento-fonte XML  
 Os pontos de interrupção podem ser definidas em elementos, atributos, no nó de namespace, nos comentários, na instrução de processamento, e os nós de texto de um documento-fonte XML. Você não pode definir um ponto de interrupção no nó do documento, ou em um nó de namespace que é herdada de elemento pai.  
  
#### <a name="to-set-a-breakpoint-in-an-xml-source-document"></a>Para definir um ponto de interrupção em um documento-fonte XML  
  
1.  Abra o documento XML no editor XML.  
  
2.  Posicione o cursor no local do ponto de interrupção, clique com botão direito, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.  
  
3.  Clique no botão Procurar no botão Procurar (**...** ) sobre o **folha de estilos** campo da janela de propriedades do documento.  
  
4.  Localize o documento XML de origem e clique em **aberto**.  
  
     Isso define o arquivo de documento de origem que é usado para a transformação XSLT.  
  
5.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: depurar uma folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)

