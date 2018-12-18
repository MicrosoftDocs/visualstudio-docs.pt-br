---
title: Testar aplicativos Windows UWP e 8.1 da Windows Store com testes de UI codificados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c8d9c15e-ce3c-401a-86ec-c5c124a239d8
caps.latest.revision: 26
ms.author: gewarren
manager: douge
ms.openlocfilehash: 70973305764319ecb8ebf902945c92eb4723af7a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934295"
---
# <a name="test-windows-uwp-and-81-store-apps-with-coded-ui-tests"></a>Testar aplicativos Windows UWP e 8.1 da Windows Store com testes de UI codificados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use este passo a passo para criar testes de interface do usuário para aplicativos UWP e aplicativos Store 8.1 baseados em XAML.
  
## <a name="create-a-simple-windows-store-app"></a>Criar um aplicativo simples da Windows Store  
  
1.  Se desejar executar testes de IU codificados no aplicativo da Windows Store baseado em XAML, será necessário [definir uma propriedade de automação exclusiva que identifica cada controle](../test/set-a-unique-automation-property-for-windows-store-controls-for-testing.md).  
  
     No menu **Ferramentas**, aponte para **Opções** e escolha **Editor de Texto**, **XAML** e **Diversos**.  
  
     Marque a caixa de seleção para nomear automaticamente elementos interativos na criação.  
  
     ![Opções diversas de XAML](../test/media/cuit-windowsstoreapp-b.png "CUIT_WindowsStoreApp_B")  
  
2.  Crie um novo projeto para um aplicativo da Windows Store baseado em XAML usando um modelo Visual C# ou Visual Basic.  
  
     ![Criar um aplicativo em branco da Windows Store &#40;XAML&#41;](../test/media/cuit-windowsstoreapp-newproject-blankstoreapp.png "CUIT_WindowsStoreApp_NewProject_BlankStoreApp")  
  
3.  No Gerenciador de Soluções, abra MainPage.xaml. Na Caixa de Ferramentas, arraste um controle de botão e um controle de caixa de texto para a superfície do design.  
  
     ![Criar o aplicativo da Windows Store](../test/media/cuit-windowsstoreapp-design.png "CUIT_WindowsStoreApp_Design")  
  
4.  Clique duas vezes no controle de botão e adicione o código a seguir:  
  
    ```csharp  
    private void button_Click_1(object sender, RoutedEventArgs e)  
    {  
        this.textBox.Text = this.button.Name;  
    }  
  
    ```  
  
    ```vb  
    Public NotInheritable Class MainPage  
        Inherits Page  
  
        Private Sub button_Click(sender As Object, e As RoutedEventArgs) Handles Button.Click  
            Me.textBox.Text = Me.button.Name  
        End Sub  
    End Class  
    ```  
  
5.  Pressione F5 para executar o aplicativo da Windows Store.  
  
## <a name="create-and-run-a-coded-ui-test-for-the-windows-store-app"></a>Crie e execute um teste de IU codificado no aplicativo da Windows Store  

[Como criar testes de IU codificados para aplicativos UWP (Plataforma Universal do Windows)?](#uwpapps)
  
1. Crie um novo projeto de teste de IU codificado para o aplicativo da Windows Store.  
  
    ![Novo projeto de teste de IU codificado &#40;Aplicativos da Windows Store&#41;](../test/media/cuit-windowsstore-newproject.png "CUIT_WindowsStore_NewProject")  
  
2. Escolha editar o mapa de interface do usuário usando a ferramenta de fios.  
  
    ![Optar por editar o mapa de interface do usuário ou adicionar declarações](../test/media/cuit-windowsstoreapp-createproject-gencodedialog.png "CUIT_WindowsStoreApp_CreateProject_GenCodeDialog")  
  
3. Use a ferramenta de fios no Construtor de Teste de IU Codificado para selecionar o bloco de aplicativos, clique com o botão direito do mouse em **AutomationId** e escolha **Copiar Valor para a Área de Transferência**. O valor na área de transferência será usado mais tarde para gravar a ação para ativar o aplicativo para teste.  
  
    ![Copiar AutomationId para a área de transferência](../test/media/cuit-windows-store-tileautomationid.png "CUIT_Windows_Store_TileAutomationID")  
  
4. No aplicativo da Windows Store em execução, use a ferramenta de fios para selecionar o controle de botão e o controle de caixa de texto. Depois de adicionar cada controle, escolha o botão **Adicionar controle ao mapa de controle de interface do usuário** na barra de ferramentas do Construtor de Teste de IU Codificado.  
  
    ![Adicionar controle ao mapa de interface do usuário](../test/media/cuit-windowsstoreapp-uimap.png "CUIT_WindowsStoreApp_UIMap")  
  
5. Escolha o botão **Gerar Código** na barra de ferramentas do Construtor de Teste de IU Codificado e escolha **Gerar** para criar o código para alterações no mapa de controle de interface do usuário.  
  
    ![Gerar código para o mapa de interface do usuário](../test/media/cuit-windowsstoreapp-generate.png "CUIT_WindowsStoreApp_Generate")  
  
6. Escolha o botão para definir um valor na caixa de texto.  
  
    ![Clicar em um controle de botão para definir o valor da caixa de texto](../test/media/cuit-windowsstoreapp-clickbutton.png "CUIT_WindowsStoreApp_ClickButton")  
  
7. Use a ferramenta de fios para selecionar o controle de caixa de texto e, em seguida, selecione a propriedade **Text**.  
  
    ![Selecionar a propriedade Text](../test/media/cuit-windowsstoreapp-selecttextproperty.png "CUIT_WindowsStoreApp_SelectTextProperty")  
  
8. Adicione uma asserção. Ela será usada no teste para verificar se o valor está correto.  
  
    ![Escolher a caixa de texto com fios e adicionar declaração](../test/media/cuit-windowsstoreapp-textbox-addassertion.png "CUIT_WindowsStoreApp_Textbox_AddAssertion")  
  
9. Adicione e gere o código para a asserção.  
  
     ![Gerar código para a declaração de caixa de texto](../test/media/cuit-windowsstoreapp-textbox-generate-assertion.png "CUIT_WindowsStoreApp_Textbox_Generate_Assertion")  
  
10. **Visual C#**  
  
     No Gerenciador de Soluções, abra o arquivo UIMap.Designer.cs para exibir o código adicionado aos controles e ao método assert.  
  
     **Visual Basic**  
  
     No Gerenciador de Soluções, abra o arquivo CodedUITest1.vb e, no código do método de teste CodedUITestMethod1(), clique com o botão direito do mouse na chamada ao método de declaração adicionado automaticamente `Me.UIMap.AssertMethod1()` e escolha **Ir para Definição**. Isso abrirá o arquivo UIMap.Designer.vb no editor de código para ser possível exibir o código adicionado aos controles e ao método assert.  
  
    > [!WARNING]
    >  Não modifique o arquivo UIMap.designer.cs ou UIMap.Designer.vb diretamente. Se fizer isso, as alterações no arquivo serão substituídas sempre que o teste for gerado.  
  
     **Método assert**  
  
    ```csharp  
    public void AssertMethod1()  
    {  
        #region Variable Declarations  
        XamlEdit uITextBoxEdit = this.UIApp1Window.UITextBoxEdit;  
        #endregion  
  
        // Verify that the 'Text' property of 'textBox' text box equals 'button'  
        Assert.AreEqual(this.AssertMethod3ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text);  
    }  
    ```  
  
    ```vb  
    Public Sub AssertMethod1()  
        Dim uITextBoxEdit As XamlEdit = Me.UIApp2Window.UITextBoxEdit  
  
        'Verify that the 'Text' property of 'textBox' text box equals 'button'  
        Assert.AreEqual(Me.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text)  
    End Sub  
    ```  
  
     **Controles**  
  
    ```csharp  
    #region Properties  
    public XamlButton UIButtonButton  
    {  
        get  
        {  
            if ((this.mUIButtonButton == null))  
            {  
                this.mUIButtonButton = new XamlButton(this);  
                #region Search Criteria  
                this.mUIButtonButton.SearchProperties[XamlButton.PropertyNames.AutomationId] = "button";  
                this.mUIButtonButton.WindowTitles.Add("App1");  
                #endregion  
            }  
            return this.mUIButtonButton;  
        }  
    }  
  
    public XamlEdit UITextBoxEdit  
    {  
        get  
        {  
            if ((this.mUITextBoxEdit == null))  
            {  
                this.mUITextBoxEdit = new XamlEdit(this);  
                #region Search Criteria  
                this.mUITextBoxEdit.SearchProperties[XamlEdit.PropertyNames.AutomationId] = "textBox";  
                this.mUITextBoxEdit.WindowTitles.Add("App1");  
                #endregion  
            }  
            return this.mUITextBoxEdit;  
        }  
    }  
    #endregion  
  
    #region Fields  
    private XamlButton mUIButtonButton;  
  
    private XamlEdit mUITextBoxEdit;  
    #endregion  
    ```  
  
    ```vb  
    #Region "Properties"  
    Public ReadOnly Property UIButtonButton() As XamlButton  
        Get  
            If (Me.mUIButtonButton Is Nothing) Then  
                Me.mUIButtonButton = New XamlButton(Me)  
                Me.mUIButtonButton.SearchProperties(XamlButton.PropertyNames.AutomationId) = "button"  
                Me.mUIButtonButton.WindowTitles.Add("App2")  
            End If  
            Return Me.mUIButtonButton  
        End Get  
    End Property  
  
    Public ReadOnly Property UITextBoxEdit() As XamlEdit  
        Get  
            If (Me.mUITextBoxEdit Is Nothing) Then  
                Me.mUITextBoxEdit = New XamlEdit(Me)  
                Me.mUITextBoxEdit.SearchProperties(XamlEdit.PropertyNames.AutomationId) = "textBox"  
                Me.mUITextBoxEdit.WindowTitles.Add("App2")  
            End If  
            Return Me.mUITextBoxEdit  
        End Get  
    End Property  
    #End Region  
  
    #Region "Fields"  
    Private mUIButtonButton As XamlButton  
  
    Private mUITextBoxEdit As XamlEdit  
    #End Region  
    ```  
  
11. No Gerenciador de Soluções, abra o arquivo CodedUITest1.cs ou CodedUITest1.vb. Agora, é possível adicionar código ao método CodedUTTestMethod1 para as ações necessárias para executar o teste usando os controles adicionados ao UIMap:  
  
    1. Ative o aplicativo da Windows Store usando a propriedade de ID de automação copiada anteriormente na área de transferência.  
  
       ```csharp  
       XamlWindow.Launch("8ebca7c4-effe-4c86-9998-068daccee452_cyrqexqw8cc7c!App")  
       ```  
  
       ```vb  
       XamlWindow myAppWindow = XamlWindow.Launch("7254db3e-20a7-424e-8e05-7c4dabf4f28d_cyrqexqw8cc7c!App");  
       ```  
  
    2. Adicione um gesto para tocar no controle de botão:  
  
       ```csharp  
       Gesture.Tap(this.UIMap.UIApp1Window. UIButtonButton);  
       ```  
  
       ```vb  
       Gesture.Tap(Me.UIMap.UIApp2Window. UIButtonButton)  
       ```  
  
    3. Verifique se a chamada ao método de asserção gerada automaticamente vem depois da inicialização do aplicativo e do gesto de toque no botão:  
  
       ```csharp  
       this.UIMap.AssertMethod1();  
       ```  
  
       ```vb  
       Me.UIMap.AssertMethod1()  
       ```  
  
       Depois de adicionar o código, o método de teste CodedUITestMethod1 deve aparecer da seguinte maneira:  
  
    ```csharp  
    [TestMethod]  
    public void CodedUITestMethod1()  
    {  
        // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.  
  
        // Launch the app.  
        XamlWindow myAppWindow = XamlWindow.Launch("7254db3e-20a7-424e-8e05-7c4dabf4f28d_cyrqexqw8cc7c!App");  
  
        // Tap the button.  
        Gesture.Tap(this.UIMap.UIApp1Window.UIButtonButton);  
  
        this.UIMap.AssertMethod1();  
    }  
    ```  
  
    ```vb  
    <CodedUITest(CodedUITestType.WindowsStore)>  
    Public Class CodedUITest1  
  
        <TestMethod()>  
        Public Sub CodedUITestMethod1()  
            '              
            ' To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.  
            '  
  
            ' Launch the app.  
            XamlWindow.Launch("8ebca7c4-effe-4c86-9998-068daccee452_cyrqexqw8cc7c!App")  
  
            '// Tap the button.  
            Gesture.Tap(Me.UIMap.UIApp2Window.UIButtonButton)  
  
            Me.UIMap.AssertMethod1()  
        End Sub  
    ```  
  
12. Compile seu teste e execute-o usando o gerenciador de testes.  
  
     ![Executar o teste de IU codificado no Gerenciador de Testes](../test/media/cuit-windowsstoreapp-runtest.png "CUIT_WindowsStoreApp_RunTest")  
  
     O aplicativo da Windows Store é ativado, o botão da ação de tocar está concluído e a propriedade Texto da caixa de texto é preenchida e validada usando o método assert.  
  
     ![Executando um teste de IU codificado](../test/media/cuit-windowsstoreapp-running.png "CUIT_WindowsStoreApp_Running")  
  
     Depois da conclusão do teste, o gerenciador de testes exibe que o teste foi aprovado.  
  
     ![Exibições de teste aprovado no Gerenciador de Testes](../test/media/cuit-windowsstorapp-passedtest.png "CUIT_WindowsStorApp_PassedTest")  
  
## <a name="q--a"></a>Perguntas e respostas  
  
-   **P: Por que não vejo a opção para registrar meu teste de IU codificado na caixa de diálogo Gerar Código para Teste de IU Codificado?**  
  
     **R**: Não há suporte para a opção de registro em aplicativos da Windows Store.  
  
-   **P: Posso criar um teste de IU codificado para meus aplicativos da Windows Store baseados em WinJS?**  
  
     **R**: Não. Há suporte apenas para aplicativos baseados em XAML.  
  
-   **P: Posso criar testes de IU codificados para meus aplicativos da Windows Store em um sistema que não executa o Windows 8.1 nem o Windows 10?**  
  
     **R**: Não, os modelos de Projeto de Teste de IU Codificado estão disponíveis somente no Windows 8.1 e Windows 10. Para criar a automação para aplicativos UWP (Plataforma Universal do Windows), você precisará do Windows 10.  

<a name="uwpapps"></a>
- **P: Como fazer para criar testes de IU codificados para aplicativos UWP (Plataforma Universal do Windows)?**  
  
   **R**: Dependendo da plataforma em que você está testando o aplicativo UWP, crie o projeto de teste de IU codificado de uma destas maneiras:  
  
  - Um aplicativo UWP em execução no computador local será executado como um aplicativo da Loja. Para testar isso, é necessário usar o modelo **Projeto de Teste de IU Codificado (Windows)**. Para encontrar esse modelo ao criar um novo projeto, acesse o nó **Windows**, **Universal**. Se preferir, acesse o nó **Windows**, **Windows 8**, **Windows**.  
  
  - Um aplicativo UWP em execução em um emulador ou dispositivo móvel será executado como um aplicativo do Windows Phone. Para testar isso, é necessário usar o modelo **Projeto de Teste de IU Codificado (Windows Phone)**. Para encontrar esse modelo ao criar um novo projeto, acesse o nó **Windows**, **Universal**. Se preferir, acesse o nó **Windows**, **Windows 8**, **Windows Phone**.  
  
    Depois de criar o projeto, a criação de um teste permanece a mesma que antes.  
  
- **P: Por que não posso modificar o código no arquivo UIMap.Designer?**  
  
   **R**: Todas as alterações de código feitas no arquivo UIMapDesigner.cs serão substituídas sempre que você gerenciar o código usando o UIMap – Construtor de Teste de IU Codificado. Se você tiver de modificar um método gravado, copie-o para o arquivo UIMap.cs e renomeie-o. O arquivo UIMap.cs pode ser usado para substituir métodos e propriedades no arquivo UIMapDesigner.cs. Você deve remover a referência para o método original no arquivo Coded UITest.cs e substituí-la pelo nome do método renomeado.  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Definir uma propriedade de automação exclusiva para controles da Windows Store para teste](../test/set-a-unique-automation-property-for-windows-store-controls-for-testing.md)



