---
title: 'Como: Executar uma transformação XSLT do editor XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 892f82d64bb022c20c786a996bf9f89cf557b4c2
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34548265"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>Como: executar uma transformação XSLT do Editor de XML

O editor XML permite que você associe uma folha de estilos XSLT com um documento XML, execute a transformação, e exibe a saída. A saída resultante de transformação XSLT são exibidas em uma nova janela do documento.

O **saída** propriedade especifica o nome do arquivo para a saída. Se o **saída** propriedade estiver em branco, um nome de arquivo é gerado no diretório temporário. A extensão de arquivo se baseia o `xsl:output` elemento no seu estilo de planilha e pode ser. *XML*,. *txt* ou. *htm*.

Se o **saída** propriedade especifica um nome de arquivo com um. *htm* ou. *HTML* extensão, a saída XSLT é visualizada usando [!INCLUDE[msCoName](../xml-tools/includes/msconame_md.md)] Internet Explorer. Todas as extensões de arquivo restantes é aberto usando o editor padrão escolhido por [!INCLUDE[msCoName](../xml-tools/includes/msconame_md.md)] Visual Studio. Por exemplo, se a extensão de arquivo. *xml*, o Visual Studio usa o Editor de XML.

## <a name="to-execute-an-xslt-transformation-from-an-xml-document"></a>Para executar uma transformação XSLT de um documento XML

1.  Abrir um documento XML no editor XML.

2.  Associar uma folha de estilos XSLT com o documento XML.

    -   Adicione uma instrução de processamento de `xml-stylesheet` para o documento XML. Por exemplo, adicione a seguinte linha `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>` ao prólogo do documento.

         -ou-

    -   Adicionar a folha de estilo XSLT usando o **propriedades** janela. O documento **janela propriedades**, clique no **procurar** botão para o **folha de estilos** campo, selecione a folha de estilos XSLT e clique em **abrir**.

3.  Clique o **ShowXSL saída** botão o **Editor XML** barra de ferramentas.

    > [!NOTE]
    > Se não houver nenhuma folha de estilos associada com o documento XML, avisos de uma caixa de diálogo você fornecer a folha de estilos ao uso.
    >
    >  A saída resultante de transformação XSLT são exibidas em uma nova janela do documento.

## <a name="to-execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>Para executar uma transformação XSLT de uma folha de estilos XSLT

1.  Abra uma folha de estilos XSLT no editor XML.

2.  Especifique um documento XML de **entrada** campo do documento **propriedades** janela.

    > [!NOTE]
    > O documento XML é o documento de entrada usado para a transformação. Se um documento não for especificado quando a transformação XSLT é iniciada, o **abrir arquivo** caixa de diálogo é exibida e você pode especificar um documento no momento.

3.  Clique o **ShowXSLT saída** botão o **Editor XML** barra de ferramentas.

     A saída resultante de transformação XSLT são exibidas em uma nova janela do documento.

## <a name="to-provide-a-different-output-file-name"></a>Para fornecer um nome de arquivo diferente de saída

1.  Especifique um nome de arquivo de **saída** campo do documento **propriedades** janela.

2.  Clique o **ShowXSLT saída** botão o **Editor XML** barra de ferramentas.

     A saída resultante da transformação XSLT é exibida em uma nova janela de documento e o editor usado na janela de saída depende da extensão de arquivo de sua **saída** propriedade do documento.

## <a name="see-also"></a>Consulte também

- [Editor de XML](../xml-tools/xml-editor.md)