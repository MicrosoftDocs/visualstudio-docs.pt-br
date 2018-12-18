---
title: Depuração de um formulário do Windows | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 545155f622111c2452af3bacb57fd88930ce5ab0
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066750"
---
# <a name="walkthrough-debugging-a-windows-form"></a>Passo a passo: Depurando um Windows Form
Um Windows Form é um dos aplicativos gerenciados mais comuns. Um Windows Form cria um aplicativo padrão do Windows. Você pode concluir este passo a passo usando o Visual Basic, C# ou C++.  
  
 Primeiro, você deve fechar as soluções abertas.  
  
### <a name="to-prepare-for-this-walkthrough"></a>Para preparar-se para esse passo a passo  
  
-   Se você já tiver uma solução aberta, feche-a. (No menu **Arquivo**, selecione **Fechar Solução**.)  
  
## <a name="create-a-new-windows-form"></a>Criar um novo Windows Form  
 Em seguida, você criará um Windows Form.  
  
#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>Para criar o formulário do Windows para este passo a passo  
  
1.  No menu **Arquivo**, escolha **Novo** e clique em **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  No painel Tipos de Projeto, abra o nó **Visual Basic**, **Visual C#** ou **Visual C++**, em seguida,  
  
    1.  Para o Visual Basic ou Visual c#, selecione **área de trabalho do Windows** > **aplicativo de formulário do Windows**.  
  
    2.  Para o Visual C++, selecione **aplicativo de área de trabalho do Windows**.  
  
3.  Na caixa **Nome**, dê ao projeto um nome exclusivo (por exemplo, Walkthrough_SimpleDebug).  
  
4.  Clique em **OK**.  
  
     O Visual Studio cria um novo projeto e exibe um novo formulário no designer do Windows Forms. Para obter mais informações, confira [Designer de Formulários do Windows](/previous-versions/visualstudio/visual-studio-2010/e06hs424\(v\=vs.100\)).  
  
5.  No menu **Exibir**, selecione **Caixa de ferramentas**.  
  
     A caixa de ferramentas é aberta. Para saber mais, confira [Caixa de Ferramentas](../ide/reference/toolbox.md).  
  
6.  Na Caixa de ferramentas, clique no controle de **Botão** e arraste-o para a superfície de design do formulário. Remova o botão do formulário.  
  
7.  Na caixa de ferramentas, clique no controle **TextBox** e arraste-o para a superfície de design do formulário. Remova **TextBox** do formulário.  
  
8. Na superfície de design do formulário, clique duas vezes no botão.  
  
     Isso leva à página de código. O cursor deve estar em `button1_Click`.  
  
10. Na função `button1_Click`, adicione o seguinte código:  
  
    ```vb  
    textBox1.Text = "Button was clicked!"
    ```  
  
    ```csharp 
    textBox1.Text = "Button was clicked!";
    ```  
  
    ```cpp  
    textBox1->Text = "Button was clicked!";  
    ```  
  
11. No menu **Build**, selecione **Compilar Solução**.  
  
     O projeto deve ser compilado sem erros.  
  
## <a name="debug-your-form"></a>Depurar seu formulário  
 Agora, você está pronto para iniciar a depuração.  
  
#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>Para depurar o Windows Form criado para este passo a passo  
  
1.  Na janela de origem, clique na margem esquerda na mesma linha que o texto que você adicionou:  
  
     ```vb  
    textBox1.Text = "Button was clicked!"
    ```  
  
    ```csharp 
    textBox1.Text = "Button was clicked!";
    ```  
  
    ```cpp  
    textBox1->Text = "Button was clicked!";  
    ``` 
  
     Um ponto vermelho aparece e o texto da linha é realçado em vermelho. O ponto vermelho representa um ponto de interrupção. Para obter mais informações, confira [Pontos de interrupção](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583). Quando você executa o aplicativo no depurador, o depurador interromperá a execução nesse local quando o código é atingido. Você pode exibir o estado do aplicativo e depurá-lo.  
  
    > [!NOTE]
    >  Você também pode clicar com o botão direito do mouse em qualquer linha de código, apontar para **Ponto de Interrupção** e clicar em **Inserir Ponto de Interrupção** para adicionar um ponto de interrupção nessa linha.  
  
2.  No menu **Depurar**, escolha **Iniciar**.  
  
     O Windows Form começa a ser executado.  
  
3.  No Windows Form, clique no botão que você adicionou.  
  
     No Visual Studio, isso o leva à linha onde você definiu seu ponto de interrupção na página de código. Essa linha deve ser realçada em amarelo. Agora você pode exibir as variáveis em seu aplicativo e controlar sua execução. Seu aplicativo parou de executar, aguardando uma ação.  
  
4.  No menu **Depurar**, escolha **Windows**, em seguida, **Inspeção** e clique em **Watch1**.  
  
5.  Na janela **Watch1**, clique em uma linha em branco. No **nome** coluna, digite `textBox1.Text` (se você estiver usando Visual Basic ou Visual c#) ou `textBox1->Text` (se você estiver usando C++), em seguida, pressione ENTER.  
  
     A janela **Watch1** mostra o valor dessa variável entre aspas como:  
  
    `""`  
 
6.  No menu **Depurar**, escolha **Intervir**.  
  
     O valor de TextBox1.Text é alterado na **Watch1** janela para:  
  
    `Button was clicked!`  
  
7.  No menu **Depurar**, escolha **Continuar** para retomar a depuração do programa.  
  
8.  No Windows Form, clique no botão novamente.  
  
     O Visual Studio interromperá a execução novamente.  
  
9. Clique no ponto vermelho que representa o ponto de interrupção.  
  
     Isso remove o ponto de interrupção do seu código.  
  
10. No menu **Depurar**, escolha **Parar depuração**.  
  
## <a name="attach-to-your-windows-form-application-for-debugging"></a>Anexar ao seu aplicativo do Windows Form para depurar  
 No [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)], você pode anexar o depurador a um processo em execução. Se você estiver usando um Express Edition, esse recurso não terá suporte.  
  
#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>Para anexar ao aplicativo do Windows Form para depurar  
  
1.  No projeto que você criou anteriormente, clique na margem esquerda para definir mais uma vez um ponto de interrupção na linha que você adicionou:  
  
     ```vb  
    textBox1.Text = "Button was clicked!"
    ```  
  
    ```csharp 
    textBox1.Text = "Button was clicked!";
    ```  
  
    ```cpp  
    textBox1->Text = "Button was clicked!";   
  
2.  On the **Debug** menu, select **Start Without Debugging**.  
  
     The Windows Form starts running under Windows, just as if you had double-clicked its executable. The debugger is not attached.  
  
3.  On the **Debug** menu, select **Attach to Process**. (This command is also available on the **Tools** menu.)  
  
     The **Attach to Process** dialog box appears.  
  
4.  In the **Available Processes** pane, find the process name (Walkthrough_SimpleDebug.exe) in the **Process** column and click it.  
  
5.  Click the **Attach** button.  
  
6.  In your Windows Form, click the one and only button.  
  
     The debugger breaks execution of the Windows Form at the breakpoint.  
  
## See Also  
 [Debugging Managed Code](../debugger/debugging-managed-code.md)   
 [Debugger Security](../debugger/debugger-security.md)