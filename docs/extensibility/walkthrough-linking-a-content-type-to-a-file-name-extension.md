---
title: 'Walkthrough: vinculando um tipo de conteúdo a uma extensão de nome de arquivo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b4e5ba3cd82090b5fad76d48c4600e0814bd91eb
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904690"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo
Você pode definir seu próprio tipo de conteúdo e vincular uma extensão de nome de arquivo a ele usando as extensões de Managed Extensibility Framework do editor (MEF). Em alguns casos, a extensão de nome de arquivo já está definida por um serviço de idioma. Mas, para usá-lo com o MEF, você ainda deve vinculá-lo a um tipo de conteúdo.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-mef-project"></a>Criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `ContentTypeTest` .

2. No arquivo **Source. Extension. vsixmanifest** , vá para a guia **ativos** e defina o campo **tipo** como **Microsoft. VisualStudio. MefComponent**, o campo de **origem** para **um projeto na solução atual**e o campo **projeto** como o nome do projeto.

## <a name="define-the-content-type"></a>Definir o tipo de conteúdo

1. Adicione um arquivo de classe e nomeie-o `FileAndContentTypes` .

2. Adicione referências aos assemblies a seguir:

    1. System. ComponentModel. composição

    2. Microsoft. VisualStudio. Text. Logic

    3. Microsoft. VisualStudio. CoreUtility

3. Adicione as seguintes `using` diretivas.

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. Declare uma classe estática que contenha as definições.

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. Nessa classe, exporte um <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> chamado "HID" e declare sua definição de base como "text".

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>Vincular uma extensão de nome de arquivo a um tipo de conteúdo

- Para mapear esse tipo de conteúdo para uma extensão de nome de arquivo, exporte um <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> que tenha a extensão *. HID* e o tipo de conteúdo "HID".

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
         [Export]
         [Name("hid")]
         [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;

         [Export]
         [FileExtension(".hid")]
         [ContentType("hid")]
        internal static FileExtensionToContentTypeDefinition hiddenFileExtensionDefinition;
    }
    ```

## <a name="add-the-content-type-to-an-editor-export"></a>Adicionar o tipo de conteúdo a uma exportação do editor

1. Crie uma extensão de editor. Por exemplo, você pode usar a extensão de glifo de margem descrita em [Walkthrough: criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md).

2. Adicione a classe que você definiu neste procedimento.

3. Ao exportar a classe de extensão, adicione um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> do tipo "HID" a ela.

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>Confira também
- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
