---
title: Criar um editor de corpo HTTP personalizado para o Editor de Testes de Desempenho Web
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, custom HTTP body editor
ms.assetid: a0b2d8ff-3e2a-487e-9172-90047174f336
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 02faf2a6c495d7fd5566c8f4291ecaad20ef5eb7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288137"
---
# <a name="how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor"></a>Como criar um editor de corpo HTTP personalizado para o Editor de Testes de Desempenho Web

Você pode criar um editor de conteúdo personalizado que permite editar o conteúdo do corpo da cadeia de caracteres ou o conteúdo binário do corpo de uma solicitação de serviço Web, por exemplo, SOAP, REST, asmx, wcf, RIA e outros tipos de solicitação de serviço Web.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

Você pode implementar estes tipos de editores:

- **Editor de conteúdo de cadeias de caracteres** É implementado usando a interface <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin>.

- **Editor de conteúdo binário** É implementado usando a interface <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>.

Essas interfaces estão contidas no namespace <xref:Microsoft.VisualStudio.TestTools.WebTesting>.

## <a name="create-a-windows-control-library-project"></a>Criar um projeto de biblioteca de controle do Windows

1. No Visual Studio, crie um projeto de **Biblioteca de Controle do Windows Forms**. Dê ao projeto o nome **MessageEditors**.

   O projeto é adicionado à nova solução e um <xref:System.Windows.Forms.UserControl> chamado *UserControl1.cs* é apresentado no Designer.

1. Da **Caixa de Ferramentas**, na categoria **Controles Comuns**, arraste uma <xref:System.Windows.Forms.RichTextBox> para a superfície de UserControl1.

1. Escolha o glifo de marcação de ação (![Glifo de Marcação Inteligente](../test/media/vs_winformsmttagglyph.gif)) no canto superior direito do controle <xref:System.Windows.Forms.RichTextBox> e, em seguida, selecione **Encaixar no Contêiner Pai**.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto de biblioteca Windows Forms e selecione **Propriedades**.

1. Nas **Propriedades**, selecione a guia **aplicativo** .

1. Na lista suspensa **Estrutura de destino**, selecione .NET Framework 4 (ou posterior).

1. A caixa de diálogo **Alteração da Estrutura de Destino** é exibida.

1. Escolha **Sim**.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó **referências** e selecione **Adicionar referência**.

1. A caixa de diálogo **Adicionar Referência** é exibida.

1. Escolha a guia .**NET**, role para baixo e selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework** e clique em **OK**.

1. Se o **Designer de exibição** ainda não estiver aberto, em **Gerenciador de soluções**, clique com o botão direito do mouse em **UserControl1.cs** e selecione **Designer de exibição**.

1. Na superfície de design, clique com o botão direito do mouse e selecione **Exibir Código**.

1. (Opcional) Altere o nome da classe e o construtor de UserControl1 para um nome significativo, por exemplo, MessageEditorControl:

    > [!NOTE]
    > O exemplo usa MessageEditorControl.

    ```csharp
    namespace MessageEditors
    {
        public partial class MessageEditorControl : UserControl
        {
            public MessageEditorControl()
            {
                InitializeComponent();
            }
        }
    }
    ```

1. Adicione as seguintes propriedades para que seja possível obter e definir o texto em RichTextBox1. A interface de <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> usará EditString e <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> usará EditByteArray:

    ```csharp
    public String EditString
    {
       get
       {
           return this.richTextBox1.Text;
       }
       set
       {
           this.richTextBox1.Text = value;
       }
    }

    public byte[] EditByteArray
    {
       get
       {
           return System.Convert.FromBase64String(richTextBox1.Text);
       }
       set
       {
           richTextBox1.Text = System.Convert.ToBase64String(value, 0, value.Length);
       }
    }
    ```

## <a name="add-a-class-to-the-windows-control-library-project"></a>Adicionar uma classe ao projeto da Biblioteca de Controles do Windows

Adicione uma classe ao projeto. Será usado para implementar as interfaces <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>.

**Visão geral do código neste procedimento**

O MessageEditorControl <xref:System.Windows.Forms.UserControl> criado no primeiro procedimento anterior é instanciado como messageEditorControl:

```csharp
private MessageEditorControl messageEditorControl
```

A instância do messageEditorControl é hospedada na caixa de diálogo de plug-in que é criada pelo método <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.CreateEditor*>. Além disso, <xref:System.Windows.Forms.RichTextBox> de messageEditorControl é preenchido com o conteúdo em <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>. No entanto, a criação do plug-in não pode ocorrer a menos que <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> retorne `true`. No caso deste editor, <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.SupportsContentType*> retorna `true` se <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> em <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> contiver "xml".

Quando a edição do corpo da cadeia de caracteres terminar e o usuário clicar em **OK** na caixa de diálogo de plug-in, <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin.GetNewValue*> será chamado para obter o texto editado como uma cadeia de caracteres e atualizar **Corpo da string** na solicitação no Editor de desempenho de teste na Web.

### <a name="create-a-class-and-implement-the-istringhttpbodyeditorplugin-interface"></a>Criar uma classe e implementar a interface IStringHttpBodyEditorPlugin

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto de biblioteca de controle de Windows Forms e selecione **Adicionar novo item**.

   A caixa de diálogo **Adicionar novo item** é exibida.

2. Selecione **classe**.

3. Na caixa de texto **Nome**, digite um nome significativo para a classe, por exemplo, `MessageEditorPlugins`.

4. Escolha **Adicionar**.

   Class1 é adicionado ao projeto e aberto no editor de código.

5. No Editor de Códigos, adicione a seguinte instrução `using`:

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    ```

6. Cole o código a seguir para implementar a interface:

    ```csharp
    /// <summary>
    /// Editor for generic text based hierarchical messages such as XML and JSON.
    /// </summary>
    public class XmlMessageEditor : IStringHttpBodyEditorPlugin
    {
        public XmlMessageEditor()
        {
        }

        /// <summary>
        /// Determine if this plugin supports the content type.
        /// </summary>
        /// <param name="contentType">The content type to test.</param>
        /// <returns>Returns true if the plugin supports the specified content type.</returns>
        public bool SupportsContentType(string contentType)
        {
            return contentType.ToLower().Contains("xml");
        }

        /// <summary>
        /// Create a UserControl to edit the specified bytes.
        /// This control will be hosted in the
        /// plugin dialog which provides OK and Cancel buttons.
        /// </summary>
        /// <param name="contentType">The content type of the BinaryHttpBody.</param>
        /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
        /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
        public object CreateEditor(string contentType, string initialValue)
        {
            messageEditorControl = new MessageEditorControl();
            messageEditorControl.EditString = initialValue;
            return this.messageEditorControl;
        }

        /// <summary>
        /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
        /// </summary>
        public string GetNewValue()
        {
            return messageEditorControl.EditString;
        }

        private MessageEditorControl messageEditorControl;
    }
    ```

## <a name="add-a-ibinaryhttpbodyeditorplugin-to-the-class"></a>Adicionar um IBinaryHttpBodyEditorPlugin à classe

Implemente a interface <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>.

**Visão geral do código neste procedimento**

A implementação de código para a interface do <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> é semelhante ao <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin> abrangido no procedimento anterior. No entanto, a versão binária usa uma matriz de bytes para manipular os dados binários em vez de uma cadeia de caracteres.

O MessageEditorControl <xref:System.Windows.Forms.UserControl> criado no primeiro procedimento é instanciado como messageEditorControl:

```csharp
private MessageEditorControl messageEditorControl
```

A instância do messageEditorControl é hospedada na caixa de diálogo de plug-in que é criada pelo método <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.CreateEditor*>. Além disso, <xref:System.Windows.Forms.RichTextBox> de messageEditorControl é preenchido com o conteúdo em <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>. No entanto, a criação do plug-in não pode ocorrer a menos que <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> retorne `true`. No caso deste editor, <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.SupportsContentType*> retorna `true` se <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody.ContentType*> em <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody> contiver “msbin1”.

Quando a edição do corpo da cadeia de caracteres terminar e o usuário clicar em **OK** na caixa de diálogo de plug-in, <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin.GetNewValue*> será chamado para obter o texto editado como uma cadeia de caracteres e atualizar **BinaryHttpBody.Data** na solicitação no Editor de desempenho de teste na Web.

### <a name="to-add-the-ibinaryhttpbodyeditorplugin-to-the-class"></a>Para adicionar o IBinaryHttpBodyEditorPlugin à classe

- Escreva ou copie o seguinte código sob a classe de XmlMessageEditor adicionada ao procedimento anterior para criar uma instância da classe de Msbin1MessageEditor de interface de <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin> e para implementar métodos necessários:

    ```csharp
    /// <summary>
        /// Editor for MSBin1 content type (WCF messages)
        /// </summary>
        public class Msbin1MessageEditor : IBinaryHttpBodyEditorPlugin
        {
            /// <summary>
            ///
            /// </summary>
            public Msbin1MessageEditor()
            {
            }

            /// <summary>
            /// Determine if this plugin supports a content type.
            /// </summary>
            /// <param name="contentType">The content type to test.</param>
            /// <returns>Returns true if the plugin supports the specified content type.</returns>
            public bool SupportsContentType(string contentType)
            {
                return contentType.ToLower().Contains("msbin1");
            }

            /// <summary>
            /// Create a UserControl to edit the specified bytes. This control will be hosted in the
            /// plugin dialog which provides OK and Cancel buttons.
            /// </summary>
            /// <param name="contentType">The content type of the BinaryHttpBody.</param>
            /// <param name="initialValue">The bytes to edit. The bytes are the payload of a BinaryHttpBody.</param>
            /// <returns>A UserControl capable of displaying and editing the byte array value of the specified content type.</returns>
            public object CreateEditor(string contentType, byte[] initialValue)
            {
                messageEditorControl = new MessageEditorControl();
                messageEditorControl.EditByteArray = initialValue;
                return messageEditorControl;
            }

            /// <summary>
            /// Gets the edited bytes after the OK button is clicked on the plugin dialog.
            /// </summary>
            public byte[] GetNewValue()
            {
                return messageEditorControl.EditByteArray;
            }

            private MessageEditorControl messageEditorControl;
            private object originalMessage;
        }
    ```

## <a name="build-and-deploy-the-plug-ins"></a>Compilar e implantar os plug-ins

1. No menu **Compilar** , escolha **Compilar \<Windows Form Control Library project name> **.

2. Feche todas as instâncias do Visual Studio.

   > [!NOTE]
   > Fechar o Visual Studio garante que o arquivo *.dll* não seja bloqueado antes que você tente copiá-lo.

3. Copie o arquivo *. dll* resultante da pasta *bin\Debug* do projeto (por exemplo, *MessageEditors.dll*) para *%ProgramFiles%\Microsoft Visual Studio\2017 \\ \<edition> \Common7\IDE\PrivateAssemblies\WebTestPlugins*.

4. Abra o Visual Studio.

   O *. dll* agora está registrado no Visual Studio.

## <a name="verify-the-plug-ins-using-a-web-performance-test"></a>Verificar os plug-ins usando um Teste de Desempenho Web

1. Criar um projeto de teste.

2. Crie um teste de desempenho Web e insira uma URL no navegador para um serviço Web.

3. Quando você concluir a gravação, na Editor de Testes de Desempenho Web, expanda a solicitação para o serviço Web e selecione um **corpo de cadeia de caracteres** ou um **corpo binário**.

4. Na janela **Propriedades** , selecione corpo da cadeia de caracteres ou corpo binário e escolha as reticências **(...)**.

   A caixa de diálogo **Editar corpo de dados HTTP** é exibida.

5. Agora você pode editar os dados e escolher **OK**. Isso chama o método GetNewValue aplicável para atualizar o conteúdo no <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>.

## <a name="compile-the-code"></a>Compilar o código

Verifique se o framework de destino para o projeto da Biblioteca de Controles do Windows é o .NET Framework 4.5. Por padrão, os projetos de biblioteca de controle do Windows destinam-se à estrutura do cliente do .NET Framework 4.5, que não permitirá a inclusão de referência de Microsoft.VisualStudio.QualityTools.WebTestFramework.

Para obter mais informações, confira [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md).

## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IStringHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IBinaryHttpBodyEditorPlugin>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.IHttpBody>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.RichTextBox>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [Como criar um plug-in no nível da solicitação](../test/how-to-create-a-request-level-plug-in.md)
- [Codificar uma regra de extração personalizada para um teste de desempenho Web](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
- [Codificar uma regra de validação personalizada para um teste de desempenho Web](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
- [Como criar um plug-in de teste de carga](../test/how-to-create-a-load-test-plug-in.md)
- [Gerar e executar um teste de desempenho para Web codificado](../test/generate-and-run-a-coded-web-performance-test.md)
- [Como: criar um suplemento do Visual Studio para o Visualizador de Resultados de Teste de desempenho da Web](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)
