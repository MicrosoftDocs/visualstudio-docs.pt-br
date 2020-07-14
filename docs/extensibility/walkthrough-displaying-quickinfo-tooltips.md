---
title: 'Walkthrough: exibindo dicas de ferramenta QuickInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: 0eb70e5d39708ffd532fe39d6d597043621158d5
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904827"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>Walkthrough: Exibir dicas de ferramenta QuickInfo
QuickInfo é um recurso do IntelliSense que exibe assinaturas de método e descrições quando um usuário move o ponteiro sobre um nome de método. Você pode implementar recursos baseados em linguagem, como QuickInfo, definindo os identificadores para os quais você deseja fornecer descrições de QuickInfo e, em seguida, criando uma dica de ferramenta para exibir o conteúdo. Você pode definir QuickInfo no contexto de um serviço de idioma ou pode definir sua própria extensão de nome de arquivo e tipo de conteúdo e exibir o QuickInfo para apenas esse tipo, ou pode exibir QuickInfo para um tipo de conteúdo existente (como "texto"). Este tutorial mostra como exibir QuickInfo para o tipo de conteúdo "text".

 O exemplo de QuickInfo neste passo a passos exibe as dicas de ferramenta quando um usuário move o ponteiro sobre um nome de método. Esse design exige que você implemente essas quatro interfaces:

- interface de origem

- interface do provedor de origem

- interface do controlador

- interface do provedor do controlador

  Os provedores de origem e controlador são Managed Extensibility Framework (MEF) partes de componente e são responsáveis por exportar as classes de origem e controlador e importar serviços e agentes, como o <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> , que cria o buffer de texto de dica de ferramenta e o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> , que dispara a sessão QuickInfo.

  Neste exemplo, a origem QuickInfo usa uma lista embutida em código de nomes e descrições de métodos, mas em implementações completas, o serviço de idioma e a documentação do idioma são responsáveis por fornecer esse conteúdo.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não precisa instalar o SDK do Visual Studio no centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-mef-project"></a>Criar um projeto do MEF

### <a name="to-create-a-mef-project"></a>Para criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `QuickInfoTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

## <a name="implement-the-quickinfo-source"></a>Implementar a origem do QuickInfo
 A origem QuickInfo é responsável por coletar o conjunto de identificadores e suas descrições e adicionar o conteúdo ao buffer de texto de dica de ferramenta quando um dos identificadores é encontrado. Neste exemplo, os identificadores e suas descrições são adicionados apenas no construtor de origem.

#### <a name="to-implement-the-quickinfo-source"></a>Para implementar a origem do QuickInfo

1. Adicione um arquivo de classe e nomeie-o `TestQuickInfoSource` .

2. Adicione uma referência a *Microsoft. VisualStudio. Language. IntelliSense*.

3. Adicione as seguintes importações.

     [!code-vb[VSSDKQuickInfoTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_1.vb)]
     [!code-csharp[VSSDKQuickInfoTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_1.cs)]

4. Declare uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> e nomeie-a `TestQuickInfoSource` .

     [!code-vb[VSSDKQuickInfoTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_2.vb)]
     [!code-csharp[VSSDKQuickInfoTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_2.cs)]

5. Adicione campos para o provedor de origem QuickInfo, o buffer de texto e um conjunto de nomes de método e assinaturas de método. Neste exemplo, os nomes de método e as assinaturas são inicializados no `TestQuickInfoSource` Construtor.

     [!code-vb[VSSDKQuickInfoTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_3.vb)]
     [!code-csharp[VSSDKQuickInfoTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_3.cs)]

6. Adicione um construtor que defina o provedor de origem QuickInfo e o buffer de texto e preencha o conjunto de nomes de método e as assinaturas e descrições de método.

     [!code-vb[VSSDKQuickInfoTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_4.vb)]
     [!code-csharp[VSSDKQuickInfoTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_4.cs)]

7. Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> . Neste exemplo, o método localiza a palavra atual ou a palavra anterior se o cursor estiver no final de uma linha ou um buffer de texto. Se a palavra for um dos nomes de método, a descrição desse nome de método será adicionada ao conteúdo QuickInfo.

     [!code-vb[VSSDKQuickInfoTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_5.vb)]
     [!code-csharp[VSSDKQuickInfoTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_5.cs)]

8. Você também deve implementar um método Dispose (), desde que <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> implemente <xref:System.IDisposable> :

     [!code-vb[VSSDKQuickInfoTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_6.vb)]
     [!code-csharp[VSSDKQuickInfoTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_6.cs)]

## <a name="implement-a-quickinfo-source-provider"></a>Implementar um provedor de origem QuickInfo
 O provedor da origem do QuickInfo serve principalmente para exportar a si mesmo como uma parte do componente do MEF e instanciar a origem do QuickInfo. Como é uma parte do componente do MEF, ele pode importar outras partes do componente do MEF.

#### <a name="to-implement-a-quickinfo-source-provider"></a>Para implementar um provedor de origem QuickInfo

1. Declare um provedor de origem QuickInfo chamado `TestQuickInfoSourceProvider` que implemente <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider> e exporte-o com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "código-fonte QuickInfo", um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes de = "default" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text".

     [!code-vb[VSSDKQuickInfoTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_7.vb)]
     [!code-csharp[VSSDKQuickInfoTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_7.cs)]

2. Importe dois serviços do editor <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> e <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> , como propriedades de `TestQuickInfoSourceProvider` .

     [!code-vb[VSSDKQuickInfoTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_8.vb)]
     [!code-csharp[VSSDKQuickInfoTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_8.cs)]

3. Implemente <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> para retornar um novo `TestQuickInfoSource` .

     [!code-vb[VSSDKQuickInfoTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_9.vb)]
     [!code-csharp[VSSDKQuickInfoTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_9.cs)]

## <a name="implement-a-quickinfo-controller"></a>Implementar um controlador QuickInfo
 Os controladores QuickInfo determinam quando QuickInfo é exibido. Neste exemplo, QuickInfo aparece quando o ponteiro está sobre uma palavra que corresponde a um dos nomes de método. O controlador QuickInfo implementa um manipulador de eventos de foco do mouse que dispara uma sessão QuickInfo.

### <a name="to-implement-a-quickinfo-controller"></a>Para implementar um controlador QuickInfo

1. Declare uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> e nomeie-a `TestQuickInfoController` .

     [!code-vb[VSSDKQuickInfoTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_10.vb)]
     [!code-csharp[VSSDKQuickInfoTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_10.cs)]

2. Adicione campos particulares para a exibição de texto, os buffers de texto representados na exibição de texto, a sessão QuickInfo e o provedor do controlador QuickInfo.

     [!code-vb[VSSDKQuickInfoTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_11.vb)]
     [!code-csharp[VSSDKQuickInfoTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_11.cs)]

3. Adicione um construtor que defina os campos e adicione o manipulador de eventos de foco do mouse.

     [!code-vb[VSSDKQuickInfoTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_12.vb)]
     [!code-csharp[VSSDKQuickInfoTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_12.cs)]

4. Adicione o manipulador de eventos de foco do mouse que dispara a sessão QuickInfo.

     [!code-vb[VSSDKQuickInfoTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_13.vb)]
     [!code-csharp[VSSDKQuickInfoTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_13.cs)]

5. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A> método para que ele remova o manipulador de eventos de foco do mouse quando o controlador for desanexado da exibição de texto.

     [!code-vb[VSSDKQuickInfoTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_14.vb)]
     [!code-csharp[VSSDKQuickInfoTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_14.cs)]

6. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A> método e o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> método como métodos vazios para este exemplo.

     [!code-vb[VSSDKQuickInfoTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_15.vb)]
     [!code-csharp[VSSDKQuickInfoTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_15.cs)]

## <a name="implementing-the-quickinfo-controller-provider"></a>Implementando o provedor do controlador QuickInfo
 O provedor do controlador QuickInfo serve principalmente para exportar a si mesmo como uma parte de componente do MEF e instanciar o controlador QuickInfo. Como é uma parte do componente do MEF, ele pode importar outras partes do componente do MEF.

### <a name="to-implement-the-quickinfo-controller-provider"></a>Para implementar o provedor do controlador QuickInfo

1. Declare uma classe denominada `TestQuickInfoControllerProvider` que implemente <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider> e exporte-a com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "controlador QuickInfo de dica de ferramenta" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto":

     [!code-vb[VSSDKQuickInfoTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_16.vb)]
     [!code-csharp[VSSDKQuickInfoTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_16.cs)]

2. Importe o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> como uma propriedade.

     [!code-vb[VSSDKQuickInfoTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_17.vb)]
     [!code-csharp[VSSDKQuickInfoTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_17.cs)]

3. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> método instanciando o controlador QuickInfo.

     [!code-vb[VSSDKQuickInfoTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_18.vb)]
     [!code-csharp[VSSDKQuickInfoTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_18.cs)]

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução QuickInfoTest e execute-a na instância experimental.

### <a name="to-build-and-test-the-quickinfotest-solution"></a>Para compilar e testar a solução QuickInfoTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto que inclua as palavras "Adicionar" e "subtrair".

4. Mova o ponteiro sobre uma das ocorrências de "Adicionar". A assinatura e a descrição do `add` método devem ser exibidas.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
