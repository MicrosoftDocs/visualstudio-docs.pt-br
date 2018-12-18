---
title: Criar um teste de IU codificado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: fe8bed9c1f1f8aee9ae8e6d1ba460bf226d7b818
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895516"
---
# <a name="walkthrough-create-edit-and-maintain-a-coded-ui-test"></a>Passo a passo: Criar, editar e manter um teste de IU codificado

Neste passo a passo, você saberá como criar, editar e manter um teste de IU codificado para testar um aplicativo WPF (Windows Presentation Framework). O passo a passo fornece soluções para corrigir os testes que foram interrompidos por vários problemas de tempo e refatoração de controles.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="create-a-wpf-app"></a>Criar um aplicativo WPF

1.  No menu **Arquivo**, aponte para **Novo** e selecione **Projeto**.

     A caixa de diálogo **Novo Projeto** é exibida.

2.  No painel **Instalado**, expanda **Visual C#** e selecione **Área de Trabalho do Windows**.

3.  Acima do painel central, verifique se a lista suspensa da estrutura de destino está definida como **.NET Framework 4.5**.

4.  No painel do meio, selecione o modelo **Aplicativo WPF**.

5.  Na caixa de texto **Nome**, digite **SimpleWPFApp**.

6.  Escolha a pasta em que você salvará o projeto. Na caixa de texto **Local**, digite o nome da pasta.

7.  Escolha **OK**.

     O **WPF Designer for Visual Studio** é aberto e exibe a MainWindow do projeto.

8.  Se a caixa de ferramentas não estiver aberta, abra-a. Escolha o menu **Exibir** e a opção **Caixa de Ferramentas**.

9. Na seção **Todos os Controles do WPF**, arraste um controle **Button**, **CheckBox** e **ProgressBar** para a MainWindow na superfície de design.

10. Selecione o controle de **Botão**. Na janela **Propriedades**, altere o valor da propriedade **Nome** de \<No Name> para button1. Em seguida, altere o valor da propriedade **Conteúdo** de Button para Start.

11. Selecione o controle **ProgressBar**. Na janela **Propriedades**, altere o valor da propriedade **Nome** de \<No Name> para progressBar1. Em seguida, altere o valor da propriedade **Máximo** de **100** para **10000**.

12. Selecione o controle **Caixa de Seleção**. Na janela **Propriedades**, altere o valor da propriedade **Nome** de \<No Name> para checkBox1 e desmarque a propriedade **IsEnabled**.

     ![Aplicativo WPF simples](../test/media/codedui_wpfapp.png)

13. Clique duas vezes no controle de botão para adicionar um manipulador de eventos de clique.

     O *MainWindow.xmal.cs* é exibido no Editor de Códigos com o cursor no novo método button1_Click.

14. Na parte superior da classe MainWindow, adicione um delegado. O delegado será usado para a barra de progresso. Para adicionar o delegado, adicione o seguinte código:

    ```csharp
    public partial class MainWindow : Window
    {
            private delegate void ProgressBarDelegate(System.Windows.DependencyProperty dp, Object value);

        public MainWindow()
        {

            InitializeComponent();
        }
    ```

15. No método button1_Click, adicione o seguinte código:

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        double progress = 0;

        ProgressBarDelegate updatePbDelegate =
            new ProgressBarDelegate(progressBar1.SetValue);

        do
        {
            progress ++;

            Dispatcher.Invoke(updatePbDelegate,
                System.Windows.Threading.DispatcherPriority.Background,
                new object[] { ProgressBar.ValueProperty, progress });
            progressBar1.Value = progress;
        }
        while (progressBar1.Value != progressBar1.Maximum);

        checkBox1.IsEnabled = true;
    }
    ```

16. Salve o arquivo.

### <a name="run-the-wpf-app"></a>Executar o aplicativo WPF

1.  No menu **Depurar**, selecione **Iniciar Depuração** ou pressione **F5**.

2.  Observe que o controle da caixa de seleção está desabilitado. Escolha **Iniciar**.

     Em alguns segundos, a barra de progresso deve estar 100% concluída.

3.  Agora é possível selecionar o controle da caixa de seleção.

4.  Feche o SimpleWPFApp.

## <a name="create-a-shortcut-to-the-wpf-app"></a>Criar um atalho para o aplicativo WPF

1.  Localize o aplicativo SimpleWPFApp criado anteriormente.

2.  Crie um atalho na área de trabalho para o aplicativo SimpleWPFApp. Clique com o botão direito do mouse em *SimpleWPFApp.exe* e escolha **Copiar**. Na área de trabalho, clique com o botão direito do mouse e escolha **Colar atalho**.

    > [!TIP]
    > Um atalho para o aplicativo facilita adicionar ou modificar testes de IU codificados para seu aplicativo, porque permite iniciá-lo rapidamente.

## <a name="create-a-coded-ui-test-for-simplewpfapp"></a>Criar um teste de IU codificado para SimpleWPFApp

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução, escolha **Adicionar** e, em seguida, selecione **Novo Projeto**.

     A caixa de diálogo **Adicionar Novo Projeto** é exibida.

1. No painel **Instalado**, expanda **Visual C#** e selecione **Testar**.

1. No painel central, selecione o modelo **Projeto de Teste de Interface de Usuário Codificado**.

   > [!NOTE]
   > Se o modelo **Projeto de Teste de IU Codificado** não for exibido, será necessário [instalar o componente Teste de IU Codificado](../test/use-ui-automation-to-test-your-code.md#install-the-coded-ui-test-component).

1. Escolha **OK**.

     O novo projeto de teste de IU codificado chamado **CodedUITestProject1** é adicionado à solução.

     A caixa de diálogo **Gerar Código para Teste de IU Codificado** é exibida.

1. Selecione a opção **Gravar ações, editar o mapa de IU ou adicionar asserções** e escolha **OK**.

     A caixa de diálogo **UIMap – Construtor de Teste de IU Codificado** é exibida, e a janela do Visual Studio é minimizada.

     Para obter mais informações sobre as opções da caixa de diálogo, confira [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md).

1. Escolha **Iniciar Gravação** na caixa de diálogo **UIMap – Construtor de Teste de IU Codificado**.

     ![Iniciar gravação](../test/media/cuit_builder_record.png)

     Se necessário, será possível pausar a gravação, por exemplo, se você tiver que lidar com um email recebido.

     ![Pausar a gravação](../test/media/cuit_.png)

    > [!WARNING]
    > Todas as ações realizadas na área de trabalho serão registradas. Pause a gravação se estiver realizando ações que possam levar à exclusão de dados confidenciais na gravação.

1. Abra o SimpleWPFApp usando o atalho da área de trabalho.

     Como antes, observe que o controle da caixa de seleção está desabilitado.

1. No SimpleWPFApp, escolha **Iniciar**.

     Em alguns segundos, a barra de progresso deve estar 100% concluída.

1. Marque o controle de caixa de seleção, que agora está habilitado.

1. Feche o aplicativo SimpleWPFApp.

1. Na caixa de diálogo **UIMap – Construtor de teste de IU codificado**, escolha **Gerar Código**.

1. Na caixa **Nome do método**, digite **SimpleAppTest** e escolha **Adicionar e gerar**. Em alguns segundos, o teste de IU codificado é exibido e adicionado à solução.

1. Feche o **UIMap – Construtor de teste de IU codificado**.

     O arquivo *CodedUITest1.cs* é exibido no editor de código.

1. Salve seu projeto.

### <a name="run-the-test"></a>Executar o teste

1. No menu **Testar**, escolha **Windows** e **Gerenciador de Testes**.

2. No menu **Compilação**, escolha **Compilar Solução**.

3. No arquivo *CodedUITest1.cs*, localize o método **CodedUITestMethod**, clique com o botão direito do mouse e selecione **Executar testes** ou execute o teste no **Gerenciador de Testes**.

   Durante a execução do teste de IU codificado, o SimpleWPFApp permanece visível. Ele conduz as etapas realizadas no procedimento anterior. No entanto, quando o teste tenta marcar a caixa de seleção do controle de caixa de seleção, a janela **Resultados do Teste** mostra que o teste falhou. Isso ocorre porque o teste tenta marcar a caixa de seleção, mas não sabe que o controle de caixa de seleção permanece desabilitado até a barra de progresso ficar 100% concluída. Você pode corrigir esse e outros problemas semelhantes usando os vários métodos `UITestControl.WaitForControlXXX()` que estão disponíveis para testes de IU codificados. O próximo procedimento demonstrará o uso do método `WaitForControlEnabled()` para corrigir o problema que causou a falha desse teste. Para obter mais informações, confira [Fazer os testes de IU codificados aguardarem eventos específicos durante a reprodução](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md).

## <a name="edit-and-rerun-the-coded-ui-test"></a>Editar e executar novamente o teste de IU codificado

1.  Na janela **Gerenciador de Testes**, selecione o teste com falha e, na seção **StackTrace**, escolha o primeiro link para **UIMap.SimpleAppTest()**.

2.  O arquivo *UIMap.Designer.cs* é aberto com o ponto de erro realçado no código:

    ```csharp
    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

3.  Para corrigir esse problema, você pode fazer o teste de IU codificado esperar o controle CheckBox ser habilitado antes de continuar nessa linha usando o método `WaitForControlEnabled()`.

    > [!WARNING]
    > Não modifique o arquivo *UIMap.Designer.cs*. Quaisquer alterações que você fizer no código serão substituídas sempre que você gerar código usando o **UIMap – Construtor de Teste de IU Codificado**. Se precisar modificar um método registrado, copie-o para o arquivo *UIMap.cs* e renomeie-o. O arquivo *UIMap.cs* pode ser usado para substituir métodos e propriedades no arquivo *UIMapDesigner.cs*. É necessário remover a referência ao método original no arquivo *CodedUITest.cs* e substituí-la pelo nome do método renomeado.

4.  No **Gerenciador de Soluções**, localize *UIMap.uitest* em seu projeto de teste de IU codificado.

5.  Abra o menu de atalho de *UIMap.uitest* e escolha **Abrir**.

     O teste de IU codificado é exibido no Editor de Teste de IU Codificado. Agora você pode ver e editar o teste de IU codificado.

6.  No painel **Ação de interface do usuário**, selecione o método de teste (SimpleAppTest) que você deseja mover para o arquivo *UIMap.cs* ou *UIMap.vb*. Mover o método para um arquivo diferente permitirá que um código personalizado seja adicionado que não será substituído quando o código de teste for recompilado.

7.  Escolha o botão **Mover Código** na barra de ferramentas **Editor de Teste de IU Codificado**.

8.  Uma caixa de diálogo do Microsoft Visual Studio é exibida. Ela avisa que o método será movido do arquivo *UIMap.uitest* para o arquivo *UIMap.cs* e que não será mais possível editar o método usando o Editor de Teste de IU Codificado. Escolha **Sim**.

     O método de teste é removido do arquivo *UIMap.uitest* e não será mais exibido no painel Ações de Interface do Usuário. Para editar o arquivo de teste movido, abra o arquivo *UIMap.cs* no **Gerenciador de Soluções**.

9. Na barra de ferramentas do Visual Studio, escolha **Salvar**.

     As atualizações do método de teste são salvas no arquivo *UIMap.Designer*.

    > [!WARNING]
    > Depois de mover o método, você não pode mais editá-lo usando o Editor de Teste de IU Codificado. Você deve adicionar seu código personalizado e mantê-lo usando o Editor de Códigos.

10. Renomear o método de `SimpleAppTest()` para `ModifiedSimpleAppTest()`

11. Adicione o seguinte usando a instrução para o arquivo:

    ```csharp
    using Microsoft.VisualStudio.TestTools.UITesting.WpfControls;
    ```

12. Adicione o seguinte método `WaitForControlEnabled()` antes da linha de código problemática identificada anteriormente:

    ```csharp
    uICheckBoxCheckBox.WaitForControlEnabled();

    // Select 'CheckBox' check box
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;
    ```

13. No arquivo *CodedUITest1.cs*, localize o método **CodedUITestMethod** e comente ou renomeie a referência ao método SimpleAppTest() original e, em seguida, substitua-a pelo novo ModifiedSimpleAppTest():

    ```csharp
    [TestMethod]
            public void CodedUITestMethod1()
            {
                // To generate code for this test, select "Generate Code for Coded UI Test" from the shortcut menu and select one of the menu items.
                // For more information on generated code, see http://go.microsoft.com/fwlink/?LinkId=179463
                //this.UIMap.SimpleAppTest();
                this.UIMap.ModifiedSimpleAppTest();
            }
    ```

14. No menu **Compilar**, escolha **Compilar Solução**.

15. Clique com o botão direito do mouse no método **CodedUITestMethod** e selecione **Executar Testes**.

16. Dessa vez, o teste de IU codificado conclui com êxito todas as etapas no teste, e **Aprovado** é exibido na janela **Gerenciador de Testes**.

## <a name="refactor-a-control-in-simplewpfapp"></a>Refatorar um controle em SimpleWPFApp

1.  No arquivo *MainWindow.xaml*, no designer, selecione o controle de botão.

2.  Na parte superior da janela **Propriedades**, altere o valor da propriedade **Nome** de **button1** para **buttonA**.

3.  No menu **Compilar**, escolha **Compilar Solução**.

4.  No **Gerenciador de Testes**, execute **CodedUITestMethod1**.

     O teste falha porque o teste de IU codificado não consegue localizar o controle button mapeado originalmente no UIMap como button1. A refatoração pode afetar os teste de IU codificados dessa forma.

5.  No **Gerenciador de Testes**, na seção **StackTrace**, escolha o primeiro link ao lado de **UIMpa.ModifiedSimpleAppTest()**.

     O arquivo *UIMap.cs* é aberto. O ponto de erro é realçado no código:

    ```csharp
    // Click 'Start' button
    Mouse.Click(uIStartButton, new Point(27, 10));
    ```

     Observe que a linha de código anterior neste procedimento está usando `UiStartButton`, que é o nome do UIMap antes de ser refatorado.

     Para corrigir o problema, é possível adicionar o controle refatorado ao UIMap usando o **Construtor de Teste de IU Codificado**. Você pode atualizar o código do teste para usar o código, como demonstrado no próximo procedimento.

## <a name="map-refactored-control-rerun-the-test"></a>Mapear controle refatorado executar o teste novamente

1.  No arquivo *CodedUITest1.cs*, no método **CodedUITestMethod1()**, clique com o botão direito do mouse, selecione **Gerar Código para Teste de IU Codificado** e, em seguida, escolha **Usar Construtor de Teste de IU Codificado**.

     O **UIMap – Construtor de Teste de IU Codificado** é exibido.

2.  Usando o atalho na área de trabalho criado anteriormente, execute o aplicativo SimpleWPFApp criado antes.

3.  Na caixa de diálogo **UIMap – Construtor de Teste de IU Codificado**, arraste a ferramenta de fios para o botão **Iniciar** em SimpleWPFApp.

     O botão **Iniciar** está contido em uma caixa azul. O **Construtor de Teste de IU Codificado** demora alguns segundos para processar os dados do controle selecionado e para exibir as propriedades do controle. Observe que o valor de **AutomationUId** é **buttonA**.

4.  Nas propriedades do controle, escolha a seta no canto superior esquerdo para expandir o Mapa de Controles de IU. Observe que **UIStartButton1** está selecionado.

5.  Na barra de ferramentas, escolha **Adicionar controle para o Mapa de Controles de IU**.

     O status na parte inferior da janela verifica a ação exibindo **O controle selecionado foi adicionado ao mapa de controles de IU**.

6.  Na caixa de diálogo **UIMap – Construtor de teste de IU codificado**, escolha **Gerar Código**.

     A caixa de diálogo **Construtor de Teste de IU Codificado – Gerar código** aparece com uma nota indicando que nenhum novo método é necessário e que o código será gerado somente para as alterações no mapa de controles de interface do usuário.

7.  Escolha **Gerar**.

8.  Feche o SimpleWPFApp.

9. Feche o **UIMap – Construtor de teste de IU codificado**.

10. No **Gerenciador de Soluções**, abra o arquivo *UIMap.Designer.cs*.

11. No arquivo *UIMap.Designer.cs*, localize a propriedade **UIStartButton1**. Observe que `SearchProperties` está definido como `"buttonA"`:

    ```csharp
    public WpfButton UIStartButton1
            {
                get
                {
                    if ((this.mUIStartButton1 == null))
                    {
                        this.mUIStartButton1 = new WpfButton(this);
                        #region Search Criteria
                        this.mUIStartButton1.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
                        this.mUIStartButton1.WindowTitles.Add("MainWindow");
                        #endregion
                    }
                    return this.mUIStartButton1;
                }
            }
    ```

     Agora você pode modificar o teste de IU codificado para usar o controle recém-mapeado. Conforme indicado no procedimento anterior, caso deseje substituir métodos ou propriedades no teste de IU codificado, faça isso no arquivo *UIMap.cs*.

12. No arquivo *UIMap.cs*, adicione um construtor e especifique a propriedade `SearchProperties` da propriedade `UIStartButton` para usar a propriedade `AutomationID` com um valor de `"buttonA":`

    ```csharp
    public UIMap()
            {
                this.UIMainWindowWindow.UIStartButton.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";
            }
    ```

13. No menu **Compilar**, escolha **Compilar Solução**.

14. No **Gerenciador de Testes**, execute **CodedUITestMethod1**.

     Dessa vez, o teste de IU codificado conclui com sucesso todas as etapas do teste. Na janela **Resultados do Teste**, você verá um status **Aprovado**.

## <a name="videos"></a>Vídeos

![link para vídeo](../data-tools/media/playvideo.gif) [Introdução aos testes de IU codificados](http://go.microsoft.com/fwlink/?LinkID=230573)

![link para vídeo](../data-tools/media/playvideo.gif) [Manutenção e depuração de testes de IU codificados](http://go.microsoft.com/fwlink/?LinkID=230574)

![link para vídeo](../data-tools/media/playvideo.gif) [Codificação manual de testes de IU codificados](http://go.microsoft.com/fwlink/?LinkID=230575)

## <a name="faq"></a>Perguntas Frequentes

[Perguntas frequentes sobre testes de IU codificados](https://social.msdn.microsoft.com/Forums/vsautotest/3a74dd2c-cef8-4923-abbf-7a91f489e6c4/faqs)

## <a name="see-also"></a>Consulte também

- [Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)
- [Configurações e plataformas compatíveis para testes de IU codificados e gravações de ação](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [Editar testes de IU codificados usando o editor de teste de IU codificado](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)
