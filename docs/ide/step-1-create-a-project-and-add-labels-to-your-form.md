---
title: 'Etapa 1: Criar um projeto e adicionar rótulos ao formulário'
description: Saiba como criar o projeto, adicionar rótulos, um botão e outros controles a um formulário e definir propriedades para cada controle que você adicionar.
ms.custom: SEO-VS-2020
ms.date: 10/15/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.assetid: f44e50be-a5f5-4d77-9cff-dd52374c3f74
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 75019a9f292a07c1dffe6cce5118ef6502014ce6
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296593"
---
# <a name="step-1-create-a-project-and-add-labels-to-your-form"></a>Etapa 1: Criar um projeto e adicionar rótulos ao formulário

Nas primeiras etapas do desenvolvimento deste teste, você o cria o projeto, e adiciona rótulos, um botão, e outros controles a um formulário. Você também define as propriedades para cada controle adicionado. O projeto conterá o formulário, controles e (posteriormente neste tutorial) o código. O botão inicia o teste, os rótulos mostram os problemas do teste e outros controles mostram as respostas dos teste e o tempo permanece para concluir o teste.

> [!NOTE]
> Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md).

## <a name="to-create-a-project-for-a-form"></a>Para criar um projeto para um formulário

::: moniker range="vs-2017"

1. Na barra de menus, escolha **arquivo** > **novo** > **projeto**.

1. Escolha **Visual C#** ou **Visual Basic** no lado esquerdo da caixa de diálogo **Novo Projeto** e, em seguida, escolha **Windows Desktop**.

1. Na lista de modelos, escolha o modelo de **Aplicativo do Windows Forms (.NET Framework)**, dê o nome *MathQuiz* a ele e, então, clique no botão **OK**.

    Um formulário chamado *Form1.cs* ou *Form1.vb* aparece, dependendo da linguagem de programação que você escolheu.

   > [!NOTE]
   > Se o modelo **Aplicativo do Windows Forms (.NET Framework)** não for exibido, use o Instalador do Visual Studio para instalar a carga de trabalho **Desenvolvimento para área de trabalho do .NET**.<br/><br/>![Carga de trabalho de desenvolvimento para carga de trabalho do .NET no Instalador do Visual Studio](../ide/media/dot-net-desktop-dev-workload.png)<br/><br/> Para obter mais informações, confira a página [Instalar o Visual Studio](../install/install-visual-studio.md).

::: moniker-end

::: moniker range="vs-2019"

1. Na janela iniciar, escolha **criar um novo projeto**.

   ![Exibir a janela 'Criar um novo projeto'](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **Criar um novo projeto**, insira ou digite *Windows Forms* na caixa de pesquisa. Em seguida, escolha **área de trabalho** na lista tipo de **projeto** .

   Depois de aplicar o filtro de **tipo de projeto** , escolha o modelo **aplicativo de Windows Forms (.NET Framework)** para C# ou Visual Basic e, em seguida, escolha **Avançar**.

   ![Escolha o modelo C# ou Visual Basic para o aplicativo Windows Forms (.NET Framework)](./media/create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > Se você não encontrar o modelo do **Aplicativo do Windows Forms (.NET Framework)**, poderá instalá-lo a partir da janela **Criar um novo projeto**. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.
   >
   > ![O link 'Instalar mais ferramentas e recursos' da mensagem 'Não encontrou o que precisa?' na janela 'Criar novo projeto'](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > Em seguida, no Instalador do Visual Studio, escolha Escolher a carga de trabalho de **desenvolvimento de área de trabalho do .NET**.
   >
   > ![Carga de trabalho do .NET Core no Instalador do Visual Studio](../ide/media/install-dot-net-desktop-env.png)
   >
   > Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Pode ser solicitado que você salve seu trabalho; nesse caso, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho.

1. Na janela **Configurar seu novo projeto**, digite ou insira *MathQuiz* na caixa **Nome do projeto**. Em seguida, escolha **criar**.

::: moniker-end

## <a name="to-set-properties-for-a-form"></a>Para definir propriedades para um formulário

1. No Visual Studio, escolha o formulário (*Form1.cs* ou *Form1.vb*, dependendo da linguagem de programação), e altere sua propriedade **Texto** para **Math Quiz**.

     A janela **Propriedades** contém propriedades para o formulário.

1. Altere o tamanho do formulário para 500 pixels de largura por 400 pixels de altura.

     É possível redimensionar o formulário arrastando as bordas até que o tamanho correto apareça no canto inferior esquerdo do ambiente de desenvolvimento integrado (IDE). Como alternativa, você pode alterar os valores da propriedade **Size**.

1. Altere o valor da propriedade **FormBorderStyle** para **Fixed3D** e defina a propriedade **MaximizeBox** para **False**.

     Esses valores impedem que os participantes de teste redimensionem o formulário.

## <a name="to-create-the-time-remaining-box"></a>Para criar a caixa tempo restante

1. Adicione um controle <xref:System.Windows.Forms.Label> da **caixa de ferramentas** e, em seguida, defina o valor de sua propriedade **(Name)** para **timeLabel**.

     Este rótulo se tornará uma caixa no canto superior direito que mostra o número de segundos que permanece em teste.

2. Altere a propriedade **AutoSize** para **False** de modo que você possa redimensionar a caixa.

3. Altere a propriedade **BorderStyle** para **FixedSingle** para desenhar uma linha em torno da caixa.

4. Defina a propriedade **Size** como **200, 30**.

5. Mova o rótulo para o canto superior direito do formulário, onde as linhas espaçadoras azuis serão exibidas.

     Essas linhas ajudam você a alinhar controles no formulário.

6. Na janela **Propriedades**, escolha a propriedade **Text** e pressione a tecla **Backspace** para apagar o seu valor.

7. Escolha o sinal de adição ( **+** ) ao lado da propriedade **fonte** e, em seguida, altere o valor da propriedade **tamanho** para **15,75**.

     Você pode alterar várias propriedades de fonte, como mostra a captura de tela a seguir.

     ![Tamanho da fonte de exibição na janela Propriedades](../ide/media/express_setfontsize.png)

8. Adicione outro controle Label da **caixa de ferramentas** e, em seguida, defina seu tamanho da fonte para **15,75**.

9. Defina a propriedade **Text** como **Time Left**.

10. Mova o rótulo de modo que ele alinhe apenas à esquerda do rótulo **timeLabel**.

### <a name="to-add-controls-for-the-addition-problems"></a>Para adicionar controles para os problemas de adição

1. Adicione um controle Label da **caixa de ferramentas** e, em seguida, defina sua propriedade **Text** para **?** (ponto de interrogação).

2. Defina a propriedade **AutoSize** para **False**.

3. Defina a propriedade **Size** como **60, 50**.

4. Defina o tamanho da fonte como **18**.

5. Defina a propriedade **TextAlign** como **MiddleCenter**.

6. Defina a propriedade **Location** para **50, 75** para posicionar o controle no formulário.

7. Defina a propriedade **(Name)** como **plusLeftLabel**.

8. Escolha o rótulo **plusLeftLabel** e, em seguida, pressione as teclas **Ctrl**+**C** ou **Copiar** no menu **Editar**.

9. Cole o rótulo três vezes escolhendo as teclas **Ctrl** + **V** ou **colar** no menu **Editar** .

10. Organize os três novos rótulos de modo que fiquem em uma linha à direita do rótulo **plusLeftLabel**.

     É possível as linhas separadoras para separá-las e alinhá-las.

11. Defina o valor da segunda propriedade **Text** do rótulo para **+** (sinal de mais).

12. Defina o valor da propriedade **(Name)** do terceiro rótulo como **plusRightLabel**.

13. Defina o valor da propriedade **Text** do rótulo para **=** (sinal de igual).

14. Adicione um controle <xref:System.Windows.Forms.NumericUpDown> da **caixa de ferramentas**, defina seu tamanho da fonte para **18** e sua largura para **100**.

     Você aprenderá mais sobre esse tipo de controle posteriormente.

15. Alinhe o controle NumericUpDown com os controles Label para o problema de adição.

16. Altere o valor da propriedade **(Name)** do controle NumericUpDown para **sum**.

     Você criou a primeira linha, conforme mostrado na ilustração a seguir.

     ![A primeira linha do teste de matemática](../ide/media/express_firstrow.png)

## <a name="to-add-controls-for-the-subtraction-multiplication-and-division-problems"></a>Para adicionar controles para subtração, multiplicação e problemas de divisão

1. Copiar todos os cinco controles para o problema de adição (os quatro controles de rótulo e o controle NumericUpDown) e, em seguida, cola-os.

     O formulário contém cinco novos controles, que ainda são selecionados.

2. Mova todos os controles no local de modo que eles se alinhem abaixo dos controles de adição.

     É possível usar as linhas separadoras para fornecer distância suficiente entre as duas linhas.

3. Altere o valor da propriedade **Text** do segundo rótulo para **-** (sinal de subtração).

4. Nomeie o primeiro rótulo de interrogação **minusLeftLabel**.

5. Nomeie o segundo rótulo de interrogação **minusRightLabel**.

6. Nomeie o controle NumericUpDown como **difference**.

7. Cole os cinco controles mais duas vezes.

8. Para a terceira linha, nomeie o primeiro rótulo como **timesLeftLabel**, altere a propriedade **Text** para **x** (sinal de multiplicação), nomeie o terceiro rótulo como **timesRightLabel** e nomeie o controle NumericUpDown como **product**.

9. Para a quarta linha, nomeie o primeiro rótulo como **dividedLeftLabel**, altere a propriedade **Text** para **÷** (sinal de divisão), nomeie o terceiro rótulo como **dividedRightLabel** e nomeie o controle NumericUpDown como **quotient**.

    > [!NOTE]
    > É possível copiar os sinais de multiplicação × e de divisão ÷ deste tutorial e colá-los no formulário.

## <a name="to-add-a-start-button-and-set-the-tab-index-order"></a>Para adicionar um botão Iniciar e definir a ordem do índice de guias

1. Adicione um controle de <xref:System.Windows.Forms.Button> da **caixa de ferramentas** e, em seguida, defina sua propriedade **(Name)** para **startButton**.

2. Defina a propriedade **Text** como **Iniciar o teste**.

3. Defina o tamanho da fonte como **14**.

4. Defina a propriedade **AutoSize** como **True**, o que faz com que o botão seja redimensionado automaticamente para se ajustar ao texto.

5. Centralize o botão próximo à parte inferior do formulário.

6. Defina o valor da propriedade **TabIndex** para o controle **startButton** como **1**.

    > [!NOTE]
    > A propriedade **TabIndex** define a ordem dos controles quando a pessoa realizando o teste escolhe a tecla **Tab**. Para ver como funciona, abra qualquer caixa de diálogo (por exemplo, na barra de menus, escolha **arquivo**  >  **abrir**) e, em seguida, escolha a tecla **Tab** algumas vezes. Inspecione como o cursor move o controle para controlar cada vez que você escolhe a tecla **Tab**. Um programador decidiu a ordem ao criar o formulário.

7. Defina o valor da propriedade de **TabIndex** para o controle de soma NumericUpDown como **2**, o controle da diferença como **3**, o controle do produto como **4** e o controle do quociente como **5**.

     O formulário deve ser semelhante à captura de tela a seguir.

     ![Formulário inicial do teste de matemática](../ide/media/express_formlaidout.png)

8. Para verificar se a propriedade **TabIndex** funciona como você espera, salve e execute seu programa escolhendo a tecla **F5** ou a barra de menus **Depurar** > **Iniciar Depuração** na barra de menus. Em seguida, escolha a tecla **Tab** algumas vezes.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 2: criar um problema de adição aleatória](../ide/step-2-create-a-random-addition-problem.md)**.

- Para retornar ao tópico de visão geral, veja [Tutorial 2: Criar um teste de matemática temporizado](../ide/tutorial-2-create-a-timed-math-quiz.md).
