---
title: Executar uma transformação XSLT
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e74beb2903cd133dfdd322ce4c297692eae3411
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817184"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>Como executar uma transformação XSLT do editor de XML

O editor de XML permite associar uma folha de estilos XSLT a um documento XML, executar a transformação e exibir a saída. A saída resultante de transformação XSLT são exibidas em uma nova janela do documento.

A propriedade **output** especifica o nome do arquivo para a saída. Se a propriedade de **saída** estiver em branco, um nome de arquivo será gerado no diretório temporário. A extensão do arquivo é baseada no `xsl:output` elemento em sua folha de estilos e pode ser.* XML*,. *txt* ou. *htm*.

Se a propriedade de **saída** especificar um nome de arquivo com um. *htm* ou. extensão *HTML* , a saída XSLT é visualizada usando um navegador da Web. Todas as outras extensões de arquivo são abertas usando o editor padrão escolhido pelo Visual Studio. Por exemplo, se a extensão de arquivo for. *XML*, o Visual Studio usa o editor de XML.

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>Executar uma transformação XSLT de um arquivo XML

1. Abra um documento XML no editor de XML.

2. Associar uma folha de estilos XSLT com o documento XML.

    - Adicione uma instrução de processamento de `xml-stylesheet` para o documento XML. Por exemplo, adicione a seguinte linha ao prólogo do documento:`<?xml-stylesheet type='text/xsl' href='filename.xsl'?>`

       -ou-

    - Adicione a folha de estilos XSLT usando a janela **Propriedades** . Com o arquivo XML aberto no editor, clique com o botão direito do mouse em qualquer lugar no editor e escolha **Propriedades**. Na janela **Propriedades** , clique no campo **folha de estilos** e escolha o botão procurar (...). Selecione a folha de estilos XSLT e, em seguida, escolha **abrir**.

3. Na barra de menus, escolha **XML**  >  **Iniciar XSLT sem depuração**. Ou pressione **Ctrl** + **ALT** + **F5**.

   A saída da transformação XSLT é exibida em uma nova janela de documento.

   > [!NOTE]
   > Se não houver nenhuma folha de estilos associada com o documento XML, avisos de uma caixa de diálogo você fornecer a folha de estilos ao uso.

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>Executar uma transformação XSLT de uma folha de estilos XSLT

1. Abra uma folha de estilos XSLT no editor de XML.

2. Especifique um documento XML no campo de **entrada** da janela **Propriedades** do documento.

   > [!NOTE]
   > O documento XML é o documento de entrada usado para a transformação. Se um documento não for especificado quando a transformação XSLT for iniciada, a caixa de diálogo **Abrir arquivo** será exibida e você poderá especificar um documento nesse momento.

3. Na barra de menus, escolha **XML**  >  **Iniciar XSLT sem depuração**. Ou pressione **Ctrl** + **ALT** + **F5**.

   A saída da transformação XSLT é exibida em uma nova janela de documento.

## <a name="specify-an-output-file-name"></a>Especificar um nome de arquivo de saída

Você pode especificar um nome de arquivo de saída para arquivos XML e XSL. Abra a janela **Propriedades** e especifique um nome de arquivo no campo **saída** .

## <a name="see-also"></a>Veja também

- [Editor de XML](../xml-tools/xml-editor.md)
