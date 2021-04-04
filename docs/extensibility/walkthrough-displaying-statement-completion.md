---
title: 'Walkthrough: exibindo a conclusão da instrução | Microsoft Docs'
description: Saiba como implementar a conclusão de instrução baseada em linguagem para conteúdo de texto não criptografado usando este passo a passos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: leslierichardson95
ms.author: lerich
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 51281c261baf5744c1d3aa0903985a173ff240f2
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217470"
---
# <a name="walkthrough-display-statement-completion"></a>Passo a passo: exibir preenchimento de declaração
Você pode implementar a conclusão da instrução baseada em linguagem definindo os identificadores para os quais você deseja fornecer a conclusão e, em seguida, disparando uma sessão de conclusão. Você pode definir a conclusão da instrução no contexto de um serviço de idioma, definir sua própria extensão de nome de arquivo e tipo de conteúdo e, em seguida, exibir a conclusão apenas para esse tipo. Ou, você pode disparar a conclusão para um tipo de conteúdo existente — por exemplo, "texto sem formatação". Este tutorial mostra como disparar a conclusão da instrução para o tipo de conteúdo "texto não criptografado", que é o tipo de conteúdo dos arquivos de texto. O tipo de conteúdo "text" é o ancestral de todos os outros tipos de conteúdo, incluindo arquivos de código e XML.

 A conclusão da instrução é normalmente disparada digitando-se determinados caracteres — por exemplo, digitando o início de um identificador, como "usando". Normalmente, é Descartado pressionando-se a **barra de espaços**, a **guia** ou a tecla **Enter** para confirmar uma seleção. Você pode implementar os recursos do IntelliSense que disparam ao digitar um caractere usando um manipulador de comando para os pressionamentos de tecla (a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface) e um provedor de manipulador que implementa a <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> interface. Para criar a origem de conclusão, que é a lista de identificadores que participam da conclusão, implemente a <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> interface e um provedor de origem de conclusão (a <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> interface). Os provedores são partes de componente Managed Extensibility Framework (MEF). Eles são responsáveis por exportar as classes de origem e controlador e importar serviços e agentes — por exemplo, o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> , que permite a navegação no buffer de texto e o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> , que dispara a sessão de conclusão.

 Este tutorial mostra como implementar a conclusão de uma instrução para um conjunto embutido de identificadores. Em implementações completas, o serviço de idioma e a documentação do idioma são responsáveis por fornecer esse conteúdo.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-mef-project"></a>Criar um projeto do MEF

#### <a name="to-create-a-mef-project"></a>Para criar um projeto do MEF

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade** e, em seguida, **projeto VSIX**.) Nomeie a solução `CompletionTest` .

2. Adicione um modelo de item de classificação do editor ao projeto. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Exclua os arquivos de classe existentes.

4. Adicione as seguintes referências ao projeto e verifique se **CopyLocal** está definido como `false` :

     Microsoft. VisualStudio. editor

     Microsoft. VisualStudio. Language. IntelliSense

     Microsoft. VisualStudio. OLE. Interop

     Microsoft. VisualStudio. Shell. 15.0

     Microsoft. VisualStudio. Shell. imutável. 10.0

     Microsoft. VisualStudio. Textmanager. Interop

## <a name="implement-the-completion-source"></a>Implementar a origem de conclusão
 A fonte de conclusão é responsável por coletar o conjunto de identificadores e adicionar o conteúdo à janela de conclusão quando um usuário digita um gatilho de conclusão, como as primeiras letras de um identificador. Neste exemplo, os identificadores e suas descrições são embutidos em código no <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> método. Na maioria dos usos do mundo real, você usaria o analisador de seu idioma para obter os tokens para preencher a lista de conclusão.

### <a name="to-implement-the-completion-source"></a>Para implementar a origem de conclusão

1. Adicione um arquivo de classe e nomeie-o `TestCompletionSource` .

2. Adicione estas importações:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet1":::

3. Modifique a declaração de classe para `TestCompletionSource` que ela implemente <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> :

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet2":::

4. Adicione campos particulares para o provedor de origem, o buffer de texto e uma lista de <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> objetos (que correspondem aos identificadores que participarão da sessão de conclusão):

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet3":::

5. Adicione um construtor que define o provedor de origem e o buffer. A `TestCompletionSourceProvider` classe é definida em etapas posteriores:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet4":::

6. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> método adicionando um conjunto de conclusão que contenha as conclusões que você deseja fornecer no contexto. Cada conjunto de conclusão contém um conjunto de <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> conclusões e corresponde a uma guia da janela de conclusão. (Em projetos Visual Basic, as guias de janela de conclusão são nomeadas como **comuns** e **todas**.) O `FindTokenSpanAtPosition` método é definido na próxima etapa.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet5":::

7. O método a seguir é usado para localizar a palavra atual da posição do cursor:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet6":::

8. Implemente o `Dispose()` método:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet7":::

## <a name="implement-the-completion-source-provider"></a>Implementar o provedor de origem de conclusão
 O provedor de origem de conclusão é a parte do componente do MEF que instancia a origem de conclusão.

### <a name="to-implement-the-completion-source-provider"></a>Para implementar o provedor de origem de conclusão

1. Adicione uma classe chamada `TestCompletionSourceProvider` que implementa <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> . Exporte essa classe com um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "texto sem formatação" e uma <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "conclusão do teste".

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet8":::

2. Importar um <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> , que localiza a palavra atual na fonte de conclusão.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet9":::

3. Implemente o <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> método para instanciar a origem de conclusão.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet10":::

## <a name="implement-the-completion-command-handler-provider"></a>Implementar o provedor do manipulador de comandos de conclusão
 O provedor do manipulador de comandos de conclusão é derivado de a <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> , que escuta um evento de criação de exibição de texto e converte a exibição de um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> — que permite a adição do comando à cadeia de comandos do shell do Visual Studio — a um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> . Como essa classe é uma exportação de MEF, você também pode usá-la para importar os serviços exigidos pelo próprio manipulador de comandos.

#### <a name="to-implement-the-completion-command-handler-provider"></a>Para implementar o provedor do manipulador de comandos de conclusão

1. Adicione um arquivo chamado `TestCompletionCommandHandler` .

2. Adicione-as usando as diretivas:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet11":::

3. Adicione uma classe chamada `TestCompletionHandlerProvider` que implementa <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> . Exporte essa classe com um <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "manipulador de conclusão de token", um <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> de "texto sem formatação" e um <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> de <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable> .

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet12":::

4. Importe o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> , que permite a conversão de um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para um <xref:Microsoft.VisualStudio.Text.Editor.ITextView> , um <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> e um <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> que habilita o acesso aos serviços padrão do Visual Studio.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet13":::

5. Implemente o <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> método para instanciar o manipulador de comandos.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet14":::

## <a name="implement-the-completion-command-handler"></a>Implementar o manipulador de comandos de conclusão
 Como a conclusão da instrução é disparada por pressionamentos de teclas, você deve implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para receber e processar os pressionamentos de teclas que disparam, confirmam e descartam a sessão de conclusão.

#### <a name="to-implement-the-completion-command-handler"></a>Para implementar o manipulador de comando de conclusão

1. Adicione uma classe chamada `TestCompletionCommandHandler` que implemente <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> :

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet15":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet15":::

2. Adicione campos particulares para o próximo manipulador de comandos (para o qual você passa o comando), a exibição de texto, o provedor de manipulador de comandos (que permite o acesso a vários serviços) e uma sessão de conclusão:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet16":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet16":::

3. Adicione um construtor que defina a exibição de texto e os campos de provedor e adicione o comando à cadeia de comandos:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet17":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet17":::

4. Implemente o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método passando o comando ao longo de:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet18":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet18":::

5. Implementar o método de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> . Quando esse método recebe um pressionamento de tecla, ele deve executar uma destas ações:

   - Permitir que o caractere seja gravado no buffer e, em seguida, disparar ou filtrar a conclusão. (Imprimir caracteres faça isso.)

   - Confirme a conclusão, mas não permita que o caractere seja gravado no buffer. (Espaço em branco, **guia** e **digite** fazer isso quando uma sessão de conclusão for exibida.)

   - Permitir que o comando seja passado para o próximo manipulador. (Todos os outros comandos).

     Como esse método pode exibir a interface do usuário, chame para certificar-se de <xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> que ele não seja chamado em um contexto de automação:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet19":::

6. Esse código é um método particular que dispara a sessão de conclusão:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet20":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet20":::

7. O exemplo a seguir é um método particular que cancela a assinatura do <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> evento:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet21":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet21":::

## <a name="build-and-test-the-code"></a>Compilar e testar o código
 Para testar esse código, crie a solução CompletionTest e execute-a na instância experimental.

#### <a name="to-build-and-test-the-completiontest-solution"></a>Para compilar e testar a solução CompletionTest

1. Compile a solução.

2. Quando você executa esse projeto no depurador, uma segunda instância do Visual Studio é iniciada.

3. Crie um arquivo de texto e digite algum texto que inclua a palavra "Adicionar".

4. Conforme você digita o primeiro "a" e, em seguida, "d", uma lista que contém "adição" e "adaptação" deve aparecer. Observe que a adição está selecionada. Quando você digita outro "d", a lista deve conter apenas "adição", que agora é selecionada. Você pode confirmar "adição" pressionando a **barra de espaços**, a **guia** ou a tecla **Enter** , ou descartar a lista digitando ESC ou qualquer outra chave.

## <a name="see-also"></a>Confira também
- [Walkthrough: vincular um tipo de conteúdo a uma extensão de nome de arquivo](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
