---
title: 'Passo a passo: Escrevendo um visualizador em c# | Microsoft Docs'
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
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: 53467461-8e0f-45ee-9bc4-374bbaeaf00f
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e265810e30423064e27b1650f57fb054743341ce
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817328"
---
# <a name="walkthrough-writing-a-visualizer-in-c"></a>Instruções passo a passo: escrevendo um visualizador em C# #
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como escrever um visualizador simples usando C#. O visualizador que você criará neste passo a passo exibe o conteúdo de uma cadeia de caracteres usando uma caixa de mensagem do Windows Forms. Esse visualizador simples de cadeia de caracteres não é especialmente útil em si mesmo, mas mostra as etapas básicas a seguir para criar visualizadores mais úteis para outros tipos de dados.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar suas configurações, vá para o **ferramentas** menu e escolha **Import and Export Settings**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 O código do visualizador deve ser colocado em uma DLL, que será lido pelo depurador. Consequentemente, a primeira etapa é criar um projeto da Biblioteca de Classes para a DLL.  
  
#### <a name="to-create-a-class-library-project"></a>Para criar um projeto da biblioteca de classes  
  
1. Sobre o **arquivo** menu, escolha **New** e, em seguida, clique em **novo projeto**.  
  
2. No **novo projeto** caixa de diálogo **tipo de projeto**s, selecione **Visual c#**.  
  
3. No **modelos** , escolha **biblioteca de classes**.  
  
4. No **nome** , digite um nome apropriado para a biblioteca de classes, por exemplo, MyFirstVisualizer.  
  
5. Clique em **OK**.  
  
   Depois de ter criado a biblioteca de classes, você deverá adicionar uma referência a Microsoft.VisualStudio.DebuggerVisualizers.DLL de forma que possa usar as classes definidas nela. Antes de adicionar a referência, no entanto, você deverá renomear algumas classes de modo que tenham nomes significativos.  
  
#### <a name="to-rename-class1cs-and-add-microsoftvisualstudiodebuggervisualizers"></a>Para renomear Class1.cs e adicionar Microsoft.VisualStudio.DebuggerVisualizers  
  
1. Na **Gerenciador de soluções**, clique com botão direito Class1.cs e escolha **Renomear** no menu de atalho.  
  
2. Altere o nome de Class1.cs para algo significativo, por exemplo, DebuggerSide.cs.  
  
   > [!NOTE]
   >  O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] automaticamente altera a declaração de classes em DebuggerSide.cs para corresponder ao novo nome do arquivo.  
  
3. Na **Gerenciador de soluções**, clique com botão direito **referências** e escolha **Add Reference** no menu de atalho.  
  
4. No **adicionar referência** caixa de diálogo do **.NET** guia, escolha DebuggerVisualizers.  
  
5. Clique em **OK**.  
  
6. Em DebuggerSide.cs, adicione a seguinte instrução às instruções `using`:  
  
   ```  
   using Microsoft.VisualStudio.DebuggerVisualizers;  
   ```  
  
   Agora você está pronto para criar o código do lado do depurador. Este é o código executado no depurador para exibir as informações que você deseja visualizar. Primeiro, você tem que alterar a declaração do objeto `DebuggerSide` de forma que ele herde da classe base `DialogDebuggerVisualizer`.  
  
#### <a name="to-inherit-from-dialogdebuggervisualizer"></a>Para herdar de DialogDebuggerVisualizer  
  
1. Em DebuggerSide.cs, vá para a seguinte linha de código:  
  
   ```  
   public class DebuggerSide  
   ```  
  
2. Altere o código para:  
  
   ```  
   public class DebuggerSide : DialogDebuggerVisualizer  
   ```  
  
   `DialogDebuggerVisualizer` tem um método abstrato (`Show`) que você deve substituir.  
  
#### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>Para substituir o método DialogDebuggerVisualizer.Show  
  
- Na `public class DebuggerSide`, adicione o seguinte **método:**  
  
  ```  
  override protected void Show(IDialogVisualizerService windowService, IVisualizerObjectProvider objectProvider)  
  {  
  }  
  ```  
  
  O método `Show` contém o código que realmente cria a caixa de diálogo DO visualizador ou outra interface de usuário e exibe as informações que foram passadas para o visualizador do depurador. Adicione o código que cria a caixa de diálogo e exibe as informações. Neste passo a passo, você fará isso usando uma caixa de mensagem do Windows Forms. Primeiro, você deve adicionar uma referência e uma instrução `using` para System.Windows.Forms.  
  
#### <a name="to-add-systemwindowsforms"></a>Para adicionar System.Windows.Forms  
  
1. Na **Gerenciador de soluções**, clique com botão direito **referências** e escolha **Add Reference** no menu de atalho.  
  
2. No **adicionar referência** caixa de diálogo do **.NET** guia, escolha a dll.  
  
3. Clique em **OK**.  
  
4. Em DebuggerSide.cs, adicione a seguinte instrução às instruções `using`:  
  
   ```  
   using System.Windows.Forms;  
   ```  
  
   Agora, você adicionará um código para criar e exibir a interface de usuário para o visualizador. Como esse é o primeiro visualizador, manteremos a interface do usuário simples e usaremos uma caixa de mensagem.  
  
#### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>Para mostrar a saída do visualizador em uma caixa de diálogo  
  
1. No método `Show`, adicione a seguinte linha de código:  
  
   ```  
   MessageBox.Show(objectProvider.GetObject().ToString());  
   ```  
  
    Esse código de exemplo não inclui tratamento de erros. Você deve incluir o tratamento de erros em um visualizador real ou qualquer outro tipo de aplicativo.  
  
2. Sobre o **construir** menu, escolha **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
   Esse é o final do código do lado do depurador. Há mais uma etapa, porém; o atributo que diz ao lado a ser depurado qual coleção de classes integra o visualizador.  
  
#### <a name="to-add-the-debuggee-side-code"></a>Para adicionar o código do lado a ser depurado  
  
1. Adicione o seguinte código do atributo a DebuggerSide.cs, depois das instruções `using`, mas antes de `namespace MyFirstVisualizer`:  
  
   ```  
   [assembly:System.Diagnostics.DebuggerVisualizer(  
   typeof(MyFirstVisualizer.DebuggerSide),  
   typeof(VisualizerObjectSource),  
   Target  = typeof(System.String),  
   Description  = "My First Visualizer")]  
   ```  
  
2. Sobre o **construir** menu, escolha **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
   Neste momento, o primeiro visualizador é concluído. Se você seguiu as etapas corretamente, poderá compilar o visualizador e instalá-lo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Antes de instalar um visualizador no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], no entanto, você deverá testá-lo para garantir que seja executado corretamente. Agora você criará um teste automatizado para executar o visualizador sem instalá-lo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
#### <a name="to-add-a-test-method-to-show-the-visualizer"></a>Para adicionar um método de teste para mostrar o visualizador  
  
1. Adicione o método a seguir à classe `public DebuggerSide`.  
  
   ```  
   public static void TestShowVisualizer(object objectToVisualize)  
   {  
      VisualizerDevelopmentHost visualizerHost = new VisualizerDevelopmentHost(objectToVisualize, typeof(DebuggerSide));  
      visualizerHost.ShowVisualizer();  
   }  
   ```  
  
2. Sobre o **construir** menu, escolha **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
   Em seguida, você deverá criar um projeto executável para chamar sua DLL do visualizador. Para simplificar, usaremos um projeto de aplicativo de console.  
  
#### <a name="to-add-a-console-application-project-to-the-solution"></a>Para adicionar um projeto de aplicativo de console à solução  
  
1. Sobre o **arquivo** menu, escolha **Add** e, em seguida, clique em **novo projeto**.  
  
2. No **adicionar novo projeto** na caixa de **modelos** , escolha **aplicativo de Console**.  
  
3. No **nome** , digite um nome significativo para o aplicativo de console, como `MyTestConsole`.  
  
4. Clique em **OK**.  
  
   Agora, você deve adicionar as referências necessárias para que MyTestConsole possa chamar MyFirstVisualizer.  
  
#### <a name="to-add-necessary-references-to-mytestconsole"></a>Para adicionar as referências necessárias a MyTestConsole  
  
1. Na **Gerenciador de soluções**, clique com botão direito **MyTestConsole** e escolha **Add Reference** no menu de atalho.  
  
2. No **adicionar referência** caixa de diálogo **.NET** guia, escolha DebuggerVisualizers.  
  
3. Clique em **OK**.  
  
4. Clique com botão direito **MyTestConsole** e escolha **adicionar referência** novamente.  
  
5. No **adicionar referência** caixa de diálogo, clique o **projetos** guia e, em seguida, clique em MyFirstVisualizer.  
  
6. Clique em **OK**.  
  
   Agora, você adicionará o código para concluir um teste automatizado.  
  
#### <a name="to-add-code-to-mytestconsole"></a>Para adicionar código a MyTestConsole  
  
1. Na **Gerenciador de soluções**, clique com botão direito Program.cs e escolha **Renomear** no menu de atalho.  
  
2. Edite o nome de Program.cs para algo mais significativo, por exemplo, TestConsole.cs.  
  
    **Observação** [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] automaticamente altera a declaração de classe em TestConsole.cs para corresponder ao novo nome de arquivo.  
  
3. Em TestConsole.cs, adicione o seguinte código às instruções `using`:  
  
   ```  
   using MyFirstVisualizer;  
   ```  
  
4. No método `Main`, adicione o seguinte código:  
  
   ```  
   String myString = "Hello, World";  
   DebuggerSide.TestShowVisualizer(myString);  
   ```  
  
   Agora, você está pronto para testar seu primeiro visualizador.  
  
#### <a name="to-test-the-visualizer"></a>Para testar o visualizador  
  
1. Na **Gerenciador de soluções**, clique com botão direito **MyTestConsole** e escolha **Set as Startup Project** no menu de atalho.  
  
2. Sobre o **Debug** menu, escolha **iniciar**.  
  
    O aplicativo de console inicia e o visualizador aparece e exibe a cadeia de caracteres “Hello World”.  
  
   Parabéns. Você acabou de criar e testar seu primeiro visualizador.  
  
   Se você quiser usar o visualizador no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] em vez de apenas chamá-lo do teste automatizado, será preciso instalá-lo. Para obter mais informações, consulte [como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md).  
  
## <a name="using-the-visualizer-item-template"></a>Usando o modelo de item do visualizador  
 Até agora, este passo a passo mostrou como criar um visualizador manualmente. Isto foi feito como um exercício de aprendizado. Agora que você sabe como um visualizador simples funciona, há uma forma mais fácil de criar um: usando o modelo de item do visualizador.  
  
 Primeiro, você precisará criar um novo projeto de biblioteca de classes.  
  
#### <a name="to-create-a-new-class-library"></a>Para criar uma nova biblioteca de classes  
  
1. Sobre o **arquivo** menu, escolha **Add** e, em seguida, clique em **novo projeto**.  
  
2. No **adicionar novo projeto** caixa de diálogo **tipo de projeto**s, selecione **Visual c#**.  
  
3. No **modelos** , escolha **biblioteca de classes**.  
  
4. No **nome** , digite um nome apropriado para a biblioteca de classes, por exemplo, MySecondVisualizer.  
  
5. Clique em **OK**.  
  
   Agora, você pode adicionar um item de visualizador a ele:  
  
#### <a name="to-add-a-visualizer-item"></a>Para adicionar um item de visualizador  
  
1. Na **Gerenciador de soluções**, clique com botão direito MySecondVisualizer.  
  
2. No menu de atalho, escolha **Add** e, em seguida, clique em **Novo Item**.  
  
3. No **Adicionar Novo Item** caixa de diálogo **modelos**, **Visual Studio Installed Templates**, selecione **Visualizador de depurador**.  
  
4. No **nome** , digite um nome apropriado, por exemplo, SecondVisualizer.cs.  
  
5. Clique em **Adicionar**.  
  
   É tudo que se precisa. Examine o arquivo SecondVisualizer.cs e exiba o código que o modelo adicionou para você. Agora tente com o código. Agora que você conhece as noções básicas, está em condições de criar visualizadores mais complexos e úteis.  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura do Visualizador](../debugger/visualizer-architecture.md)   
 [Como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md)   
 [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)



