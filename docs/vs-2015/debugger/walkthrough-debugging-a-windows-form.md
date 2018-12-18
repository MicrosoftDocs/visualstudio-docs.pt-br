---
title: 'Passo a passo: Depurando um formulário do Windows | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- debugging managed code, Windows Forms
- debugging [Visual Studio], Windows Forms
- Attach to Process dialog box
- debugger, attaching to programs
- Attach to Process dialog box, walkthroughs
- Windows Forms, debugging
- debugging Windows Forms, walkthroughs
ms.assetid: 529db1e2-d9ea-482a-b6a0-7c543d17f114
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8f43835374ac74d50e1e81623ecf268fbfbfe8ca
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726598"
---
# <a name="walkthrough-debugging-a-windows-form"></a>Instruções passo a passo: um Windows Form
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um Windows Form é um dos aplicativos gerenciados mais comuns. Um Windows Form cria um aplicativo padrão do Windows. Você pode concluir este passo a passo usando o Visual Basic, C# ou C++.  
  
 Primeiro, você deve fechar as soluções abertas.  
  
### <a name="to-prepare-for-this-walkthrough"></a>Para preparar-se para esse passo a passo  
  
-   Se você já tiver uma solução aberta, feche-a. (Sobre o **arquivo** menu, selecione **fechar solução**.)  
  
## <a name="create-a-new-windows-form"></a>Criar um novo Windows Form  
 Em seguida, você criará um Windows Form.  
  
#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>Para criar o formulário do Windows para este passo a passo  
  
1.  Sobre o **arquivo** menu, escolha **New** e clique em **projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  No painel de tipos de projeto, abra o **Visual Basic**, **Visual c#**, ou **Visual C++** nó, em seguida,  
  
    1.  Para o Visual Basic ou Visual c#, selecione a **Windows** nó, em seguida, selecione **aplicativo de formulário do Windows** no **modelos** painel.  
  
    2.  Para o Visual C++, selecione o **CLR** nó, em seguida, selecione **aplicativo de formulário do Windows** no **modelos** painel...  
  
3.  No **modelos** painel, selecione **aplicativo do Windows**.  
  
4.  No **nome** caixa, dê ao projeto um nome exclusivo (por exemplo, Walkthrough_SimpleDebug).  
  
5.  Clique em **OK**.  
  
     O Visual Studio cria um novo projeto e exibe um novo formulário no designer do Windows Forms. Para obter mais informações, consulte [Designer de formulários do Windows](http://msdn.microsoft.com/en-us/3c3d61f8-f36c-4d41-b9c3-398376fabb15).  
  
6.  Sobre o **modo de exibição** menu, selecione **caixa de ferramentas**.  
  
     A caixa de ferramentas é aberta. Para saber mais, confira [Caixa de Ferramentas](../ide/reference/toolbox.md).  
  
7.  Na caixa de ferramentas, clique no **botão** controlar e arraste o controle para a superfície de design do formulário. Remova o botão do formulário.  
  
8.  Na caixa de ferramentas, clique no **caixa de texto** controlar e arraste o controle para a superfície de design do formulário. Descartar os **caixa de texto** no formulário.  
  
9. Na superfície de design do formulário, clique duas vezes no botão.  
  
     Isso leva à página de código. O cursor deve estar em `button1_Click`.  
  
10. Na função `button1_Click`, adicione o seguinte código:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
11. No menu **Build**, selecione **Compilar Solução**.  
  
     O projeto deve ser compilado sem erros.  
  
## <a name="debug-your-form"></a>Depurar seu formulário  
 Agora, você está pronto para iniciar a depuração.  
  
#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>Para depurar o Windows Form criado para este passo a passo  
  
1.  Na janela de origem, clique na margem esquerda na mesma linha que o texto que você adicionou:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
     Um ponto vermelho aparece e o texto da linha é realçado em vermelho. O ponto vermelho representa um ponto de interrupção. Para obter mais informações, consulte [pontos de interrupção](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583). Quando você executa o aplicativo no depurador, o depurador interromperá a execução nesse local quando o código é atingido. Você pode exibir o estado do aplicativo e depurá-lo.  
  
    > [!NOTE]
    >  Você pode também clique qualquer linha de código, aponte para **ponto de interrupção**e, em seguida, clique em **Inserir ponto de interrupção** para adicionar um ponto de interrupção nessa linha.  
  
2.  ON a **Debug** menu, escolha **iniciar**.  
  
     O Windows Form começa a ser executado.  
  
3.  No Windows Form, clique no botão que você adicionou.  
  
     No Visual Studio, isso o leva à linha onde você definiu seu ponto de interrupção na página de código. Essa linha deve ser realçada em amarelo. Agora você pode exibir as variáveis em seu aplicativo e controlar sua execução. Seu aplicativo parou de executar, aguardando uma ação.  
  
4.  No **depurar** menu, escolha **Windows**, em seguida, **inspeção**e clique em **Watch1**.  
  
5.  No **Watch1** janela, clique em uma linha em branco. No **nome** coluna, digite `textBox1.Text` (se você estiver usando Visual Basic, Visual c# ou j#) ou `textBox1->Text` (se você estiver usando C++), em seguida, pressione ENTER.  
  
     O **Watch1** janela mostra o valor dessa variável entre aspas como:  
  
    ```  
    ""  
    ```  
  
6.  Sobre o **Debug** menu, escolha **intervir**.  
  
     O valor de TextBox1.Text é alterado na **Watch1** janela para:  
  
    ```  
    Button was clicked!  
    ```  
  
7.  Sobre o **depurar** menu, escolha **continuar** para retomar a depurar seu programa.  
  
8.  No Windows Form, clique no botão novamente.  
  
     O Visual Studio interromperá a execução novamente.  
  
9. Clique no ponto vermelho que representa o ponto de interrupção.  
  
     Isso remove o ponto de interrupção do seu código.  
  
10. Sobre o **Debug** menu, escolha **parar depuração**.  
  
## <a name="attach-to-your-windows-form-application-for-debugging"></a>Anexar ao seu aplicativo do Windows Form para depurar  
 No [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)], você pode anexar o depurador a um processo em execução. Se você estiver usando um Express Edition, esse recurso não terá suporte.  
  
#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>Para anexar ao aplicativo do Windows Form para depurar  
  
1.  No projeto que você criou anteriormente, clique na margem esquerda para definir mais uma vez um ponto de interrupção na linha que você adicionou:  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!"  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
2.  Sobre o **Debug** menu, selecione **Start Without Debugging**.  
  
     O Windows Form inicia a execução no Windows, como se você tivesse clicado duas vezes em seu executável. O depurador não está anexado.  
  
3.  Sobre o **Debug** menu, selecione **anexar ao processo**. (Este comando também está disponível na **ferramentas** menu.)  
  
     A caixa de diálogo **Anexar ao Processo** é exibida.  
  
4.  No **processos disponíveis** painel, localize o nome do processo (Walkthrough_SimpleDebug.exe) na **processo** coluna e clique nele.  
  
5.  Clique o **Attach** botão.  
  
6.  No seu Windows Form, clique no único botão.  
  
     O depurador interromperá a execução do Windows Form no ponto de interrupção.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Segurança do depurador](../debugger/debugger-security.md)



