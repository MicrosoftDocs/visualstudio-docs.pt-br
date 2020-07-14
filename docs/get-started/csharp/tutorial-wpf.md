---
title: Aplicativo Olá, Mundo com o WPF em C#
description: Crie um aplicativo .NET de Área de Trabalho do Windows simples em C# com o Visual Studio usando a estrutura de interface do usuário do Windows Presentation Foundation (WPF).
ms.custom: seodec18, get-started
ms.date: 08/09/2019
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: tutorial
dev_langs:
- CSharp
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 26beadbe6963a685f10aef1db7bd8779434927d2
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419270"
---
# <a name="tutorial-create-a-simple-application-with-c"></a>Tutorial: criar um aplicativo simples com C\#

Ao concluir este tutorial, você estará familiarizado com vários designers, ferramentas e caixas de diálogo que poderão ser usados no desenvolvimento de aplicativos com o Visual Studio. Você vai criar um aplicativo "Olá, Mundo", projetar a interface do usuário, adicionar código e depurar erros enquanto aprende sobre o trabalho no [IDE](visual-studio-ide.md) (ambiente de desenvolvimento integrado).

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range="vs-2017"
Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?) para instalá-lo gratuitamente.
::: moniker-end
::: moniker range=">=vs-2019"

- Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.
- Você pode usar o .NET Framework ou o .NET Core para este tutorial. O .NET Core é a estrutura mais recente e mais moderna. O .NET Core requer o Visual Studio 2019 versão 16,3 ou posterior.
::: moniker-end

## <a name="configure-the-ide"></a>Configurar o IDE

::: moniker range="vs-2017"

Ao abrir o Visual Studio pela primeira vez, você será solicitado a entrar. Esta etapa é opcional neste tutorial. Em seguida, você poderá ver uma caixa de diálogo que solicita a escolha das configurações de desenvolvimento e o tema de cores. Mantenha os padrões e escolha **Iniciar o Visual Studio**.

![Caixa de diálogo Escolher configurações](../media/exploreide-settings.png)

Depois que o Visual Studio for iniciado, você verá as janelas de ferramentas, os menus e as barras de ferramentas, bem como o espaço da Janela principal. As janelas de ferramentas estão encaixadas nos lados esquerdo e direito da janela do aplicativo, com **Início Rápido**, a barra de menus e a barra de ferramentas padrão na parte superior. No centro da janela do aplicativo está a **Página Inicial**. Ao carregar uma solução ou um projeto, os editores e designers são exibidos no espaço em que a **Página Inicial** está localizada. Ao desenvolver um aplicativo, você passará a maior parte do seu tempo nessa área central.

![IDE do Visual Studio 2017 com configurações gerais aplicadas](../media/exploreide-idewithgeneralsettings.png "Captura de tela do IDE do Visual Studio 2017 com as configurações gerais aplicadas")

::: moniker-end

::: moniker range=">=vs-2019"

Quando você inicia o Visual Studio, a janela de início é aberta primeiro. Selecione **Continuar sem código** para abrir o ambiente de desenvolvimento. Você verá as janelas de ferramentas, os menus e as barras de ferramentas, além do espaço da janela principal. As janelas de ferramentas estão encaixadas nos lados esquerdo e direito da janela do aplicativo, com uma caixa de pesquisa, a barra de menus e a barra de ferramentas padrão na parte superior. Quando você carrega uma solução ou um projeto, os editores e designers são exibidos no espaço central da janela do aplicativo. Ao desenvolver um aplicativo, você passará a maior parte do seu tempo nessa área central.

::: moniker-end

## <a name="create-the-project"></a>Criar o projeto

Ao criar um aplicativo no Visual Studio, você cria primeiro um projeto e uma solução. Para este exemplo, você criará um projeto do WPF (Windows Presentation Foundation).

::: moniker range="vs-2017"

1. Criar um novo projeto. Na barra de menus, selecione **arquivo**  >  **novo**  >  **projeto**.

     ![Na barra de menus, escolha Arquivo, novo, projeto](../media/exploreide-filenewproject.png "Captura de tela da barra de menus onde você escolhe arquivo, novo, projeto")

1. Na caixa de diálogo **Novo Projeto**, selecione a categoria **Instalado** > **Visual C#** > **Área de Trabalho do Windows** e, em seguida, selecione o modelo **Aplicativo WPF (.NET Framework)**. Nomeie o projeto como **HelloWPFApp** e selecione **OK**.

     ![Modelo do aplicativo WPF na caixa de diálogo Novo Projeto do Visual Studio](media/exploreide-newprojectcsharp.png "Captura de tela do modelo de aplicativo do WPF na caixa de diálogo novo projeto")

::: moniker-end

::: moniker range="vs-2019"

1. Abra o Visual Studio 2019.

1. Na tela Iniciar, selecione **Criar projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../../get-started/media/vs-2019/start-window-create-new-project.png "Captura de tela da janela ' criar um novo projeto '")

1. Na tela **criar um novo projeto** , pesquise "WPF", escolha **aplicativo WPF (.NET Core)** e, em seguida, escolha **Avançar**.

   ![Modelo do aplicativo WPF na caixa de diálogo 'Criar projeto'](media/vs-2019/exploreide-newprojectcsharp-vs2019.png "Captura de tela do modelo de aplicativo do WPF na caixa de diálogo ' criar um novo projeto '")

   > [!NOTE]
   > Você pode encontrar dois modelos de área de trabalho do WPF, um para .NET Framework e outro para o .NET Core. O modelo .NET Core está disponível no Visual Studio 2019 versão 16,3 e posterior. Você pode usar qualquer um para este tutorial, mas recomendamos o .NET Core para o novo desenvolvimento.

1. Na próxima tela, dê o nome **HelloWPFApp** ao projeto e escolha **Criar**.

   ![Nomeie seu projeto ' HelloWPFApp '](./media/vs-2019/exploreide-nameproject.png "Captura de tela da janela na qual você nomeou seu projeto")

::: moniker-end

O Visual Studio cria o projeto e a solução HelloWPFApp e o **Gerenciador de Soluções** mostra os diversos arquivos. O **Designer do WPF** mostra um modo de exibição de Design e um modo de exibição XAML de *MainWindow.xaml* em um modo divisão. É possível deslizar o divisor para mostrar mais ou menos de cada exibição. É possível optar por ver apenas a exibição visual ou apenas a exibição XAML.

![Projeto e solução do WPF no IDE](media/exploreide-wpfproject-cs.png "Captura de tela do projeto e da solução do WPF no IDE")

> [!NOTE]
> Para saber mais informações sobre XAML (eXtensible Application Markup Language), confira a página [Visão geral do XAML para WPF](/dotnet/framework/wpf/advanced/xaml-overview-wpf).

Depois de criar o projeto, você poderá personalizá-lo. Para tanto, escolha **Janela de Propriedades** do menu **Exibir**, ou pressione **F4**. Em seguida, você pode exibir e alterar opções de itens de projeto, controles e outros itens em um aplicativo.

   ![Janela de Propriedades](../media/exploreide-hellowpfappfiles.png "Captura de tela da janela Propriedades com nomes de aplicativo de arquivo do WPF")   

### <a name="change-the-name-of-mainwindowxaml"></a>Alterar o nome de MainWindow.xaml

Vamos dar um nome mais específico para MainWindow. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *MainWindow. XAML* e escolha **renomear**. Renomeie o arquivo para *Greetings. XAML*.

## <a name="design-the-user-interface-ui"></a>Criar a interface do usuário

Se o designer não estiver aberto, selecione *Greetings. XAML* e pressione **Shift** + **F7** para abrir o designer.

Adicionaremos três tipos de controles a este aplicativo: um controle <xref:System.Windows.Controls.TextBlock>, dois controles <xref:System.Windows.Controls.RadioButton> e um controle <xref:System.Windows.Controls.Button>.

### <a name="add-a-textblock-control"></a>Adicionar um controle TextBlock

1. Pressione **Ctrl** + **Q** para ativar a caixa de pesquisa e digite **Toolbox**. Escolha **Exibir > Caixa de ferramentas** na lista de resultados.

1. No **Caixa de Ferramentas**, expanda o nó **Controles Comuns do WPF** para ver o controle TextBlock.

     ![Caixa de ferramentas com o controle TextBlock realçado](../media/exploreide-textblocktoolbox.png "Captura de tela da janela caixa de ferramentas com o controle TextBlock realçado")

1. Adicione um controle TextBlock à superfície de design escolhendo o item **TextBlock** e arrastando-o para a janela na superfície de design. Centralize o controle próximo à parte superior da janela. No Visual Studio 2019 e posterior, você pode usar as diretrizes vermelhas para centralizar o controle.

    Sua janela deve se parecer com a ilustração a seguir:

    ![Controle TextBlock no formulário Saudações](../media/exploreide-greetingswithtextblockonly.png "Captura de tela do controle TextBlock no formulário Greetings")

   A marcação XAML deve ter uma aparência semelhante ao exemplo a seguir:

    ```xaml
    <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="387,60,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
    </Grid>
    ```

### <a name="customize-the-text-in-the-text-block"></a>Personalizar o texto no bloco de texto

1. Na exibição XAML, localize a marcação **TextBlock** e altere o atributo **Text** de `TextBox` para `Select a message option and then choose the Display button.`

   A marcação XAML deve ter uma aparência semelhante ao exemplo a seguir:

   ```xaml
   <Grid>
       <TextBlock HorizontalAlignment="Left" Margin="387,60,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
   </Grid>
   ```

1. Se necessário, centralize novamente o TextBlock e salve as alterações pressionando **Ctrl+S** ou usando o item de menu **Arquivo**.

Em seguida, você adicionará dois controles [RadioButton](/dotnet/framework/wpf/controls/radiobutton) ao formulário.

### <a name="add-radio-buttons"></a>Adicionar botões de opção

1. Na **Caixa de Ferramentas**, localize o controle **RadioButton**.

     ![Janela de ferramentas com o controle RadioButton selecionado](../media/exploreide-radiobuttontoolbox.png "Captura de tela da janela caixa de ferramentas com o controle RadioButton selecionado")

1. Adicione dois controles RadioButton à superfície de design escolhendo o item **RadioButton** e arrastando-o para a janela na superfície de design. Mova os botões (selecionando-os e usando as teclas de direção) para que os botões sejam exibidos lado a lado sob o controle TextBlock. Use as diretrizes vermelhas para alinhar os controles.

   A sua janela deve se parecer com esta:

   ![Formulário de saudações com TextBlock e dois botões de opção](../media/exploreide-greetingswithradiobuttons.png "Captura de tela do formulário de saudações com TextBlock e dois botões de opção")

1. Na janela **Propriedades** do controle RadioButton esquerdo, altere a propriedade **Nome** (a propriedade na parte superior da janela **Propriedades**) para `HelloButton`.

    ![Janela Propriedades RadioButton](../media/exploreide-buttonproperties.png "Captura de tela da janela Propriedades do botão de opção")

1. Na janela **Propriedades** do controle RadioButton direito, altere a propriedade **Name** para `GoodbyeButton` e, em seguida, salve as alterações.

Em seguida, adicione o texto de exibição para cada controle RadioButton. O procedimento a seguir atualiza a propriedade **Conteúdo** de um controle RadioButton.

### <a name="add-display-text-for-each-radio-button"></a>Adicionar o texto de exibição de cada botão de opção

1. Atualize o atributo de **conteúdo** para o `HelloButton` e `GoodbyeButton` para `"Hello"` e `"Goodbye"` no XAML. A marcação XAML deve agora ser semelhante ao exemplo a seguir:

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

### <a name="set-a-radio-button-to-be-checked-by-default"></a>Definir que um botão de opção faça check-in por padrão

Nesta etapa, definiremos que o HelloButton permaneça marcado por padrão, de maneira que um dos dois botões de opção esteja sempre selecionado.

1. Na exibição XAML, localize a marcação HelloButton.

1. Adicione um atributo **IsChecked** e configure-o como **True**. Especificamente, adicione `IsChecked="True"`.

   A marcação XAML deve agora ser semelhante ao exemplo a seguir:

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" IsChecked="True" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
   </Grid>
   ```

O elemento da interface do usuário final que você adicionará é um controle de [botão](/dotnet/framework/wpf/controls/button) .

### <a name="add-the-button-control"></a>Adicionar o controle de botão

1. Na **Caixa de Ferramentas**, localize o controle de **Botão** e, em seguida, adicione-o à superfície de design sob os controles RadioButton, arrastando-o para o formulário no modo de exibição de Design. Se você estiver usando o Visual Studio 2019 ou posterior, uma linha vermelha o ajudará a centralizar o controle.

1. Na exibição XAML, altere o valor de **Conteúdo** do controle de Botão, de `Content="Button"` para `Content="Display"` e salve as alterações.

     Sua janela deve se parecer com a ilustração a seguir.

     ![Formulário Saudações com rótulos de controle](media/exploreide-greetingswithcontrollabels-cs.png "Captura de tela do formulário de saudações com rótulos de controle")

   A marcação XAML deve agora ser semelhante ao exemplo a seguir:

   ```xaml
   <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="252,47,0,0" TextWrapping="Wrap" Text="Select a message option and then choose the Display button." VerticalAlignment="Top"/>
        <RadioButton x:Name="HelloButton" Content="Hello" IsChecked="True" HorizontalAlignment="Left" Margin="297,161,0,0" VerticalAlignment="Top"/>
        <RadioButton x:Name="GoodbyeButton" Content="Goodbye" HorizontalAlignment="Left" Margin="488,161,0,0" VerticalAlignment="Top"/>
        <Button Content="Display" HorizontalAlignment="Left" Margin="377,270,0,0" VerticalAlignment="Top" Width="75"/>
   </Grid>
   ```

### <a name="add-code-to-the-display-button"></a>Adicionar um código ao botão de exibição

Quando esse aplicativo é executado, uma caixa de mensagem é exibida depois que um usuário escolhe um botão de opção e, em seguida, escolhe o botão **Exibir**. Uma caixa de mensagem será exibida para Olá e outra para Até logo. Para criar esse comportamento, adicione um código ao evento `Button_Click` em *Greetings.xaml.cs*.

1. Na superfície de design, clique duas vezes no botão **Exibição**.

     *Greetings.xaml.cs* é aberto, com o cursor no evento `Button_Click`.

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {

    }
    ```

1. Insira o seguinte código:

    ```csharp
    if (HelloButton.IsChecked == true)
    {
         MessageBox.Show("Hello.");
    }
    else if (GoodbyeButton.IsChecked == true)
    {
        MessageBox.Show("Goodbye.");
    }
    ```

1. Salve o aplicativo.

## <a name="debug-and-test-the-application"></a>Depurar e testar o aplicativo

Em seguida, você depurará o aplicativo para procurar erros e testar se ambas as caixas de mensagem são exibidas corretamente. As instruções a seguir descrevem como criar e iniciar o depurador, mas, posteriormente, leia [Compilar um aplicativo WPF (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf) e [Depurar o WPF](../../debugger/debugging-wpf.md) para obter mais informações.

### <a name="find-and-fix-errors"></a>Localizar e corrigir erros

Nesta etapa, você encontrará o erro que causamos anteriormente alterando o nome do arquivo *MainWindow. XAML* .

#### <a name="start-debugging-and-find-the-error"></a>Iniciar a depuração e localizar o erro

1. Inicie o depurador pressionando **F5** ou selecionando **Depurar** e depois **Iniciar Depuração**.

   Uma janela de **Modo de Interrupção** é exibida e a janela **Saída** indica que houve uma IOException: não é possível localizar o recurso 'mainwindow.xaml'.

   ![Mensagem IOException](../media/exploreide-ioexception.png "Captura de tela da mensagem de IOException")

1. Pare o depurador escolhendo **depurar**  >  **parar depuração**.

Renomeamos o *MainWindow.xaml* como *Greetings.xaml* no início deste tutorial, mas o código ainda se refere a *MainWindow.xaml* como o URI de inicialização do aplicativo. Portanto, o projeto não pode ser iniciado.

#### <a name="specify-greetingsxaml-as-the-startup-uri"></a>Especificar Greetings.xaml como o URI de inicialização

1. No **Gerenciador de Soluções**, abra o arquivo *App.xaml*.

1. Altere `StartupUri="MainWindow.xaml"` para `StartupUri="Greetings.xaml"` e salve as alterações.

Inicie o depurador novamente (pressione **F5**). Você deverá ver a janela **Saudações** do aplicativo.

::: moniker range="vs-2017"
![Captura de tela do aplicativo em execução](media/exploreide-wpf-running-app.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Captura de tela do aplicativo em execução](media/vs-2019/exploreide-wpf-running-app.png)
::: moniker-end

Agora, feche a janela do aplicativo para parar a depuração.

### <a name="debug-with-breakpoints"></a>Depurar com pontos de interrupção

Você pode testar o código durante a depuração ao adicionar alguns pontos de interrupção. Você pode adicionar pontos de interrupção escolhendo **depurar**  >  **alternar ponto de interrupção**, clicando na margem esquerda do editor ao lado da linha de código onde você deseja que a interrupção ocorra ou pressionando **F9**.

#### <a name="add-breakpoints"></a>Adicionar pontos de interrupção

1. Abra *Greetings.XAML.cs*e selecione a seguinte linha:`MessageBox.Show("Hello.")`

1. Adicione um ponto de interrupção por meio do menu selecionando **Depurar** e, em seguida, **Ativar/Desativar Ponto de Interrupção**.

     Um círculo vermelho aparece ao lado da linha de código na margem da extrema esquerda da janela do editor.

1. Selecione a linha a seguir: `MessageBox.Show("Goodbye.")`.

1. Pressione a tecla **F9** para adicionar um ponto de interrupção e, em seguida, pressione **F5** para iniciar a depuração.

1. Na janela **Saudações**, escolha o botão de opção **Olá** e depois o botão **Exibição**.

    A linha `MessageBox.Show("Hello.")` é realçada em amarelo. Na parte inferior do IDE, as janelas Automáticos, Locais e Inspeção estão encaixadas juntas no lado esquerdo e as janelas Pilha de Chamadas, Pontos de Interrupção, Configurações de Exceção, Comando, Imediato e Saída estão encaixadas no lado direito.

    ![Ponto de interrupção no depurador](media/exploreide-debugbreakpoint.png "Captura de tela de ponto de interrupção no depurador")

1. Na barra de menus, escolha **depurar depuração**  >  **Step Out**.

     O aplicativo retomará a execução e uma caixa de mensagem com a palavra "Olá" será exibida.

1. Escolha o botão **OK** na caixa de mensagem para fechá-la.

1. Na janela **Saudações**, escolha o botão de opção **Até logo** e depois o botão **Exibição**.

     A linha `MessageBox.Show("Goodbye.")` é realçada em amarelo.

1. Escolha a tecla **F5** para continuar a depuração. Quando a caixa de mensagem for exibida, escolha o botão **OK** na caixa de mensagem para fechá-la.

1. Feche a janela do aplicativo para parar a depuração.

1. Na barra de menus, escolha **depurar**  >  **desabilitar todos os pontos de interrupção**.

### <a name="view-a-representation-of-the-ui-elements"></a>Exibir uma representação dos elementos da interface do usuário

No aplicativo em execução, você verá um widget que aparece na parte superior da janela. Esse é um auxiliar de tempo de execução que fornece acesso rápido a alguns recursos úteis de depuração. Clique no primeiro botão, **vá para árvore visual dinâmica**. Você deve ver uma janela com uma árvore que contém todos os elementos visuais da sua página. Expanda os nós para localizar os botões que você adicionou.

![Captura de tela da janela de árvore visual ao vivo](media/vs-2019/exploreide-live-visual-tree.png)

### <a name="build-a-release-version-of-the-application"></a>Criar uma versão de lançamento do aplicativo

Agora que você verificou que tudo está funcionando, já pode preparar um build de versão do aplicativo.

1. No menu principal, selecione **criar**  >  **solução limpa** para excluir arquivos intermediários e arquivos de saída que foram criados durante as compilações anteriores. Isso não é necessário, mas limpa as saídas de build da depuração.

1. Altere a configuração de Build de HelloWPFApp de **debug** para **Release** usando o controle DropDown na barra de ferramentas (ele diz "debug" no momento).

1. Crie a solução escolhendo **criar**  >  **solução de compilação**.

Parabéns por concluir este tutorial. Você pode encontrar o *. exe* criado sob sua solução e o diretório do projeto (*. ..\HelloWPFApp\HelloWPFApp\bin\Release*).

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este tutorial. Para saber ainda mais, acompanhe os tutoriais a seguir.

> [!div class="nextstepaction"]
> [Continuar com mais tutoriais do WPF](/dotnet/framework/wpf/getting-started/wpf-walkthroughs/)

## <a name="see-also"></a>Veja também

- [Dicas de produtividade](../../ide/productivity-features.md)
