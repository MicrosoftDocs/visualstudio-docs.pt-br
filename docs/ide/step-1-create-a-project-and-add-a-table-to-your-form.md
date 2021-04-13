---
title: 'Etapa 1: Criar um projeto e adicionar uma tabela ao formulário'
description: Saiba como criar o projeto de jogo correspondente e adicionar uma tabela ao formulário.
ms.custom: SEO-VS-2020
ms.date: 10/15/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.assetid: 1cac4ba4-f3cd-43bd-ad5d-50fc599234e8
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4b4d500eb808e5a4f5d4c49cde9a84e740dc54d0
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296606"
---
# <a name="step-1-create-a-project-and-add-a-table-to-your-form"></a>Etapa 1: Criar um projeto e adicionar uma tabela ao formulário

A primeira etapa da criação de um jogo da memória é criar o projeto e adicionar uma tabela ao formulário. A tabela ajuda a alinhar os ícones em uma grade 4x4 de forma ordenada. Você também define várias propriedades para aprimorar a aparência do tabuleiro do jogo.

## <a name="to-create-a-project-and-add-a-table-to-your-form"></a>Para criar um projeto e adicionar uma tabela ao formulário

::: moniker range="vs-2017"

1. Na barra de menus, escolha **arquivo** > **novo** > **projeto**.

1. Escolha **Visual C#** ou **Visual Basic** no lado esquerdo da caixa de diálogo **Novo Projeto** e, em seguida, escolha **Windows Desktop**.

1. Na lista de modelos, escolha o modelo de **Aplicativo do Windows Forms (.NET Framework)**, dê o nome *MatchingGame* a ele e, então, clique no botão **OK**.

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

1. Na janela **Configurar seu novo projeto**, digite ou insira *MatchingGame* na caixa **Nome do projeto**. Em seguida, escolha **criar**.

::: moniker-end

## <a name="to-set-properties-for-a-form"></a>Para definir propriedades para um formulário

1. Na janela **Propriedades**, defina as propriedades de formulário a seguir.

   1. Altere a propriedade **Texto** do formulário, de **Form1** para **Jogo da Memória**. Esse texto aparece na parte superior da janela do jogo.

   2. Defina o tamanho do formulário para 550 pixels de largura por 550 de altura. Você pode fazer isso definindo a propriedade **Tamanho** como **550, 550** ou arrastando o canto do formulário até visualizar o tamanho correto no canto inferior direito do IDE (ambiente de desenvolvimento integrado).

2. Exiba a caixa de ferramentas escolhendo a guia **Caixa de Ferramentas** no lado esquerdo do IDE.

3. Arraste um controle <xref:System.Windows.Forms.TableLayoutPanel> da categoria **Contêineres** na caixa de ferramentas e, em seguida, defina as propriedades a seguir para ele.

   1. Defina a propriedade **BackColor** como **CornflowerBlue**. Para isso, abra a caixa de diálogo **BackColor** escolhendo a seta suspensa próxima à propriedade **BackColor** na janela **Propriedades**.  Em seguida, escolha a guia **Web** na caixa de diálogo **BackColor** para exibir uma lista de nomes de cores disponíveis.

      > [!NOTE]
      > As cores não estão em ordem alfabética e **CornflowerBlue** está quase no fim da lista.

   2. Defina a propriedade **Encaixar** como **Preenchimento** escolhendo o botão suspenso próximo à propriedade e escolhendo o botão grande do meio. Isso estende a tabela para que ela cubra o formulário inteiro.

   3. Defina a propriedade **CellBorderStyle** como **Baixo-relevo**. Isso fornece bordas visuais entre cada célula no tabuleiro.

   4. Escolha o botão triangular no canto superior direito do TableLayoutPanel para exibir o menu de tarefas.

   5. No menu de tarefas, escolha **Adicionar Linha** duas vezes para adicionar mais duas linhas e escolha **Adicionar Coluna** duas vezes para adicionar mais duas colunas.

   6. No menu de tarefas, escolha **Editar Linhas e Colunas** para abrir a janela **Estilos de Coluna e Linha**. Escolha cada uma das colunas, escolha o botão de opção **Porcentagem** e defina a largura de cada coluna como 25% da largura total. Em seguida, selecione **Linhas** na caixa suspensa na parte superior da janela e defina a altura de cada linha como 25%. Ao terminar, escolha o botão **OK** .

      O TableLayoutPanel agora deve ser uma grade 4x4, com dezesseis células quadradas de igual tamanho. Essas linhas e colunas estão onde as imagens do ícone aparecerão mais tarde.

4. Certifique-se de que TableLayoutPanel esteja selecionado no editor de formulários. Para confirmar isso, você deve ver **tableLayoutPanel1** na parte superior da janela **Propriedades**. Se não estiver selecionado, escolha TableLayoutPanel no formulário ou escolha-o no controle suspenso na parte superior da janela **Propriedades**.

    Enquanto TableLayoutPanel estiver selecionado, abra a caixa de ferramentas e adicione um controle <xref:System.Windows.Forms.Label> (localizado na categoria **Controles Comuns**) à célula superior esquerda de TableLayoutPanel. O controle Label agora deve ser selecionado no IDE. Defina as propriedades a seguir para ele.

   1. Verifique se a propriedade **BackColor** do rótulo está definida como **CornflowerBlue**.

   2. Defina a propriedade **AutoSize** para **False**.

   3. Defina a propriedade **Encaixar** como **Preenchimento**.

   4. Defina a propriedade **TextAlign** como **MiddleCenter** escolhendo o botão suspenso próximo à propriedade e escolhendo o botão do meio. Isso garante que o ícone apareça no meio da célula.

   5. Escolha a propriedade **Fonte**. O botão reticências (**...**) deverá aparecer.

   6. Escolha o botão de reticências e defina o valor de **Fonte** como **Webdings**, o **Estilo da Fonte** como **Negrito** e o **Tamanho** como **48**.

   7. Defina a propriedade **Texto** do rótulo como a letra **c**.

        A célula superior esquerda no TableLayoutPanel agora deve conter uma caixa preta centrada em um plano de fundo azul.

       > [!NOTE]
       > A fonte Webdings é uma fonte de ícones que acompanha o sistema operacional Windows. No seu jogo da memória, o jogador precisa encontrar pares de ícones, de modo que você usa essa fonte para exibir os ícones a serem encontrados. Em vez de colocar **c** na propriedade **Texto**, tente inserir diferentes letras para ver quais ícones são exibidos. Um ponto de exclamação é uma aranha, um N maiúsculo é um olho e uma vírgula é uma pimenta.

5. Escolha o controle de rótulo e copie-o ao lado da célula no TableLayoutPanel. (Escolha **Ctrl** + **C** , ou na barra de menus, escolha **Editar**  >  **cópia**.) Em seguida, Cole-o. (Escolha **Ctrl** + **V** Keys, ou na barra de menus, escolha **Editar**  >  **colar**.) Uma cópia do primeiro rótulo aparece na segunda célula do TableLayoutPanel. Cole-o novamente e outro rótulo aparecerá na terceira célula. Continue colando controles Label até que todas as células sejam preenchidas.

   > [!NOTE]
   > Se você colar muitas vezes, o IDE adicionará uma nova linha ao TableLayoutPanel para que ele tenha um local para adicionar seu novo controle de rótulo. Isso pode ser desfeito. Para remover a nova célula, escolha as  + teclas **Z** CTRL ou, na barra de menus, escolha **Editar**  >  **desfazer**.

    Agora seu formulário está disposto. Ele deve ser semelhante à imagem a seguir.

    ![Formulário inicial do jogo da memória](../ide/media/express_tut4step1.png)<br/>*Formulário inicial do jogo da memória*

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, veja [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).

- Para retornar ao tópico de visão geral, veja [Tutorial 3: Criar um jogo da memória](../ide/tutorial-3-create-a-matching-game.md).
