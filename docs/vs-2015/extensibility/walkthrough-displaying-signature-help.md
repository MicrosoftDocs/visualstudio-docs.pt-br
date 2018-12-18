---
title: 'Passo a passo: Exibindo a Ajuda da assinatura | Microsoft Docs'
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
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7a3b902c32563da6bc21778a09b4aeaebaeabeaa
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734639"
---
# <a name="walkthrough-displaying-signature-help"></a>Passo a passo: exibindo a ajuda da assinatura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ajuda da assinatura (também conhecido como *informações de parâmetro*) exibe a assinatura de um método em uma dica de ferramenta quando um usuário digita o caractere de início da lista de parâmetro (normalmente um parêntese de abertura). Como um parâmetro e o separador de parâmetro (geralmente uma vírgula) são digitadas, a dica de ferramenta é atualizada para mostrar o próximo parâmetro em negrito. Você pode definir a Ajuda de assinatura no contexto de um serviço de linguagem, ou você pode definir seu próprio tipo de conteúdo e a extensão de nome do arquivo e exibir a Ajuda de assinatura para apenas esse tipo, ou você pode exibir a Ajuda de assinatura para um tipo de conteúdo existente (por exemplo, "texto"). Este passo a passo mostra como exibir a Ajuda de assinatura para o tipo de conteúdo "text".  
  
 Ajuda da assinatura costuma ser disparada, digitando um caractere específico, por exemplo, "(" (parêntese de abertura) e será descartada digitando outro caractere, por exemplo, ")" (parêntese de fechamento). Recursos do IntelliSense que são disparados, digitando um caractere podem ser implementados usando um manipulador de comandos para os pressionamentos de tecla (o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface) e um provedor de manipulador que implementa o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> interface. Para criar a fonte de ajuda de assinatura, que é a lista de assinaturas que participam de ajuda de assinatura, implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> interface e um provedor de código-fonte que implementa o <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> interface. Os provedores são partes do componente Managed Extensibility Framework (MEF) e são responsáveis pelas classes de origem e o controlador de exportação e importação de serviços e agentes, por exemplo, o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>, que permite que você navegue no buffer de texto e o <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>, que dispara a sessão de ajuda de assinatura.  
  
 Este passo a passo mostra como implementar a Ajuda de assinatura para um conjunto de identificadores de embutido em código. Em implementações completas, a linguagem é responsável por fornecer esse conteúdo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-mef-project"></a>Criando um projeto MEF  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `SignatureHelpTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
4.  Adicione as seguintes referências ao projeto e verifique se **CopyLocal** é definido como `false`:  
  
     Microsoft.VisualStudio.Editor  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     Microsoft.VisualStudio.Shell.14.0  
  
     Microsoft.VisualStudio.TextManager.Interop  
  
## <a name="implementing-signature-help-signatures-and-parameters"></a>Implementando a assinatura ajuda assinaturas e parâmetros  
 A fonte de ajuda de assinatura se baseia em assinaturas que implementam <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>, cada uma delas contém parâmetros que implementam <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>. Em uma implementação completa, essas informações seriam obtidas com a documentação da linguagem, mas neste exemplo, as assinaturas são embutidos.  
  
#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>Para implementar os parâmetros e assinaturas de ajuda de assinatura  
  
1.  Adicione um arquivo de classe e denomine- `SignatureHelpSource`.  
  
2.  Adicione as importações a seguir.  
  
     [!code-csharp[VSSDKSignatureHelpTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#1)]
     [!code-vb[VSSDKSignatureHelpTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#1)]  
  
3.  Adicione uma classe chamada `TestParameter` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#2)]
     [!code-vb[VSSDKSignatureHelpTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#2)]  
  
4.  Adicione um construtor que define todas as propriedades.  
  
     [!code-csharp[VSSDKSignatureHelpTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#3)]
     [!code-vb[VSSDKSignatureHelpTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#3)]  
  
5.  Adicione as propriedades de <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#4)]
     [!code-vb[VSSDKSignatureHelpTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#4)]  
  
6.  Adicione uma classe chamada `TestSignature` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#5)]
     [!code-vb[VSSDKSignatureHelpTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#5)]  
  
7.  Adicione alguns campos particulares.  
  
     [!code-csharp[VSSDKSignatureHelpTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#6)]
     [!code-vb[VSSDKSignatureHelpTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#6)]  
  
8.  Adicione um construtor que define os campos e assina o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos.  
  
     [!code-csharp[VSSDKSignatureHelpTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#7)]
     [!code-vb[VSSDKSignatureHelpTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#7)]  
  
9. Declarar um `CurrentParameterChanged` eventos. Esse evento é gerado quando o usuário preenche um dos parâmetros na assinatura.  
  
     [!code-csharp[VSSDKSignatureHelpTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#8)]
     [!code-vb[VSSDKSignatureHelpTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#8)]  
  
10. Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> propriedade para que ele gera o `CurrentParameterChanged` eventos quando o valor da propriedade é alterado.  
  
     [!code-csharp[VSSDKSignatureHelpTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#9)]
     [!code-vb[VSSDKSignatureHelpTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#9)]  
  
11. Adicione um método que gera o `CurrentParameterChanged` eventos.  
  
     [!code-csharp[VSSDKSignatureHelpTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#10)]
     [!code-vb[VSSDKSignatureHelpTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#10)]  
  
12. Adicione um método que calcula o parâmetro atual, comparando o número de vírgulas no <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> para o número de vírgulas na assinatura.  
  
     [!code-csharp[VSSDKSignatureHelpTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#11)]
     [!code-vb[VSSDKSignatureHelpTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#11)]  
  
13. Adicionar um manipulador de eventos para o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> eventos que chama o `ComputeCurrentParameter()` método.  
  
     [!code-csharp[VSSDKSignatureHelpTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#12)]
     [!code-vb[VSSDKSignatureHelpTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#12)]  
  
14. Implemente a propriedade <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>. Esta propriedade contém um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> que corresponde ao trecho de texto no buffer ao qual a assinatura se aplica.  
  
     [!code-csharp[VSSDKSignatureHelpTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#13)]
     [!code-vb[VSSDKSignatureHelpTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#13)]  
  
15. Implemente os outros parâmetros.  
  
     [!code-csharp[VSSDKSignatureHelpTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#14)]
     [!code-vb[VSSDKSignatureHelpTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#14)]  
  
## <a name="implementing-the-signature-help-source"></a>Implementando a origem de ajuda de assinatura  
 A origem de ajuda de assinatura é o conjunto de assinaturas para o qual você pode fornecer informações.  
  
#### <a name="to-implement-the-signature-help-source"></a>Para implementar a origem de ajuda de assinatura  
  
1.  Adicione uma classe chamada `TestSignatureHelpSource` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#15)]
     [!code-vb[VSSDKSignatureHelpTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#15)]  
  
2.  Adicione uma referência para o buffer de texto.  
  
     [!code-csharp[VSSDKSignatureHelpTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#16)]
     [!code-vb[VSSDKSignatureHelpTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#16)]  
  
3.  Adicione um construtor que define o buffer de texto e o provedor de ajuda de assinatura de código-fonte.  
  
     [!code-csharp[VSSDKSignatureHelpTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#17)]
     [!code-vb[VSSDKSignatureHelpTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#17)]  
  
4.  Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> . Neste exemplo, as assinaturas são embutidos, mas uma implementação completa, você obteria essas informações na documentação do idioma.  
  
     [!code-csharp[VSSDKSignatureHelpTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#18)]
     [!code-vb[VSSDKSignatureHelpTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#18)]  
  
5.  O método auxiliar `CreateSignature()` é fornecido apenas para ilustração.  
  
     [!code-csharp[VSSDKSignatureHelpTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#19)]
     [!code-vb[VSSDKSignatureHelpTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#19)]  
  
6.  Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> . Neste exemplo, há apenas duas assinaturas, cada um deles tem dois parâmetros. Portanto, esse método não é necessário. Em uma implementação mais completa, em que mais de uma fonte de ajuda de assinatura está disponível, esse método é usado para decidir se a origem de ajuda de assinatura de prioridade mais alta pode fornecer uma assinatura correspondente. Se não for possível, o método retornará nulo e a origem do próximo maior prioridade é solicitada a fornecer uma correspondência.  
  
     [!code-csharp[VSSDKSignatureHelpTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#20)]
     [!code-vb[VSSDKSignatureHelpTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#20)]  
  
7.  Implemente o método Dispose ():  
  
     [!code-csharp[VSSDKSignatureHelpTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#21)]
     [!code-vb[VSSDKSignatureHelpTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#21)]  
  
## <a name="implementing-the-signature-help-source-provider"></a>Implementando o provedor de origem de ajuda de assinatura  
 O provedor de ajuda de assinatura de código-fonte é responsável para exportar a parte do componente Managed Extensibility Framework (MEF) e para criar uma instância de fonte de ajuda de assinatura.  
  
#### <a name="to-implement-the-signature-help-source-provider"></a>Para implementar o provedor de ajuda de assinatura de código-fonte  
  
1.  Adicione uma classe chamada `TestSignatureHelpSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>e exportá-lo com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute>, uma <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "text" e um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes = "default".  
  
     [!code-csharp[VSSDKSignatureHelpTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#22)]
     [!code-vb[VSSDKSignatureHelpTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#22)]  
  
2.  Implemente <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A> instanciando a `TestSignatureHelpSource`.  
  
     [!code-csharp[VSSDKSignatureHelpTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#23)]
     [!code-vb[VSSDKSignatureHelpTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#23)]  
  
## <a name="implementing-the-command-handler"></a>Implementando o manipulador de comando  
 Ajuda da assinatura normalmente é disparada por um (caractere e ignorado por um) caracteres. Você pode lidar com esses pressionamentos de tecla implementando um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> , de modo que ele dispara uma sessão de ajuda de assinatura quando ela recebe um (caractere precedido por um nome de método conhecidos e descarta a sessão quando ele recebe um) caracteres.  
  
#### <a name="to-implement-the-command-handler"></a>Para implementar o manipulador de comandos  
  
1.  Adicione uma classe chamada `TestSignatureHelpCommand` que implementa <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#24)]
     [!code-vb[VSSDKSignatureHelpTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#24)]  
  
2.  Adicionar campos privados para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> adaptador (o que permite que você adicione o manipulador de comandos para os manipuladores de cadeia de comando), a exibição de texto, o agente de ajuda de assinatura e a sessão, uma <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>e o próximo <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#25)]
     [!code-vb[VSSDKSignatureHelpTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#25)]  
  
3.  Adicione um construtor para inicializar esses campos e adicionar o filtro de comando com os filtros de cadeia de comando.  
  
     [!code-csharp[VSSDKSignatureHelpTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#26)]
     [!code-vb[VSSDKSignatureHelpTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#26)]  
  
4.  Implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método para disparar a sessão de ajuda de assinatura quando o filtro de comando recebe um (caractere depois que um dos nomes de método conhecidos e para ignorar a sessão quando ele recebe um) de caracteres enquanto a sessão ainda estiver ativa. Em todos os casos, o comando é encaminhado.  
  
     [!code-csharp[VSSDKSignatureHelpTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#27)]
     [!code-vb[VSSDKSignatureHelpTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#27)]  
  
5.  Implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> , de modo que ele sempre encaminha o comando.  
  
     [!code-csharp[VSSDKSignatureHelpTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#28)]
     [!code-vb[VSSDKSignatureHelpTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#28)]  
  
## <a name="implementing-the-signature-help-command-provider"></a>Implementando o provedor de comando de ajuda de assinatura  
 Você pode fornecer o comando de ajuda de assinatura, Implementando o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> para instanciar o manipulador de comando quando o modo de texto é criado.  
  
#### <a name="to-implement-the-signature-help-command-provider"></a>Para implementar o provedor de comando de ajuda de assinatura  
  
1.  Adicione uma classe chamada `TestSignatureHelpController` que implementa <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> e exportá-lo com o <xref:Microsoft.VisualStudio.Utilities.NameAttribute>, <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>, e <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>.  
  
     [!code-csharp[VSSDKSignatureHelpTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#29)]
     [!code-vb[VSSDKSignatureHelpTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#29)]  
  
2.  Importar o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> (usado para obter o <xref:Microsoft.VisualStudio.Text.Editor.ITextView>, dado o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto), o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> (usada para localizar a palavra atual) e o <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> (para disparar a sessão de ajuda de assinatura).  
  
     [!code-csharp[VSSDKSignatureHelpTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#30)]
     [!code-vb[VSSDKSignatureHelpTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#30)]  
  
3.  Implemente a <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> método instanciando a `TestSignatureCommandHandler`.  
  
     [!code-csharp[VSSDKSignatureHelpTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#31)]
     [!code-vb[VSSDKSignatureHelpTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#31)]  
  
## <a name="building-and-testing-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução SignatureHelpTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>Para compilar e testar a solução SignatureHelpTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui a palavra "Adicionar" Além de um parêntese de abertura.  
  
4.  Depois que você digita o parêntese de abertura, você deverá ver uma dica de ferramenta que exibe uma lista de duas assinaturas para o `add()` método.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

