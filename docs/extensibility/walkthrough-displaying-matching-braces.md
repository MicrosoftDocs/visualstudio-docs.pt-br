---
title: 'Walkthrough: exibindo chaves correspondentes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65a0bc2c53d5d6e970b4aaa956170bc06c24e7c9
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904837"
---
# <a name="walkthrough-display-matching-braces"></a>Walkthrough: Exibir chaves correspondentes
Implemente recursos baseados em linguagem, como correspondência de chaves, definindo as chaves que você deseja corresponder e adicionando uma marca de marcador de texto às chaves correspondentes quando o cursor estiver em uma das chaves. Você pode definir chaves no contexto de um idioma, definir sua própria extensão de nome de arquivo e tipo de conteúdo e aplicar as marcas a apenas esse tipo ou aplicar as marcas a um tipo de conteúdo existente (como "texto"). A instrução a seguir mostra como aplicar marcas de correspondência de chaves ao tipo de conteúdo "text".

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto Managed Extensibility Framework (MEF)

#### <a name="to-create-a-mef-project"></a>Para criar um projeto do MEF

1. Crie um projeto classificador de editor. Nomeie a solução `BraceMatchingTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

## <a name="implement-a-brace-matching-tagger"></a>Implementar um marcador de correspondência de chaves
 Para obter um efeito de realce de chave que se assemelha a um que é usado no Visual Studio, você pode implementar um marcador do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> . O código a seguir mostra como definir o marcador para pares de chaves em qualquer nível de aninhamento. Neste exemplo, os pares de chaves de [] e {} são definidos no construtor do marcador, mas em uma implementação de idioma completo, os pares de chaves relevantes seriam definidos na especificação da linguagem.

### <a name="to-implement-a-brace-matching-tagger"></a>Para implementar um marcador de correspondência de chaves

1. Adicione um arquivo de classe e nomeie-o BraceMatching.

2. Importe os namespaces a seguir.

     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]

3. Defina uma classe `BraceMatchingTagger` que herda de <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> do tipo <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> .

     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]

4. Adicione Propriedades para a exibição de texto, o buffer de origem, o ponto de instantâneo atual e também um conjunto de pares de chaves.

     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]

5. No construtor de marca, defina as propriedades e assine os eventos de alteração de exibição <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> e <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> . Neste exemplo, para fins ilustrativos, os pares correspondentes também são definidos no construtor.

     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]

6. Como parte da <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> implementação, declare um evento tagschanged.

     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]

7. Os manipuladores de eventos atualizam a posição atual do cursor da `CurrentChar` propriedade e geram o evento tagschanged.

     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]

8. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método para corresponder chaves quando o caractere atual for uma chave de abertura ou quando o caractere anterior for uma chave de fechamento, como no Visual Studio. Quando a correspondência é encontrada, esse método instancia duas marcas, uma para a chave de abertura e outra para a chave de fechamento.

     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]

9. Os métodos privados a seguir localizam a chave correspondente em qualquer nível de aninhamento. O primeiro método localiza o caractere de fechamento que corresponde ao caractere aberto:

     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]

10. O seguinte método auxiliar localiza o caractere aberto que corresponde a um caractere de fechamento:

     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]

## <a name="implement-a-brace-matching-tagger-provider"></a>Implementar um provedor de marcação de correspondência de chaves
 Além de implementar um marcador, você também deve implementar e exportar um provedor de marca. Nesse caso, o tipo de conteúdo do provedor é "texto". Portanto, a correspondência de chaves aparecerá em todos os tipos de arquivos de texto, mas uma implementação mais completa aplica a correspondência de chaves somente a um tipo de conteúdo específico.

### <a name="to-implement-a-brace-matching-tagger-provider"></a>Para implementar um provedor de marcação de correspondência de chaves

1. Declare um provedor de marcação que herde de <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> , nomeie-o BraceMatchingTaggerProvider e exporte-o com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> .

     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]

2. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> método para criar uma instância de um BraceMatchingTagger.

     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução BraceMatchingTest e execute-a na instância experimental.

#### <a name="to-build-and-test-bracematchingtest-solution"></a>Para compilar e testar a solução BraceMatchingTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto que inclua chaves correspondentes.

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. Quando você posiciona o cursor antes de uma chave de abertura, essa chave e a chave de fechamento correspondente devem ser realçadas. Quando você posiciona o cursor logo após a chave de fechamento, essa chave e a chave de abertura correspondente devem ser realçadas.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
