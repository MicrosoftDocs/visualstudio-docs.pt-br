---
title: Como editar arquivos XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3754bcf87d77a3a67801ef7f9df8e07dc687b052
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34549123"
---
# <a name="how-to-edit-xml-files"></a>Como: editar arquivos XML

O editor XML é o novo editor para arquivos XML. Ele pode ser usado em um arquivo XML independente, ou em um arquivo associado a um projeto o Visual Studio. O Editor de XML está associado com as seguintes extensões de arquivo: *. config*, *. DTD*, *. XML*, *. xsd*, *XDR*, *. xsl*, *. XSLT*, e *vssettings*. O Editor de XML também está associado a qualquer outro tipo de arquivo que não tenha nenhum editor específico registrado e que contenha o conteúdo XML ou DTD.

> [!NOTE]
> Os documentos XHTML são tratados pelo Editor de HTML.

## <a name="to-edit-an-xml-file"></a>Para editar um arquivo XML

1.  Clique duas vezes no arquivo que você deseja editar.

### <a name="to-add-a-new-xml-file-to-a-project"></a>Para adicionar um novo arquivo XML a um projeto

1.  Do **projeto** menu, selecione **Adicionar Novo Item**.

2.  Selecione **arquivo XML** do **modelos** painel.

3.  Insira o nome do arquivo de **nome** campo e pressione **adicionar**.

     O arquivo XML é adicionado ao projeto e aberto no Editor de XML. O arquivo contém a declaração XML padrão, `<?xml version="1.0" encoding="utf-8" ?>`.

## <a name="to-add-an-existing-xml-file-to-a-project"></a>Para adicionar um arquivo XML existente a um projeto

1.  Do **projeto** menu, selecione **Add Existing Item**.

     O **Add Existing Item** caixa de diálogo é exibida.

2.  Selecione um arquivo XML e pressione **adicionar**.

## <a name="to-create-a-new-xml-or-xslt-file"></a>Para criar um novo arquivo XML ou XSLT

1.  Do **arquivo** menu, selecione **novo**.

     O **novo arquivo** caixa de diálogo é exibida.

2.  Selecione **arquivo XML** para criar um novo arquivo XML; ou, selecione **arquivo XSLT** para criar uma nova folha de estilos XSLT.

3.  Clique em **abrir**.

## <a name="to-create-a-project-for-xml-files"></a>Para criar um projeto para arquivos XML

1.  Do **arquivo** menu, selecione **novo**e, em seguida, selecione **projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

2.  Selecione o idioma de código de sua escolha, selecione **projeto vazio**e clique em **Okey**.

3.  Adicionar arquivos XML ao projeto.

     O Editor de XML localiza os esquemas que você adiciona a esse projeto e os usa para validação e IntelliSense em qualquer XML, esquema ou arquivos XSLT que você editar quando o projeto for aberto.

## <a name="see-also"></a>Consulte também

- [Editor de XML](../xml-tools/xml-editor.md)
- [Propriedades de documento XML, janela de propriedades](../xml-tools/xml-document-properties-properties-window.md)
- [Como: criar um esquema XML de um documento XML](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)