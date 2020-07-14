---
title: 'Walkthrough: estrutura de tópicos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb338803d50b2ecc9af8c8db6a6b6dc2f3631161
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906179"
---
# <a name="walkthrough-outlining"></a>Passo a passo: estrutura de tópicos
Configure recursos baseados em idioma, como estrutura de tópicos, definindo os tipos de regiões de texto que você deseja expandir ou recolher. Você pode definir regiões no contexto de um serviço de idioma ou definir sua própria extensão de nome de arquivo e tipo de conteúdo e aplicar a definição de região somente a esse tipo, ou aplicar as definições de região a um tipo de conteúdo existente (como "texto"). Este tutorial mostra como definir e exibir regiões de estrutura de tópicos.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto Managed Extensibility Framework (MEF)

### <a name="to-create-a-mef-project"></a>Para criar um projeto do MEF

1. Crie um projeto VSIX. Nomeie a solução `OutlineRegionTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

## <a name="implement-an-outlining-tagger"></a>Implementar um marca-estruturador de tópicos
 As regiões de estrutura de tópicos são marcadas por um tipo de marca ( <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> ). Essa marca fornece o comportamento de estrutura de tópicos padrão. A região contornada pode ser expandida ou recolhida. A região contornada é marcada por um sinal de adição ( **+** ) se for recolhida ou um sinal de subtração ( **-** ) se for expandido e a região expandida for demarcadasda por uma linha vertical.

 As etapas a seguir mostram como definir um marcador que cria regiões de estrutura de tópicos para todas as regiões delimitadas pelos colchetes (**[**,**]**).

### <a name="to-implement-an-outlining-tagger"></a>Para implementar um marca-estruturador de tópicos

1. Adicione um arquivo de classe e nomeie-o `OutliningTagger` .

2. Importe os namespaces a seguir.

     [!code-csharp[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/CSharp/walkthrough-outlining_1.cs)]
     [!code-vb[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_1.vb)]

3. Crie uma classe chamada `OutliningTagger` e implemente-a <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> :

     [!code-csharp[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/CSharp/walkthrough-outlining_2.cs)]
     [!code-vb[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_2.vb)]

4. Adicione alguns campos para acompanhar o buffer de texto e o instantâneo e para acumular os conjuntos de linhas que devem ser marcados como regiões de estrutura de tópicos. Esse código inclui uma lista de objetos Region (a serem definidos posteriormente) que representam as regiões de estrutura de tópicos.

     [!code-csharp[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/CSharp/walkthrough-outlining_3.cs)]
     [!code-vb[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_3.vb)]

5. Adicione um construtor de marcação que inicializa os campos, analisa o buffer e adiciona um manipulador de eventos ao <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> evento.

     [!code-csharp[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/CSharp/walkthrough-outlining_4.cs)]
     [!code-vb[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_4.vb)]

6. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método, que instancia as extensões de marca. Este exemplo supõe que as extensões em <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> passado para o método são contíguas, embora talvez nem sempre sejam o caso. Esse método instancia um novo Span de marca para cada uma das regiões de estrutura de tópicos.

     [!code-csharp[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/CSharp/walkthrough-outlining_5.cs)]
     [!code-vb[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_5.vb)]

7. Declare um `TagsChanged` manipulador de eventos.

     [!code-csharp[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/CSharp/walkthrough-outlining_6.cs)]
     [!code-vb[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_6.vb)]

8. Adicione um `BufferChanged` manipulador de eventos que responda a <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos analisando o buffer de texto.

     [!code-csharp[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/CSharp/walkthrough-outlining_7.cs)]
     [!code-vb[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_7.vb)]

9. Adicione um método que analisa o buffer. O exemplo fornecido aqui é apenas para ilustração. Ele analisa de forma síncrona o buffer em regiões aninhadas da estrutura de tópicos.

     [!code-csharp[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/CSharp/walkthrough-outlining_8.cs)]
     [!code-vb[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_8.vb)]

10. O método auxiliar a seguir obtém um inteiro que representa o nível da estrutura de tópicos, de modo que 1 é o par de chaves mais à esquerda.

     [!code-csharp[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/CSharp/walkthrough-outlining_9.cs)]
     [!code-vb[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_9.vb)]

11. O método auxiliar a seguir converte uma região (definida mais adiante neste artigo) em um SnapshotSpan.

     [!code-csharp[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/CSharp/walkthrough-outlining_10.cs)]
     [!code-vb[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_10.vb)]

12. O código a seguir é apenas para ilustração. Ele define uma classe PartialRegion que contém o número de linha e o deslocamento do início de uma região de estrutura de tópicos e uma referência à região pai (se houver). Esse código permite que o analisador configure regiões de estrutura de tópicos aninhadas. Uma classe de região derivada contém uma referência ao número de linha do final de uma região de estrutura de tópicos.

     [!code-csharp[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/CSharp/walkthrough-outlining_11.cs)]
     [!code-vb[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_11.vb)]

## <a name="implement-a-tagger-provider"></a>Implementar um provedor de marca
 Exportar um provedor de marcação para o seu marcador. O provedor de marcação cria um `OutliningTagger` para um buffer do tipo de conteúdo "text" ou, caso contrário, retorna um `OutliningTagger` se o buffer já tiver um.

### <a name="to-implement-a-tagger-provider"></a>Para implementar um provedor de marcador

1. Crie uma classe chamada `OutliningTaggerProvider` que implementa e <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> exporte-a com os atributos ContentType e TagType.

     [!code-csharp[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/CSharp/walkthrough-outlining_12.cs)]
     [!code-vb[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_12.vb)]

2. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A> método adicionando um `OutliningTagger` às propriedades do buffer.

     [!code-csharp[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/CSharp/walkthrough-outlining_13.cs)]
     [!code-vb[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_13.vb)]

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução OutlineRegionTest e execute-a na instância experimental.

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>Para compilar e testar a solução OutlineRegionTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto. Digite um texto que inclua os colchetes de abertura e os colchetes de fechamento.

    ```
    [
       Hello
    ]
    ```

4. Deve haver uma região de estrutura de tópicos que inclua ambos os colchetes. Você deve ser capaz de clicar no sinal de subtração à esquerda do colchete de abertura para recolher a região de estrutura de tópicos. Quando a região é recolhida, o símbolo de reticências (*...*) deve aparecer à esquerda da região recolhida e um pop-up contendo o **texto de foco** do texto deve aparecer quando você move o ponteiro sobre as reticências.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
