---
title: 'Passo a passo: Vinculação de um tipo de conteúdo para uma extensão de nome de arquivo | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 54570ec03788f88f58f14249f200ed2028686c37
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566747"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>Passo a passo: Vincular um tipo de conteúdo para uma extensão de nome de arquivo
Você pode definir seu próprio tipo de conteúdo e vincular a uma extensão de nome de arquivo a ela usando as extensões do editor Managed Extensibility Framework (MEF). Em alguns casos, a extensão de nome de arquivo já está definida por um serviço de linguagem. Mas, para usá-lo com o MEF, você deve ainda vinculá-lo para um tipo de conteúdo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-mef-project"></a>Criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `ContentTypeTest`.  
  
2.  No **vsixmanifest** arquivo, vá para o **ativos** guia e defina o **tipo** campo **mefcomponent**, o **código-fonte** campo **um projeto na solução atual**e o **projeto** campo para o nome do projeto.  
  
## <a name="define-the-content-type"></a>Definir o tipo de conteúdo  
  
1.  Adicione um arquivo de classe e denomine- `FileAndContentTypes`.  
  
2.  Adicione referências aos assemblies a seguir:  
  
    1.  System.ComponentModel.Composition  
  
    2.  Microsoft.VisualStudio.Text.Logic  
  
    3.  Microsoft.VisualStudio.CoreUtility  
  
3.  Adicione o seguinte `using` diretivas.  
  
    ```csharp  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio.Text.Classification;  
    using Microsoft.VisualStudio.Utilities;  
  
    ```  
  
4.  Declare uma classe estática que contém as definições.  
  
    ```csharp  
    internal static class FileAndContentTypeDefinitions  
    {. . .}  
    ```  
  
5.  Nessa classe, exportar um <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> denominado "hid" e declarar sua definição de base para ser "text".  
  
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
  
-   Para mapear esse tipo de conteúdo para uma extensão de nome de arquivo, exporte uma <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> que tem a extensão *. HID* e o tipo de conteúdo "hid".  
  
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
  
## <a name="add-the-content-type-to-an-editor-export"></a>Adicione o tipo de conteúdo para uma exportação de editor  
  
1.  Crie uma extensão do editor. Por exemplo, você pode usar a extensão de glifo de margem descrita em [instruções passo a passo: criar um glifo de margem](../extensibility/walkthrough-creating-a-margin-glyph.md).  
  
2.  Adicione a classe definida neste procedimento.  
  
3.  Quando você exportar a classe de extensão, adicione um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> do tipo "hid" a ele.  
  
    ```csharp  
    [Export]  
    [ContentType("hid")]  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)