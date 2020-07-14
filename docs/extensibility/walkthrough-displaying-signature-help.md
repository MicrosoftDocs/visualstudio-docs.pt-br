---
title: 'Walkthrough: exibindo a ajuda da assinatura | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b88c8555904bb31c2804579459ad3096d640b0c2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904816"
---
# <a name="walkthrough-display-signature-help"></a>Walkthrough: exibir a ajuda da assinatura
A ajuda da assinatura (também conhecida como *informações do parâmetro*) exibe a assinatura de um método em uma dica de ferramenta quando um usuário digita o caractere de início da lista de parâmetros (normalmente um parêntese de abertura). Como um separador de parâmetro e parâmetro (normalmente uma vírgula) são digitados, a dica de ferramenta é atualizada para mostrar o próximo parâmetro em negrito. Você pode definir a ajuda da assinatura das seguintes maneiras: no contexto de um serviço de idioma, defina sua própria extensão de nome de arquivo e tipo de conteúdo e exiba a ajuda da assinatura apenas para esse tipo, ou exiba a ajuda da assinatura para um tipo de conteúdo existente (por exemplo, "texto"). Este tutorial mostra como exibir a ajuda da assinatura para o tipo de conteúdo "texto".

 A ajuda da assinatura é normalmente disparada digitando um caractere específico, por exemplo, "(" (parêntese de abertura) e descartado digitando outro caractere, por exemplo, ")" (parêntese de fechamento). Os recursos do IntelliSense que são disparados pela digitação de um caractere podem ser implementados usando um manipulador de comando para os pressionamentos de tecla (a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface) e um provedor de manipulador que implementa a <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> interface. Para criar a fonte de ajuda da assinatura, que é a lista de assinaturas que participam da ajuda da assinatura, implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> interface e um provedor de origem que executa a <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> interface. Os provedores são partes de componente Managed Extensibility Framework (MEF) e são responsáveis por exportar as classes de origem e controlador e importar serviços e agentes, por exemplo, o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> , que permite que você navegue no buffer de texto e o <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> , que dispara a sessão de ajuda de assinatura.

 Este tutorial mostra como configurar a ajuda de assinatura para um conjunto de identificadores embutido em código. Em implementações completas, a linguagem é responsável por fornecer esse conteúdo.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="creating-a-mef-project"></a>Criando um projeto do MEF

#### <a name="to-create-a-mef-project"></a>Para criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `SignatureHelpTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

4. Adicione as seguintes referências ao projeto e verifique se **CopyLocal** está definido como `false` :

     Microsoft. VisualStudio. editor

     Microsoft. VisualStudio. Language. IntelliSense

     Microsoft. VisualStudio. OLE. Interop

     Microsoft. VisualStudio. Shell. 14.0

     Microsoft. VisualStudio. Textmanager. Interop

## <a name="implement-signature-help-signatures-and-parameters"></a>Implementar assinaturas e parâmetros de ajuda de assinatura
 A fonte de ajuda da assinatura é baseada em assinaturas que implementam <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> , cada uma delas contendo parâmetros que implementam <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> . Em uma implementação completa, essas informações seriam obtidas na documentação do idioma, mas neste exemplo, as assinaturas são embutidas em código.

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>Para implementar a assinatura ajuda de assinaturas e parâmetros

1. Adicione um arquivo de classe e nomeie-o `SignatureHelpSource` .

2. Adicione as seguintes importações.

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. Adicione uma classe chamada `TestParameter` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> .

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. Adicione um construtor que define todas as propriedades.

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. Adicione as propriedades de <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> .

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. Adicione uma classe chamada `TestSignature` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> .

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. Adicione alguns campos particulares.

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. Adicione um construtor que defina os campos e assine o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> evento.

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. Declare um `CurrentParameterChanged` evento. Esse evento é gerado quando o usuário preenche um dos parâmetros na assinatura.

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. Implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> propriedade para que ela gere o `CurrentParameterChanged` evento quando o valor da propriedade for alterado.

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. Adicione um método que gera o `CurrentParameterChanged` evento.

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. Adicione um método que computa o parâmetro atual comparando o número de vírgulas no <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> para o número de vírgulas na assinatura.

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. Adicione um manipulador de eventos para o <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> evento que chama o `ComputeCurrentParameter()` método.

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. Implemente a propriedade <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>. Essa propriedade contém um <xref:Microsoft.VisualStudio.Text.ITrackingSpan> que corresponde ao intervalo de texto no buffer ao qual a assinatura se aplica.

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. Implemente os outros parâmetros.

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>Implementar a fonte de ajuda da assinatura
 A fonte de ajuda da assinatura é o conjunto de assinaturas para as quais você fornece informações.

#### <a name="to-implement-the-signature-help-source"></a>Para implementar a fonte de ajuda da assinatura

1. Adicione uma classe chamada `TestSignatureHelpSource` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> .

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. Adicione uma referência ao buffer de texto.

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. Adicione um construtor que defina o buffer de texto e o provedor de origem de ajuda de assinatura.

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> . Neste exemplo, as assinaturas são embutidas em código, mas em uma implementação completa, você obteria essas informações da documentação do idioma.

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. O método auxiliar `CreateSignature()` é fornecido apenas para ilustração.

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. Implementar o método de <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> . Neste exemplo, há apenas duas assinaturas, cada uma delas tem dois parâmetros. Portanto, esse método não é necessário. Em uma implementação mais completa, na qual mais de uma fonte de ajuda de assinatura está disponível, esse método é usado para decidir se a fonte de ajuda de assinatura de prioridade mais alta pode fornecer uma assinatura correspondente. Se não puder, o método retornará NULL e a fonte Next-mais alta-Priority será solicitada a fornecer uma correspondência.

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. Implemente o `Dispose()` método:

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>Implementar o provedor de origem de ajuda de assinatura
 O provedor de origem de ajuda de assinatura é responsável por exportar a parte do componente Managed Extensibility Framework (MEF) e para instanciar a fonte de ajuda da assinatura.

#### <a name="to-implement-the-signature-help-source-provider"></a>Para implementar o provedor de origem de ajuda de assinatura

1. Adicione uma classe chamada `TestSignatureHelpSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> e exporte-a com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> , um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto" e um <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> de antes = "padrão".

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. Implemente <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A> ao instanciar o `TestSignatureHelpSource` .

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>Implementar o manipulador de comandos
 A ajuda da assinatura é normalmente disparada por um caractere de parêntese de abertura "(" e ignorado por um caractere de parêntese de fechamento ")". Você pode lidar com esses pressionamentos de teclas executando um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> para que ele dispare uma sessão de ajuda de assinatura quando recebe um caractere de parêntese de abertura precedido por um nome de método conhecido e ignora a sessão quando recebe um caractere de parêntese de fechamento.

#### <a name="to-implement-the-command-handler"></a>Para implementar o manipulador de comandos

1. Adicione uma classe chamada `TestSignatureHelpCommand` que implementa <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> .

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. Adicione campos particulares para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> adaptador (que permite que você adicione o manipulador de comandos à cadeia de manipuladores de comandos), a exibição de texto, a assinatura, o agente de ajuda e a sessão, a <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> e a próxima <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> .

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. Adicione um construtor para inicializar esses campos e adicionar o filtro de comando à cadeia de filtros de comando.

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. Implemente o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método para disparar a sessão de ajuda de assinatura quando o filtro de comando receber um caractere de parêntese de abertura "(" depois de um dos nomes de método conhecidos e ignorar a sessão quando receber um caractere de parêntese de fechamento ")" enquanto a sessão ainda estiver ativa. Em todos os casos, o comando é encaminhado.

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. Implemente o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método para que ele sempre encaminhe o comando.

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>Implementar o provedor de comandos de ajuda de assinatura
 Você pode fornecer o comando de ajuda de assinatura implementando o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> para instanciar o manipulador de comandos quando a exibição de texto for criada.

### <a name="to-implement-the-signature-help-command-provider"></a>Para implementar o provedor de comandos de ajuda de assinatura

1. Adicione uma classe chamada `TestSignatureHelpController` que implemente <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> e exporte-a com o <xref:Microsoft.VisualStudio.Utilities.NameAttribute> , o <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> e o <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> .

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. Importe o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> (usado para obter o <xref:Microsoft.VisualStudio.Text.Editor.ITextView> , dado o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto), o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> (usado para localizar a palavra atual) e o <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> (para disparar a sessão de ajuda da assinatura).

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. Implemente o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> método instanciando o `TestSignatureCommandHandler` .

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução SignatureHelpTest e execute-a na instância experimental.

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>Para compilar e testar a solução SignatureHelpTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto que inclua a palavra "Adicionar", além de um parêntese de abertura.

4. Depois de digitar o parêntese de abertura, você deverá ver uma dica de ferramenta que exibe uma lista das duas assinaturas do `add()` método.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
