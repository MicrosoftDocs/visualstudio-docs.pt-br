---
title: 'Passo a passo: Exibindo SmartTags | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], new - smart tags
ms.assetid: 10bb4f69-b259-41f0-b91a-69b04385d9a5
caps.latest.revision: 31
manager: douge
ms.openlocfilehash: 459530726628819587a3c228910baa3b902ae865
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939092"
---
# <a name="walkthrough-displaying-smarttags"></a>Passo a passo: Exibindo SmartTags
Marcas inteligentes foram preteridas em favor de lâmpadas. Ver [instruções passo a passo: Exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md).  
  
 Marcas inteligentes são marcas no texto que se expandem para exibir um conjunto de ações. Por exemplo, em um projeto do Visual Basic ou Visual c#, uma linha vermelha aparecerá sob uma palavra ao renomear um identificador como um nome de variável. Quando você move o ponteiro sobre o sublinhado, um botão é exibido próximo o ponteiro. Se você clicar no botão, uma ação sugerida é exibida, por exemplo, **IsRead renomear para IsReady**. Se você clicar em ação, todas as referências aos **IsRead** no projeto são renomeados **IsReady**.  
  
 Embora as marcas inteligentes são parte da implementação do IntelliSense no editor, você pode implementar marcas inteligentes, a criação de subclasses <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag>e, em seguida, Implementando a <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> interface e o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> interface.  
  
> [!NOTE]
>  Outros tipos de marcas podem ser implementados de maneira semelhante.  
  
 A instrução a seguir mostra como criar uma marca inteligente que aparece na palavra atual e tem duas ações sugeridas: **convertida em letras maiusculas** e **converter em letras minúsculas**.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Criando um projeto do Managed Extensibility Framework (MEF)  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de classificador do Editor. Nomeie a solução `SmartTagTest`.  
  
2.  Abra o arquivo de vsixmanifest no Editor de manifesto do VSIX.  
  
3.  Certifique-se de que o **ativos** seção contém uma `Microsoft.VisualStudio.MefComponent` tipo, o **fonte** é definido como `A project in current solution`, e **projeto** é definido como SmartTagTest.dll.  
  
4.  Salve e feche vsixmanifest.  
  
5.  Adicione a seguinte referência ao projeto e defina **CopyLocal** para `false`:  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
6.  Exclua os arquivos de classe existentes.  
  
## <a name="implementing-a-tagger-for-smart-tags"></a>Implementando um marcador de marcas inteligentes  
  
#### <a name="to-implement-a-tagger-for-smart-tags"></a>Para implementar um marcador de marcas inteligentes  
  
1.  Adicione um arquivo de classe e denomine- `TestSmartTag`.  
  
2.  Adicione as importações a seguir:  
  
     [!code-csharp[VSSDKSmartTagTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#1)]
     [!code-vb[VSSDKSmartTagTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#1)]  
  
3.  Adicione uma classe chamada `TestSmartTag` que herda de <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag>.  
  
     [!code-csharp[VSSDKSmartTagTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#2)]
     [!code-vb[VSSDKSmartTagTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#2)]  
  
4.  Adicione um construtor para essa classe que chama o construtor base com um <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType> de <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType>, que fará com que uma linha azul sejam exibidos sob o primeiro caractere de uma palavra. (Se você usar <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTagType>, uma linha vermelha aparecerá sob o último caractere da palavra.)  
  
     [!code-csharp[VSSDKSmartTagTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#3)]
     [!code-vb[VSSDKSmartTagTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#3)]  
  
5.  Adicione uma classe chamada `TestSmartTagger` que herda de <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> do tipo `TestSmartTag`e implementa <xref:System.IDisposable>.  
  
     [!code-csharp[VSSDKSmartTagTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#4)]
     [!code-vb[VSSDKSmartTagTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#4)]  
  
6.  Adicione os seguintes campos privados para a classe de marcador.  
  
     [!code-csharp[VSSDKSmartTagTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#5)]
     [!code-vb[VSSDKSmartTagTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#5)]  
  
7.  Adicione um construtor que define os campos particulares e assina o <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> eventos.  
  
     [!code-csharp[VSSDKSmartTagTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#6)]
     [!code-vb[VSSDKSmartTagTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#6)]  
  
8.  Implementar <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> para que a marca é criada para a palavra atual. (Esse método também chama um método particular `GetSmartTagActions` que será explicado posteriormente.)  
  
     [!code-csharp[VSSDKSmartTagTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#7)]
     [!code-vb[VSSDKSmartTagTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#7)]  
  
9. Adicionar um `GetSmartTagActions` método para configurar as ações de marca inteligente. As ações propriamente ditas são implementadas em etapas posteriores.  
  
     [!code-csharp[VSSDKSmartTagTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#8)]
     [!code-vb[VSSDKSmartTagTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#8)]  
  
10. Declare o `SmartTagsChanged` eventos.  
  
     [!code-csharp[VSSDKSmartTagTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#9)]
     [!code-vb[VSSDKSmartTagTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#9)]  
  
11. Implemente a `OnLayoutChanged` manipulador de eventos para gerar o `TagsChanged` evento, que faz com que <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> a ser chamado.  
  
     [!code-csharp[VSSDKSmartTagTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#10)]
     [!code-vb[VSSDKSmartTagTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#10)]  
  
12. Implemente a <xref:System.IDisposable.Dispose%2A> , de modo que ele cancela a assinatura do <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> eventos.  
  
     [!code-csharp[VSSDKSmartTagTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#11)]
     [!code-vb[VSSDKSmartTagTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#11)]  
  
## <a name="implementing-the-smart-tag-tagger-provider"></a>Implementando o provedor de marcador de marca inteligente  
  
#### <a name="to-implement-the-smart-tag-tagger-provider"></a>Para implementar o provedor de marcador de marca inteligente  
  
1.  Adicione uma classe chamada `TestSmartTagTaggerProvider` que herda de <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>. Exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text", uma <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes = "default" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Language.Intellisense.SmartTag>.  
  
     [!code-csharp[VSSDKSmartTagTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#12)]
     [!code-vb[VSSDKSmartTagTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#12)]  
  
2.  Importar o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> como uma propriedade.  
  
     [!code-csharp[VSSDKSmartTagTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#13)]
     [!code-vb[VSSDKSmartTagTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#13)]  
  
3.  Implementar o método de <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> .  
  
     [!code-csharp[VSSDKSmartTagTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#14)]
     [!code-vb[VSSDKSmartTagTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#14)]  
  
## <a name="implementing-smart-tag-actions"></a>Implementação de ações de marca inteligente  
  
#### <a name="to-implement-smart-tag-actions"></a>Para implementar as ações de marca inteligente  
  
1. Crie duas classes, a primeira chamada `UpperCaseSmartTagAction` e a segunda chamada `LowerCaseSmartTagAction`. Ambas as classes implementam <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagAction>.  
  
    [!code-csharp[VSSDKSmartTagTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#15)]
    [!code-vb[VSSDKSmartTagTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#15)]  
  
    [!code-csharp[VSSDKSmartTagTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#16)]
    [!code-vb[VSSDKSmartTagTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#16)]  
  
   Ambas as classes são semelhantes, exceto que um chama <xref:System.String.ToUpper%2A> e as outras chamadas <xref:System.String.ToLower%2A>. As etapas a seguir abrangem apenas a classe de ação em maiusculas, mas você deve implementar as duas classes. Use as etapas para implementar a ação de letras maiusculas como um padrão para implementar a ação em minúsculas.  
  
2. Declare um conjunto de campos particulares.  
  
    [!code-csharp[VSSDKSmartTagTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#17)]
    [!code-vb[VSSDKSmartTagTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#17)]  
  
3. Adicione um construtor que define os campos.  
  
    [!code-csharp[VSSDKSmartTagTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#18)]
    [!code-vb[VSSDKSmartTagTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#18)]  
  
4. Implemente as propriedades da seguinte maneira.  
  
    [!code-csharp[VSSDKSmartTagTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#19)]
    [!code-vb[VSSDKSmartTagTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#19)]  
  
5. Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagAction.Invoke%2A> método, substituindo o texto no trecho com seu equivalente em maiusculas.  
  
    [!code-csharp[VSSDKSmartTagTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksmarttagtest/cs/testsmarttag.cs#20)]
    [!code-vb[VSSDKSmartTagTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksmarttagtest/vb/testsmarttag.vb#20)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução SmartTagTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-the-smarttagtest-solution"></a>Para compilar e testar a solução SmartTagTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
3.  Crie um arquivo de texto e digite algum texto.  
  
     Uma linha azul deve ser exibida na primeira letra da primeira palavra do texto.  
  
4.  Mova o ponteiro sobre a linha azul.  
  
     Um botão deve ser exibido perto do ponteiro.  
  
5.  Quando você clica no botão, duas sugeridas ações devem ser exibidas: **convertida em letras maiusculas** e **converter em letras minúsculas**. Se você clicar na primeira ação, todo o texto da palavra atual deve ser convertido em letras maiusculas. Se você clicar na segunda ação, todo o texto deve ser convertido em letras minúsculas.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)