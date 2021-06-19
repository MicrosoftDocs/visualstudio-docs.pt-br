---
title: Escrever um visualizador em Visual Basic | Microsoft Docs
description: Siga um passo a passo para criar um visualizador simples Visual Basic. Você também cria um harness de teste para testar o visualizador.
ms.custom: SEO-VS-2020
ms.date: 05/27/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: c93bf5a1-3e5e-422f-894e-bd72c9bc1b57
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b1a4fc7d6f33d1bdfd469ec352674b08dd2495e6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384995"
---
# <a name="walkthrough-writing-a-visualizer-in-visual-basic"></a>Instruções passo a passo: escrevendo um visualizador no Visual Basic

Este passo a passo mostra como escrever um visualizador simples usando [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]. O visualizador que você criará neste passo a passo exibe o conteúdo de uma cadeia de caracteres usando uma caixa de mensagem do Windows Forms. Esse visualizador simples de cadeia de caracteres é um exemplo básico para mostrar como você pode criar visualizadores para outros tipos de dados mais aplicáveis a seus projetos.

> [!NOTE]
> As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar suas configurações, acesse o menu **Ferramentas** e escolha **Importar e Exportar**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

O código do visualizador deve ser colocado em uma DLL, que será lido pelo depurador. A primeira etapa é criar um projeto da biblioteca de classes para a DLL.

## <a name="create-and-prepare-a-class-library-project"></a>Criar e preparar um projeto da biblioteca de classes

### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe

1. Crie um novo projeto de biblioteca de classes.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, digite visual **basic,** escolha Modelos **e,** em seguida, escolha Criar uma nova biblioteca de **classes (.NET Framework)**. Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **Arquivo**  >  **Novo**  >  **Projeto**. No painel esquerdo da  caixa de diálogo Novo projeto, em **Visual Basic**, escolha .NET Standard e, em seguida, no painel central, escolha Biblioteca de Classes **(.NET Standard)**.
    ::: moniker-end

2. Digite um nome apropriado para a biblioteca de classes, como `MyFirstVisualizer` e clique em **Criar** ou **OK.**

   Quando você criou a biblioteca de classes, você deverá adicionar uma referência a Microsoft.VisualStudio.DebuggerVisualizers.DLL de forma que possa usar as classes definidas nela. Primeiro, no entanto, dê ao seu projeto um nome significativo.

### <a name="to-rename-class1vb-and-add-microsoftvisualstudiodebuggervisualizers"></a>Para renomear Class1.vb e adicionar Microsoft.VisualStudio.DebuggerVisualizers

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Class1.vb** e no menu de atalho, clique em **Renomear**.

2. Altere o nome de Class1.vb para algo significativo, por exemplo, DebuggerSide.vb.

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] altera automaticamente a declaração de classe em DebuggerSide.vb para corresponder ao novo nome de arquivo.

3. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Meu Primeiro Visualizador** e, no menu de atalho, clique em **Adicionar Referência**.

4. Na caixa **de diálogo** Adicionar Referência, na **guia Procurar,** selecione **Procurar** e encontre o Microsoft.VisualStudio.DebuggerVisualizers.DLL.

    Você pode encontrar a DLL no subdiretório *\<Visual Studio Install Directory> \Common7\IDE\PublicAssemblies* Visual Studio diretório de instalação do .

5. Clique em **OK**.

6. Em DebuggerSide.vb, adicione a seguinte instrução às instruções `Imports`:

   ```vb
   Imports Microsoft.VisualStudio.DebuggerVisualizers
   ```

## <a name="add-the-debugger-side-code"></a>Adicionar o código do lado do depurador
 Agora você está pronto para criar o código do lado do depurador. Este é o código executado no depurador para exibir as informações que você deseja visualizar. Primeiro, você tem que alterar a declaração do objeto `DebuggerSide` de forma que ele herde da classe base `DialogDebuggerVisualizer`.

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>Para herdar de DialogDebuggerVisualizer

1. Em DebuggerSide.vb, vá para a seguinte linha de código:

   ```vb
   Public Class DebuggerSide
   ```

2. Edite o código de forma que tenha esta aparência:

   ```vb
   Public Class DebuggerSide
   Inherits DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` tem um método abstrato, `Show` , que você deve substituir.

### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>Para substituir o método DialogDebuggerVisualizer.Show

- Em `public class DebuggerSide`, adicione o seguinte método:

  ```vb
  Protected Overrides Sub Show(ByVal windowService As Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService, ByVal objectProvider As Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider)

      End Sub
  ```

  O método `Show` contém o código que realmente cria a caixa de diálogo DO visualizador ou outra interface de usuário e exibe as informações que foram passadas para o visualizador do depurador. Adicione o código que cria a caixa de diálogo e exibe as informações. Neste passo a passo, você fará isso usando uma caixa de mensagem do Windows Forms. Primeiro, você deve adicionar uma referência e uma instrução `Imports` para <xref:System.Windows.Forms>.

### <a name="to-add-systemwindowsforms"></a>Para adicionar System.Windows.Forms

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e, no menu de atalho, clique em **Adicionar Referência**.

2. Na caixa **de diálogo** Adicionar Referência, na **guia Procurar,** selecione **Procurar** e encontre o System.Windows.Forms.DLL.

    Você pode encontrar a DLL *em C:\Windows\Microsoft.NET\Framework\v4.0.30319*.

3. Clique em **OK**.

4. Em DebuggerSide.cs, adicione a seguinte instrução às instruções `Imports`:

    ```vb
    Imports System.Windows.Forms
    ```

## <a name="create-your-visualizers-user-interface"></a>Criar a interface de usuário do visualizador
 Agora, você adicionará um código para criar e exibir a interface de usuário para o visualizador. Como esse é o primeiro visualizador, você manterá a interface do usuário simples e usará uma caixa de mensagem.

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>Para mostrar a saída do visualizador em uma caixa de diálogo

1. No método `Show`, adicione a linha de código a seguir:

    ```vb
    MessageBox.Show(objectProvider.GetObject().ToString())
    ```

     Esse código de exemplo não inclui tratamento de erros. Você deve incluir o tratamento de erros em um visualizador real ou qualquer outro tipo de aplicativo.

2. No menu **Compilar**, clique em **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

## <a name="add-the-necessary-attribute"></a>Adicionar o atributo necessário
 Esse é o final do código do lado do depurador. Há mais uma etapa, porém: o atributo que diz ao lado a ser depurado qual coleção de classes integra o visualizador.

### <a name="to-add-the-type-to-visualize-for-the-debuggee-side-code"></a>Para adicionar o tipo a ser visualizado para o código do lado do rodo de depuração

No código do lado do depurador, especifique o tipo a ser visualizado (a origem do objeto) para o depurador usando o <xref:System.Diagnostics.DebuggerVisualizerAttribute> atributo . A `Target` propriedade define o tipo a ser visualizado.

1. Adicione o seguinte código do atributo a DebuggerSide.vb, depois das instruções `Imports`, mas antes de `namespace MyFirstVisualizer`:

    ```vb
    <Assembly: System.Diagnostics.DebuggerVisualizer(GetType(MyFirstVisualizer.DebuggerSide), GetType(VisualizerObjectSource), Target:=GetType(System.String), Description:="My First Visualizer")>
    ```

2. No menu **Compilar**, clique em **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

## <a name="create-a-test-harness"></a>Criar um agente de teste
 Neste momento, o primeiro visualizador é concluído. Se você seguiu as etapas corretamente, poderá compilar o visualizador e instalá-lo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Antes de instalar um visualizador no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], no entanto, você deverá testá-lo para garantir que seja executado corretamente. Agora você criará um teste automatizado para executar o visualizador sem instalá-lo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>Para adicionar um método de teste para mostrar o visualizador

1. Adicione o método a seguir à classe `public DebuggerSide`.

   ```vb
   Shared Public Sub TestShowVisualizer(ByVal objectToVisualize As Object)
       Dim visualizerHost As New VisualizerDevelopmentHost(objectToVisualize, GetType(DebuggerSide))
   visualizerHost.ShowVisualizer()
   End Sub
   ```

2. No menu **Compilar**, clique em **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

   Em seguida, você deverá criar um projeto executável para chamar sua DLL do visualizador. Para simplificar, use um projeto de aplicativo de console.

### <a name="to-add-a-console-application-project-to-the-solution"></a>Para adicionar um projeto de aplicativo de console à solução

1. No Gerenciador de Soluções, clique com o botão direito do mouse na solução, escolha **Adicionar** e clique **em Novo Projeto.**

    ::: moniker range=">=vs-2019"
    Na caixa Pesquisar, digite **visual basic,** escolha **Modelos** e, em seguida, escolha **Criar um novo aplicativo de console (.NET Framework)**. Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **Arquivo**  >  **Novo**  >  **Projeto**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual Basic**, escolha **Área de Trabalho do Windows** e, em seguida, no painel central, escolha **Aplicativo de Console (.NET Framework)**.
    ::: moniker-end

2. Digite um nome apropriado para a biblioteca de classes, como `MyTestConsole` e clique em **Criar** ou **OK.**

   Agora, você deve adicionar as referências necessárias para que MyTestConsole possa chamar MyFirstVisualizer.

### <a name="to-add-necessary-references-to-mytestconsole"></a>Para adicionar as referências necessárias a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **MyTestConsole** e, no menu de atalho, clique em **Adicionar Referência**.

2. Na caixa **de diálogo** Adicionar Referência, na **guia Procurar,** clique em Microsoft.VisualStudio.DebuggerVisualizers.

3. Clique em **OK**.

4. Clique com o botão direito do mouse em **MyTestConsole** e, em seguida, clique em **Adicionar Referência** novamente.

5. Na caixa de diálogo **Adicionar Referência**, clique na guia **Projetos** e, em seguida, selecione MyFirstVisualizer.

6. Clique em **OK**.

## <a name="finish-your-test-harness-and-test-your-visualizer"></a>Conclua seu agente de teste e teste o visualizador
 Agora, você adicionará o código para concluir um teste automatizado.

### <a name="to-add-code-to-mytestconsole"></a>Para adicionar código a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Program.vb** e, no menu de atalho, clique em **Renomear**.

2. Edite o nome de Module1.vb para algo apropriado, como **TestConsole.vb**.

    Observe que o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] automaticamente altera a declaração de classes em TestConsole.vb para corresponder ao novo nome do arquivo.

3. Em TestConsole. VB, adicione a seguinte `Imports` instrução:

   ```vb
   Imports MyFirstVisualizer
   ```

4. No método `Main`, adicione o seguinte código:

   ```vb
   Dim myString As String = "Hello, World"
   DebuggerSide.TestShowVisualizer(myString)
   ```

   Agora, você está pronto para testar seu primeiro visualizador.

### <a name="to-test-the-visualizer"></a>Para testar o visualizador

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **MyTestConsole** e, no menu de atalho, clique em **Definir como Projeto de Inicialização**.

2. No menu **Depurar** , clique em **Iniciar**.

    O aplicativo de console é iniciado. O visualizador aparece e exibe a cadeia de caracteres “Hello, World”.

   Parabéns. Você acabou de criar e testar seu primeiro visualizador.

   Se você quiser usar o visualizador no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em vez de apenas chamá-lo do teste automatizado, será preciso instalá-lo. Para obter mais informações, consulte [como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md).

## <a name="see-also"></a>Confira também

- [Arquitetura do Visualizador](../debugger/visualizer-architecture.md)
- [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)