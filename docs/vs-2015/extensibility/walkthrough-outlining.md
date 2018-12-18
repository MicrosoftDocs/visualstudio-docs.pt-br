---
title: 'Instruções passo a passo: a estrutura de tópicos | Microsoft Docs'
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
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
caps.latest.revision: 31
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 897ff6a39716f424c40fa587d905847a0dbb3682
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51805262"
---
# <a name="walkthrough-outlining"></a>Passo a passo: estrutura de tópicos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode implementar recursos de baseada na linguagem, como a estrutura de tópicos, definindo os tipos de regiões de texto que você deseja expandir ou recolher. Você pode definir regiões no contexto de um serviço de linguagem, ou você pode definir seu próprio tipo de conteúdo e a extensão de nome do arquivo e aplicar a definição de região para apenas esse tipo, ou você pode aplicar as definições de região a um tipo de conteúdo existente (como "texto"). Este passo a passo mostra como definir e exibir regiões de estrutura de tópicos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Criando um projeto do Managed Extensibility Framework (MEF)  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto VSIX. Nomeie a solução `OutlineRegionTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="implementing-an-outlining-tagger"></a>Implementando um marcador de estrutura de tópicos  
 Regiões de estrutura de tópicos são marcados por um tipo de marca (<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>). Essa marca fornece o padrão de comportamento da estrutura de tópicos. A região de estrutura pode ser expandido ou recolhido. A região de estrutura é marcado por um sinal de adição, se ele estiver recolhido ou um sinal de menos se ela é expandida e a região expandida é delimitada por uma linha vertical.  
  
 As etapas a seguir mostram como definir um marcador que cria regiões de estrutura de tópicos para todas as regiões que são delimitadas por "[" e "]".  
  
#### <a name="to-implement-an-outlining-tagger"></a>Para implementar um marcador de estrutura de tópicos  
  
1.  Adicione um arquivo de classe e denomine- `OutliningTagger`.  
  
2.  Importe os seguintes namespaces.  
  
     [!code-csharp[VSSDKOutlineRegionTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#1)]
     [!code-vb[VSSDKOutlineRegionTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#1)]  
  
3.  Crie uma classe denominada `OutliningTagger`, e fazê-lo a implementar <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>:  
  
     [!code-csharp[VSSDKOutlineRegionTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#2)]
     [!code-vb[VSSDKOutlineRegionTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#2)]  
  
4.  Adicione alguns campos para acompanhar o instantâneo e o buffer de texto e a se acumular os conjuntos de linhas que devem ser marcadas como regiões de estrutura de tópicos. Esse código inclui uma lista de objetos de região (a ser definido mais tarde) que representam as regiões de estrutura de tópicos.  
  
     [!code-csharp[VSSDKOutlineRegionTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#3)]
     [!code-vb[VSSDKOutlineRegionTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#3)]  
  
5.  Adicione um construtor de marcador que inicializa os campos, analisa o buffer e adiciona um manipulador de eventos para o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos.  
  
     [!code-csharp[VSSDKOutlineRegionTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#4)]
     [!code-vb[VSSDKOutlineRegionTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#4)]  
  
6.  Implementar o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> abrange de método, que instancia a marca. Este exemplo supõe que os intervalos no <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> passado para o método são contíguos, embora isso possa não ser sempre o caso. Esse método cria uma instância de um novo intervalo de marca para cada uma das regiões de estrutura de tópicos.  
  
     [!code-csharp[VSSDKOutlineRegionTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#5)]
     [!code-vb[VSSDKOutlineRegionTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#5)]  
  
7.  Declarar um `TagsChanged` manipulador de eventos.  
  
     [!code-csharp[VSSDKOutlineRegionTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#6)]
     [!code-vb[VSSDKOutlineRegionTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#6)]  
  
8.  Adicionar um `BufferChanged` manipulador de eventos que responde a <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos analisando o buffer de texto.  
  
     [!code-csharp[VSSDKOutlineRegionTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#7)]
     [!code-vb[VSSDKOutlineRegionTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#7)]  
  
9. Adicione um método que analisa o buffer. O exemplo fornecido aqui é apenas para fins ilustrativos. Analisa o buffer de forma síncrona em regiões de estrutura de tópicos aninhadas.  
  
     [!code-csharp[VSSDKOutlineRegionTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#8)]
     [!code-vb[VSSDKOutlineRegionTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#8)]  
  
10. O método auxiliar a seguir obtém um inteiro que representa o nível de estrutura de tópicos, de forma que 1 é o par de chaves mais à esquerda.  
  
     [!code-csharp[VSSDKOutlineRegionTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#9)]
     [!code-vb[VSSDKOutlineRegionTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#9)]  
  
11. O método auxiliar a seguir converte uma região (definida mais tarde neste tópico) em um SnapshotSpan.  
  
     [!code-csharp[VSSDKOutlineRegionTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#10)]
     [!code-vb[VSSDKOutlineRegionTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#10)]  
  
12. O código a seguir é apenas para fins ilustrativos. Ele define uma classe PartialRegion que contém o número de linha e o deslocamento do início de uma região de estrutura de tópicos e também uma referência para a região pai (se houver). Isso permite que o analisador configurar aninhados regiões de estrutura de tópicos. Uma classe derivada de região contém uma referência para o número de linha de final de uma região de estrutura de tópicos.  
  
     [!code-csharp[VSSDKOutlineRegionTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#11)]
     [!code-vb[VSSDKOutlineRegionTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#11)]  
  
## <a name="implementing-a-tagger-provider"></a>Implementando um provedor de marcador  
 Você deve exportar um provedor de marcador para o marcador. O provedor de marcador cria uma `OutliningTagger` para um buffer do tipo de conteúdo "text", ou outra retornará um `OutliningTagger` se o buffer já tenha um.  
  
#### <a name="to-implement-a-tagger-provider"></a>Para implementar um provedor de marcador  
  
1.  Crie uma classe denominada `OutliningTaggerProvider` que implementa <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>e exportá-lo com os atributos ContentType e TagType.  
  
     [!code-csharp[VSSDKOutlineRegionTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#12)]
     [!code-vb[VSSDKOutlineRegionTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#12)]  
  
2.  Implemente a <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A> método adicionando um `OutliningTagger` às propriedades do buffer.  
  
     [!code-csharp[VSSDKOutlineRegionTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#13)]
     [!code-vb[VSSDKOutlineRegionTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#13)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução OutlineRegionTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-the-outlineregiontest-solution"></a>Para compilar e testar a solução OutlineRegionTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
3.  Crie um arquivo de texto. Digite algum texto que inclui a chave de abertura e a chave de fechamento.  
  
    ```  
    [  
       Hello  
    ]  
    ```  
  
4.  Deve haver uma região de estrutura de tópicos que inclui a ambas as chaves. Você poderá clicar no sinal de subtração à esquerda da chave de abertura para recolher a região de estrutura de tópicos. Quando a região estiver recolhido, o símbolo de reticências (...) devem aparecer à esquerda de um pop-up que contém o texto e a região recolhida **passe o mouse texto** deve aparecer quando você move o ponteiro sobre o botão de reticências.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

