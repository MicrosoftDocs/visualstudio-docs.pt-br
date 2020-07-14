---
title: 'Walkthrough: Criando um glifo de margem | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b94ab61f56d74537758c189adc9c104516f67f92
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905053"
---
# <a name="walkthrough-create-a-margin-glyph"></a>Walkthrough: criar um glifo de margem
Você pode personalizar a aparência das margens do editor usando extensões de editor personalizadas. Este passo a passos coloca um glifo personalizado na margem do indicador sempre que a palavra "todo" aparecer em um comentário de código.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-mef-project"></a>Criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `TodoGlyphTest` .

2. Adicione um item de projeto de classificação do editor. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

## <a name="define-the-glyph"></a>Definir o glifo
 Defina um glifo executando a <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> interface.

### <a name="to-define-the-glyph"></a>Para definir o glifo

1. Adicione um arquivo de classe e nomeie-o `TodoGlyphFactory` .

2. Adicione o código a seguir usando declarações.

     [!code-csharp[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_1.cs)]
     [!code-vb[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_1.vb)]

3. Adicione uma classe chamada `TodoGlyphFactory` que implementa <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> .

     [!code-csharp[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_2.cs)]
     [!code-vb[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_2.vb)]

4. Adicione um campo particular que define as dimensões do glifo.

     [!code-csharp[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_3.cs)]
     [!code-vb[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_3.vb)]

5. Implemente `GenerateGlyph` definindo o elemento da interface do usuário de glifos. `TodoTag`é definido posteriormente neste passo a passos.

     [!code-csharp[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_4.cs)]
     [!code-vb[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_4.vb)]

6. Adicione uma classe chamada `TodoGlyphFactoryProvider` que implementa <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> . Exporte essa classe com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "TodoGlyph", um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de após VsTextMarker, um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "Code" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de TodoTag.

     [!code-csharp[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_5.cs)]
     [!code-vb[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_5.vb)]

7. Implemente o <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A> método instanciando o `TodoGlyphFactory` .

     [!code-csharp[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_6.cs)]
     [!code-vb[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_6.vb)]

## <a name="define-a-todo-tag-and-tagger"></a>Definir uma marcação e marca de tarefas
 Defina a relação entre o elemento de interface do usuário que você definiu nas etapas anteriores e a margem do indicador. Crie um tipo de marca e um marcador e exporte-o usando um provedor de marca.

### <a name="to-define-a-todo-tag-and-tagger"></a>Para definir uma marcação e marca de tarefas

1. Adicione um novo arquivo de classe ao projeto e nomeie-o `TodoTagger` .

2. Adicione as seguintes importações.

     [!code-csharp[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_7.cs)]
     [!code-vb[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_7.vb)]

3. Adicione uma classe chamada `TodoTag`.

     [!code-csharp[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_8.cs)]
     [!code-vb[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_8.vb)]

4. Modifique a classe chamada `TodoTagger` que implementa o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> tipo `TodoTag` .

     [!code-csharp[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_9.cs)]
     [!code-vb[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_9.vb)]

5. Para a `TodoTagger` classe, adicione campos particulares para um <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> e para o texto a ser localizado nos intervalos de classificação.

     [!code-csharp[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_10.cs)]
     [!code-vb[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_10.vb)]

6. Adicione um construtor que define o classificador.

     [!code-csharp[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_11.cs)]
     [!code-vb[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_11.vb)]

7. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> método encontrando todos os intervalos de classificação cujos nomes incluem a palavra "comentário" e cujo texto inclui o texto de pesquisa. Sempre que o texto de pesquisa for encontrado, gere novamente um novo <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> tipo `TodoTag` .

     [!code-csharp[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_12.cs)]
     [!code-vb[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_12.vb)]

8. Declare um `TagsChanged` evento.

     [!code-csharp[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_13.cs)]
     [!code-vb[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_13.vb)]

9. Adicione uma classe chamada `TodoTaggerProvider` que implementa <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> e exporte-a com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "código" e um <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> de TodoTag.

     [!code-csharp[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_14.cs)]
     [!code-vb[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_14.vb)]

10. Importe o <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> .

     [!code-csharp[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_15.cs)]
     [!code-vb[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_15.vb)]

11. Implemente o <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A> método instanciando o `TodoTagger` .

     [!code-csharp[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_16.cs)]
     [!code-vb[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_16.vb)]

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução TodoGlyphTest e execute-a na instância experimental.

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>Para compilar e testar a solução TodoGlyphTest

1. Compile a solução.

2. Execute o projeto pressionando **F5**. Uma segunda instância do Visual Studio é iniciada.

3. Verifique se a margem do indicador está sendo exibida. (No menu **ferramentas** , clique em **Opções**. Na página **Editor de texto** , verifique se a **margem do indicador** está selecionada.)

4. Abra um arquivo de código que tenha comentários. Adicione a palavra "todo" a uma das seções de comentário.

5. Um círculo azul claro com um contorno azul escuro aparece na margem do indicador à esquerda da janela de código.
