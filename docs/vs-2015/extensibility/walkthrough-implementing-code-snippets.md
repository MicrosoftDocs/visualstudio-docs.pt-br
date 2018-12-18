---
title: 'Passo a passo: Implementar trechos de código | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6fe91fd4e80c14e9b4cf59136fa6d3e0e003f554
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752057"
---
# <a name="walkthrough-implementing-code-snippets"></a>Passo a passo: implementando snippets de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar trechos de código e incluí-los em uma extensão de editor para que os usuários da extensão podem adicioná-los para seu próprio código.  
  
 Um trecho de código é um fragmento de código ou outro texto que pode ser incorporado em um arquivo. Para exibir todos os trechos de código que foram registrados para linguagens de programação específicas na **ferramentas** menu, clique em **Gerenciador de trechos de código**. Para inserir um trecho de código em um arquivo, o botão direito do mouse onde você deseja que o trecho de código, clique em **Inserir trecho** ou **envolver com**, localize o trecho de código que você deseja e, em seguida, clique duas vezes nele. Pressione TAB ou SHIFT + TAB para modificar as partes relevantes do trecho de código e, em seguida, pressione ENTER ou ESC para aceitá-lo. Para obter mais informações, consulte [Snippets de Código](../ide/code-snippets.md).  
  
 Um trecho de código está contido em um arquivo XML que tem a extensão de nome de arquivo. snippet. Um trecho de código pode conter campos que são realçados depois que o trecho de código é inserido para que o usuário possa encontrar e alterá-los. Um arquivo de trecho de código também fornece informações para o **Gerenciador de trechos de código** para que ele possa exibir o nome do trecho de código na categoria correta. Para obter informações sobre o esquema de trecho de código, consulte [referência de esquema de trechos de código](../ide/code-snippets-schema-reference.md).  
  
 Este passo a passo ensina como realizar essas tarefas:  
  
1. Crie e registre os trechos de código para um idioma específico.  
  
2. Adicione a **Inserir trecho** comando ao menu de atalho.  
  
3. Implementar a expansão de trecho de código.  
  
   Este passo a passo se baseia [instruções passo a passo: exibindo o preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-and-registering-code-snippets"></a>Criando e registrando trechos de código  
 Normalmente, os trechos de código são associados com um serviço de linguagem registrado. No entanto, você não precisa implementar um <xref:Microsoft.VisualStudio.Package.LanguageService> registrar trechos de código. Em vez disso, basta especificar um GUID no arquivo de índice de trecho de código e, em seguida, use o mesmo GUID no <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> que você adicionar ao seu projeto.  
  
 As etapas a seguir demonstram como criar trechos de código e associá-los com um GUID específico.  
  
1. Crie a seguinte estrutura de diretório:  
  
    **%InstallDir%\TestSnippets\Snippets\1033\\**  
  
    em que *% InstallDir %* é a pasta de instalação do Visual Studio. (Embora esse caminho normalmente é usado para instalar os trechos de código, você pode especificar qualquer caminho.)  
  
2. Na pasta \1033\, crie um arquivo. XML e denomine **TestSnippets.xml**. (Embora esse nome é usado normalmente para um arquivo de índice de trecho de código, você pode especificar qualquer nome desde que ele tenha uma extensão de nome de arquivo. XML.) Adicione o seguinte texto e, em seguida, exclua o GUID do espaço reservado e adicione seus próprios.  
  
   ```xml  
   <?xml version="1.0" encoding="utf-8" ?>  
   <SnippetCollection>  
       <Language Lang="TestSnippets" Guid="{00000000-0000-0000-0000-000000000000}">  
           <SnippetDir>  
               <OnOff>On</OnOff>  
               <Installed>true</Installed>  
               <Locale>1033</Locale>  
               <DirPath>%InstallRoot%\TestSnippets\Snippets\%LCID%\</DirPath>  
               <LocalizedName>Snippets</LocalizedName>  
           </SnippetDir>  
       </Language>  
   </SnippetCollection>  
   ```  
  
3. Crie um arquivo na pasta de trecho de código, nomeie- **testar**`.snippet`e, em seguida, adicione o seguinte texto:  
  
   ```xml  
   <?xml version="1.0" encoding="utf-8" ?>  
   <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
       <CodeSnippet Format="1.0.0">  
           <Header>  
               <Title>Test replacement fields</Title>  
               <Shortcut>test</Shortcut>  
               <Description>Code snippet for testing replacement fields</Description>  
               <Author>MSIT</Author>  
               <SnippetTypes>  
                   <SnippetType>Expansion</SnippetType>  
               </SnippetTypes>  
           </Header>  
           <Snippet>  
               <Declarations>  
                   <Literal>  
                     <ID>param1</ID>  
                       <ToolTip>First field</ToolTip>  
                       <Default>first</Default>  
                   </Literal>  
                   <Literal>  
                       <ID>param2</ID>  
                       <ToolTip>Second field</ToolTip>  
                       <Default>second</Default>  
                   </Literal>  
               </Declarations>  
               <References>  
                  <Reference>  
                      <Assembly>System.Windows.Forms.dll</Assembly>  
                  </Reference>  
               </References>  
               <Code Language="TestSnippets">  
                   <![CDATA[MessageBox.Show("$param1$");  
        MessageBox.Show("$param2$");]]>  
               </Code>    
           </Snippet>  
       </CodeSnippet>  
   </CodeSnippets>  
   ```  
  
   As etapas a seguir mostram como registrar os trechos de código.  
  
#### <a name="to-register-code-snippets-for-a-specific-guid"></a>Para registrar os trechos de código para um GUID específico  
  
1.  Abra o **CompletionTest** projeto. Para obter informações sobre como criar este projeto, consulte [instruções passo a passo: exibindo o preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md).  
  
2.  No projeto, adicione referências aos assemblies a seguir:  
  
    -   Microsoft.VisualStudio.TextManager.Interop  
  
    -   Microsoft.VisualStudio.TextManager.Interop.8.0  
  
    -   Microsoft.MSXML  
  
3.  No projeto, abra o arquivo de vsixmanifest.  
  
4.  Certifique-se de que o **ativos** guia contém uma **VsPackage** tipo e que conteúdo **projeto** é definido como o nome do projeto.  
  
5.  Selecione o projeto CompletionTest e na janela Propriedades, defina **gerar arquivo de Pkgdef** à **verdadeiro**. Salvar o projeto.  
  
6.  Adicionar um estático `SnippetUtilities` classe ao projeto.  
  
     [!code-csharp[VSSDKCompletionTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#22)]
     [!code-vb[VSSDKCompletionTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#22)]  
  
7.  Na classe SnippetUtilities, definir um GUID e dê a ele o valor usado no arquivo SnippetsIndex.xml.  
  
     [!code-csharp[VSSDKCompletionTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#23)]
     [!code-vb[VSSDKCompletionTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#23)]  
  
8.  Adicione a <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> para o `TestCompletionHandler` classe. Esse atributo pode ser adicionado a qualquer classe de público ou interno (não estático) no projeto. (Talvez você precise adicionar um `using` instrução para o namespace Microsoft.VisualStudio.Shell.)  
  
     [!code-csharp[VSSDKCompletionTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#24)]
     [!code-vb[VSSDKCompletionTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#24)]  
  
9. Compile e execute o projeto. Na instância experimental do Visual Studio é iniciado quando o projeto é executado, o trecho de código que você acabou de registrar deve ser exibido na **Gerenciador de trechos de código** sob o **TestSnippets** idioma.  
  
## <a name="adding-the-insert-snippet-command-to-the-shortcut-menu"></a>Adicionando o comando de trecho de código de inserção para o Menu de atalho  
 O **Inserir trecho** comando não está incluído no menu de atalho para um arquivo de texto. Portanto, você deve habilitar o comando.  
  
#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>Para adicionar o comando Inserir trecho de código para o menu de atalho  
  
1.  Abra o `TestCompletionCommandHandler` arquivo de classe.  
  
     Como essa classe implementa <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>, você pode ativar o **Inserir trecho** comando o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método. Antes de habilitar o comando, verifique se esse método não está sendo chamado dentro de uma função de automação porque quando o **Inserir trecho** comando é clicado, ele será exibido da interface de usuário do seletor de trecho de código (UI).  
  
     [!code-csharp[VSSDKCompletionTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#25)]
     [!code-vb[VSSDKCompletionTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#25)]  
  
2.  Compile e execute o projeto. Na instância experimental, abra um arquivo que tem a extensão de nome de arquivo. zzz e, em seguida, clique duas vezes nele. O **Inserir trecho** comando deve aparecer no menu de atalho.  
  
## <a name="implementing-snippet-expansion-in-the-snippet-picker-ui"></a>Implementação de expansão de trecho de código no seletor de trecho de código da interface do usuário  
 Esta seção mostra como implementar a expansão de trecho de código para que o seletor de trecho de código da interface do usuário é exibido quando **Inserir trecho** é clicado no menu de atalho. Um trecho de código também é expandido quando um usuário digita o atalho de trecho de código e, em seguida, pressiona TAB.  
  
 Para exibir o seletor de trecho de código da interface do usuário e habilitar a navegação e a aceitação de pós-inserção de trecho de código, use o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método. A inserção em si é tratada pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> método.  
  
 A implementação de expansão de trecho de código usa herdado <xref:Microsoft.VisualStudio.TextManager.Interop> interfaces. Quando você traduzir das classes de editor atual para o código herdado, lembre-se de que as interfaces herdadas usar uma combinação de números de linha e coluna para especificar os locais em um buffer de texto, mas as classes atuais usam um índice. Portanto, se um buffer tem três linhas cada um deles tem dez caracteres (mais de uma nova linha, que conta como caractere de 1), o quarto caractere na terceira linha está na posição 27 na implementação atual, mas ele está na linha 2, posicione 3 na implementação do antiga.  
  
#### <a name="to-implement-snippet-expansion"></a>Para implementar a expansão de trecho de código  
  
1.  Para o arquivo que contém o `TestCompletionCommandHandler` da classe, adicione o seguinte `using` instruções.  
  
     [!code-csharp[VSSDKCompletionTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#26)]
     [!code-vb[VSSDKCompletionTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#26)]  
  
2.  Verifique as `TestCompletionCommandHandler` implementam a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> interface.  
  
     [!code-csharp[VSSDKCompletionTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#27)]
     [!code-vb[VSSDKCompletionTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#27)]  
  
3.  No `TestCompletionCommandHandlerProvider` classe, importe o <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>.  
  
     [!code-csharp[VSSDKCompletionTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#28)]
     [!code-vb[VSSDKCompletionTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#28)]  
  
4.  Adicione alguns campos particulares para as interfaces de expansão de código e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.  
  
     [!code-csharp[VSSDKCompletionTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#29)]
     [!code-vb[VSSDKCompletionTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#29)]  
  
5.  No construtor do `TestCompletionCommandHandler` de classe, defina os campos a seguir.  
  
     [!code-csharp[VSSDKCompletionTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#30)]
     [!code-vb[VSSDKCompletionTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#30)]  
  
6.  Para exibir o seletor de trecho de código quando o usuário clica o **Inserir trecho** de comando, adicione o seguinte código para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método. (Para tornar essa explicação mais legível, o código de EXEC () que é usado para preenchimento de declaração não é mostrado; em vez disso, os blocos de código são adicionados para o método existente). Adicione o seguinte bloco de código após o código que verifica se há um caractere.  
  
     [!code-csharp[VSSDKCompletionTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#31)]
     [!code-vb[VSSDKCompletionTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#31)]  
  
7.  Se um trecho de código tem campos que podem ser navegados, a sessão de expansão é mantida em aberto até que a expansão explicitamente for aceito; Se o trecho de código não tem campos, a sessão é fechada e é retornada como `null` pelo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> método. No <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método, após o seletor de trecho de código de interface do usuário que você adicionou na etapa anterior, adicione o seguinte código para lidar com navegação de trecho de código (quando o usuário pressiona TAB ou SHIFT + TAB após a inserção de trecho de código).  
  
     [!code-csharp[VSSDKCompletionTest#32](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#32)]
     [!code-vb[VSSDKCompletionTest#32](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#32)]  
  
8.  Para inserir o trecho de código quando o usuário digita o atalho correspondente e, em seguida, pressiona TAB, adicione código para o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> método. O método particular que insere o trecho de código será mostrado em uma etapa posterior. Adicione o seguinte código após o código de navegação que você adicionou na etapa anterior.  
  
     [!code-csharp[VSSDKCompletionTest#33](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#33)]
     [!code-vb[VSSDKCompletionTest#33](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#33)]  
  
9. Implementar os métodos do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> interface. Nessa implementação, são os únicos métodos de interesse <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>. Os outros métodos devem retornar apenas <xref:Microsoft.VisualStudio.VSConstants.S_OK>.  
  
     [!code-csharp[VSSDKCompletionTest#34](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#34)]
     [!code-vb[VSSDKCompletionTest#34](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#34)]  
  
10. Implementar o método de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> . O método auxiliar que insere, na verdade, as expansões será abordado em uma etapa posterior. O <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> fornece informações de linha e coluna, que pode ser obtido a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.  
  
     [!code-csharp[VSSDKCompletionTest#35](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#35)]
     [!code-vb[VSSDKCompletionTest#35](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#35)]  
  
11. O seguinte método privado insere um trecho de código, com base no atalho ou no título e no caminho. Em seguida, ele chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> método com o trecho de código.  
  
     [!code-csharp[VSSDKCompletionTest#36](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#36)]
     [!code-vb[VSSDKCompletionTest#36](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#36)]  
  
## <a name="building-and-testing-code-snippet-expansion"></a>Compilando e testando a expansão de trecho de código  
 Você pode testar se a expansão de trecho de código funciona em seu projeto.  
  
1.  Compile a solução. Quando você executar esse projeto no depurador, uma segunda instância do Visual Studio é instanciada.  
  
2.  Abra um arquivo de texto e digite algum texto.  
  
3.  Clique com botão direito em algum lugar no texto e, em seguida, clique em **Inserir trecho de código**.  
  
4.  Seletor de trecho de interface do usuário deve aparecer com um pop-up que diz **campos de substituição de teste**. Clique duas vezes o pop-up.  
  
     O trecho a seguir deve ser inserido.  
  
    ```  
    MessageBox.Show("first");  
    MessageBox.Show("second");  
    ```  
  
     Não pressione ENTER ou ESC.  
  
5.  Pressione TAB e SHIFT + TAB para alternar entre "first" e "segundo".  
  
6.  Aceite a inserção pressionando ENTER ou ESC.  
  
7.  Em uma parte diferente do texto, digite "teste" e, em seguida, pressione TAB. Como "teste" é o atalho de trecho de código, o trecho de código deve ser inserido novamente.  
  
## <a name="next-steps"></a>Próximas etapas

