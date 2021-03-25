---
title: Estender Propriedades, Lista de Tarefas, saída, janelas de opções
description: Saiba como integrar informações sobre sua janela de ferramentas no Visual Studio em uma nova página de opções e uma nova configuração na página Propriedades.
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 970ab167434da4ba9c28eb6bbf9a8ea5f6cc6af0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070135"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>Estenda as propriedades, Lista de Tarefas, saída e opções do Windows
Você pode acessar qualquer janela de ferramentas no Visual Studio. Este tutorial mostra como integrar informações sobre a janela da ferramenta em uma nova página **Opções** e uma nova configuração na página **Propriedades** e também como gravar nas janelas **lista de tarefas** e **saída** .

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-an-extension-with-a-tool-window"></a>Criar uma extensão com uma janela de ferramentas

1. Crie um projeto chamado **ToDoList** usando o modelo VSIX e adicione um modelo de item de janela de ferramenta personalizada chamado **TodoWindow**.

    > [!NOTE]
    > Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

## <a name="set-up-the-tool-window"></a>Configurar a janela de ferramentas
 Adicione uma caixa de texto na qual você deseja digitar um novo item de tarefas pendentes, um botão para adicionar o novo item à lista e uma caixa de listagem para exibir os itens na lista.

1. Em *TodoWindow. XAML*, exclua os controles Button, TextBox e StackPanel do UserControl.

    > [!NOTE]
    > Isso não exclui o manipulador de eventos **Button1_Click** , que será reutilizado em uma etapa posterior.

2. Na seção **todos os controles do WPF** da **caixa de ferramentas**, arraste um controle **Canvas** para a grade.

3. Arraste uma **caixa de texto**, um **botão** e um **ListBox** para a tela. Organize os elementos para que a caixa de texto e o botão estejam no mesmo nível e a ListBox preencha o restante da janela abaixo deles, como na imagem abaixo.

     ![Janela de ferramentas concluída](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. No painel XAML, localize o botão e defina sua propriedade Content para **Adicionar**. Reconecte o manipulador de eventos de botão ao controle de botão adicionando um `Click="button1_Click"` atributo. O bloco Canvas deve ser assim:

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>Personalizar o Construtor

1. No arquivo *TodoWindowControl. XAML. cs* , adicione o seguinte usando a diretiva:

    ```csharp
    using System;
    ```

2. Adicione uma referência pública ao TodoWindow e faça com que o Construtor TodoWindowControl use um parâmetro TodoWindow. Seu código deve ficar assim:

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. No *TodoWindow. cs*, altere o Construtor TodoWindowControl para incluir o parâmetro TodoWindow. Seu código deve ficar assim:

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>Criar uma página de opções
 Você pode fornecer uma página na caixa de diálogo **Opções** para que os usuários possam alterar as configurações da janela de ferramentas. A criação de uma página de opções requer uma classe que descreva as opções e uma entrada no arquivo *TodoListPackage. cs* ou *TodoListPackage. vb* .

1. Adicione uma classe chamada `ToolsOptions.cs`. Faça a `ToolsOptions` herança da classe <xref:Microsoft.VisualStudio.Shell.DialogPage> .

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. Adicione o seguinte usando a orientação:

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. A página opções neste passo a passo fornece apenas uma opção chamada DaysAhead. Adicione um campo particular chamado **daysAhead** e uma propriedade chamada **daysAhead** à `ToolsOptions` classe:

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   Agora você deve fazer com que o projeto reconheça essa página de opções.

### <a name="make-the-options-page-available-to-users"></a>Tornar a página de opções disponível para os usuários

1. Em *TodoWindowPackage. cs*, adicione um <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> à `TodoWindowPackage` classe:

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. O primeiro parâmetro para o Construtor ProvideOptionPage é o tipo da classe `ToolsOptions` , que você criou anteriormente. O segundo parâmetro, "ToDo", é o nome da categoria na caixa de diálogo **Opções** . O terceiro parâmetro, "General", é o nome da subcategoria da caixa de diálogo **Opções** em que a página opções estará disponível. Os dois parâmetros seguintes são IDs de recurso para cadeias de caracteres; o primeiro é o nome da categoria e o segundo é o nome da subcategoria. O parâmetro final determina se essa página pode ser acessada usando a automação.

     Quando um usuário abre a página de opções, ele deve ser semelhante à imagem a seguir.

     ![Página Opções](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     Observe a categoria **todo** e a subcategoria **geral**.

## <a name="make-data-available-to-the-properties-window"></a>Tornar os dados disponíveis para o janela Propriedades
 Você pode disponibilizar as informações da lista de tarefas criando uma classe denominada `TodoItem` que armazena informações sobre os itens individuais na lista de tarefas.

1. Adicione uma classe chamada `TodoItem.cs`.

     Quando a janela de ferramentas estiver disponível para os usuários, os itens na caixa de listagem serão representados por TodoItems. Quando o usuário seleciona um desses itens na caixa de listagem, a janela **Propriedades** exibirá informações sobre o item.

     Para disponibilizar dados na janela **Propriedades** , você transforma os dados em propriedades públicas que têm dois atributos especiais `Description` e `Category` . `Description` é o texto que aparece na parte inferior da janela **Propriedades** . `Category` determina onde a propriedade deve aparecer quando a janela **Propriedades** é exibida na exibição **categorizada** . Na imagem a seguir, a janela **Propriedades** está no modo de exibição **Categorizado** , a propriedade **nome** na categoria **campos de tarefas** está selecionada e a descrição da propriedade **nome** é exibida na parte inferior da janela.

     ![Janela Propriedades](../extensibility/media/t5properties.png "T5Properties")

2. Adicione o seguinte usando as diretivas do arquivo *TodoItem. cs* .

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. Adicione o `public` modificador de acesso à declaração de classe.

    ```csharp
    public class TodoItem
    {
    }
    ```

     Adicione as duas propriedades `Name` e `DueDate` . Faremos o `UpdateList()` e `CheckForErrors()` posterior.

    ```csharp
    public class TodoItem
    {
        private TodoWindowControl parent;
        private string name;
        [Description("Name of the ToDo item")]
        [Category("ToDo Fields")]
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                parent.UpdateList(this);
            }
        }

        private DateTime dueDate;
        [Description("Due date of the ToDo item")]
        [Category("ToDo Fields")]
        public DateTime DueDate
        {
            get { return dueDate; }
            set
            {
                dueDate = value;
                parent.UpdateList(this);
                parent.CheckForErrors();
            }
        }
    }
    ```

4. Adicione uma referência privada ao controle de usuário. Adicione um construtor que usa o controle de usuário e o nome para este item de tarefas. Para localizar o valor de `daysAhead` , ele obtém a propriedade de página de opções.

    ```csharp
    private TodoWindowControl parent;

    public TodoItem(TodoWindowControl control, string itemName)
    {
        parent = control;
        name = itemName;
        dueDate = DateTime.Now;

        double daysAhead = 0;
        IVsPackage package = parent.parent.Package as IVsPackage;
        if (package != null)
        {
            object obj;
            package.GetAutomationObject("ToDo.General", out obj);

            ToolsOptions options = obj as ToolsOptions;
            if (options != null)
            {
                daysAhead = options.DaysAhead;
            }
        }

        dueDate = dueDate.AddDays(daysAhead);
    }
    ```

5. Como as instâncias da `TodoItem` classe serão armazenadas na caixa de listagem e a caixa de listagem chamará a `ToString` função, você deve sobrecarregar a `ToString` função. Adicione o código a seguir a *TodoItem. cs*, após o construtor e antes do final da classe.

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. Em *TodoWindowControl. XAML. cs*, adicione métodos stub à `TodoWindowControl` classe para os `CheckForError` métodos e `UpdateList` . Coloque-os após ProcessDialogChar e antes do final do arquivo.

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     O `CheckForError` método chamará um método que tem o mesmo nome no objeto pai e esse método verificará se ocorreram erros e tratá-los corretamente. O `UpdateList` método atualizará a caixa de listagem no controle pai; o método é chamado quando `Name` as `DueDate` Propriedades e nessa classe são alteradas. Eles serão implementados mais tarde.

## <a name="integrate-into-the-properties-window"></a>Integre-se ao janela Propriedades
 Agora, escreva o código que gerencia a ListBox, que será vinculada à janela **Propriedades** .

 Você deve alterar o manipulador de clique de botão para ler a caixa de texto, criar um TodoItem e adicioná-lo à ListBox.

1. Substitua a `button1_Click` função existente pelo código que cria um novo TodoItem e o adiciona à caixa de listagem. Ele chama `TrackSelection()` , que será definido mais tarde.

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. No modo de exibição de Design selecione o controle ListBox. Na janela **Propriedades** , clique no botão **manipuladores de eventos** e localize o evento **SelectionChanged** . Preencha a caixa de texto com **listBox_SelectionChanged**. Isso adiciona um stub para um manipulador de SelectionChanged e o atribui ao evento.

3. Implementar o método de `TrackSelection()` . Como você precisará obter os <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> serviços, será necessário tornar o <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> acessível pelo TodoWindowControl. Adicione o seguinte método à classe `TodoWindow`:

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. Adicione as seguintes diretivas using a *TodoWindowControl. XAML. cs*:

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. Preencha o manipulador de SelectionChanged da seguinte maneira:

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. Agora, preencha a função TrackSelection, que fornecerá integração com a janela **Propriedades** . Essa função é chamada quando o usuário adiciona um item à caixa de listagem ou clica em um item na caixa de listagem. Ele adiciona o conteúdo da ListBox a um SelectionContainer e passa o SelectionContainer para o manipulador de eventos da janela de **Propriedades** <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> . O serviço TrackSelection rastreia os objetos selecionados na interface do usuário e exibe suas propriedades

    ```csharp
    private SelectionContainer mySelContainer;
    private System.Collections.ArrayList mySelItems;
    private IVsWindowFrame frame = null;

    private void TrackSelection()
    {
        if (frame == null)
        {
            var shell = parent.GetVsService(typeof(SVsUIShell)) as IVsUIShell;
            if (shell != null)
            {
                var guidPropertyBrowser = new
                Guid(ToolWindowGuids.PropertyBrowser);
                shell.FindToolWindow((uint)__VSFINDTOOLWIN.FTW_fForceCreate,
                ref guidPropertyBrowser, out frame);
            }
        }
        if (frame != null)
            {
                frame.Show();
            }
        if (mySelContainer == null)
        {
            mySelContainer = new SelectionContainer();
        }

        mySelItems = new System.Collections.ArrayList();

        var selected = listBox.SelectedItem as TodoItem;
        if (selected != null)
        {
            mySelItems.Add(selected);
        }

        mySelContainer.SelectedObjects = mySelItems;

        ITrackSelection track = parent.GetVsService(typeof(STrackSelection))
                                as ITrackSelection;
        if (track != null)
        {
            track.OnSelectChange(mySelContainer);
        }
    }
    ```

     Agora que você tem uma classe que a janela **Propriedades** pode usar, você pode integrar a janela **Propriedades** com a janela de ferramentas. Quando o usuário clica em um item na caixa de listagem na janela de ferramentas, a janela **Propriedades** deve ser atualizada de acordo. Da mesma forma, quando o usuário altera um item de tarefas pendentes na janela **Propriedades** , o item associado deve ser atualizado.

7. Agora, adicione o restante do código da função UpdateList em *TodoWindowControl. XAML. cs*. Ele deve descartar e adicionar novamente o TodoItem modificado da caixa de listagem.

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. Teste seu código. Compile o projeto e comece a depuração. A instância experimental deve aparecer.

9. Abra a   >  página **Opções** de ferramentas. Você deve ver a categoria ToDo no painel esquerdo. As categorias são listadas em ordem alfabética, portanto, olhe sob o TS.

10. Na página opções de **tarefas** , você deve ver a `DaysAhead` propriedade definida como **0**. Altere-o para **2**.

11. No menu **Exibir/outras janelas** , abra **TodoWindow**. Digite **EndDate** na caixa de texto e clique em **Adicionar**.

12. Na caixa de listagem, você deve ver uma data dois dias posterior a hoje.

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>Adicionar texto à janela de saída e itens à Lista de Tarefas
 Para o **lista de tarefas**, você cria um novo objeto do tipo tarefa e, em seguida, adiciona esse objeto de tarefa ao **lista de tarefas** chamando seu `Add` método. Para gravar na janela de **saída** , você chama seu `GetPane` método para obter um objeto de painel e, em seguida, chama o `OutputString` método do objeto de painel.

1. Em *TodoWindowControl. XAML. cs*, no `button1_Click` método, adicione o código para obter o painel **geral** da janela de **saída** (que é o padrão) e grave nela. O método deverá ter esta aparência:

    ```csharp
    private void button1_Click(object sender, EventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);

            var outputWindow = parent.GetVsService(
                typeof(SVsOutputWindow)) as IVsOutputWindow;
            IVsOutputWindowPane pane;
            Guid guidGeneralPane = VSConstants.GUID_OutWindowGeneralPane;
            outputWindow.GetPane(ref guidGeneralPane, out pane);
            if (pane != null)
            {
                 pane.OutputString(string.Format(
                    "To Do item created: {0}\r\n",
                 item.ToString()));
        }
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. Para adicionar itens ao Lista de Tarefas, você precisa de um para adicionar uma classe aninhada à classe TodoWindowControl. A classe aninhada precisa derivar de <xref:Microsoft.VisualStudio.Shell.TaskProvider> . Adicione o código a seguir ao final da `TodoWindowControl` classe.

    ```csharp
    [Guid("72de1eAD-a00c-4f57-bff7-57edb162d0be")]
    public class TodoWindowTaskProvider : TaskProvider
    {
        public TodoWindowTaskProvider(IServiceProvider sp)
            : base(sp)
        {
        }
    }
    ```

3. Em seguida, adicione uma referência privada a `TodoTaskProvider` e um `CreateProvider()` método à `TodoWindowControl` classe. Seu código deve ficar assim:

    ```csharp
    private TodoWindowTaskProvider taskProvider;
    private void CreateProvider()
    {
        if (taskProvider == null)
        {
            taskProvider = new TodoWindowTaskProvider(parent);
            taskProvider.ProviderName = "To Do";
        }
    }
    ```

4. Adicionar `ClearError()` , que limpa a lista de tarefas e `ReportError()` , que adiciona uma entrada ao lista de tarefas, à `TodoWindowControl` classe.

    ```csharp
    private void ClearError()
    {
        CreateProvider();
        taskProvider.Tasks.Clear();
    }
    private void ReportError(string p)
    {
        CreateProvider();
        var errorTask = new Task();
        errorTask.CanDelete = false;
        errorTask.Category = TaskCategory.Comments;
        errorTask.Text = p;

        taskProvider.Tasks.Add(errorTask);

        taskProvider.Show();

        var taskList = parent.GetVsService(typeof(SVsTaskList))
            as IVsTaskList2;
        if (taskList == null)
        {
            return;
        }

        var guidProvider = typeof(TodoWindowTaskProvider).GUID;
         taskList.SetActiveProvider(ref guidProvider);
    }
    ```

5. Agora, implemente o `CheckForErrors` método, da seguinte maneira.

    ```csharp
    public void CheckForErrors()
    {
        foreach (TodoItem item in listBox.Items)
        {
            if (item.DueDate < DateTime.Now)
            {
                ReportError("To Do Item is out of date: "
                    + item.ToString());
            }
        }
    }
    ```

## <a name="try-it-out"></a>Experimente

1. Compile o projeto e comece a depuração. A instância experimental é exibida.

2. Abra o **TodoWindow** (**Exibir**  >  **outros**  >  **TodoWindow** do Windows).

3. Digite algo na caixa de texto e clique em **Adicionar**.

     Uma data de vencimento 2 dias depois de hoje é adicionada à caixa de listagem. Nenhum erro é gerado e o **lista de tarefas** (**View**  >  **lista de tarefas**) não deve ter entradas.

4. Agora, altere a configuração na   >    >  página opções de ferramentas **todo** de **2** volta para **0**.

5. Digite outra coisa no **TodoWindow** e clique em **Adicionar** novamente. Isso dispara um erro e também uma entrada no **lista de tarefas**.

     À medida que você adiciona itens, a data inicial é definida como agora mais 2 dias.

6. No menu **Exibir** , clique em **saída** para abrir a janela **saída** .

     Observe que sempre que você adicionar um item, uma mensagem será exibida no painel de **lista de tarefas** .

7. Clique em um dos itens na caixa de listagem.

     A janela **Propriedades** exibe as duas propriedades do item.

8. Altere uma das propriedades e pressione **Enter**.

     O item é atualizado na caixa de listagem.
