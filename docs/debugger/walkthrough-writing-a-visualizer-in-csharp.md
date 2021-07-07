---
title: Escrever um visualizador em C# | Microsoft Docs
description: Siga um passo a passos para criar um visualizador simples em C#. Ele mostra as etapas necessárias com e sem usar o modelo de item do visualizador.
ms.custom: SEO-VS-2020
ms.date: 07/02/2021
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: 53467461-8e0f-45ee-9bc4-374bbaeaf00f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 47c7fa8eaa5a735f05b338101a1aefe0601e9915
ms.sourcegitcommit: 4cd3eb514e9fa48e586279e38fe7c2e111ebb304
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2021
ms.locfileid: "113298265"
---
# <a name="walkthrough-writing-a-visualizer-in-c"></a>Instruções passo a passo: escrevendo um visualizador em C\#

Este passo a passo mostra como escrever um visualizador simples usando C#. o visualizador que você criará neste passo a passos exibe o conteúdo de uma cadeia de caracteres usando um formulário de Windows. Esse visualizador simples de cadeia de caracteres não é especialmente útil em si mesmo, mas mostra as etapas básicas a seguir para criar visualizadores mais úteis para outros tipos de dados.

> [!NOTE]
> As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar as configurações, vá para o menu **Ferramentas** e escolha **Importar e Exportar Configurações**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

O código do visualizador deve ser colocado em uma DLL, que será lido pelo depurador. Consequentemente, a primeira etapa é criar um projeto da Biblioteca de Classes para a DLL.

## <a name="create-a-visualizer-manually"></a>Criar um visualizador manualmente

Siga as tarefas abaixo para criar um visualizador.

### <a name="to-create-a-class-library-project"></a>Para criar um projeto de biblioteca de classe

* Crie um novo projeto de biblioteca de classes.

    ::: moniker range=">=vs-2019"
    escolha **arquivo**  >  **novo**  >  **Project**. Na lista suspensa idioma, escolha **C#**. Na caixa de pesquisa, digite **biblioteca de classes** e escolha **biblioteca de classes (.NET Framework)**. Clique em **Próximo**. Na caixa de diálogo exibida, digite o nome `MyFirstVisualizer` e clique em **criar**.

    para o projeto do visualizador, certifique-se de selecionar um .NET Framework biblioteca de classes e não .net. embora o visualizador precise ser .NET Framework, o aplicativo de chamada pode ser .net Core.
    ::: moniker-end
    ::: moniker range="vs-2017"
    na barra de menus superior, escolha **arquivo**  >  **novo**  >  **Project**. no painel esquerdo da caixa de diálogo **novo projeto** , em **Visual C#**, escolha **.NET Framework** e, no painel central, escolha **biblioteca de classes (.NET Framework)**.

    Digite um nome apropriado para a biblioteca de classes, como `MyFirstVisualizer` e clique em **criar** ou em **OK**.
    ::: moniker-end

   Depois de ter criado a biblioteca de classes, você deverá adicionar uma referência a Microsoft.VisualStudio.DebuggerVisualizers.DLL de forma que possa usar as classes definidas nela. Antes de adicionar a referência, no entanto, você deverá renomear algumas classes de modo que tenham nomes significativos.

### <a name="to-rename-class1cs-and-add-microsoftvisualstudiodebuggervisualizers"></a>Para renomear Class1.cs e adicionar Microsoft.VisualStudio.DebuggerVisualizers

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em Class1.cs e escolha **Renomear** no menu de atalho.

2. Altere o nome de Class1.cs para algo significativo, por exemplo, DebuggerSide.cs.

   > [!NOTE]
   > O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] automaticamente altera a declaração de classes em DebuggerSide.cs para corresponder ao novo nome do arquivo.

3. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e escolha **Adicionar Referência** no menu de atalho.

4. Na caixa de diálogo **Adicionar referência** , na guia **procurar** , selecione **procurar** e localize o Microsoft.VisualStudio.DebuggerVisualizers.DLL.

    você pode encontrar a DLL no subdiretório *\<Visual Studio Install Directory> \Common7\IDE\PublicAssemblies* do diretório de instalação do Visual Studio.

5. Clique em **OK**.

6. No DebuggerSide. cs, adicione o seguinte às `using` diretivas:

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

  O método `Show` contém o código que realmente cria a caixa de diálogo DO visualizador ou outra interface de usuário e exibe as informações que foram passadas para o visualizador do depurador. Adicione o código que cria a caixa de diálogo e exibe as informações. Neste passo a passo, você fará isso usando uma caixa de mensagem do Windows Forms. Primeiro, você deve adicionar uma referência e uma `using` diretiva para System. Windows. Formas.

### <a name="to-add-systemwindowsforms"></a>Para adicionar System.Windows.Forms

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Referências** e escolha **Adicionar Referência** no menu de atalho.

2. Na caixa de diálogo **Adicionar referência** , na guia **procurar** , selecione **procurar** e localize o System.Windows.Forms.DLL.

    você pode encontrar a DLL em *C:\ Windows \Microsoft.NET\Framework\v4.0.30319*.

3. Clique em **OK**.

4. No DebuggerSide. cs, adicione o seguinte às `using` diretivas:

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

1. Adicione o seguinte código de atributo a DebuggerSide. cs, após as `using` diretivas, mas antes de `namespace MyFirstVisualizer` :

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

   Em seguida, você deverá criar um projeto executável para chamar sua DLL do visualizador. Para simplificar, use um projeto de aplicativo de console.

### <a name="to-add-a-console-application-project-to-the-solution"></a>Para adicionar um projeto de aplicativo de console à solução

1. Em Gerenciador de Soluções, clique com o botão direito do mouse na solução, escolha **Adicionar** e, em seguida, clique em **novo Project**.

    ::: moniker range=">=vs-2019"

    escolha **arquivo**  >  **novo**  >  **Project**. Na lista suspensa idioma, escolha **C#**. na caixa de pesquisa, digite **aplicativo de console** e, em seguida, selecione aplicativo de **console (.NET Framework)** ou **aplicativo de console** para .net. Clique em **Próximo**. Na caixa de diálogo exibida, digite o nome `MyTestConsole` e clique em **criar**.

    > [!NOTE]
    > se você quiser testar facilmente o visualizador usando um equipamento de teste, crie um aplicativo de console .NET Framework. Em vez disso, você pode criar um aplicativo de console .NET, mas o conjunto de teste descrito posteriormente ainda não tem suporte para .NET, portanto, você precisará instalar o visualizador para testá-lo. Para este cenário, primeiro crie o aplicativo de console aqui e siga as etapas descritas em [Adicionar um objeto de dados do lado do depurador](#add-a-debuggee-side-data-object).
    ::: moniker-end
    ::: moniker range="vs-2017"
    na barra de menus superior, escolha **arquivo**  >  **novo**  >  **Project**. No painel esquerdo da caixa de diálogo **Novo projeto**, em **Visual C#**, escolha **Área de Trabalho do Windows** e, em seguida, no painel central, escolha **Aplicativo de Console (.NET Framework)**.

    Digite um nome apropriado para a biblioteca de classes, como `MyTestConsole` e clique em **OK**.
    ::: moniker-end

   Agora, você deve adicionar as referências necessárias para que MyTestConsole possa chamar MyFirstVisualizer.

### <a name="to-add-necessary-references-to-mytestconsole"></a>Para adicionar as referências necessárias a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **MyTestConsole** e escolha **Adicionar Referência** no menu de atalho.

2. Na caixa **de diálogo Adicionar** Referência, **guia** Procurar, escolha Microsoft.VisualStudio.DebuggerVisualizers.DLL.

3. Clique em **OK**.

4. Clique com o botão direito do mouse em **MyTestConsole** e escolha **Adicionar Referência** novamente.

5. Na caixa de diálogo **Adicionar Referência**, clique na guia **Projetos** e clique em MyFirstVisualizer.

6. Clique em **OK**.

   Agora, você adicionará o código para concluir um teste automatizado.

### <a name="to-add-code-to-mytestconsole"></a>Para adicionar código a MyTestConsole

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em Program.cs e escolha **Renomear** no menu de atalho.

2. Edite o nome de Program.cs para algo mais significativo, por exemplo, TestConsole.cs.

    > [!NOTE]
    > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] altera automaticamente a declaração de classe em TestConsole.cs para corresponder ao novo nome de arquivo.

3. Em TestConsole.cs, adicione o seguinte código às `using` diretivas:

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

2. No menu **Depurar,** escolha **Iniciar**.

    O aplicativo de console inicia e o visualizador aparece e exibe a cadeia de caracteres “Hello World”.

   Parabéns. Você acabou de construir e testar seu primeiro visualizador!

   Se você quiser usar o visualizador no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em vez de apenas chamá-lo do teste automatizado, será preciso instalá-lo. Para obter mais informações, [consulte Como instalar um visualizador.](../debugger/how-to-install-a-visualizer.md)

::: moniker range=">=vs-2019"
## <a name="add-a-debuggee-side-data-object"></a>Adicionar um objeto de dados do lado do rodo de depuração

Nesta seção, você alterna do objeto `System.String` de dados para um objeto de dados personalizado.  

1. Escolha **Arquivo**  >  **Novo**  >  **Project**. Na lista de idiomas, escolha **C#**. Na caixa de pesquisa, digite **biblioteca de** classes e escolha Biblioteca de Classes **(.NET Framework)** ou Biblioteca de Classes **para** .NET Standard.

   >[!NOTE]
   >Se você estiver usando um .NET Framework de console de teste, crie um projeto .NET Framework biblioteca de classes.

1. Clique em **Próximo**. Na caixa de diálogo exibida, digite o nome `MyDataObject` e clique em **Criar**.

1. (.NET Standard biblioteca de classes) No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e **escolha Editar Project Arquivo**. Altere `<TargetFramework>` o valor para `netstandard2.0` .

1. Dentro do `MyDataObject` namespace, substitua o código padrão pelo código a seguir.

   ```csharp
   [Serializable] 
   public class CustomDataObject
   {
      public CustomDataObject()
      {
         this.MyData = "MyTestData";
      }
      public string MyData { get; set; }
   }
   ```

   Para um visualizador somente leitura, como neste exemplo, não é necessário implementar métodos de [VisualizerObjectSource](/dotnet/api/microsoft.visualstudio.debuggervisualizers.visualizerobjectsource).

   Em seguida, atualize o projeto MyFirstVisualizer para usar o novo objeto de dados.

1. No Gerenciador de Soluções no projeto MyFirstVisualizer, clique com  o botão direito do mouse no nó Referências e escolha **Adicionar Referência**.

1. Em **Projetos,** selecione o **projeto MyDataObject.**

1. No código de atributo de DebuggerSide.cs, atualize o valor de Destino, alterando `System.String` para `MyDataObject.CustomDataObject` .

   ```csharp
   Target = typeof(MyDataObject.CustomDataObject),
   ```

1. No projeto MyFirstVisualizer, substitua o código do `Show` método pelo código a seguir.

   ```csharp
   var data = objectProvider.GetObject() as MyDataObject.CustomDataObject;

   // You can replace displayForm with your own custom Form or Control.  
   Form displayForm = new Form();
   displayForm.Text = data.MyData;
   windowService.ShowDialog(displayForm);
   ```

   O código anterior usa uma propriedade do objeto de dados para mostrar no título do formulário.

   Em seguida, atualize o aplicativo de console para usar o objeto de dados personalizado.

1. No Gerenciador de Soluções no projeto MyTestConsole, clique com o  botão direito do mouse no nó Referências ou **Dependências** e adicione uma referência de projeto a `MyDataObject` .

1. Em Program.cs, substitua o código no `Main` método pelo código a seguir.

   ```csharp
   // String myString = "Hello, World";
   CustomDataObject customDataObject = new CustomDataObject();

   DebuggerSide.TestShowVisualizer(customDataObject.MyData);
   ```

1. (Aplicativo de console do .NET) Coloque a chamada para `TestShowVisualizer` em uma instrução try-catch, pois não há suporte para o harness de teste.

   ```csharp
   try
   {
         DebuggerSide.TestShowVisualizer(customDataObject.MyData);
   }
   catch (Exception) {
   }
   ```

   O depurador precisa de uma referência ao visualizador. Uma maneira de manter a referência é manter o código anterior em uso.

1. Para um .NET Framework de console, você pode executar o harness de teste (pressione **F5**) ou pode seguir as instruções em Como [instalar um visualizador](../debugger/how-to-install-a-visualizer.md).

   Se você executar o aplicativo usando o harness de teste, o aplicativo mostrará o Windows Formulário.

1. Para um aplicativo de console do .NET, copie o e o para as pastas descritas em `MyFirstVisualizer.dll` Como instalar um `MyDataObject.dll` [visualizador.](../debugger/how-to-install-a-visualizer.md)

1. Depois de instalar o visualizador, de definir um ponto de interrupção, execute o aplicativo de console e passe o mouse sobre `customDataObject` . Se tudo estiver definido corretamente, você deverá ver o ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "Ícone do visualizador").

   :::image type="content" source="../debugger/media/vs-2019/visualizer-csharp-data-object.png" alt-text="Ícone de lupa do visualizador.":::

   Ao escolher **MyFirstVisualizer** na lupa, você verá o Formulário com o texto do objeto de dados no título.

   ![Visualizador mostrando um formulário Windows dados](../debugger/media/vs-2019/visualizer-csharp-windows-form.png)

::: moniker-end

::: moniker range="vs-2017"

## <a name="create-a-visualizer-using-the-visualizer-item-template"></a>Criar um visualizador usando o modelo de item visualizador

Até agora, este passo a passo mostrou como criar um visualizador manualmente. Isto foi feito como um exercício de aprendizado. Agora que você sabe como um visualizador simples funciona, há uma forma mais fácil de criar um: usando o modelo de item do visualizador.

Primeiro, você precisará criar um novo projeto de biblioteca de classes.

### <a name="to-create-a-new-class-library"></a>Para criar uma nova biblioteca de classes

1. No menu **Arquivo,** escolha **Novo > Project**.

2. Na caixa **de diálogo Project,** em **Visual C#,** selecione **.NET Framework**.

3. No painel central, escolha Biblioteca **de Classes**.

4. Na caixa **Nome**, digite um nome apropriado para a biblioteca de classes, por exemplo, MySecondVisualizer.

5. Clique em **OK**.

   Agora, você pode adicionar um item de visualizador a ele:

### <a name="to-add-a-visualizer-item"></a>Para adicionar um item de visualizador

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse em MySecondVisualizer.

2. No menu de atalho, escolha **Adicionar** e clique em **Novo Item**.

3. Na caixa **de diálogo Adicionar Novo Item,** em Itens do Visual **C#,** selecione **Visualizador do Depurador**.

4. Na caixa **Nome**, digite um nome apropriado, por exemplo, SecondVisualizer.cs.

5. Clique em **Adicionar**.

   É tudo que se precisa. Examine o arquivo SecondVisualizer.cs e exiba o código que o modelo adicionou para você. Agora tente com o código. Agora que você conhece as noções básicas, está em condições de criar visualizadores mais complexos e úteis.
::: moniker-end

## <a name="see-also"></a>Confira também

- [Arquitetura do visualizador](../debugger/visualizer-architecture.md)
- [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)
