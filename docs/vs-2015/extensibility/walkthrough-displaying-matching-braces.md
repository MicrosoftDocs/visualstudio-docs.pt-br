---
title: 'Passo a passo: Exibindo chaves correspondentes | Microsoft Docs'
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
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
caps.latest.revision: 28
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9795cd3c40eeff714d55f4bb95f78cf1f7f8aea9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745881"
---
# <a name="walkthrough-displaying-matching-braces"></a>Passo a passo: exibindo chaves correspondentes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode implementar recursos de baseada na linguagem, como correspondência definindo as chaves que você deseja corresponder e, em seguida, adicionar uma marca de marcador de texto as chaves correspondentes quando o cursor está em uma das chaves de chaves. Você pode definir chaves no contexto de um idioma, ou você pode definir seu próprio tipo de conteúdo e a extensão de nome do arquivo e aplicar as marcas a apenas esse tipo, ou você pode aplicar marcas a um tipo de conteúdo existente (como "texto"). A instrução a seguir mostra como aplicar marcas para o tipo de conteúdo "texto" a correspondência de chaves.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Criando um projeto do Managed Extensibility Framework (MEF)  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de classificador do Editor. Nomeie a solução `BraceMatchingTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="implementing-a-brace-matching-tagger"></a>Implementando um marcador de correspondência de chaves  
 Para obter um efeito semelhante ao que é usado no Visual Studio de realce de chave, você pode implementar um marcador de tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>. O código a seguir mostra como definir o marcador para pares de chave em qualquer nível de aninhamento. Neste exemplo, os pares de chave []. [], e {} são definidos no construtor de marcador, mas em uma implementação da linguagem completa de pares de chave relevante seriam definidos na especificação da linguagem.  
  
#### <a name="to-implement-a-brace-matching-tagger"></a>Para implementar um marcador de correspondência de chaves  
  
1.  Adicione um arquivo de classe e nomeie-a correspondência de chaves.  
  
2.  Importe os seguintes namespaces.  
  
     [!code-csharp[VSSDKBraceMatchingTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#1)]
     [!code-vb[VSSDKBraceMatchingTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#1)]  
  
3.  Definir uma classe `BraceMatchingTagger` que herda de <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>.  
  
     [!code-csharp[VSSDKBraceMatchingTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#2)]
     [!code-vb[VSSDKBraceMatchingTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#2)]  
  
4.  Adicione propriedades para a exibição de texto, o buffer de origem e o ponto do instantâneo atual e também um conjunto de pares de chave.  
  
     [!code-csharp[VSSDKBraceMatchingTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#3)]
     [!code-vb[VSSDKBraceMatchingTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#3)]  
  
5.  No construtor de marcador, defina as propriedades e assinar os eventos de alteração do modo de exibição <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>. Neste exemplo, para fins ilustrativos, os pares correspondentes também são definidos no construtor.  
  
     [!code-csharp[VSSDKBraceMatchingTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#4)]
     [!code-vb[VSSDKBraceMatchingTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#4)]  
  
6.  Como parte do <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> implementação, declare um evento TagsChanged.  
  
     [!code-csharp[VSSDKBraceMatchingTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#5)]
     [!code-vb[VSSDKBraceMatchingTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#5)]  
  
7.  Os manipuladores de eventos atualizar a posição atual do cursor do `CurrentChar` propriedade e gerar o evento TagsChanged.  
  
     [!code-csharp[VSSDKBraceMatchingTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#6)]
     [!code-vb[VSSDKBraceMatchingTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#6)]  
  
8.  Implementar o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método para corresponder chaves a quando o caractere atual for uma chave de abertura ou quando o caractere anterior for um colchete de fechamento, como no Visual Studio. Quando a correspondência for encontrada, esse método cria uma instância de duas marcas, um para a chave de abertura e outra para o colchete de fechamento.  
  
     [!code-csharp[VSSDKBraceMatchingTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#7)]
     [!code-vb[VSSDKBraceMatchingTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#7)]  
  
9. Os seguintes métodos privados encontrar a chave correspondente em qualquer nível de aninhamento. O primeiro método encontra o caractere de fechamento que corresponde ao caractere aberto:  
  
     [!code-csharp[VSSDKBraceMatchingTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#8)]
     [!code-vb[VSSDKBraceMatchingTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#8)]  
  
10. O método auxiliar a seguir localiza o caractere aberto que corresponde a um caractere de fechamento:  
  
     [!code-csharp[VSSDKBraceMatchingTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#9)]
     [!code-vb[VSSDKBraceMatchingTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#9)]  
  
## <a name="implementing-a-brace-matching-tagger-provider"></a>Implementando um provedor de marcador de correspondência de chaves  
 Além de implementar um marcador, você também deve implementar e exportar um provedor de marcador. Nesse caso, o tipo do provedor de conteúdo é "text". Isso significa que a correspondência de chaves será exibido em todos os tipos de arquivos de texto, mas uma implementação mais completa se aplica somente a um tipo específico de conteúdo a correspondência de chaves.  
  
#### <a name="to-implement-a-brace-matching-tagger-provider"></a>Para implementar um provedor de marcador de correspondência de chaves  
  
1.  Declarar um provedor de marcador que herda de <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>, nomeie-o BraceMatchingTaggerProvider e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>.  
  
     [!code-csharp[VSSDKBraceMatchingTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#10)]
     [!code-vb[VSSDKBraceMatchingTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#10)]  
  
2.  Implementar o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> método para instanciar um BraceMatchingTagger.  
  
     [!code-csharp[VSSDKBraceMatchingTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#11)]
     [!code-vb[VSSDKBraceMatchingTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#11)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução BraceMatchingTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-bracematchingtest-solution"></a>Para compilar e testar a solução BraceMatchingTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui chaves correspondentes.  
  
    ```  
    hello {  
    goodbye}  
  
    {}  
  
    {hello}  
    ```  
  
4.  Quando você posiciona o cursor antes de uma chave de abertura, essa chave e o colchete de fechamento correspondente deve ser realçado. Quando você posiciona o cursor logo após o colchete de fechamento, essa chave e a chave de abertura correspondente deve ser realçada.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

