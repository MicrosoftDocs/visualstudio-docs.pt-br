---
title: Escrever um visualizador em C# | Microsoft Docs
ms.custom: seodec18
ms.date: 05/27/2020
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: 53467461-8e0f-45ee-9bc4-374bbaeaf00f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: b3b8a67d1b01d7f3a3ada7b391423676b9294e8d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286295"
---
# <a name="walkthrough-writing-a-visualizer-in-c"></a>Instruções passo a passo: escrevendo um visualizador em C\#

Este passo a passo mostra como escrever um visualizador simples usando C#. O visualizador que você criará neste passo a passo exibe o conteúdo de uma cadeia de caracteres usando uma caixa de mensagem do Windows Forms. Esse visualizador simples de cadeia de caracteres não é especialmente útil em si mesmo, mas mostra as etapas básicas a seguir para criar visualizadores mais úteis para outros tipos de dados.

> [!NOTE]
> As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar as configurações, vá para o menu **Ferramentas** e escolha **Importar e Exportar Configurações**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

O código do visualizador deve ser colocado em uma DLL, que será lido pelo depurador. Consequentemente, a primeira etapa é criar um projeto da Biblioteca de Classes para a DLL.

## <a name="create-a-visualizer-manually"></a>Criar um visualizador manualmente

Siga as tarefas abaixo para criar um visualizador.

### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe

1. Crie um novo projeto de biblioteca de classes.

    ::: moniker range=">=vs-2019"
    Pressione **Esc** para fechar a janela de início. Digite **Ctrl + Q** para abrir a caixa de pesquisa, **digite biblioteca de classes**, escolha **modelos**e, em seguida, escolha **criar uma nova biblioteca de classes (.NET Framework)**. Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , em **Visual C#**, escolha **.NET Framework**e, no painel central, escolha **biblioteca de classes (.NET Framework)**.
    ::: moniker-end

2. Digite um nome apropriado para a biblioteca de classes, como `MyFirstVisualizer` e clique em **criar** ou em **OK**.

   Depois de ter criado a biblioteca de classes, você deverá adicionar uma referência a Microsoft.VisualStudio.DebuggerVisualizers.DLL de forma que possa usar as classes definidas nela. Antes de adicionar a referência, no entanto, você deverá renomear algumas classes de modo que tenham nomes significativos.

### <a name="to-rename-class1cs-and-add-microsoftvisualstudiodebuggervisualizers"></a>Para renomear Class1.cs e adicionar Microsoft.VisualStudio.DebuggerVisualizers

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em Class1.cs e escolha **Renomear** no menu de atalho.

2. Altere o nome de Class1.cs para algo significativo, por exemplo, DebuggerSide.cs.

   > [!NOTE]
   > O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] automaticamente altera a declaração de classes em DebuggerSide.cs para corresponder ao novo nome do arquivo.

3. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e escolha **Adicionar Referência** no menu de atalho.

4. Na caixa de diálogo **Adicionar referência** , na guia **procurar** , selecione **procurar** e localize o Microsoft.VisualStudio.DebuggerVisualizers.DLL.

    Você pode encontrar a DLL no subdiretório * \<Visual Studio Install Directory> \Common7\IDE\PublicAssemblies* do diretório de instalação do Visual Studio.

5. Clique em **OK**.

6. No DebuggerSide.cs, adicione o seguinte às `using` diretivas:

   ```csharp
   using Microsoft.VisualStudio.DebuggerVisualizers;
   ```

   Agora você está pronto para criar o código do lado do depurador. Este é o código executado no depurador para exibir as informações que você deseja visualizar. Primeiro, você tem que alterar a declaração do objeto `DebuggerSide` de forma que ele herde da classe base `DialogDebuggerVisualizer`.

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>Para herdar de DialogDebuggerVisualizer

1. Em DebuggerSide.cs, vá para a seguinte linha de código:

   ```csharp
   public class DebuggerSide
   ```

2. Altere o código para:

   ```csharp
   public class DebuggerSide : DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` tem um método abstrato (`Show`) que você deve substituir.

#### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>Para substituir o método DialogDebuggerVisualizer.Show

- No `public class DebuggerSide` , adicione o seguinte **método:**

  ```csharp
  protected override void Show(IDialogVisualizerService windowService, IVisualizerObjectProvider objectProvider)
  {
  }
  ```

  O método `Show` contém o código que realmente cria a caixa de diálogo DO visualizador ou outra interface de usuário e exibe as informações que foram passadas para o visualizador do depurador. Adicione o código que cria a caixa de diálogo e exibe as informações. Neste passo a passo, você fará isso usando uma caixa de mensagem do Windows Forms. Primeiro, você deve adicionar uma referência e uma `using` diretiva para System. Windows. Forms.

### <a name="to-add-systemwindowsforms"></a>Para adicionar System.Windows.Forms

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e escolha **Adicionar Referência** no menu de atalho.

2. Na caixa de diálogo **Adicionar referência** , na guia **procurar** , selecione **procurar**e localize o System.Windows.Forms.DLL.

    Você pode encontrar a DLL em *C:\Windows\Microsoft.NET\Framework\v4.0.30319*.

3. Clique em **OK**.

4. No DebuggerSide.cs, adicione o seguinte às `using` diretivas:

   ```csharp
   using System.Windows.Forms;
   ```

   Agora, você adicionará um código para criar e exibir a interface de usuário para o visualizador. Como esse é o primeiro visualizador, manteremos a interface do usuário simples e usaremos uma caixa de mensagem.

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>Para mostrar a saída do visualizador em uma caixa de diálogo

1. No método `Show`, adicione a linha de código a seguir:

   ```csharp
   MessageBox.Show(objectProvider.GetObject().ToString());
   ```

    Esse código de exemplo não inclui tratamento de erros. Você deve incluir o tratamento de erros em um visualizador real ou qualquer outro tipo de aplicativo.

2. No menu **Compilar**, escolha **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

   Esse é o final do código do lado do depurador. Há mais uma etapa, porém; o atributo que diz ao lado a ser depurado qual coleção de classes integra o visualizador.

### <a name="to-add-the-type-to-visualize-for-the-debuggee-side-code"></a>Para adicionar o tipo a ser visualizado para o código do lado do depurador

No código do lado do depurador, você especifica o tipo a ser visualizado (a origem do objeto) para o depurado usando o <xref:System.Diagnostics.DebuggerVisualizerAttribute> atributo. A `Target` propriedade define o tipo a ser visualizado.

1. Adicione o seguinte código de atributo a DebuggerSide.cs, após as `using` diretivas, mas antes de `namespace MyFirstVisualizer` :

   ```csharp
   [assembly:System.Diagnostics.DebuggerVisualizer(
   typeof(MyFirstVisualizer.DebuggerSide),
   typeof(VisualizerObjectSource),
   Target = typeof(System.String),
   Description = "My First Visualizer")]
   ```

2. No menu **Compilar**, escolha **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

   Neste momento, o primeiro visualizador é concluído. Se você seguiu as etapas corretamente, poderá compilar o visualizador e instalá-lo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Antes de instalar um visualizador no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], no entanto, você deverá testá-lo para garantir que seja executado corretamente. Agora você criará um teste automatizado para executar o visualizador sem instalá-lo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>Para adicionar um método de teste para mostrar o visualizador

1. Adicione o método a seguir à classe `public DebuggerSide`.

   ```csharp
   public static void TestShowVisualizer(object objectToVisualize)
   {
      VisualizerDevelopmentHost visualizerHost = new VisualizerDevelopmentHost(objectToVisualize, typeof(DebuggerSide));
      visualizerHost.ShowVisualizer();
   }
   ```

2. No menu **Compilar**, escolha **Compilar MyFirstVisualizer**. O projeto deve ser compilado com êxito. Corrija os erros de compilação antes de continuar.

   Em seguida, você deverá criar um projeto executável para chamar sua DLL do visualizador. Para simplificar, usaremos um projeto de aplicativo de console.

### <a name="to-add-a-console-application-project-to-the-solution"></a>Para adicionar um projeto de aplicativo de console à solução

1. Em Gerenciador de Soluções, clique com o botão direito do mouse na solução, escolha **Adicionar**e clique em **novo projeto**.

    ::: moniker range=">=vs-2019"
    Na caixa de pesquisa, digite **aplicativo de console**, escolha **modelos**e, em seguida, escolha **criar um novo aplicativo de console (.NET Framework)**. Na caixa de diálogo que aparece, escolha **Criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual C#**, escolha **Área de Trabalho do Windows** e, em seguida, no painel central, escolha **Aplicativo de Console (.NET Framework)**.
    ::: moniker-end

2. Digite um nome apropriado para a biblioteca de classes, como `MyTestConsole` e clique em **criar** ou em **OK**.

   Agora, você deve adicionar as referências necessárias para que MyTestConsole possa chamar MyFirstVisualizer.

### <a name="to-add-necessary-references-to-mytestconsole"></a>Para adicionar as referências necessárias a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **MyTestConsole** e escolha **Adicionar Referência** no menu de atalho.

2. Na caixa de diálogo **Adicionar referência** , guia **procurar** , escolha Microsoft.VisualStudio.DebuggerVisualizers.DLL.

3. Clique em **OK**.

4. Clique com o botão direito do mouse em **MyTestConsole** e escolha **Adicionar Referência** novamente.

5. Na caixa de diálogo **Adicionar Referência**, clique na guia **Projetos** e clique em MyFirstVisualizer.

6. Clique em **OK**.

   Agora, você adicionará o código para concluir um teste automatizado.

### <a name="to-add-code-to-mytestconsole"></a>Para adicionar código a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em Program.cs e escolha **Renomear** no menu de atalho.

2. Edite o nome de Program.cs para algo mais significativo, por exemplo, TestConsole.cs.

    > [!NOTE]
    > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]altera automaticamente a declaração de classe em TestConsole.cs para corresponder ao novo nome de arquivo.

3. No TestConsole.cs, adicione o seguinte código às `using` diretivas:

   ```csharp
   using MyFirstVisualizer;
   ```

4. No método `Main`, adicione o seguinte código:

   ```csharp
   String myString = "Hello, World";
   DebuggerSide.TestShowVisualizer(myString);
   ```

   Agora, você está pronto para testar seu primeiro visualizador.

### <a name="to-test-the-visualizer"></a>Para testar o visualizador

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **MyTestConsole** e escolha **Definir como Projeto de Inicialização** no menu de atalho.

2. No menu **depurar** , escolha **Iniciar**.

    O aplicativo de console inicia e o visualizador aparece e exibe a cadeia de caracteres “Hello World”.

   Parabéns! Você acabou de criar e testar seu primeiro visualizador.

   Se você quiser usar o visualizador no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em vez de apenas chamá-lo do teste automatizado, será preciso instalá-lo. Para obter mais informações, consulte [como: instalar um visualizador](../debugger/how-to-install-a-visualizer.md).

::: moniker range="vs-2017"

## <a name="create-a-visualizer-using-the-visualizer-item-template"></a>Criar um visualizador usando o modelo de item do Visualizador

Até agora, este passo a passo mostrou como criar um visualizador manualmente. Isto foi feito como um exercício de aprendizado. Agora que você sabe como um visualizador simples funciona, há uma forma mais fácil de criar um: usando o modelo de item do visualizador.

Primeiro, você precisará criar um novo projeto de biblioteca de classes.

### <a name="to-create-a-new-class-library"></a>Para criar uma nova biblioteca de classes

1. No menu **arquivo** , escolha **novo projeto de >**.

2. Na caixa de diálogo **novo projeto** , em **Visual C#**, selecione **.NET Framework**.

3. No painel central, escolha **biblioteca de classes**.

4. Na caixa **Nome**, digite um nome apropriado para a biblioteca de classes, por exemplo, MySecondVisualizer.

5. Clique em **OK**.

   Agora, você pode adicionar um item de visualizador a ele:

### <a name="to-add-a-visualizer-item"></a>Para adicionar um item de visualizador

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em MySecondVisualizer.

2. No menu de atalho, escolha **Adicionar** e clique em **Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , em **itens do Visual C#**, selecione **Visualizador do depurador**.

4. Na caixa **Nome**, digite um nome apropriado, por exemplo, SecondVisualizer.cs.

5. Clique em **Adicionar**.

   É tudo que se precisa. Examine o arquivo SecondVisualizer.cs e exiba o código que o modelo adicionou para você. Agora tente com o código. Agora que você conhece as noções básicas, está em condições de criar visualizadores mais complexos e úteis.
::: moniker-end

## <a name="see-also"></a>Veja também

- [Arquitetura do visualizador](../debugger/visualizer-architecture.md)
- [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)
