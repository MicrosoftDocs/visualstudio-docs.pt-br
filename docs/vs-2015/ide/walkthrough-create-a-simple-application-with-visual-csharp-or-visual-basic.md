---
title: 'Passo a passo: Criar um aplicativo simples com o Visual C# ou o Visual Basic | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 51fc073046833165097a8a9a4fb2f169ed3a04e7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49851680"
---
# <a name="walkthrough-create-a-simple-application-with-visual-c-or-visual-basic"></a>Instruções passo a passo: criar um aplicativo simples com o Visual C# ou o Visual Basic
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao concluir este passo a passo, você estará familiarizado com vários designers, ferramentas e caixas de diálogo que poderão ser usados no desenvolvimento de aplicativos com o Visual Studio. Você vai criar um aplicativo simples no estilo "Olá, Mundo", criar uma interface de usuário, adicionar código e depurar erros enquanto aprende mais sobre como trabalhar no IDE (ambiente de desenvolvimento integrado).  
  
 Esse tópico contém as seguintes seções:  
  
 [Configurar o IDE](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_ConfigureIDE)  
  
 [Criar um aplicativo simples](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_CreateApp)  
  
 [Depurar e testar o aplicativo](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md#BKMK_DebugTest)  
  
> [!NOTE]
>  Este passo a passo se baseia no Visual Studio Professional, que oferece o modelo de aplicativo WPF no qual você criará o projeto. O Visual Studio Express para Windows Desktop também oferece esse modelo, mas o Visual Studio Express para Windows e Visual Studio Express for Web, não. Para obter informações introdutórias sobre como usar o Visual Studio Express para Windows, consulte o [Centro de Desenvolvedores de Aplicativos da Windows Store](http://msdn.microsoft.com/windows/apps/br229519). Para obter informações introdutórias sobre como usar o Visual Studio Express para a Web, consulte [Introdução ao ASP.NET](http://www.asp.net/get-started). Além disso, sua edição do Visual Studio e as configurações que você usa determinam os nomes e os locais de alguns elementos da interface do usuário. Consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
##  <a name="BKMK_ConfigureIDE"></a> Configurar o IDE  
 Ao iniciar o Visual Studio pela primeira vez, o Visual Studio solicita que você se conecte com uma MSA (Conta de Serviço da Microsoft), [Entrar no Visual Studio](http://blogs.msdn.com/b/visualstudio/archive/2013/06/28/welcome-sign-in-to-visual-studio.aspx). Você não precisa entrar e pode fazer isso mais tarde.  
  
 Ao iniciar o Visual Studio, é necessário escolher uma combinação de configurações que aplica um conjunto de personalizações predefinidas à IDE. Cada combinação de configurações foi desenvolvida para facilitar o desenvolvimento de aplicativos.  
  
 Este passo a passo pressupõe que você aplicou as **Configurações Gerais de Desenvolvimento**, que aplica a menor quantidade de personalização à IDE. Se você já tiver escolhido o C# ou o Visual Basic (ambas são boas opções), não é necessário alterar as configurações.  Se desejar alterar as configurações, será possível usar o **Assistente de Importação e Exportação de Configurações**. Consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Depois de abrir o Visual Studio, você poderá identificar as janelas de ferramenta, os menus e as barras de ferramentas, bem como o espaço da janela principal. As janelas de ferramentas estão encaixadas nos lados esquerdo e direito da janela do aplicativo, com **Início Rápido**, a barra de menus e a barra de ferramentas padrão na parte superior. No centro da janela do aplicativo está a **Página Inicial**. Ao carregar uma solução ou um projeto, os editores e designers são exibidos no espaço em que a **Página Inicial** está localizada. Ao desenvolver um aplicativo, você passará a maior parte do seu tempo nessa área central.  
  
 Figura 2: IDE do Visual Studio  
  
 ![IDE com configurações gerais aplicadas](../ide/media/exploreide-idewithgeneralsettings.png "ExploreIDE-IDEwithgeneralsettings")  
  
 É possível fazer personalizações adicionais no Visual Studio, como alterar a face da fonte e o tamanho do texto no editor ou o tema da cor do IDE, usando a caixa de diálogo **Opções**. Dependendo da combinação de configurações que você tiver aplicado, alguns itens na caixa de diálogo poderão não aparecer automaticamente. É possível garantir que todas as opções possíveis são exibidas escolhendo a caixa de seleção **Mostrar todas as configurações**.  
  
 Figura 3: Caixa de diálogo Opções  
  
 ![Caixa de diálogo Opções com Mostrar todas as opções de configuração](../ide/media/exploreide-optionsdialogbox.png "ExploreIDE-Optionsdialogbox")  
  
 Nesse exemplo, você vai alterar o tema da cor do IDE, de claro para escuro.  É possível ignorar para criar um projeto, se desejado.  
  
#### <a name="to-change-the-color-theme-of-the-ide"></a>Para alterar o tema da cor do IDE  
  
1. Abra o **opções** caixa de diálogo, escolhendo o **ferramentas** menu na parte superior e, em seguida, o **opções...** item.  
  
    ![Comando Opções no menu Ferramentas](../ide/media/exploreide-toolsoptionsmenu.png "ExploreIDE-ToolsOptionsmenu")  
  
2. Altere o **Tema da cor** para **Escuro** e clique em **OK**.  
  
    ![Tema de cor escura selecionado](../ide/media/exploreide-darkthemeoptionsdlgbox.png "ExploreIDE-Darkthemeoptionsdlgbox")  
  
   As cores no Visual Studio devem corresponder à seguinte imagem:  
  
   ![IDE com tema escuro aplicado](../ide/media/exploreide-darkthemeide.png "ExploreIDE-DarkThemeIDE")  
  
   O tema da cor usado para as imagens no restante deste passo a passo é o tema claro. Para obter mais informações sobre como personalizar o IDE, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
##  <a name="BKMK_CreateApp"></a> Criar um aplicativo simples  
  
### <a name="create-the-project"></a>Criar o projeto  
 Ao criar um aplicativo no Visual Studio, você cria primeiro um projeto e uma solução. Para este exemplo, você criará um projeto do WPF (Windows Presentation Foundation).  
  
##### <a name="to-create-the-wpf-project"></a>Para criar o projeto WPF  
  
1. Crie um novo projeto. Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto…**.  
  
    ![Na barra de menus, escolha Arquivo, Novo, Projeto](../ide/media/exploreide-filenewproject.png "ExploreIDE-FileNewProject")  
  
    Você também pode digitar **Novo Projeto** na caixa **Início Rápido** para obter o mesmo resultado.  
  
    ![Na caixa Início Rápido, especificar novo projeto](../ide/media/exploreide-quicklaunchnewprojectsmall.png "ExploreIDE-QuickLaunchNewProjectsmall")  
  
2. Escolha o modelo de Aplicativo WPF do Visual Basic ou do Visual C# escolhendo no painel esquerdo **Instalados**, **Modelos**, **Visual C#**, **Windows**, por exemplo e, em seguida, escolhendo Aplicativo WPF no painel central.  Nomeie o projeto HelloWPFApp na parte inferior da caixa de diálogo Novo Projeto.  
  
    ![Criar um projeto do WPF do Visual Basic, HelloWPFApp](../ide/media/exploreide-newprojectvb.png "ExploreIDE-NewProjectVB")  
  
    OU  
  
    ![Criar um projeto do WPF do Visual C&#35;, HelloWPFApp](../ide/media/exploreide-newprojectcsharp.png "ExploreIDE-NewProjectcsharp")  
  
   O Visual Studio cria o projeto HelloWPFApp e a solução, e o **Gerenciador de Soluções** mostra os vários arquivos. O Designer do WPF mostra um modo de exibição de Design e um modo de exibição XAML de MainWindow.xaml em um modo divisão. É possível deslizar o divisor para mostrar mais ou menos de cada exibição.  É possível optar por ver apenas a exibição visual ou apenas a exibição XAML. (Para obter mais informações, consulte [Designer do WPF para desenvolvedores do Windows Forms](http://msdn.microsoft.com/en-us/47ad0909-e89b-4996-b4ac-874d929f94ca)). Os seguintes itens aparecem no **Gerenciador de Soluções**:  
  
   Figura 5: Itens do projeto  
  
   ![Gerenciador de Soluções com os arquivos do HelloWPFApp carregados](../ide/media/exploreide-hellowpfappfiles.png "ExploreIDE-HelloWPFAppFiles")  
  
   Depois de criar o projeto, você poderá personalizá-lo. Ao usar a janela **Propriedades** (encontrada no menu **Exibir**), é possível exibir e alterar opções para itens de projeto, controles e outros itens em um aplicativo. Usando as propriedades e as páginas de propriedades do projeto, você pode exibir e alterar opções para projetos e soluções.  
  
##### <a name="to-change-the-name-of-mainwindowxaml"></a>Para alterar o nome de MainWindow.xaml  
  
1. No procedimento a seguir, você dará a MainWindow um nome mais específico. No **Gerenciador de Soluções**, selecione MainWindow.xaml. Você deverá ver a janela **Propriedades**, mas se ela não for exibida, escolha o menu **Exibir** e o item **Janela Propriedade**. Altere a propriedade **Nome de Arquivo** para `Greetings.xaml`.  
  
    ![Janela Propriedades com nome de arquivo realçado](../ide/media/exploreide-filenameinpropertieswindow.png "ExploreIDE-FilenameinPropertiesWindow")  
  
    O **Gerenciador de Soluções** mostra que o nome do arquivo agora é Greetings.xaml e, se você expandir o nó MainWindow.xaml (colocando o foco no nó e pressionando a tecla de seta para a direita), verá que o nome MainWindow.xaml.vb ou MainWindow.xaml.cs agora é Greetings.xaml.vb ou Greetings.xaml.cs. Esse arquivo de código é aninhado sob o nó do arquivo .xaml para mostrar que eles estão intimamente relacionados.  
  
   > [!WARNING]
   >  Essa alteração causa um erro que você aprenderá a depurar e corrigir em uma etapa posterior.  
  
2. No **Gerenciador de Soluções**, abra Greetings.xaml no modo de exibição de Designer (pressionando a tecla Enter enquanto o nó tem o foco) e selecione a barra de título da janela usando o mouse.  
  
3. Na janela **Propriedades**, altere o valor da propriedade **Título** para `Greetings`.  
  
   A barra de título de MainWindow.xaml agora exibe Saudações.  
  
### <a name="design-the-user-interface-ui"></a>Criar a interface do usuário  
 Adicionaremos três tipos de controle a este aplicativo: um controle TextBlock, dois controles RadioButton e um controle Button.  
  
##### <a name="to-add-a-textblock-control"></a>Para adicionar um controle TextBlock  
  
1. Abra a janela **Caixa de ferramentas** escolhendo o menu **Exibir** e o item **Caixa de ferramentas**.  
  
2. Na **Caixa de Ferramentas**, pesquise controle TextBlock.  
  
    ![Caixa de ferramentas com o controle TextBlock realçado](../ide/media/exploreide-textblocktoolbox.png "ExploreIDE-TextBlockToolbox")  
  
3. Adicione um controle TextBlock à superfície de design escolhendo o item TextBlock e arrastando-o para a janela na superfície de design.  Centralize o controle próximo à parte superior da janela.  
  
   Sua janela deve se parecer com a ilustração a seguir:  
  
   Figura 7: Janela Saudações com controle TextBlock  
  
   ![Controle TextBlock no formulário Greetings](../ide/media/exploreide-greetingswithtextblockonly.png "ExploreIDE-GreetingswithTextblockonly")  
  
   A marcação XAML deve ter uma aparência semelhante a esta:  
  
```  
<TextBlock HorizontalAlignment="Center" TextWrapping="Wrap" VerticalAlignment="Center" RenderTransformOrigin="4.08,2.312" Margin="237,57,221,238"><Run Text="TextBlock"/><InlineUIContainer><TextBlock TextWrapping="Wrap" Text="TextBlock"/>  
```  
  
##### <a name="to-customize-the-text-in-the-text-block"></a>Para personalizar o texto no bloco de texto  
  
1. No modo de exibição XAML, localize a marcação de TextBlock e altere o atributo Text: `Text=”Select a message option and then choose the Display button.”`  
  
2. Se o TextBlock não expandir para se ajustar ao modo de exibição de Design, amplie o controle TextBlock (usando as alças de captura nas bordas) de modo que ele exiba todo o texto.  
  
3. Salve as alterações pressionando Ctrl-s ou usando o item de menu **Arquivo**.  
  
   Em seguida, você adicionará dois controles [RadioButton](http://msdn.microsoft.com/library/6c9ba847-eab7-4bba-9c74-6b56ef72067b) ao formulário.  
  
##### <a name="to-add-radio-buttons"></a>Para adicionar botões de opção  
  
1. Na **Caixa de Ferramentas**, pesquise controle RadioButton.  
  
    ![Janela de ferramentas com o controle RadioButton selecionado](../ide/media/exploreide-radiobuttontoolbox.png "ExploreIDE-RadioButtonToolbox")  
  
2. Adicione dois controles RadioButton à superfície de design escolhendo o item RadioButton e arrastando-o para a janela na superfície de design duas vezes e mova os botões (selecionando-os e usando as teclas de direção), para que eles sejam exibidos lado a lado sob o controle TextBlock.  
  
    A sua janela deve se parecer com esta:  
  
    Figura 8: RadioButtons na janela Saudações.  
  
    ![Formulário Greetings com bloco de texto e dois botões de opção](../ide/media/exploreide-greetingswithradiobuttons.png "ExploreIDE-Greetingswithradiobuttons")  
  
3. Na janela **Propriedades** do controle RadioButton esquerdo, altere a propriedade **Nome** (a propriedade na parte superior da janela **Propriedades**) para `RadioButton1`.  Verifique se você selecionou o RadioButton e não o Grid da tela de fundo no formulário; o campo Type da Janela de Propriedade sob o campo Name deve indicar RadioButton.  
  
4. Na janela **Propriedades** do controle RadioButton direito, altere a propriedade **Nome** para `RadioButton2` e salve as alterações pressionando Ctrl-s ou usando o item de menu **Arquivo**.  Verifique se você selecionou o RadioButton antes de alterar e salvar.  
  
   Agora você pode adicionar o texto de exibição para cada controle RadioButton. O procedimento a seguir atualiza a propriedade **Conteúdo** de um controle RadioButton.  
  
##### <a name="to-add-display-text-for-each-radio-button"></a>Para adicionar o texto de exibição para cada botão de opção  
  
1. Na superfície de design, abra o menu de atalho de RadioButton1 pressionando o botão direito do mouse enquanto seleciona RadioButton1, escolha **Editar Texto** e insira `Hello`.  
  
2. Abra o menu de atalho de RadioButton2 pressionando o botão direito do mouse enquanto seleciona RadioButton2, escolha **Editar Texto** e, em seguida, insira `Goodbye`.  
  
   O elemento final da interface do usuário que você adicionará é um controle de [Botão](http://msdn.microsoft.com/library/a9d8f5a5-c98c-463e-808a-5a4e63173098).  
  
##### <a name="to-add-the-button-control"></a>Para adicionar o controle de botão  
  
1. Em **Caixa de ferramentas**, pesquise o controle de **Botão** e, em seguida, adicione-o à superfície de design sob os controles RadioButton selecionando Button e arrastando-o para o formulário no modo de exibição de Design.  
  
2. No modo de exibição XAML, altere o valor de **Conteúdo** do controle de Botão, de `Content=”Button”` para `Content=”Display”` e salve as alterações (Ctrl-s ou use o menu **Arquivo**).  
  
    A marcação deve se parecer com o exemplo a seguir: `<Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>`  
  
   Sua janela deve se parecer com a ilustração a seguir.  
  
   Figura 9: Interface do usuário final de Saudações  
  
   ![Formulário Greetings com rótulos de controle](../ide/media/exploreide-greetingswithconrollabels.png "ExploreIDE-Greetingswithconrollabels")  
  
### <a name="add-code-to-the-display-button"></a>Adicionar código ao botão Exibir  
 Quando esse aplicativo é executado, uma caixa de mensagem é exibida depois que um usuário escolhe pela primeira vez um botão de opção e depois escolhe o botão **Exibição**. Uma caixa de mensagem será exibida para Olá e outra para Até logo. Para criar esse comportamento, você adicionará código ao evento Button_Click em Greetings.xaml.vb ou em Greetings.xaml.cs.  
  
##### <a name="add-code-to-display-message-boxes"></a>Adicionar código a caixas de mensagem de exibição  
  
1.  Na superfície de design, clique duas vezes no botão **Exibição**.  
  
     Greetings.xaml.vb ou Greetings.xaml.cs é aberto, com o cursor no evento Button_Click. Também é possível adicionar um manipulador de eventos de clique da seguinte maneira (se o código colado tiver um rabisco vermelho sob os nomes, isso significa que você provavelmente não selecionou os controles RadioButton na superfície de design nem os renomeou):  
  
     No Visual Basic, o manipulador de eventos deve se parecer com este:  
  
    ```vb  
    Private Sub Button_Click_1(sender As Object, e As RoutedEventArgs)  
  
    End Sub  
    ```  
  
     No Visual C#, o manipulador de eventos deve se parecer com este:  
  
    ```csharp  
    private void Button_Click_1(object sender, RoutedEventArgs e)  
    {  
  
    }  
    ```  
  
2.  No Visual Basic, insira o código a seguir:  
  
    ```vb  
    If RadioButton1.IsChecked = True Then  
        MessageBox.Show("Hello.")  
    Else RadioButton2.IsChecked = True  
        MessageBox.Show("Goodbye.")  
    End If  
  
    ```  
  
     No Visual C#, insira o código a seguir:  
  
    ```  
    if (RadioButton1.IsChecked == true)  
    {  
        MessageBox.Show("Hello.");  
    }  
    else  
    {  
        RadioButton2.IsChecked = true;  
        MessageBox.Show("Goodbye.");  
    }  
    ```  
  
3.  Salve o aplicativo.  
  
##  <a name="BKMK_DebugTest"></a> Depurar e testar o aplicativo  
 Em seguida, você depurará o aplicativo para procurar erros e testar se ambas as caixas de mensagem são exibidas corretamente. As instruções a seguir descrevem como compilar e iniciar o depurador, mas, posteriormente, é possível ler [Compilando um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c) e [Depurando o WPF](../debugger/debugging-wpf.md) para obter mais informações.  
  
### <a name="find-and-fix-errors"></a>Localizar e corrigir erros  
 Nesta etapa, você encontrará o erro que nós causamos anteriormente alterando o nome do arquivo XAML da janela principal.  
  
##### <a name="to-start-debugging-and-find-the-error"></a>Para iniciar a depuração e localizar o erro  
  
1. Inicie o depurador selecionando **Depurar** e **Iniciar Depuração**.  
  
    ![Comando Iniciar Depuração no menu Depurar](../ide/media/exploreide-startdebugging.png "ExploreIDE-StartDebugging")  
  
    Uma caixa de diálogo aparece, indicando que um IOException ocorreu: Não é possível localizar o recurso 'mainwindow.xaml'.  
  
2. Escolha o botão **OK** e pare o depurador.  
  
    ![Comando Parar Depuração no menu Depurar](../ide/media/exploreide-stopdebugging.png "ExploreIDE-StopDebugging")  
  
   Renomeamos Mainwindow.xaml como Greetings.xaml no início deste passo a passo, mas o código ainda se refere ao Mainwindow.xaml como o URI de inicialização do aplicativo. Portanto, o projeto não pode ser iniciado.  
  
##### <a name="to-specify-greetingsxaml-as-the-startup-uri"></a>Para especificar Greetings.xaml como o URI de inicialização  
  
1. No **Gerenciador de Soluções**, abra o arquivo App.xaml (no projeto do C#) ou o arquivo Application.xaml (no projeto do Visual Basic) no modo de exibição XAML (não pode ser aberto no modo de exibição de Design) selecionando o arquivo e pressionando Enter ou clicando nele duas vezes.  
  
2. Altere `StartupUri="MainWindow.xaml"` para `StartupUri="Greetings.xaml"` e salve as alterações com Ctrl-s.  
  
   Inicie o depurador novamente (pressione F5). Você deve ver a janela Saudações do aplicativo.  
  
### <a name="to-debug-with-breakpoints"></a>Para depurar com pontos de interrupção  
 Ao adicionar alguns pontos de interrupção, você pode testar o código durante a depuração. É possível adicionar pontos de interrupção escolhendo **Depurar** no menu principal, **Ativar/Desativar Ponto de Interrupção** ou clicando na margem esquerda do editor ao lado da linha de código em que você deseja que a quebra ocorra.  
  
##### <a name="to-add-breakpoints"></a>Para adicionar pontos de interrupção  
  
1.  Abra Greetings.xaml.vb ou Greetings.xaml.cs e selecione a linha a seguir: `MessageBox.Show("Hello.")`  
  
2.  Adicione um ponto de interrupção por meio do menu selecionando **Depurar** e, em seguida, **Ativar/Desativar Ponto de Interrupção**.  
  
     ![Comando Ativar/Desativar Pontos de Interrupção no menu Depurar](../ide/media/exploreide-togglebreakpoint.png "ExploreIDE-ToggleBreakpoint")  
  
     Um círculo vermelho aparece ao lado da linha de código na margem da extrema esquerda da janela do editor.  
  
3.  Selecione a linha a seguir: `MessageBox.Show("Goodbye.")`.  
  
4.  Pressione a tecla F9 para adicionar um ponto de interrupção e depois pressione a tecla F5 para iniciar a depuração.  
  
5.  Na janela **Saudações**, escolha o botão de opção **Olá** e depois o botão **Exibição**.  
  
     A linha `MessageBox.Show("Hello.")` é realçada em amarelo. Na parte inferior do IDE, as janelas Automáticos, Locais e Inspeção estão encaixadas juntas no lado esquerdo e as janelas Pilha de Chamadas, Pontos de Interrupção, Comando, Imediato e Saída estão encaixadas no lado direito.  
  
6.  Na barra de menus, escolha **Depurar**, **Depuração Circular**.  
  
     O aplicativo retomará a execução e uma caixa de mensagem com a palavra "Olá" será exibida.  
  
7.  Escolha o botão **OK** na caixa de mensagem para fechá-la.  
  
8.  Na janela **Saudações**, escolha o botão de opção **Até logo** e depois o botão **Exibição**.  
  
     A linha `MessageBox.Show("Goodbye.")` é realçada em amarelo.  
  
9. Escolha a tecla F5 para continuar a depuração. Quando a caixa de mensagem for exibida, escolha o botão **OK** na caixa de mensagem para fechá-la.  
  
10. Pressione as teclas SHIFT + F5 (pressione a tecla SHIFT primeiro e, enquanto a mantém pressionada, pressione F5) para interromper a depuração.  
  
11. Na barra de menus, escolha **Depurar**, **Desabilitar Todos os Pontos de Interrupção**.  
  
### <a name="build-a-release-version-of-the-application"></a>Criar uma versão de lançamento do aplicativo  
 Agora que você verificou que tudo está funcionando, já pode preparar uma versão de lançamento do aplicativo.  
  
##### <a name="to-clean-the-solution-files-and-build-a-release-version"></a>Para limpar os arquivos de solução e criar uma versão de lançamento  
  
1. No menu principal, selecione **Build** e, em seguida, **Limpar solução** para excluir arquivos intermediários e arquivos de saída criados durante builds anteriores.  Isso não é necessário, mas limpa as saídas de build de depuração.  
  
    ![O comando Limpar Solução no menu Compilar](../ide/media/exploreide-cleansolution.png "ExploreIDE-CleanSolution")  
  
2. Altere a configuração de build de HelloWPFApp, de **Depuração** para **Versão**, usando o controle suspenso na barra de ferramentas (no momento, seu nome é “Depuração”).  
  
    ![A barra de ferramentas Padrão com Versão selecionada](../ide/media/exploreide-releaseversion.png "ExploreIDE-ReleaseVersion")  
  
3. Compile a solução escolhendo **Build** e, em seguida, **Compilar Solução** ou pressione a tecla F6.  
  
    ![Comando Compilar Solução no menu Compilar](../ide/media/exploreide-buildsolution.png "ExploreIDE-BuildSolution")  
  
   Parabéns por concluir este passo a passo! É possível encontrar o .exe compilado na solução e no diretório do projeto (…\HelloWPFApp\HelloWPFApp\bin\Release\\). Se desejar explorar mais exemplos, consulte [Amostras do Visual Studio](../ide/visual-studio-samples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Novidades no Visual Studio 2015](../what-s-new-in-visual-studio-2015.md)   
 [Introdução ao desenvolvimento com o Visual Studio](../ide/get-started-developing-with-visual-studio.md)   
 [Dicas de produtividade](../ide/productivity-tips-for-visual-studio.md)



