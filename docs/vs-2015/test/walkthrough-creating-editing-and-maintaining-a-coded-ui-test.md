---
title: 'Passo a passo: criando, editando e mantendo um teste de IU codificado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7c25ba7-5c9c-455b-9242-701cda56f90c
caps.latest.revision: 43
ms.author: gewarren
manager: douge
ms.openlocfilehash: aff0363b1fe554e55cae7b58d79cd8f765e76d68
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49257524"
---
# <a name="walkthrough-creating-editing-and-maintaining-a-coded-ui-test"></a>Instruções passo a passo: criando, editando e mantendo um teste de IU codificado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você criará um aplicativo simples do Windows Presentation Foundation (WPF) para demonstrar como criar, editar e manter um teste de IU codificado. O passo a passo fornece soluções para corrigir os testes que foram interrompidos por vários problemas de timing e refatoração de controle.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para este passo a passo, será necessário:  
  
-   Visual Studio Enterprise  
  
### <a name="create-a-simple-wpf-application"></a>Criar um aplicativo WPF simples  
  
1.  No menu **ARQUIVO**, aponte para **Novo** e selecione **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  No painel **Instalado**, expanda **Visual C#** e selecione **Área de Trabalho do Windows**.  
  
3.  Acima do painel central, verifique se a lista suspensa da estrutura de destino está definida como **.NET Framework 4.5**.  
  
4.  No painel do meio, selecione o modelo **Aplicativo WPF**.  
  
5.  Na caixa de texto **Nome**, digite **SimpleWPFApp**.  
  
6.  Escolha a pasta em que você salvará o projeto. Na caixa de texto **Local**, digite o nome da pasta.  
  
7.  Clique em **OK**.  
  
     O WPF Designer for Visual Studio abre e exibe a MainWindow do projeto.  
  
8.  Se a caixa de ferramentas não estiver aberta, abra-a. Escolha o menu **EXIBIR** e a opção **Caixa de Ferramentas**.  
  
9. Na seção **Todos os Controles do WPF**, arraste um controle **Button**, **CheckBox** e **ProgressBar** para a MainWindow na superfície de design.  
  
10. Selecione o controle Button. Na janela Propriedades, altere o valor da propriedade **Nome** de \<No Name> para button1. Em seguida, altere o valor da propriedade **Conteúdo** de Button para Start.  
  
11. Selecione o controle ProgressBar. Na janela Propriedades, altere o valor da propriedade **Nome** de \<No Name> para progressBar1. Em seguida, altere o valor da propriedade **Máximo** de **100** para **10000**.  
  
12. Selecione o controle Checkbox. Na janela Propriedades, altere o valor da propriedade **Nome** de \<No Name> para checkBox1 e desmarque a propriedade **IsEnabled**.  
  
     ![Aplicativo WPF simples](../test/media/codedui-wpfapp.png "CodedUI_WPFApp")  
  
13. Clique duas vezes no controle de botão para adicionar um manipulador de eventos de clique.  
  
     O MainWindow.xmal.cs é exibido no Editor de Códigos com o cursor no novo método button1_Click.  
  
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
  
### <a name="verify-the-wpf-application-runs-correctly"></a>Verificar se o aplicativo WPF é executado corretamente  
  
1.  No menu **DEPURAR**, selecione **Iniciar Depuração** ou pressione **F5**.  
  
2.  Observe que o controle da caixa de seleção está desabilitado. Escolha **Iniciar**.  
  
     Em alguns segundos, a barra de progresso deve estar 100% concluída.  
  
3.  Agora é possível selecionar o controle da caixa de seleção.  
  
4.  Feche o SimpleWPFApp.  
  
### <a name="create-and-run-a-coded-ui-test-for-simplewpfapp"></a>Criar e executar um teste de IU codificado para SimpleWPFApp  
  
1.  Localize o aplicativo SimpleWPFApp criado anteriormente. Por padrão, o aplicativo fica localizado em C:\Users\\<nome de usuário\>\Documents\Visual Studio \<versão>\Projects\SimpleWPFApp\SimpleWPFApp\bin\Debug\SimpleWPFApp.exe  
  
2.  Crie um atalho na área de trabalho para o aplicativo SimpleWPFApp. Clique com o botão direito do mouse em SimpleWPFApp.exe e escolha **Copiar**. Na área de trabalho, clique com o botão direito do mouse e escolha **Colar atalho**.  
  
    > [!TIP]
    >  Um atalho para o aplicativo facilita adicionar ou modificar testes de IU codificados para seu aplicativo porque permite iniciar rapidamente o aplicativo.  
  
3.  No Gerenciador de Soluções, clique com o botão direito do mouse na solução, clique em **Adicionar** e selecione **Novo Projeto**.  
  
     A caixa de diálogo **Adicionar Novo Projeto** é exibida.  
  
4.  No painel **Instalado**, expanda **Visual C#** e selecione **Testar**.  
  
5.  No painel central, selecione o modelo **Projeto de Teste de Interface de Usuário Codificado**.  
  
6.  Escolha **OK**.  
  
     No Gerenciador de Soluções, o novo projeto de teste de IU codificado chamado **CodedUITestProject1** é adicionado à solução.  
  
     A caixa de diálogo **Gerar Código para Teste de IU Codificado** é exibida.  
  
7.  Selecione a opção **Gravar ações, editar o mapa de IU ou adicionar asserções** e escolha **OK**.  
  
     O UIMap – Construtor de Teste de IU Codificado é exibido e a janela do Visual Studio é minimizada.  
  
     Para obter mais informações sobre as opções da caixa de diálogo, consulte [Criando testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate).  
  
8.  Escolha **Iniciar Gravação** no UIMap – Construtor de Teste de IU Codificado.  
  
     ![Inicie a gravação](../test/media/cuit-builder-record.png "CUIT_Builder_Record")  
  
     Se necessário, será possível pausar a gravação, por exemplo, se você tiver que lidar com um email recebido.  
  
     ![Pausar a gravação](../test/media/cuit.png "CUIT_")  
  
    > [!WARNING]
    >  Todas as ações realizadas na área de trabalho serão registradas. Pause a gravação se estiver realizando ações que possam levar à exclusão de dados confidenciais na gravação.  
  
9. Abra o SimpleWPFApp usando o atalho da área de trabalho.  
  
     Como antes, observe que o controle da caixa de seleção está desabilitado.  
  
10. No SimpleWPFApp, escolha **Iniciar**.  
  
     Em alguns segundos, a barra de progresso deve estar 100% concluída.  
  
11. Marque o controle de caixa de seleção, que agora está habilitado.  
  
12. Feche o aplicativo SimpleWPFApp.  
  
13. No UIMap – Construtor de Teste de IU Codificado, escolha **Gerar Código**.  
  
14. Em Nome do Método, digite **SimpleAppTest** e escolha **Adicionar e Gerar**. Em alguns segundos, o teste de IU codificado aparece e é adicionado à solução.  
  
15. Feche o UIMap – Construtor de Teste de IU Codificado.  
  
     O arquivo CodedUITest1.cs aparece no Editor de Códigos.  
  
16. Salve seu projeto.  
  
### <a name="run-the-coded-ui-test"></a>Executar o teste de IU codificado  
  
1.  No menu **TESTAR**, escolha **Windows** e **Gerenciador de Testes**.  
  
2.  No menu **COMPILAÇÃO**, escolha **Compilar Solução**.  
  
3.  No arquivo CodedUITest1.cs, localize o método **CodedUITestMethod**, clique com o botão direito do mouse e selecione **Executar Testes** ou execute o teste do Gerenciador de Testes.  
  
     Durante a execução do teste de IU codificado, o SimpleWPFApp permanece visível. Ele conduz as etapas realizadas no procedimento anterior. No entanto, quando o teste tenta marcar a caixa de seleção do controle de caixa de seleção, a janela Resultados do Teste mostra que o teste falhou. Isso ocorre porque o teste tenta marcar a caixa de seleção, mas não sabe que o controle de caixa de seleção permanece desabilitado até a barra de progresso ficar 100% concluída. Você pode corrigir esse e outros problemas semelhantes usando os vários métodos `UITestControl.WaitForControlXXX()` que estão disponíveis para testes de IU codificados. O próximo procedimento demonstrará o uso do método `WaitForControlEnabled()` para corrigir o problema que causou a falha desse teste. Para obter mais informações, consulte [Fazendo testes de IU codificado aguardarem eventos específicos durante a reprodução](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md).  
  
### <a name="edit-and-rerun-the-coded-ui-test"></a>Editar e executar novamente o teste de IU codificado  
  
1.  Na janela do Gerenciador de Testes, selecione o teste que falhou e, na seção **StackTrace**, escolha o primeiro link para **UIMap.SimpleAppTest()**.  
  
2.  O arquivo UIMap.Designer.cs é aberto com o ponto do erro realçado no código:  
  
    ```csharp  
  
    // Select 'CheckBox' check box  
    uICheckBoxCheckBox.Checked = this.SimpleAppTestParams.UICheckBoxCheckBoxChecked;  
    ```  
  
3.  Para corrigir esse problema, você pode fazer o teste de IU codificado esperar o controle CheckBox ser habilitado antes de continuar nessa linha usando o método `WaitForControlEnabled()`.  
  
    > [!WARNING]
    >  Não modifique o arquivo UIMap.Designer.cs. Todas as alterações de código que você fez no arquivo UIMapDesigner.cs serão substituídas cada vez que você gerenciar o código usando o UIMap - Construtor de Teste de IU Codificado. Se você tiver de modificar um método gravado, copie-o para o arquivo UIMap.cs e renomeie-o. O arquivo UIMap.cs pode ser usado para substituir métodos e propriedades no arquivo UIMapDesigner.cs. Você deve remover a referência para o método original no arquivo Coded UITest.cs e substituí-la pelo nome do método renomeado.  
  
4.  No Gerenciador de Soluções, localize **UIMap.uitest** em seu projeto de teste de IU codificado.  
  
5.  Abra o menu de atalho de **UIMap.uitest** e escolha **Abrir**.  
  
     O teste de IU codificado é exibido no Editor de Teste de IU Codificado. Agora você pode ver e editar o teste de IU codificado.  
  
6.  No painel **Ação de interface do usuário**, selecione o método de teste (SimpleAppTest) que deseja mover para o arquivo UIMap.cs ou UIMap.vb para facilitar a funcionalidade de código personalizado, que não será substituída quando o código de teste for recompilado.  
  
7.  Escolha o botão **Mover o Código** na barra de ferramentas do Editor de Teste de IU Codificado.  
  
8.  Uma caixa de diálogo do Microsoft Visual Studio é exibida. Ela avisa que o método será movido do arquivo UIMap.uitest para o arquivo UIMap.cs e que você não poderá mais editar o método usando o Editor de Teste de IU Codificado. Escolha **Sim**.  
  
     O método de teste é removido do arquivo UIMap.uitest e não é mais exibido no painel Ações de interface do usuário. Para editar o arquivo de teste movido, abra o arquivo UIMap.cs no Gerenciador de Soluções.  
  
9. Na barra de ferramentas do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], escolha **Salvar**.  
  
     As atualizações do método de teste são salvas no arquivo UIMap.Designer.  
  
    > [!CAUTION]
    >  Depois de mover o método, você não pode mais editá-lo usando o Editor de Teste de IU Codificado. Você deve adicionar seu código personalizado e mantê-lo usando o Editor de Códigos.  
  
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
  
13. No arquivo CodedUITest1.cs, localize o método **CodedUITestMethod** e comente ou renomeie a referência ao método SimpleAppTest() original e substitua-o pelo novo ModifiedSimpleAppTest():  
  
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
  
14. No menu **COMPILAR**, escolha **Compilar Solução**.  
  
15. Clique com o botão direito do mouse no método **CodedUITestMethod** e selecione **Executar Testes**.  
  
16. Dessa vez, o teste de IU codificado conclui com sucesso todas as etapas do teste e **Aprovado** é exibido na janela do Gerenciador de Testes.  
  
### <a name="refactor-a-control-in-the-simplewpfapp"></a>Refatorar um controle no SimpleWPFApp  
  
1.  No arquivo MainWindow.xaml, no Designer, selecione o controle button.  
  
2.  No topo da janela Propriedades, altere o valor da propriedade **Nome** de button1 para buttonA.  
  
3.  No menu **COMPILAR**, escolha **Compilar Solução**.  
  
4.  No Gerenciador de Testes, execute **CodedUITestMethod1**.  
  
     O teste falha porque o teste de IU codificado não consegue localizar o controle button mapeado originalmente no UIMap como button1. A refatoração pode afetar os teste de IU codificados dessa forma.  
  
5.  Na janela do Gerenciador de Testes, na seção **StackTrace**, escolha o primeiro link ao lado de **UIMpa.ModifiedSimpleAppTest()**.  
  
     O arquivo UIMap.cs abre. O ponto de erro é realçado no código:  
  
    ```csharp  
  
    // Click 'Start' button  
    Mouse.Click(uIStartButton, new Point(27, 10));  
    ```  
  
     Observe que a linha de código anterior neste procedimento está usando `UiStartButton`, que é o nome do UIMap antes de ser refatorado.  
  
     Para corrigir o problema, você pode adicionar o controle refatorado ao UIMap usando o Construtor de Teste de IU Codificado. Você pode atualizar o código do teste para usar o código, como demonstrado no próximo procedimento.  
  
### <a name="map-refactored-control-and-edit-and-rerun-the-coded-ui-test"></a>Mapear o controle refatorado e editar e executar novamente o teste de IU codificado  
  
1.  No arquivo CodedUITest1.cs, no método **CodedUITestMethod1()**, clique com o botão direito do mouse, selecione **Gerar Código para Teste de IU Codificado** e escolha **Usar o Construtor de Teste de IU Codificado**.  
  
     O UIMap – Construtor de Teste de IU Codificado será exibido.  
  
2.  Usando o atalho na área de trabalho criado anteriormente, execute o aplicativo SimpleWPFApp criado antes.  
  
3.  No UIMap – Construtor de Teste de IU Codificado, arraste a ferramenta de cruz no botão **Iniciar** no SimpleWPFApp.  
  
     O botão **Iniciar** é incluído em uma caixa azul e o Construtor de Teste de IU Codificado demora alguns segundos para processar os dados do controle selecionado e exibe as propriedades dos controles. Observe que **AutomationUId** é denominado **buttonA**.  
  
4.  Nas propriedades do controle, escolha a seta no canto superior esquerdo para expandir o Mapa de Controles de IU. Observe que **UIStartButton1** está selecionado.  
  
5.  Na barra de ferramentas, escolha **Adicionar controle para o Mapa de Controles de IU**.  
  
     O status na parte inferior da janela verifica a ação exibindo **O controle selecionado foi adicionado ao mapa de controles de IU**.  
  
6.  No UIMap – Construtor de Teste de IU Codificado, escolha **Gerar Código**.  
  
     O Construtor de Teste de IU Codificado - Gerar Código aparece com uma nota indicando que nenhum novo método é necessário e que o código será gerado somente para as alterações no mapa de controles de IU.  
  
7.  Escolha **Gerar**.  
  
8.  Feche o SimpleWPFApp.exe.  
  
9. Feche o UIMap – Construtor de Teste de IU Codificado.  
  
     O UIMap – Construtor de Teste de IU Codificado demora alguns segundos para processar as alterações do mapa de controles de IU.  
  
10. No Gerenciador de Soluções, abra o arquivo UIMap.Designer.cs.  
  
11. No arquivo UIMap.Designer.cs, localize a propriedade UIStartButton1. Observe que `SearchProperties` está definido como `"buttonA"`:  
  
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
  
     Agora você pode modificar o teste de IU codificado para usar o controle recém-mapeado. Conforme indicado no procedimento anterior, se você quiser substituir métodos ou propriedades no teste de IU codificado, faça isso no arquivo UIMap.cs.  
  
12. No arquivo UIMap.cs, adicione um construtor e especifique a propriedade `SearchProperties` da propriedade `UIStartButton` para usar a propriedade `AutomationID` com o valor `"buttonA":`  
  
    ```csharp  
  
    public UIMap()  
            {  
                this.UIMainWindowWindow.UIStartButton.SearchProperties[WpfButton.PropertyNames.AutomationId] = "buttonA";  
            }  
  
    ```  
  
13. No menu **COMPILAR**, escolha **Compilar Solução**.  
  
14. No Gerenciador de Testes, execute CodedUITestMethod1.  
  
     Dessa vez, o teste de IU codificado conclui com sucesso todas as etapas do teste.  Na janela Resultados do Teste, você verá o status de **Aprovado**.  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="videos"></a>Vídeos  
 ![link para o vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Coded UI Tests-DeepDive-Episode1-GettingStarted](http://go.microsoft.com/fwlink/?LinkID=230573)  
  
 ![link para o vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Coded UI Tests-DeepDive-Episode2-MaintainenceAndDebugging](http://go.microsoft.com/fwlink/?LinkID=230574)  
  
 ![link para o vídeo](../data-tools/media/playvideo.gif "PlayVideo") [Coded UI Tests-DeepDive-Episode3-HandCoding](http://go.microsoft.com/fwlink/?LinkID=230575)  
  
### <a name="hands-on-lab"></a>Laboratório prático  
 [Laboratório Virtual do MSDN: Introdução à criação de testes de IU codificados com o Visual Studio 2010](http://go.microsoft.com/fwlink/?LinkID=22508)  
  
### <a name="faq"></a>Perguntas Frequentes  
 [Perguntas frequentes sobre testes de IU codificados – 1](http://go.microsoft.com/fwlink/?LinkID=230576)  
  
 [Perguntas frequentes sobre testes de IU codificados – 2](http://go.microsoft.com/fwlink/?LinkID=230578)  
  
### <a name="forum"></a>Fórum  
 [Teste de Automação de interface do usuário do Visual Studio (inclui CodedUI)](http://go.microsoft.com/fwlink/?LinkID=224497)  
  
## <a name="see-also"></a>Consulte também  
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Introdução ao Designer do WPF](http://msdn.microsoft.com/en-us/18e61d03-b96a-4058-a166-8ec6b3f6116b)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)   
 [Editando testes de IU codificados usando o editor de testes de IU codificados](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)



