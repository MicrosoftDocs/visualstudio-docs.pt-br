---
title: 'Passo a passo: Escrevendo um visualizador em Visual Basic | Microsoft Docs'
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
ms.assetid: c93bf5a1-3e5e-422f-894e-bd72c9bc1b57
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 549e1ce240808a3947b2780f5c96485439e44ecc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794870"
---
# <a name="walkthrough-writing-a-visualizer-in-visual-basic"></a>Instruções passo a passo: escrevendo um visualizador no Visual Basic
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como escrever um visualizador simples usando [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. O visualizador que você criará neste passo a passo exibe o conteúdo de uma cadeia de caracteres usando uma caixa de mensagem do Windows Forms. Esse visualizador simples de cadeia de caracteres é um exemplo básico para mostrar como você pode criar visualizadores para outros tipos de dados mais aplicáveis a seus projetos.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar suas configurações, vá para o **ferramentas** menu e escolha **importar e exportar** . Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 O código do visualizador deve ser colocado em uma DLL, que será lido pelo depurador. A primeira etapa é criar um projeto da biblioteca de classes para a DLL.  
  
## <a name="create-and-prepare-a-class-library-project"></a>Criar e preparar um projeto da biblioteca de classes  
  
#### <a name="to-create-a-class-library-project"></a>Para criar um projeto da biblioteca de classes  
  
1. Sobre o **arquivo** menu, escolha **New** e clique em **novo projeto**.  
  
2. No **novo projeto** caixa de diálogo **tipo de projeto**s, clique em **Visual Basic**.  
  
3. No **modelos** , clique em **biblioteca de classes**.  
  
4. No **nome** , digite um nome apropriado para a biblioteca de classes, como **MyFirstVisualizer**.  
  
5. Clique em **OK**.  
  
   Quando você criou a biblioteca de classes, você deverá adicionar uma referência a Microsoft.VisualStudio.DebuggerVisualizers.DLL de forma que possa usar as classes definidas nela. Primeiro, no entanto, dê ao seu projeto um nome significativo.  
  
#### <a name="to-rename-class1vb-and-add-microsoftvisualstudiodebuggervisualizers"></a>Para renomear Class1.vb e adicionar Microsoft.VisualStudio.DebuggerVisualizers  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **Class1.vb**e no menu de atalho, clique em **Renomear**.  
  
2.  Altere o nome de Class1.vb para algo significativo, por exemplo, DebuggerSide.vb.  
  
    > [!NOTE]
    >  O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] automaticamente altera a declaração de classes em DebuggerSide.vb para corresponder ao novo nome do arquivo.  
  
3.  Na **Gerenciador de soluções**, clique com botão direito **meu primeiro visualizador**e no menu de atalho, clique em **Add Reference**.  
  
4.  No **adicionar referência** caixa de diálogo do **.NET** , clique em DebuggerVisualizers.  
  
5.  Clique em **OK**.  
  
6.  Em DebuggerSide.vb, adicione a seguinte instrução às instruções `Imports`:  
  
    ```  
    Imports Microsoft.VisualStudio.DebuggerVisualizers  
    ```  
  
## <a name="add-the-debugger-side-code"></a>Adicionar o código do lado do depurador  
 Agora você está pronto para criar o código do lado do depurador. Este é o código executado no depurador para exibir as informações que você deseja visualizar. Primeiro, você tem que alterar a declaração do objeto `DebuggerSide` de forma que ele herde da classe base `DialogDebuggerVisualizer`.  
  
#### <a name="to-inherit-from-dialogdebuggervisualizer"></a>Para herdar de DialogDebuggerVisualizer  
  
1. Em DebuggerSide.vb, vá para a seguinte linha de código:  
  
   ```  
   Public Class DebuggerSide  
   ```  
  
2. Edite o código de forma que tenha esta aparência:  
  
   ```  
   Public Class DebuggerSide  
   Inherits DialogDebuggerVisualizer  
   ```  
  
   `DialogDebuggerVisualizer` tem um método abstrato `Show`, que você deve substituir.  
  
#### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>Para substituir o método DialogDebuggerVisualizer.Show  
  
- Em `public class DebuggerSide`, adicione o seguinte método:  
  
  ```  
  Protected Overrides Sub Show(ByVal windowService As Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService, ByVal objectProvider As Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider)  
  
      End Sub  
  ```  
  
  O método `Show` contém o código que realmente cria a caixa de diálogo DO visualizador ou outra interface de usuário e exibe as informações que foram passadas para o visualizador do depurador. Adicione o código que cria a caixa de diálogo e exibe as informações. Neste passo a passo, você fará isso usando uma caixa de mensagem do Windows Forms. Primeiro, você deve adicionar uma referência e uma instrução `Imports` para <xref:System.Windows.Forms>.  
  
#### <a name="to-add-systemwindowsforms"></a>Para adicionar System.Windows.Forms  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **referências**e no menu de atalho, clique em **Add Reference**.  
  
2.  No **adicionar referência** caixa de diálogo do **.NET** , clique em **System**.  
  
3.  Clique em **OK**.  
  
4.  Em DebuggerSide.cs, adicione a seguinte instrução às instruções `Imports`:  
  
    ```  
    Imports System.Windows.Forms  
    ```  
  
## <a name="create-your-visualizers-user-interface"></a>Criar a interface de usuário do visualizador  
 Agora, você adicionará um código para criar e exibir a interface de usuário para o visualizador. Como esse é o primeiro visualizador, você manterá a interface do usuário simples e usará uma caixa de mensagem.  
  
#### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>Para mostrar a saída do visualizador em uma caixa de diálogo  
  
1.  No método `Show`, adicione a seguinte linha de código:  
  
    ```  
    MessageBox.Show(objectProvider.GetObject().ToString())  
    ```  
  
     Esse código de exemplo não inclui tratamento de erros. Você deve incluir o tratamento de erros em um visualizador real ou qualquer outro tipo de aplicativo.  
  
2.  Sobre o **construir** menu, clique em **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
## <a name="add-the-necessary-attribute"></a>Adicionar o atributo necessário  
 Esse é o final do código do lado do depurador. Há mais uma etapa, porém: o atributo que diz ao lado a ser depurado qual coleção de classes integra o visualizador.  
  
#### <a name="to-add-the-debugee-side-code"></a>Para adicionar o código do lado a ser depurado  
  
1.  Adicione o seguinte código do atributo a DebuggerSide.vb, depois das instruções `Imports`, mas antes de `namespace MyFirstVisualizer`:  
  
    ```  
    <Assembly: System.Diagnostics.DebuggerVisualizer(GetType(MyFirstVisualizer.DebuggerSide), GetType(VisualizerObjectSource), Target:=GetType(System.String), Description:="My First Visualizer")>  
    ```  
  
2.  Sobre o **construir** menu, clique em **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
## <a name="create-a-test-harness"></a>Criar um agente de teste  
 Neste momento, o primeiro visualizador é concluído. Se você seguiu as etapas corretamente, poderá compilar o visualizador e instalá-lo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Antes de instalar um visualizador no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], no entanto, você deverá testá-lo para garantir que seja executado corretamente. Agora você criará um teste automatizado para executar o visualizador sem instalá-lo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
#### <a name="to-add-a-test-method-to-show-the-visualizer"></a>Para adicionar um método de teste para mostrar o visualizador  
  
1. Adicione o método a seguir à classe `public DebuggerSide`.  
  
   ```  
   Shared Public Sub TestShowVisualizer(ByVal objectToVisualize As Object)  
       Dim visualizerHost As New VisualizerDevelopmentHost(objectToVisualize, GetType(DebuggerSide))  
   visualizerHost.ShowVisualizer()  
   End Sub  
   ```  
  
2. Sobre o **construir** menu, clique em **compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.  
  
   Em seguida, você deverá criar um projeto executável para chamar sua DLL do visualizador. Para simplificar, use um projeto de aplicativo de console.  
  
#### <a name="to-add-a-console-application-project-to-the-solution"></a>Para adicionar um projeto de aplicativo de console à solução  
  
1. Sobre o **arquivo** menu, clique em **Add**e, em seguida, clique em **novo projeto**.  
  
2. No **adicionar novo projeto** na caixa de **modelos** , clique em **aplicativo de Console**.  
  
3. No **nome** , digite um nome significativo para o aplicativo de console, como **MyTestConsole**.  
  
4. Clique em **OK**.  
  
   Agora, você deve adicionar as referências necessárias para que MyTestConsole possa chamar MyFirstVisualizer.  
  
#### <a name="to-add-necessary-references-to-mytestconsole"></a>Para adicionar as referências necessárias a MyTestConsole  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **MyTestConsole**e no menu de atalho, clique em **Add Reference**.  
  
2.  No **adicionar referência** caixa de diálogo do **.NET** , clique em DebuggerVisualizers.  
  
3.  Clique em **OK**.  
  
4.  Clique com botão direito **MyTestConsole**e, em seguida, clique em **adicionar referência** novamente.  
  
5.  No **adicionar referência** caixa de diálogo, clique o **projetos** guia e, em seguida, selecione MyFirstVisualizer.  
  
6.  Clique em **OK**.  
  
## <a name="finish-your-test-harness-and-test-your-visualizer"></a>Conclua seu agente de teste e teste o visualizador  
 Agora, você adicionará o código para concluir um teste automatizado.  
  
#### <a name="to-add-code-to-mytestconsole"></a>Para adicionar código a MyTestConsole  
  
1. Na **Gerenciador de soluções**, clique com botão direito **Program. vb**e no menu de atalho, clique em **Renomear**.  
  
2. Editar o nome de Module1.vb para algo apropriado, como **TestConsole**.  
  
    Observe que o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] automaticamente altera a declaração de classes em TestConsole.vb para corresponder ao novo nome do arquivo.  
  
3. No TestConsole. VB, adicione o seguinte `Imports` instrução:  
  
   ```  
   Imports MyFirstVisualizer  
   ```  
  
4. No método `Main`, adicione o seguinte código:  
  
   ```  
   Dim myString As String = "Hello, World"  
   DebuggerSide.TestShowVisualizer(myString)  
   ```  
  
   Agora, você está pronto para testar seu primeiro visualizador.  
  
#### <a name="to-test-the-visualizer"></a>Para testar o visualizador  
  
1. Na **Gerenciador de soluções**, clique com botão direito **MyTestConsole**e no menu de atalho, clique em **Set as Startup Project**.  
  
2. Sobre o **Debug** menu, clique em **iniciar**.  
  
    O aplicativo de console é iniciado. O visualizador aparece e exibe a cadeia de caracteres “Hello, World”.  
  
   Parabéns. Você acabou de criar e testar seu primeiro visualizador.  
  
   Se você quiser usar o visualizador no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] em vez de apenas chamá-lo do teste automatizado, será preciso instalá-lo. Para obter mais informações, consulte [como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura do Visualizador](../debugger/visualizer-architecture.md)   
 [Como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md)   
 [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)



