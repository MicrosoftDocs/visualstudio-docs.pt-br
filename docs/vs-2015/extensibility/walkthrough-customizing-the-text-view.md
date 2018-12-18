---
title: 'Passo a passo: Personalizando a exibição de texto | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 38cbd0117f5f49666ee5da42d0f60dadf451ffda
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781810"
---
# <a name="walkthrough-customizing-the-text-view"></a>Passo a passo: personalizando a exibição de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode personalizar uma exibição de texto por meio da modificação de qualquer uma das seguintes propriedades em seu mapa de formatação do editor:  
  
-   Margem de indicadores  
  
-   Cursor de inserção  
  
-   Cursor de substituição  
  
-   Texto selecionado  
  
-   Texto selecionado inativo (ou seja, texto selecionado que perdeu o foco)  
  
-   Espaço em branco visível  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-mef-project"></a>Criando um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `ViewPropertyTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="defining-the-content-type"></a>Definindo o tipo de conteúdo  
  
1. Adicione um arquivo de classe e denomine- `ViewPropertyModifier`.  
  
2. Adicione o seguinte `using` diretivas:  
  
    [!code-csharp[VSSDKViewPropertyTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#1)]
    [!code-vb[VSSDKViewPropertyTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#1)]  
  
3. Declare uma classe chamada `TestViewCreationListener` que herda de <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>. Exporte essa classe com os seguintes atributos:  
  
   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> para especificar o tipo de conteúdo ao qual se aplica a este ouvinte.  
  
   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> para especificar a função desse ouvinte.  
  
     [!code-csharp[VSSDKViewPropertyTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#2)]
     [!code-vb[VSSDKViewPropertyTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#2)]  
  
4. Nessa classe, importe o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>.  
  
    [!code-csharp[VSSDKViewPropertyTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#3)]
    [!code-vb[VSSDKViewPropertyTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#3)]  
  
## <a name="changing-the-view-properties"></a>Alterando as propriedades de exibição  
  
1.  Implementar o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> método para que as propriedades de exibição são alteradas quando o modo de exibição é aberto. Para fazer a alteração, primeiro localize a <xref:System.Windows.ResourceDictionary> que corresponde ao aspecto do modo de exibição que você deseja localizar. Em seguida, altere a propriedade apropriada no dicionário de recursos e defina as propriedades. Em lote as chamadas para o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A> método chamando o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> método antes de definir as propriedades e, em seguida, o <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> depois de definir as propriedades.  
  
     [!code-csharp[VSSDKViewPropertyTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#4)]
     [!code-vb[VSSDKViewPropertyTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#4)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
  
1.  Compile a solução.  
  
     Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
2.  Crie um arquivo de texto e digite algum texto.  
  
    -   O cursor de inserção deve ser magenta e o cursor de substituição deve ser turquesa.  
  
    -   A margem de indicadores (à esquerda da exibição de texto) deve ser uma luz verde.  
  
3.  Selecione o texto que você acabou de digitar. A cor do texto selecionado deve ser luz rosa.  
  
4.  Enquanto o texto estiver selecionado, clique em qualquer lugar fora da janela de texto. A cor do texto selecionado deve ser rosa-escuro.  
  
5.  Ative o espaço em branco visível. (Sobre o **edite** , aponte para **avançado** e, em seguida, clique em **exibir espaço em branco**). Digite o texto algumas guias. As setas vermelhas que representam as guias devem ser exibidas.  
  
## <a name="see-also"></a>Consulte também  
 [Serviço de linguagem e pontos de extensão do editor](../extensibility/language-service-and-editor-extension-points.md)

