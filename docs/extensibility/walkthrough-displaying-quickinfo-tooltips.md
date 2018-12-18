---
title: 'Passo a passo: Exibindo dicas de ferramenta de QuickInfo | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e5ff8b850287e91cf2a1e5e6a546980c9087541d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49824172"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>Passo a passo: Dicas de ferramenta de QuickInfo vídeo
QuickInfo é um recurso IntelliSense, que exibe as assinaturas de método e descrições de quando um usuário move o ponteiro sobre um nome de método. Você pode implementar recursos de baseada na linguagem, como QuickInfo definindo os identificadores para o qual você deseja fornecer descrições de QuickInfo e, em seguida, criando uma dica de ferramenta para exibir o conteúdo. Você pode definir QuickInfo no contexto de um serviço de linguagem, ou você pode definir seu próprio tipo de conteúdo e a extensão de nome do arquivo e exibir o QuickInfo para apenas esse tipo, ou você pode exibir QuickInfo para um tipo de conteúdo existente (como "texto"). Este passo a passo mostra como exibir QuickInfo para o tipo de conteúdo "text".  
  
 O exemplo de QuickInfo neste passo a passo exibe as dicas de ferramenta quando um usuário move o ponteiro sobre um nome de método. Esse design requer que você implementar esses quatro interfaces:  
  
- interface de origem  
  
- interface de provedor de origem  
  
- interface do controlador  
  
- interface de provedor do controlador  
  
  Os provedores de origem e o controlador são partes do componente Managed Extensibility Framework (MEF) e serão responsáveis pela exportação as classes de origem e o controlador e importação de serviços e os agentes, como o <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>, que cria o texto de dica de ferramenta buffer e o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>, que dispara a sessão de QuickInfo.  
  
  Neste exemplo, a fonte de QuickInfo usa uma lista de embutido em código do método nomes e descrições, mas em implementações completas, o serviço de linguagem e a documentação da linguagem são responsáveis por fornecer esse conteúdo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não precisa instalar o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-mef-project"></a>Criar um projeto MEF  
  
### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `QuickInfoTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="implement-the-quickinfo-source"></a>Implementar a fonte de QuickInfo  
 A fonte de QuickInfo é responsável por coletar o conjunto de identificadores e suas descrições e adicionando o conteúdo para o buffer de texto de dica de ferramenta quando um dos identificadores é encontrado. Neste exemplo, os identificadores e suas descrições são adicionadas apenas de no construtor de origem.  
  
#### <a name="to-implement-the-quickinfo-source"></a>Para implementar o código-fonte QuickInfo  
  
1.  Adicione um arquivo de classe e denomine- `TestQuickInfoSource`.  
  
2.  Adicione uma referência ao *Microsoft.VisualStudio.Language.IntelliSense*.  
  
3.  Adicione as importações a seguir.  
  
     [!code-vb[VSSDKQuickInfoTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_1.vb)]
     [!code-csharp[VSSDKQuickInfoTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_1.cs)]  
  
4.  Declarar uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>e nomeie-o `TestQuickInfoSource`.  
  
     [!code-vb[VSSDKQuickInfoTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_2.vb)]
     [!code-csharp[VSSDKQuickInfoTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_2.cs)]  
  
5.  Adicione campos para o provedor de código-fonte QuickInfo, o buffer de texto e um conjunto de nomes de método e assinaturas de método. Neste exemplo, os nomes de método e as assinaturas são inicializadas no `TestQuickInfoSource` construtor.  
  
     [!code-vb[VSSDKQuickInfoTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_3.vb)]
     [!code-csharp[VSSDKQuickInfoTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_3.cs)]  
  
6.  Adicione um construtor que define o provedor de fonte de QuickInfo e o buffer de texto e preenche o conjunto de nomes de método e assinaturas de método e descrições.  
  
     [!code-vb[VSSDKQuickInfoTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_4.vb)]
     [!code-csharp[VSSDKQuickInfoTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_4.cs)]  
  
7.  Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> . Neste exemplo, o método localiza a palavra atual ou a palavra anterior, se o cursor estiver no final de uma linha ou um buffer de texto. Se o word é um dos nomes de método, a descrição para o nome desse método é adicionada ao conteúdo QuickInfo.  
  
     [!code-vb[VSSDKQuickInfoTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_5.vb)]
     [!code-csharp[VSSDKQuickInfoTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_5.cs)]  
  
8.  Você também deve implementar um método Dispose (), desde <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> implementa <xref:System.IDisposable>:  
  
     [!code-vb[VSSDKQuickInfoTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_6.vb)]
     [!code-csharp[VSSDKQuickInfoTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_6.cs)]  
  
## <a name="implement-a-quickinfo-source-provider"></a>Implementar um provedor de fonte de QuickInfo  
 O provedor da fonte de QuickInfo serve principalmente para exportar a mesma como uma parte do componente MEF e criar uma instância de fonte de QuickInfo. Porque é uma parte do componente de MEF, ele pode importar outras partes do componente MEF.  
  
#### <a name="to-implement-a-quickinfo-source-provider"></a>Para implementar um provedor de fonte de QuickInfo  
  
1.  Declarar um provedor de fonte de QuickInfo denominado `TestQuickInfoSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "Dica de ferramenta com a fonte QuickInfo", uma <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes = "default" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text".  
  
     [!code-vb[VSSDKQuickInfoTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_7.vb)]
     [!code-csharp[VSSDKQuickInfoTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_7.cs)]  
  
2.  Importar os dois serviços do editor, <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> e <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>, como propriedades do `TestQuickInfoSourceProvider`.  
  
     [!code-vb[VSSDKQuickInfoTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_8.vb)]
     [!code-csharp[VSSDKQuickInfoTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_8.cs)]  
  
3.  Implemente <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> para retornar um novo `TestQuickInfoSource`.  
  
     [!code-vb[VSSDKQuickInfoTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_9.vb)]
     [!code-csharp[VSSDKQuickInfoTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_9.cs)]  
  
## <a name="implement-a-quickinfo-controller"></a>Implementar um controlador de QuickInfo  
 Controladores de QuickInfo determinam quando QuickInfo for exibido. Neste exemplo, QuickInfo aparece quando o ponteiro está sobre uma palavra que corresponde a um dos nomes de método. O controlador de QuickInfo implementa um manipulador de eventos de passagem de mouse que dispara uma sessão de QuickInfo.  
  
### <a name="to-implement-a-quickinfo-controller"></a>Para implementar um controlador de QuickInfo  
  
1.  Declarar uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>e nomeie-o `TestQuickInfoController`.  
  
     [!code-vb[VSSDKQuickInfoTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_10.vb)]
     [!code-csharp[VSSDKQuickInfoTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_10.cs)]  
  
2.  Adicione campos privados para o modo de exibição de texto, os buffers de texto representados na exibição de texto, a sessão de QuickInfo e o provedor de controlador de QuickInfo.  
  
     [!code-vb[VSSDKQuickInfoTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_11.vb)]
     [!code-csharp[VSSDKQuickInfoTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_11.cs)]  
  
3.  Adicione um construtor que define os campos e adiciona o manipulador de eventos do mouse em foco.  
  
     [!code-vb[VSSDKQuickInfoTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_12.vb)]
     [!code-csharp[VSSDKQuickInfoTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_12.cs)]  
  
4.  Adicione o manipulador de eventos do mouse em foco que dispara a sessão de QuickInfo.  
  
     [!code-vb[VSSDKQuickInfoTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_13.vb)]
     [!code-csharp[VSSDKQuickInfoTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_13.cs)]  
  
5.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A> , de modo que ele remove o manipulador de eventos do mouse em foco quando o controlador é desanexado da exibição do texto.  
  
     [!code-vb[VSSDKQuickInfoTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_14.vb)]
     [!code-csharp[VSSDKQuickInfoTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_14.cs)]  
  
6.  Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A> método e o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> método como métodos vazios para este exemplo.  
  
     [!code-vb[VSSDKQuickInfoTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_15.vb)]
     [!code-csharp[VSSDKQuickInfoTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_15.cs)]  
  
## <a name="implementing-the-quickinfo-controller-provider"></a>Implementando o provedor de controlador de QuickInfo  
 O provedor do controlador QuickInfo serve principalmente para exportar a mesma como uma parte do componente MEF e instanciar o controlador de QuickInfo. Porque é uma parte do componente de MEF, ele pode importar outras partes do componente MEF.  
  
### <a name="to-implement-the-quickinfo-controller-provider"></a>Para implementar o provedor de controlador de QuickInfo  
  
1.  Declare uma classe chamada `TestQuickInfoControllerProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "Dica de ferramenta QuickInfo controlador" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text":  
  
     [!code-vb[VSSDKQuickInfoTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_16.vb)]
     [!code-csharp[VSSDKQuickInfoTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_16.cs)]  
  
2.  Importar o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> como uma propriedade.  
  
     [!code-vb[VSSDKQuickInfoTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_17.vb)]
     [!code-csharp[VSSDKQuickInfoTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_17.cs)]  
  
3.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> método instanciando o controlador de QuickInfo.  
  
     [!code-vb[VSSDKQuickInfoTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_18.vb)]
     [!code-csharp[VSSDKQuickInfoTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_18.cs)]  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução QuickInfoTest e executá-lo na instância experimental.  
  
### <a name="to-build-and-test-the-quickinfotest-solution"></a>Para compilar e testar a solução QuickInfoTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui as palavras "Adicionar" e "subtrair".  
  
4.  Mova o ponteiro sobre uma das ocorrências de "Adicionar". A assinatura e a descrição a `add` método deve ser exibido.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo para uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)