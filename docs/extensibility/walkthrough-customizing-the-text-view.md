---
title: 'Passo a passo: Personalizando a exibição de texto | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c328925fd558e01138354427a80db7a692753710
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924909"
---
# <a name="walkthrough-customize-the-text-view"></a>Passo a passo: Personalizar a exibição de texto
Você pode personalizar uma exibição de texto por meio da modificação de qualquer uma das seguintes propriedades em seu mapa de formatação do editor:  
  
-   Margem de indicadores  
  
-   Cursor de inserção  
  
-   Cursor de substituição  
  
-   Texto selecionado  
  
-   Texto selecionado inativo (ou seja, texto selecionado que perdeu o foco)  
  
-   Espaço em branco visível  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-mef-project"></a>Criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `ViewPropertyTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="define-the-content-type"></a>Definir o tipo de conteúdo  
  
1. Adicione um arquivo de classe e denomine- `ViewPropertyModifier`.  
  
2. Adicione o seguinte `using` diretivas:  
  
    [!code-csharp[VSSDKViewPropertyTest#1](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_1.cs)]
    [!code-vb[VSSDKViewPropertyTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_1.vb)]  
  
3. Declare uma classe chamada `TestViewCreationListener` que herda de <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>. Exporte essa classe com os seguintes atributos:  
  
   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> para especificar o tipo de conteúdo ao qual se aplica a este ouvinte.  
  
   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> para especificar a função desse ouvinte.  
  
     [!code-csharp[VSSDKViewPropertyTest#2](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_2.cs)]
     [!code-vb[VSSDKViewPropertyTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_2.vb)]  
  
4. Nessa classe, importe o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>.  
  
    [!code-csharp[VSSDKViewPropertyTest#3](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_3.cs)]
    [!code-vb[VSSDKViewPropertyTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_3.vb)]  
  
## <a name="change-the-view-properties"></a>Alterar as propriedades de exibição  
  
1.  Configurar o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> método para que as propriedades de exibição são alteradas quando o modo de exibição é aberto. Para fazer a alteração, primeiro localize a <xref:System.Windows.ResourceDictionary> que corresponde ao aspecto do modo de exibição que você deseja localizar. Em seguida, altere a propriedade apropriada no dicionário de recursos e definir as propriedades. Em lote as chamadas para o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A> método chamando o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> método antes de definir as propriedades e, em seguida, o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> depois de definir as propriedades.  
  
     [!code-csharp[VSSDKViewPropertyTest#4](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_4.cs)]
     [!code-vb[VSSDKViewPropertyTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_4.vb)]  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
  
1.  Compile a solução.  
  
     Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.  
  
2.  Crie um arquivo de texto e digite algum texto.  
  
    -   O cursor de inserção deve ser magenta e o cursor de substituição deve ser turquesa.  
  
    -   A margem de indicadores (à esquerda da exibição de texto) deve ser uma luz verde.  
  
3.  Selecione o texto digitado. A cor do texto selecionado deve ser luz rosa.  
  
4.  Enquanto o texto estiver selecionado, clique em qualquer lugar fora da janela de texto. A cor do texto selecionado deve ser rosa-escuro.  
  
5.  Ative o espaço em branco visível. (Sobre o **edite** , aponte para **avançado** e, em seguida, clique em **exibir espaço em branco**). Digite o texto algumas guias. As setas vermelhas que representam as guias devem ser exibidas.  
  
## <a name="see-also"></a>Consulte também  
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)