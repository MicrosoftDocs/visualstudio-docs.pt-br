---
title: 'Passo a passo: Exibindo o preenchimento de declaração | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bdd96c124dafabf5584dfa13547cdea1e2b843b8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879318"
---
# <a name="walkthrough-display-statement-completion"></a>Passo a passo: Preenchimento de declaração de exibição
Você pode implementar o preenchimento de declaração baseadas em linguagem definindo os identificadores para o qual você deseja fornecer conclusão e, em seguida, disparar uma sessão de conclusão. Você pode definir o preenchimento de declaração no contexto de um serviço de linguagem, definir sua própria extensão de nome de arquivo e o tipo de conteúdo e, em seguida, exibir conclusão para apenas esse tipo. Ou, você pode disparar o preenchimento para um tipo de conteúdo existente — por exemplo, "texto sem formatação". Este passo a passo mostra como disparar a conclusão de instrução para o tipo de conteúdo "texto sem formatação", que é o tipo de conteúdo de arquivos de texto. O tipo de conteúdo "texto" é o ancestral de todos os outros tipos de conteúdo, inclusive código e arquivos XML.  
  
 Preenchimento de declaração costuma ser disparado ao digitar determinados caracteres — por exemplo, digitando o início de um identificador, como "using". Normalmente é descartado ao pressionar o **barra de espaços**, **guia**, ou **Enter** chave para uma seleção de confirmação. Você pode implementar os recursos do IntelliSense que disparam ao digitar um caractere, usando um manipulador de comandos para os pressionamentos de tecla (o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface) e um provedor de manipulador que implementa o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> interface. Para criar a fonte de conclusão, o que é a lista de identificadores que participam de conclusão, implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> interface e um provedor de fonte de conclusão (o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> interface). Os provedores são partes do componente Managed Extensibility Framework (MEF). Eles são responsáveis pelas classes de origem e o controlador de exportação e importação de serviços e agentes — por exemplo, o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>, que permite a navegação no buffer de texto e o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>, que dispara a sessão de conclusão.  
  
 Este passo a passo mostra como implementar o preenchimento de declaração para um conjunto de identificadores de embutido em código. Em implementações completas, o serviço de linguagem e a documentação da linguagem são responsáveis por fornecer esse conteúdo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-mef-project"></a>Criar um projeto MEF  
  
#### <a name="to-create-a-mef-project"></a>Para criar um projeto MEF  
  
1.  Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `CompletionTest`.  
  
2.  Adicione um modelo de item de classificação de Editor para o projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3.  Exclua os arquivos de classe existentes.  
  
4.  Adicione as seguintes referências ao projeto e certifique-se de que **CopyLocal** é definido como `false`:  
  
     Microsoft.VisualStudio.Editor  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     Microsoft.VisualStudio.Shell.14.0  
  
     Microsoft.VisualStudio.Shell.Immutable.10.0  
  
     Microsoft.VisualStudio.TextManager.Interop  
  
## <a name="implement-the-completion-source"></a>Implementar a origem de conclusão  
 A fonte de conclusão é responsável por coletar o conjunto de identificadores e adicionando o conteúdo para a janela de conclusão quando um usuário digita um gatilho de conclusão, como as primeiras letras de um identificador. Neste exemplo, os identificadores e suas descrições são embutidos no código o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> método. A maioria dos usos do mundo real, você usaria o analisador da sua linguagem para obter os tokens para preencher a lista de conclusão.  
  
### <a name="to-implement-the-completion-source"></a>Para implementar a origem de conclusão  
  
1.  Adicione um arquivo de classe e denomine- `TestCompletionSource`.  
  
2.  Adicione essas importações:  
  
     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]  
  
3.  Modifique a declaração de classe de `TestCompletionSource` para que ele implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>:  
  
     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]  
  
4.  Adicionar campos privados para o provedor de código-fonte, o buffer de texto e uma lista de <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> objetos (que correspondem aos identificadores que participarão da sessão de conclusão):  
  
     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]  
  
5.  Adicione um construtor que define o buffer e o provedor de origem. O `TestCompletionSourceProvider` classe é definida em etapas posteriores:  
  
     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]  
  
6.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> método adicionando um conjunto de conclusão que contém as conclusões que você deseja fornecer o contexto. Cada conjunto de conclusão contém um conjunto de <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> conclusões e corresponde a uma guia da janela de conclusão. (Em projetos do Visual Basic, as guias da janela de conclusão são nomeadas **comuns** e **todos os**.) O `FindTokenSpanAtPosition` método é definido na próxima etapa.  
  
     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]  
  
7.  O método a seguir é usado para localizar a palavra atual da posição do cursor:  
  
     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]  
  
8.  Implementar o `Dispose()` método:  
  
     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]  
  
## <a name="implement-the-completion-source-provider"></a>Implemente o provedor de fonte de conclusão  
 O provedor de fonte de conclusão é a parte do componente MEF que instancia a origem de conclusão.  
  
### <a name="to-implement-the-completion-source-provider"></a>Para implementar o provedor de origem de conclusão  
  
1.  Adicione uma classe chamada `TestCompletionSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>. Exportar esta classe com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto sem formatação" e um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "conclusão de teste".  
  
     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]  
  
2.  Importar um <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>, que localiza a palavra atual na fonte de conclusão.  
  
     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]  
  
3.  Implementar o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> método para instanciar a origem de conclusão.  
  
     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]  
  
## <a name="implement-the-completion-command-handler-provider"></a>Implemente o provedor de manipulador de comando de conclusão  
 O provedor de manipulador de comando de conclusão é derivado de um <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>, que escuta um evento de criação de exibição de texto e converte o modo de exibição de um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>— que permite a adição do comando para a cadeia de comando do shell do Visual Studio — para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>. Como essa classe é uma exportação de MEF, você pode usá-lo para importar os serviços que são necessários para o manipulador de comandos.  
  
#### <a name="to-implement-the-completion-command-handler-provider"></a>Para implementar o provedor de manipulador de comando de conclusão  
  
1.  Adicione um arquivo chamado `TestCompletionCommandHandler`.  
  
2.  Adicione o seguinte usando instruções:  
  
     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]  
  
3.  Adicione uma classe chamada `TestCompletionHandlerProvider` que implementa <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>. Exportar esta classe com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> de "manipulador de conclusão de token", uma <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto sem formatação" e um <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>.  
  
     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]  
  
4.  Importar o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>, que habilita a conversão de um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView>, uma <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>e um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> que habilita o acesso a serviços padrão do Visual Studio.  
  
     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]  
  
5.  Implementar o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> método para instanciar o manipulador de comandos.  
  
     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]  
  
## <a name="implement-the-completion-command-handler"></a>Implementar o manipulador de comandos de conclusão  
 Como preenchimento de declaração é disparado por pressionamentos de tecla, você deve implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para receber e processar os pressionamentos de teclas que dispararem, confirmam e ignorar a sessão de conclusão.  
  
#### <a name="to-implement-the-completion-command-handler"></a>Para implementar o manipulador de comandos de conclusão  
  
1. Adicione uma classe chamada `TestCompletionCommandHandler` que implementa <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>:  
  
    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]  
  
2. Adicionar campos privados para o próximo manipulador de comando (para o qual você passar o comando), a exibição de texto, o provedor do manipulador de comando (o que permite o acesso a vários serviços) e uma sessão de conclusão:  
  
    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]  
  
3. Adicione um construtor que define o modo de texto e os campos de provedor e adiciona o comando para a cadeia de comando:  
  
    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]  
  
4. Implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método, passando o comando ao longo de:  
  
    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]  
  
5. Implementar o método de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> . Quando esse método recebe um pressionamento de tecla, ele deve fazer uma dessas coisas:  
  
   - Permitir que o caractere a ser gravada no buffer e, em seguida, disparar ou filtrar a conclusão. (Caracteres imprimíveis fazem isso.)  
  
   - Confirmar a conclusão, mas não permitem que o caractere a ser gravado no buffer. (Espaço em branco, **guia**, e **Enter** isso quando uma sessão de conclusão é exibida.)  
  
   - Permitir que o comando a ser passado para o próximo manipulador. (Todos os outros comandos.)  
  
     Como esse método pode exibir a interface do usuário, chame <xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> para certificar-se de que ele não é chamado em um contexto de automação:  
  
     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]  
  
6. Esse código é um método particular que dispara a sessão de conclusão:  
  
    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]  
  
7. O exemplo a seguir é um método particular que cancela a assinatura do <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> evento:  
  
    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
 Para testar esse código, compile a solução CompletionTest e executá-lo na instância experimental.  
  
#### <a name="to-build-and-test-the-completiontest-solution"></a>Para compilar e testar a solução CompletionTest  
  
1.  Compile a solução.  
  
2.  Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.  
  
3.  Crie um arquivo de texto e digite algum texto que inclui a palavra "Adicionar".  
  
4.  Conforme você digita, primeiro, "a" e, em seguida, "d", uma lista que contém "adição" e "adaptação" deve aparecer. Observe que a adição é selecionada. Quando você digitar outra "d", a lista deve conter somente "adição", que agora está selecionada. Você pode confirmar "adição" pressionando a **barra de espaços**, **guia**, ou **Enter** chave ou descartar a lista digitando Esc ou qualquer outra chave.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Vincular um tipo de conteúdo para uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)