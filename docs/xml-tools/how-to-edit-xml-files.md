---
title: Como editar arquivos XML
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1ce3e41b2fe9dfdb080e23fb4270454bbd57f7ef
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817197"
---
# <a name="how-to-edit-xml-files"></a>Como: editar arquivos XML

O editor de XML é o novo editor de arquivos XML. Ele pode ser usado em um arquivo XML independente, ou em um arquivo associado a um projeto o Visual Studio. O editor de XML está associado às seguintes extensões de arquivo: *. config*, *. DTD*, *. xml*, *. xsd*, *. XDR*, *. xsl*, *. XSLT*e *. vssettings*. O editor de XML também está associado a qualquer outro tipo de arquivo que não tenha um editor específico registrado e que contenha conteúdo XML ou DTD.

> [!NOTE]
> Os documentos XHTML são tratados pelo Editor de HTML.

Para editar um arquivo XML, clique duas vezes no arquivo que você deseja editar.

## <a name="add-a-new-xml-file-to-a-project"></a>Adicionar um novo arquivo XML a um projeto

1. No menu **projeto** , selecione **Adicionar novo item**.

2. Selecione **arquivo XML** no painel **modelos** .

3. Insira o nome do arquivo no campo **nome** e pressione **Adicionar**.

   O arquivo XML é adicionado ao projeto e é aberto no editor de XML. O arquivo contém a declaração XML padrão, `<?xml version="1.0" encoding="utf-8" ?>`.

## <a name="add-an-existing-xml-file-to-a-project"></a>Adicionar um arquivo XML existente a um projeto

1. No menu **Projeto**, selecione **Adicionar Item Existente**.

   A caixa de diálogo **Adicionar item existente** é exibida.

2. Selecione um arquivo XML e pressione **Adicionar**.

## <a name="create-a-new-xml-or-xslt-file"></a>Criar um novo arquivo XML ou XSLT

1. No menu **arquivo** , selecione **novo**.

   A caixa de diálogo **Novo Arquivo** será exibida.

2. Selecione o **arquivo XML** para criar um novo arquivo XML; ou então, selecione **arquivo XSLT** para criar uma nova folha de estilo XSLT.

3. Clique em **Abrir**.

## <a name="create-an-empty-project-for-xml-files"></a>Criar um projeto vazio para arquivos XML

::: moniker range="vs-2017"

1. No menu **Arquivo**, selecione **Novo** > **Projeto**.

   A caixa de diálogo **Novo Projeto** aparecerá.

2. Selecione o idioma de código de sua escolha e, em seguida, selecione o modelo de **projeto vazio (.NET Framework)** .

3. Clique em **OK**.

::: moniker-end

::: moniker range=">=vs-2019"

1. No menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Insira **projeto vazio** na caixa de pesquisa de modelo, selecione o modelo de **projeto vazio (.NET Framework)** e clique em **Avançar**.

3. Clique em **Criar**.

::: moniker-end

4. Adicionar arquivos XML ao projeto.

   O editor de XML localiza os esquemas que você adiciona a este projeto e os usa para validação e IntelliSense em qualquer XML, esquema ou arquivos XSLT que você editar enquanto este projeto está aberto.

## <a name="see-also"></a>Veja também

- [Editor de XML](../xml-tools/xml-editor.md)
- [Propriedades do documento XML, janela Propriedades](../xml-tools/xml-document-properties-properties-window.md)
- [Como: criar um esquema XML a partir de um documento XML](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)
