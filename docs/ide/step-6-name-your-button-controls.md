---
title: 'Etapa 6: Nomear os controles de botão'
ms.date: 08/30/2016
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22bc479ccd29a9eaf76e50f630061699856502ea
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72306218"
---
# <a name="step-6-name-your-button-controls"></a>Etapa 6: Nomear os controles de botão

Há apenas uma <xref:System.Windows.Forms.PictureBox> em seu formulário. Quando você a adicionou, o IDE a nomeou automaticamente como **pictureBox1**. Há apenas uma <xref:System.Windows.Forms.CheckBox>, que é denominada **checkBox1**. Em breve, você escreverá algum código e esse código fará referência à caixa de seleção e PictureBox. Como há apenas um desses controles, você saberá o que significa quando vir **pictureBox1** ou **checkBox1** em seu código.

> [!TIP]
> No Visual Basic, a primeira letra padrão de qualquer nome de controle é uma maiúscula inicial e, portanto, os nomes são **PictureBox1**, **CheckBox1** e assim por diante.

Há quatro botões no formulário e o IDE os nomeou **button1**, **button2**, **button3** e **button4**. Apenas olhando seus nomes atuais, você não consegue saber qual botão é o botão de **Fechar** e qual é o botão **Mostrar uma imagem**. É por isso que é útil atribuir nomes mais informativos aos controles de botão.

## <a name="to-name-your-button-controls"></a>Para nomear os controles de botão

1. No formulário, clique no botão **Fechar**. (Se você ainda tiver todos os botões selecionados, pressione a tecla **Esc** para cancelar a seleção). Role pela janela **Propriedades**, até ver a propriedade **(Name)** . (A propriedade **(Name)** fica próxima à parte superior quando as propriedades são alfabéticas.) Altere o nome para **botãoFechar**, conforme mostrado na captura de tela a seguir.

    ![A janela Propriedades com nome de closeButton](../ide/media/express_setnameproperty.png)<br>*Janela de propriedades com nome de* ***botãoFechar***

    > [!NOTE]
    > Tente alterar o nome do botão para **fechar o botão**, com um espaço entre as palavras "fechar" e "botão". Quando você fizer isso, o IDE exibirá uma mensagem de erro: "O valor da propriedade não é válido." Espaços (e mais alguns caracteres) não são permitidos em nomes de controle.

1. Renomeie os outros três botões para **backgroundButton**, **clearButton** e **showButton**.
Você pode verificar os nomes escolhendo a lista suspensa seletora de controle na janela **Propriedades**. Os nomes dos novos botões aparecem.

1. Clique duas vezes no botão **Mostrar uma imagem** no formulário. Como alternativa, escolha o botão **mostrar uma imagem** no formulário e pressione a tecla **Enter** . Quando você fizer isso, o IDE abrirá uma guia adicional na janela principal chamada **Form1.cs**. (Se você estiver usando Visual Basic, a guia será nomeada **Form1. vb**).

   Essa guia exibe o arquivo de código por trás do formulário, conforme mostrado na captura de tela a seguir.

    ![Guia Form1.cs com código do Visual C&#35;](../ide/media/express_showbuttoncode.png)<br>
Guia ***Form1.cs*** *com C# código*

    > [!NOTE]
    > A guia Form1.cs ou Form1. vb pode exibir o **botão** de **exibição como em** vez disso.

1. Foco nesta parte do código.

    ```csharp
        private void ShowButton_Click(object sender, EventArgs e)
    {
    }
    ```

    ```vb
        Private Sub showButton_Click() Handles showButton.Click

    End Sub
    ```

   [!INCLUDE [devlang-control](./includes/devlang-control.md)]

   Você está vendo o código chamado `showButton_Click()` (como alternativa, `ShowButton_Click()`). O IDE adicionou isto ao código do formulário quando você abriu o arquivo de código para o botão **showButton**. No tempo de design, quando você abre o arquivo de código para um controle em um formulário, o código é gerado para o controle se ainda não existir. Esse código, conhecido como *método*, é executado quando você executa o aplicativo e escolhe o controle, nesse caso, o botão **mostrar uma imagem** .

1. Escolha a guia **Designer de formulários do Windows** novamente (**Form1.cs [Design]** ) e, em seguida, abra o arquivo de código para o botão **limpar imagem** para criar um método para ele no código do formulário. Repita isso para os dois botões restantes. A cada vez, o IDE adiciona um novo método ao arquivo de código do formulário.

1. Para adicionar mais um método, abra o arquivo de código para o controle **CheckBox** no **Designer de Formulários do Windows** para fazer o IDE adicionar um método `checkBox1_CheckedChanged()`. Esse método é chamado sempre que o usuário seleciona ou desmarca a caixa de seleção.

   > [!TIP]
   > Ao trabalhar em um aplicativo, você geralmente se move entre o editor de código e **Designer de formulários do Windows**. O IDE torna fácil a navegação no projeto. Use **Gerenciador de soluções** para abrir **o designer de formulários do Windows** clicando duas vezes em *Form1.cs* no C# ou *Form1. vb* no Visual Basic, ou na barra de menus, escolha **Exibir** > **Designer**.

    A seguir temos o novo código que você vê no editor de códigos.

    [!code-csharp[VbExpressTutorial1Step6_#2](../ide/codesnippet/CSharp/step-6-name-your-button-controls_2.cs)]

    [!code-vb[VbExpressTutorial1Step6_#2](../ide/codesnippet/VisualBasic/step-6-name-your-button-controls_2.vb)]

    > [!NOTE]
    > Seu código pode não exibir manipuladores de eventos em letras "camelCase".

    Os cinco métodos que você adicionou são chamados de *manipuladores de eventos*, porque seu aplicativo os chama sempre que um evento (como um usuário escolhendo um botão ou uma caixa) acontece.

    Ao exibir o código para um controle no IDE em tempo de design, o Visual Studio adiciona um método manipulador de eventos para o controle se um não estiver presente. Por exemplo, quando você clica duas vezes em um botão, o IDE adiciona um manipulador de eventos para seu evento <xref:System.Windows.Forms.Control.Click> (que é chamado sempre que o usuário escolhe o botão). Quando você clica duas vezes em uma caixa de seleção, o IDE adiciona um manipulador de eventos para o evento <xref:System.Windows.Forms.CheckBox.CheckedChanged> (que é chamado sempre que o usuário seleciona ou desmarca a caixa).

    Após adicionar um manipulador de eventos para um controle, você pode retornar a ele a qualquer momento do **Designer de Formulários do Windows** clicando duas vezes no controle ou na barra de menus, selecionando **Exibir** > **Código**.

    Os nomes são importantes quando você cria programas e métodos (incluindo manipuladores de eventos) podem ter qualquer nome que você desejar. Quando você adiciona um manipulador de eventos com o IDE, cria um nome com base no nome do controle e do evento que está sendo tratado.

    Por exemplo, o evento de clique para um botão chamado " **DefaultButton** " é chamado de método de manipulador de eventos `showButton_Click()` (Alternativamente, `ShowButton_Click()`). Além disso, os parênteses de abertura e fechamento `()` são adicionados geralmente após o nome do método para indicar que os métodos estão sendo discutidos.

    Se você decidir que deseja alterar um nome de variável de código, clique com o botão direito do mouse na variável no código e então escolha **Refatorar** > **Renomear**. Todas as instâncias desta variável no código são renomeadas. Para obter mais informações, consulte [renomear refatoração](../ide/reference/rename.md).

## <a name="next-steps"></a>Próximas etapas

* Para ir para a próxima etapa do tutorial, consulte ** @ no__t-1Step 7: Adicione componentes de caixa de diálogo ao formulário @ no__t-0 @ no__t-1.

* Para retornar à etapa anterior do tutorial, confira [Etapa 5: Adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md).

## <a name="see-also"></a>Consulte também

* [Tutorial 2: Criar um teste de matemática cronometrado @ no__t-0
* [Tutorial 3: Criar um jogo correspondente @ no__t-0
