---
title: 'Passo a passo: Exibindo chaves correspondentes | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1f29596c95646db78145725f1f0cead424e1de5e
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500430"
---
# <a name="walkthrough-display-matching-braces"></a>Passo a passo: Exibir chaves correspondentes
Implemente recursos de baseada na linguagem, por exemplo, definindo as chaves que você deseja corresponder e adicionando uma marca de marcador de texto para as chaves correspondentes, quando o cursor está em uma das chaves a correspondência de chaves. Você pode definir chaves no contexto de um idioma, definir sua própria extensão de nome de arquivo e o tipo de conteúdo e aplicar as marcas para apenas esse tipo ou aplicam as marcas a um tipo de conteúdo existente (como "texto"). A instrução a seguir mostra como aplicar marcas para o tipo de conteúdo "texto" a correspondência de chaves.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto de Managed Extensibility Framework (MEF)  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de classificador do Editor. Nomeie a solução `BraceMatchingTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="implement-a-brace-matching-tagger"></a>Implementar um marcador de correspondência de chaves  
 Para obter um efeito semelhante ao que é usado no Visual Studio de realce de chave, você pode implementar um marcador de tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>. O código a seguir mostra como definir o marcador para pares de chave em qualquer nível de aninhamento. Neste exemplo, os pares de chave de [] e {} são definidos no construtor de marcador, mas em uma implementação de linguagem completa, a chave relevante pares seriam definidas na especificação da linguagem.  
  
### <a name="to-implement-a-brace-matching-tagger"></a>Para implementar um marcador de correspondência de chaves  
  
1.  Adicione um arquivo de classe e nomeie-a correspondência de chaves.  
  
2.  Importe os seguintes namespaces.  
  
     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]  
  
3.  Definir uma classe `BraceMatchingTagger` que herda de <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>.  
  
     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]  
  
4.  Adicione propriedades para a exibição de texto, o buffer de origem, o ponto do instantâneo atual e também um conjunto de pares de chave.  
  
     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]  
  
5.  No construtor de marcador, defina as propriedades e assinar os eventos de alteração do modo de exibição <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>. Neste exemplo, para fins ilustrativos, os pares correspondentes também são definidos no construtor.  
  
     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]  
  
6.  Como parte do <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> implementação, declare um evento TagsChanged.  
  
     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]  
  
7.  Os manipuladores de eventos atualizar a posição atual do cursor do `CurrentChar` propriedade e gerar o evento TagsChanged.  
  
     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]  
  
8.  Implementar o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método para corresponder chaves a quando o caractere atual for uma chave de abertura ou quando o caractere anterior for um colchete de fechamento, como no Visual Studio. Quando a correspondência for encontrada, esse método cria uma instância de duas marcas, um para a chave de abertura e outra para o colchete de fechamento.  
  
     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]  
  
9. Os seguintes métodos privados encontrar a chave correspondente em qualquer nível de aninhamento. O primeiro método encontra o caractere de fechamento que corresponde ao caractere aberto:  
  
     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]  
  
10. O método auxiliar a seguir localiza o caractere aberto que corresponde a um caractere de fechamento:  
  
     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]  
  
## <a name="implement-a-brace-matching-tagger-provider"></a>Implementar um provedor de marcador de correspondência de chaves  
 Além de implementar um marcador, você também deve implementar e exportar um provedor de marcador. Nesse caso, o tipo do provedor de conteúdo é "text". Portanto, correspondência de chaves será exibido em todos os tipos de arquivos de texto, mas uma implementação mais completa se aplica somente a um tipo específico de conteúdo a correspondência de chaves.  
  
### <a name="to-implement-a-brace-matching-tagger-provider"></a>Para implementar um provedor de marcador de correspondência de chaves  
  
1.  Declarar um provedor de marcador que herda de <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>, nomeie-o BraceMatchingTaggerProvider e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>.  
  
     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]  
  
2.  Implementar o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> método para instanciar um BraceMatchingTagger.  
  
     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução BraceMatchingTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-bracematchingtest-solution"></a>Para compilar e testar a solução BraceMatchingTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui chaves correspondentes.  
  
    ```  
    hello {  
    goodbye}  
  
    {}  
  
    {hello}  
    ```  
  
4.  Quando você posiciona o cursor antes de uma chave de abertura, essa chave e o colchete de fechamento correspondente deve ser realçado. Quando você posiciona o cursor logo após o colchete de fechamento, essa chave e a chave de abertura correspondente deve ser realçada.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo para uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)