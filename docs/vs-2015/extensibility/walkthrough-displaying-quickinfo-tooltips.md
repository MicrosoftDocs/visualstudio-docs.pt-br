---
title: 'Passo a passo: Exibindo dicas de ferramenta de QuickInfo | Microsoft Docs'
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
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
caps.latest.revision: 28
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9cd0e331536c194acdde95bdd74e5f41668a23e1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806273"
---
# <a name="walkthrough-displaying-quickinfo-tooltips"></a>Passo a passo: exibindo dicas de ferramenta de InformaçãoRápida
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

QuickInfo é um recurso IntelliSense, que exibe as assinaturas de método e descrições de quando um usuário move o ponteiro sobre um nome de método. Você pode implementar recursos de baseada na linguagem, como QuickInfo definindo os identificadores para o qual você deseja fornecer descrições de QuickInfo e, em seguida, criando uma dica de ferramenta para exibir o conteúdo. Você pode definir QuickInfo no contexto de um serviço de linguagem, ou você pode definir seu próprio tipo de conteúdo e a extensão de nome do arquivo e exibir o QuickInfo para apenas esse tipo, ou você pode exibir QuickInfo para um tipo de conteúdo existente (como "texto"). Este passo a passo mostra como exibir QuickInfo para o tipo de conteúdo "text".  
  
 O exemplo de QuickInfo neste passo a passo exibe as dicas de ferramenta quando um usuário move o ponteiro sobre um nome de método. Esse design requer que você implementar esses quatro interfaces:  
  
- interface de origem  
  
- interface de provedor de origem  
  
- interface do controlador  
  
- interface de provedor do controlador  
  
  Os provedores de origem e o controlador são partes do componente Managed Extensibility Framework (MEF) e serão responsáveis pela exportação as classes de origem e o controlador e importação de serviços e os agentes, como o <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>, que cria o texto de dica de ferramenta buffer e o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>, que dispara a sessão de QuickInfo.  
  
  Neste exemplo, a fonte de QuickInfo usa uma lista de embutido em código do método nomes e descrições, mas em implementações completas, o serviço de linguagem e a documentação da linguagem são responsáveis por fornecer esse conteúdo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-mef-project"></a>Criando um projeto MEF  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `QuickInfoTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
## <a name="implementing-the-quickinfo-source"></a>Implementando a fonte de QuickInfo  
 A fonte de QuickInfo é responsável por coletar o conjunto de identificadores e suas descrições e adicionando o conteúdo para o buffer de texto de dica de ferramenta quando um dos identificadores é encontrado. Neste exemplo, os identificadores e suas descrições são adicionadas apenas de no construtor de origem.  
  
#### <a name="to-implement-the-quickinfo-source"></a>Para implementar o código-fonte QuickInfo  
  
1.  Adicione um arquivo de classe e denomine- `TestQuickInfoSource`.  
  
2.  Adicione uma referência ao Microsoft.VisualStudio.Language.IntelliSense.  
  
3.  Adicione as importações a seguir.  
  
     [!code-csharp[VSSDKQuickInfoTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#1)]
     [!code-vb[VSSDKQuickInfoTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#1)]  
  
4.  Declarar uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>e nomeie-o `TestQuickInfoSource`.  
  
     [!code-csharp[VSSDKQuickInfoTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#2)]
     [!code-vb[VSSDKQuickInfoTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#2)]  
  
5.  Adicione campos para o provedor de código-fonte QuickInfo, o buffer de texto e um conjunto de nomes de método e assinaturas de método. Neste exemplo, os nomes de método e as assinaturas são inicializadas no `TestQuickInfoSource` construtor.  
  
     [!code-csharp[VSSDKQuickInfoTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#3)]
     [!code-vb[VSSDKQuickInfoTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#3)]  
  
6.  Adicione um construtor que define o provedor de fonte de QuickInfo e o buffer de texto e preenche o conjunto de nomes de método e assinaturas de método e descrições.  
  
     [!code-csharp[VSSDKQuickInfoTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#4)]
     [!code-vb[VSSDKQuickInfoTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#4)]  
  
7.  Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> . Neste exemplo, o método localiza a palavra atual ou a palavra anterior, se o cursor estiver no final de uma linha ou um buffer de texto. Se o word é um dos nomes de método, a descrição para o nome desse método é adicionada ao conteúdo QuickInfo.  
  
     [!code-csharp[VSSDKQuickInfoTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#5)]
     [!code-vb[VSSDKQuickInfoTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#5)]  
  
8.  Você também deve implementar um método Dispose (), desde <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> implementa <xref:System.IDisposable>:  
  
     [!code-csharp[VSSDKQuickInfoTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#6)]
     [!code-vb[VSSDKQuickInfoTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#6)]  
  
## <a name="implementing-a-quickinfo-source-provider"></a>Implementando um provedor de fonte de QuickInfo  
 O provedor da fonte de QuickInfo serve principalmente para exportar a mesma como uma parte do componente MEF e criar uma instância de fonte de QuickInfo. Porque é uma parte do componente de MEF, ele pode importar outras partes do componente MEF.  
  
#### <a name="to-implement-a-quickinfo-source-provider"></a>Para implementar um provedor de fonte de QuickInfo  
  
1.  Declarar um provedor de fonte de QuickInfo denominado `TestQuickInfoSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "Dica de ferramenta com a fonte QuickInfo", uma <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes = "default" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text".  
  
     [!code-csharp[VSSDKQuickInfoTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#7)]
     [!code-vb[VSSDKQuickInfoTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#7)]  
  
2.  Importar os dois serviços do editor, <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> e <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>, como propriedades do `TestQuickInfoSourceProvider`.  
  
     [!code-csharp[VSSDKQuickInfoTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#8)]
     [!code-vb[VSSDKQuickInfoTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#8)]  
  
3.  Implemente <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> para retornar um novo `TestQuickInfoSource`.  
  
     [!code-csharp[VSSDKQuickInfoTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#9)]
     [!code-vb[VSSDKQuickInfoTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#9)]  
  
## <a name="implementing-a-quickinfo-controller"></a>Implementando um controlador de QuickInfo  
 Controladores de QuickInfo determinam quando QuickInfo deve ser exibida. Neste exemplo, QuickInfo é exibida quando o ponteiro está sobre uma palavra que corresponde a um dos nomes de método. O controlador de QuickInfo implementa um manipulador de eventos de passagem de mouse que dispara uma sessão de QuickInfo.  
  
#### <a name="to-implement-a-quickinfo-controller"></a>Para implementar um controlador de QuickInfo  
  
1.  Declarar uma classe que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>e nomeie-o `TestQuickInfoController`.  
  
     [!code-csharp[VSSDKQuickInfoTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#10)]
     [!code-vb[VSSDKQuickInfoTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#10)]  
  
2.  Adicione campos privados para o modo de exibição de texto, os buffers de texto representados na exibição de texto, a sessão de QuickInfo e o provedor de controlador de QuickInfo.  
  
     [!code-csharp[VSSDKQuickInfoTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#11)]
     [!code-vb[VSSDKQuickInfoTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#11)]  
  
3.  Adicione um construtor que define os campos e adiciona o manipulador de eventos do mouse em foco.  
  
     [!code-csharp[VSSDKQuickInfoTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#12)]
     [!code-vb[VSSDKQuickInfoTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#12)]  
  
4.  Adicione o manipulador de eventos do mouse em foco que dispara a sessão de QuickInfo.  
  
     [!code-csharp[VSSDKQuickInfoTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#13)]
     [!code-vb[VSSDKQuickInfoTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#13)]  
  
5.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A> , de modo que ele remove o manipulador de eventos do mouse em foco quando o controlador é desanexado da exibição do texto.  
  
     [!code-csharp[VSSDKQuickInfoTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#14)]
     [!code-vb[VSSDKQuickInfoTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#14)]  
  
6.  Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A> método e o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> método como métodos vazios para este exemplo.  
  
     [!code-csharp[VSSDKQuickInfoTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#15)]
     [!code-vb[VSSDKQuickInfoTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#15)]  
  
## <a name="implementing-the-quickinfo-controller-provider"></a>Implementando o provedor de QuickInfo controlador  
 O provedor do controlador QuickInfo serve principalmente para exportar a mesma como uma parte do componente MEF e instanciar o controlador de QuickInfo. Porque é uma parte do componente de MEF, ele pode importar outras partes do componente MEF.  
  
#### <a name="to-implement-the-quickinfo-controller-provider"></a>Para implementar o provedor de controlador de QuickInfo  
  
1.  Declare uma classe chamada `TestQuickInfoControllerProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "Dica de ferramenta QuickInfo controlador" e um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text":  
  
     [!code-csharp[VSSDKQuickInfoTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#16)]
     [!code-vb[VSSDKQuickInfoTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#16)]  
  
2.  Importar o <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> como uma propriedade.  
  
     [!code-csharp[VSSDKQuickInfoTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#17)]
     [!code-vb[VSSDKQuickInfoTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#17)]  
  
3.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> método instanciando o controlador de QuickInfo.  
  
     [!code-csharp[VSSDKQuickInfoTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#18)]
     [!code-vb[VSSDKQuickInfoTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#18)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução QuickInfoTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-the-quickinfotest-solution"></a>Para compilar e testar a solução QuickInfoTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui as palavras "Adicionar" e "subtrair".  
  
4.  Mova o ponteiro sobre uma das ocorrências de "Adicionar". A assinatura e a descrição a `add` método deve ser exibido.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

