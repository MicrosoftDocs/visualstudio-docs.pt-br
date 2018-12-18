---
title: Testar um aplicativo UWP com um teste de IU codificado
ms.date: 05/31/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- uwp
ms.openlocfilehash: 3dcbd6065d45bf5350b80d555f335d3b8ec1cec7
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895958"
---
# <a name="create-a-coded-ui-test-to-test-a-uwp-app"></a>Criar um teste de IU codificado para testar um aplicativo UWP

Este artigo explica como criar um teste de IU codificado para um aplicativo UWP (Plataforma Universal do Windows).

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="create-a-uwp-app-to-test"></a>Criar um aplicativo UWP para teste

A primeira etapa é criar um aplicativo UWP simples no qual executar o teste.

1. No Visual Studio, crie um projeto usando o modelo **Aplicativo em Branco (Universal do Windows)** para o Visual C# ou o Visual Basic.

     ![Modelo de aplicativo em branco Universal do Windows](../test/media/blank-uwp-app-template.png)

1. Na caixa de diálogo **Novo Projeto da Plataforma Universal do Windows**, selecione **OK** para aceitar as versões de plataforma padrão.

1. No **Gerenciador de Soluções**, abra *MainPage.xaml*.

   O arquivo será aberto no **Designer XAML**.

1. Arraste um controle de botão e um controle de caixa de texto da **Caixa de Ferramentas** para a área de design.

     ![Projetar o aplicativo UWP](../test/media/toolbox-controls.png)

1. Forneça nomes aos controles. Selecione o controle de caixa de texto e, em seguida, na janela **Propriedades**, insira **textBox** no campo **Nome**. Selecione o controle de botão e, em seguida, na janela **Propriedades**, insira **button** no campo **Nome**.

1. Clique duas vezes no controle de botão e adicione o código a seguir ao corpo do método `Button_Click`. Esse código apenas define o texto na caixa de texto com o nome do controle de botão, só para nos fornecer algo para verificar com o teste de IU codificado que criaremos mais adiante.

   ```csharp
   this.textBox.Text = this.button.Name;
   ```

   ```vb
   Me.textBox.Text = Me.button.Name
   ```

1. Pressione **Ctrl**+**F5** para executar o aplicativo. Você deverá ver algo como o seguinte:

   ![Aplicativo UWP com botão e caixa de texto](media/uwp-app.png)

## <a name="create-a-coded-ui-test"></a>Criar um teste de IU codificado

1. Para adicionar um projeto de teste à solução, clique com o botão direito do mouse na solução no **Gerenciador de Soluções** e escolha **Adicionar** > **Novo Projeto**.

1. Na caixa de diálogo **Novo Projeto**, selecione o modelo **Projeto de Teste de IU Codificado (Universal do Windows)**. Encontre o modelo na categoria **Universal do Windows** no **Visual C#** ou no **Visual Basic**.

     ![Novo projeto de teste de IU codificado](../test/media/coded-ui-test-project-uwp-template.png)

   > [!NOTE]
   > Se o modelo **Projeto de Teste de IU Codificado (Universal do Windows)** não for exibido, você precisará [instalar o componente de teste de IU codificado](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component).

1. Na caixa de diálogo **Gerar Código para Teste de UI Codificado**, selecione **Editar o teste manualmente**.

     ![Caixa de diálogo Gerar Código para Teste de IU Codificado](../test/media/manually-edit-the-test.png)

1. Se o aplicativo UWP não estiver sendo executado, inicie-o pressionando **Ctrl**+**F5**.

1. Abra a caixa de diálogo **Construtor de Teste de IU Codificado** colocando o cursor no método `CodedUITestMethod1` e, em seguida, escolhendo **Testar** > **Gerar Código para Teste de IU Codificado** > **Usar Construtor de Teste de IU Codificado**.

1. Adicione os controles ao mapa de controle de IU. Use a ferramenta de fios **Construtor de Teste de IU Codificado** para selecionar o controle de botão no aplicativo UWP. Na caixa de diálogo **Adicionar Asserções**, expanda o painel **Mapa de Controle de IU** se necessário e, em seguida, selecione **Adicionar controle ao Mapa de Controle de IU**.

     ![Adicionar um controle ao mapa de interface do usuário](../test/media/add-control-to-ui-control-map.png)

1. Repita a etapa anterior para adicionar o controle de caixa de texto ao mapa de controle de IU.

1. Na caixa de diálogo **Construtor de Teste de IU Codificado**, selecione **Gerar Código** ou pressione **Ctrl**+**G**. Em seguida, selecione **Gerar** para criar um código de alterações no mapa de controle de IU.

     ![Gerar código para o mapa de interface do usuário](../test/media/generate-code-dialog.png)

1. Para verificar se o texto da caixa de texto é alterado para **button** quando o botão recebe um clique, clique no botão.

     ![Clicar no controle de botão para definir o valor da caixa de texto](../test/media/uwp-app-button-textbox.png)

1. Adicione uma asserção para verificar o texto no controle de caixa de texto. Use a ferramenta de fios para selecionar o controle de caixa de texto e, em seguida, selecione a propriedade **Text** na caixa de diálogo **Adicionar Asserções**. Em seguida, selecione **Adicionar Asserção** ou pressione **Alt**+**A**. Na caixa **Mensagem de Falha de Asserção**, insira **O valor da caixa de texto é inesperado.** e, em seguida, selecione **OK**.

     ![Escolher a caixa de texto com fios e adicionar asserção](../test/media/add-assertion-for-text.png)

1. Gere um código de teste para a asserção. Na caixa de diálogo **Construtor de Teste de IU Codificado**, selecione **Gerar Código**. Na caixa de diálogo **Gerar Código**, selecione **Adicionar e Gerar**.

     ![Gerar código para a asserção de caixa de texto](../test/media/add-and-generate-assert-method.png)

   No **Gerenciador de Soluções**, abra *UIMap.Designer.cs* para exibir o código adicionado aos controles e ao método de asserção.

   > [!TIP]
   > Se estiver usando o Visual Basic, abra *CodedUITest1.vb*. Em seguida, no código do método de teste `CodedUITestMethod1()`, clique com o botão direito do mouse na chamada ao método de asserção `Me.UIMap.AssertMethod1()` e escolha **Ir para definição**. *UIMap.Designer.vb* será aberto no editor de códigos e você poderá exibir o código adicionado dos controles e do método de asserção.

    > [!WARNING]
    > Não modifique o arquivo *UIMap.designer.cs* ou *UIMap.Designer.vb* diretamente. Se você fizer isso, as alterações serão substituídas quando o teste for gerado.

    O método de asserção tem esta aparência:

    ```csharp
    public void AssertMethod1()
    {
        #region Variable Declarations
        XamlEdit uITextBoxEdit = this.UIUWPAppWindow.UITextBoxEdit;
        #endregion

        // Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(this.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.");
    }
    ```

    ```vb
    Public Sub AssertMethod1()
        Dim uITextBoxEdit As XamlEdit = Me.UIApp2Window.UITextBoxEdit

        'Verify that the 'Text' property of 'textBox' text box equals 'button'
        Assert.AreEqual(Me.AssertMethod1ExpectedValues.UITextBoxEditText, uITextBoxEdit.Text, "Textbox value is unexpected.")
    End Sub
    ```
1. Em seguida, precisamos obter a **AutomationId** do [aplicativo](#create-a-uwp-app-to-test) UWP que você deseja testar. Abra o menu **Iniciar** do Windows para ver o bloco do aplicativo. Em seguida, arraste o ![Ícone de destino](media/target-icon.png) da ferramenta de fios na caixa de diálogo **Construtor de Teste de IU Codificado** para o bloco do aplicativo. Quando uma caixa azul surgir ao redor do bloco, libere o mouse.

   ![Ferramenta de fios](media/cross-hair-tool.png)

   A caixa de diálogo **Adicionar Asserções** será aberta e exibirá a **AutomationId** do aplicativo. Clique com o botão direito do mouse em **AutomationId** e escolha **Copiar Valor para a Área de Transferência**.

   ![AutomationID na caixa de diálogo Adicionar Asserção](../test/media/automation-id.png)

1. Adicione um código ao método de teste para iniciar o aplicativo UWP. No **Gerenciador de Soluções**, abra *CodedUITest1.cs* ou *CodedUITest1.vb*. Acima da chamada a `AssertMethod1`, adicione o código para iniciar o aplicativo UWP:

   ```csharp
   XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")
   ```

   ```vb
   XamlWindow myAppWindow = XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");
   ```

   Substitua a ID de automação no código de exemplo pelo valor copiado para a área de transferência na etapa anterior.

   > [!IMPORTANT]
   > Corte o início da ID de automação para remover caracteres como **P~**. Se você não cortar esses caracteres, o teste gerará uma `Microsoft.VisualStudio.TestTools.UITest.Extension.PlaybackFailureException` quando tentar iniciar o aplicativo.

1. Em seguida, adicione o código ao método de teste para clicar no botão. Na linha após `XamlWindow.Launch`, adicione um gesto para tocar no controle de botão:

   ```csharp
   Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);
   ```

   ```vb
   Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)
   ```

   Depois de adicionar o código, o método de teste `CodedUITestMethod1` completo deve ser exibido da seguinte maneira:

   ```csharp
   [TestMethod]
   public void CodedUITestMethod1()
   {
       XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App");

       Gesture.Tap(this.UIMap.UIUWPAppWindow.UIButtonButton);

       // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
       this.UIMap.AssertMethod1();
   }
   ```

   ```vb
   <CodedUITest(CodedUITestType.WindowsStore)>
   Public Class CodedUITest1

       <TestMethod()>
       Public Sub CodedUITestMethod1()

           ' Launch the app.
           XamlWindow.Launch("af5ecd75-f252-45a1-9e7e-c6f1d8f054ff_0q1pp7qrjexbp!App")

           '// Tap the button.
           Gesture.Tap(Me.UIMap.UIUWPAppWindow.UIButtonButton)

           Me.UIMap.AssertMethod1()
       End Sub
   ```

1. Compile o projeto de teste e, em seguida, abra o **Gerenciador de Testes** selecionando **Teste** > **Janelas** > **Gerenciador de Testes**.

1. Selecione **Executar Todos** para executar o teste.

   O aplicativo será aberto, o botão receberá um toque e a propriedade **Text** da caixa de texto será populada. O método de asserção valida a propriedade **Text** da caixa de texto.

   Após a conclusão do teste, o **Gerenciador de Testes** exibe que o teste foi aprovado.

   ![A mensagem "Teste aprovado" é exibida no Gerenciador de Testes](../test/media/test-explorer-coded-ui-test-passed.png)

## <a name="q--a"></a>Perguntas e respostas

### <a name="q-why-dont-i-see-the-option-to-record-my-coded-ui-test-in-the-generate-code-for-a-coded-ui-test-dialog"></a>P: Por que não vejo a opção de registrar meu teste de IU codificado no diálogo Gerar Código para Teste de IU Codificado?

**R**: A opção de registro não é compatível com aplicativos UWP.

### <a name="q-can-i-create-a-coded-ui-test-for-my-uwp-apps-based-on-winjs"></a>P: Posso criar um teste de IU codificado para meus aplicativos da UWP baseados no WinJS?

**R**: Não. Há suporte apenas para aplicativos baseados em XAML.

### <a name="q-why-cant-i-modify-the-code-in-the-uimapdesigner-file"></a>P: Por que não posso modificar o código no arquivo UIMap.Designer?

**R**: Todas as alterações de código feitas no arquivo *UIMapDesigner.cs* são substituídas sempre que você gera o código usando o **Construtor de Teste de IU Codificado**. Se você precisar modificar um método registrado, copie-o para o arquivo *UIMap.cs* e renomeie-o. O arquivo *UIMap.cs* pode ser usado para substituir métodos e propriedades no arquivo *UIMapDesigner.cs*. Remova a referência ao método original no arquivo *CodedUITest.cs* e substitua-a pelo nome do método renomeado.

## <a name="see-also"></a>Consulte também

- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Definir propriedades de automação exclusivas para controles UWP](../test/set-a-unique-automation-property-for-windows-store-controls-for-testing.md)