---
title: Estender as janelas Propriedades, Lista de Tarefas, Saída, Opções
description: Saiba como integrar informações sobre sua janela de ferramentas Visual Studio em uma nova página Opções e uma nova configuração na página Propriedades.
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: how-to
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
ms.openlocfilehash: 3334ba3694ee3c1354c152b013c38472e4b90b72
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903275"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>Estender as janelas Propriedades, Lista de Tarefas, Saída e Opções
Você pode acessar qualquer janela de ferramentas Visual Studio. Este passo a passo mostra como integrar informações  sobre sua janela de  ferramentas em uma nova página Opções e uma nova configuração na página Propriedades e também como gravar nas janelas **Lista de Tarefas** **e** Saída.

## <a name="prerequisites"></a>Pré-requisitos
 A partir Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele é incluído como um recurso opcional na Visual Studio configuração. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, [consulte Instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-an-extension-with-a-tool-window"></a>Criar uma extensão com uma janela de ferramentas

1. Crie um projeto chamado **TodoList** usando o modelo VSIX e adicione um modelo de item de janela de ferramentas personalizado chamado **TodoWindow**.

    > [!NOTE]
    > Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [Criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

## <a name="set-up-the-tool-window"></a>Configurar a janela de ferramentas
 Adicione uma TextBox na qual digitar um novo item ToDo, um Botão para adicionar o novo item à lista e uma ListBox para exibir os itens na lista.

1. Em *TodoWindow.xaml,* exclua os controles Button, TextBox e StackPanel do UserControl.

    > [!NOTE]
    > Isso não exclui o **button1_Click** de eventos, que você reutilizará em uma etapa posterior.

2. Na seção **Todos os Controles do WPF** da **Caixa de Ferramentas**, arraste um controle **Canvas** para a grade.

3. Arraste uma **Caixa de Texto,** **um Botão** e uma **ListBox** para a Tela. Organize os elementos para que TextBox e o Botão fiquem no mesmo nível e listBox preencha o restante da janela abaixo deles, como na imagem abaixo.

     ![Janela ferramenta concluída](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. No painel XAML, encontre o Botão e defina sua propriedade Content como **Adicionar**. Reconecte o manipulador de eventos de botão ao controle Button adicionando um `Click="button1_Click"` atributo . O bloco Tela deve ter esta aparência:

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>Personalizar o construtor

1. No arquivo *TodoWindowControl.xaml.cs,* adicione a seguinte diretiva using:

    ```csharp
    using System;
    ```

2. Adicione uma referência pública ao TodoWindow e fazer com que o construtor TodoWindowControl tome um parâmetro TodoWindow. Seu código deve ficar assim:

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. Em *TodoWindow.cs,* altere o construtor TodoWindowControl para incluir o parâmetro TodoWindow. Seu código deve ficar assim:

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>Página Criar opções
 Você pode fornecer uma página na caixa **de** diálogo Opções para que os usuários possam alterar as configurações da janela de ferramentas. A criação de uma página Opções requer uma classe que descreve as opções e uma entrada no arquivo *TodoListPackage.cs* *ou TodoListPackage.vb.*

1. Adicione uma classe chamada `ToolsOptions.cs`. Faça a `ToolsOptions` classe herdar de <xref:Microsoft.VisualStudio.Shell.DialogPage> .

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. Adicione o seguinte usando a orientação:

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. A página Opções neste passo a passo fornece apenas uma opção chamada DaysAhead. Adicione um campo privado chamado **daysAhead** e uma propriedade chamada **DaysAhead** à `ToolsOptions` classe :

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   Agora você deve tornar o projeto ciente desta página Opções.

### <a name="make-the-options-page-available-to-users"></a>Disponibilizar a página Opções para os usuários

1. Em *TodoWindowPackage.cs,* adicione um <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> à classe `TodoWindowPackage` :

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. O primeiro parâmetro para o construtor ProvideOptionPage é o tipo da classe `ToolsOptions` , que você criou anteriormente. O segundo parâmetro, "ToDo", é o nome da categoria na caixa **de diálogo** Opções. O terceiro parâmetro, "Geral", é o nome da  subcategoria da caixa de diálogo Opções em que a página Opções estará disponível. Os próximos dois parâmetros são IDs de recurso para cadeias de caracteres; o primeiro é o nome da categoria e o segundo é o nome da subcategoria. O parâmetro final determina se essa página pode ser acessada usando automação.

     Quando um usuário abre a página Opções, ele deve ser semelhante à imagem a seguir.

     ![Página Opções](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     Observe a categoria **ToDo** e a subcategoria **Geral**.

## <a name="make-data-available-to-the-properties-window"></a>Disponibilizar dados para o janela Propriedades
 Você pode disponibilizar informações de lista de ToDo criando uma classe chamada que armazena informações sobre os itens `TodoItem` individuais na lista ToDo.

1. Adicione uma classe chamada `TodoItem.cs`.

     Quando a janela de ferramentas estiver disponível para os usuários, os itens na ListBox serão representados por TodoItems. Quando o usuário selecionar um desses itens na ListBox, a janela **Propriedades** exibirá informações sobre o item.

     Para disponibilizar dados na janela **Propriedades,** você transforma os dados em propriedades públicas que têm dois atributos especiais, `Description` e `Category` . `Description` é o texto que aparece na parte inferior da **janela** Propriedades. `Category`determina onde a propriedade deve aparecer quando a **janela** Propriedades é exibida na **exibição Categorizada.** Na imagem a  seguir, a janela Propriedades  está na exibição **Categorizada,** a propriedade Nome  na categoria Campos **toDo** é selecionada e a descrição da propriedade Nome é exibida na parte inferior da janela.

     ![Janela Propriedades](../extensibility/media/t5properties.png "T5Properties")

2. Adicione as seguintes diretivas using ao *arquivo TodoItem.cs.*

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

     Adicione as duas propriedades e `Name` `DueDate` . Faremos o e `UpdateList()` `CheckForErrors()` posterior.

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

4. Adicione uma referência privada ao controle de usuário. Adicione um construtor que aceita o controle de usuário e o nome desse item ToDo. Para encontrar o valor de `daysAhead` , ele obtém a propriedade da página Opções.

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

5. Como as instâncias da classe serão armazenadas na ListBox e a ListBox chamará a função `TodoItem` `ToString` , você deve sobrecarregar a `ToString` função. Adicione o código a seguir *a TodoItem.cs*, após o construtor e antes do final da classe.

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. Em *TodoWindowControl.xaml.cs,* adicione métodos stub à `TodoWindowControl` classe para os métodos e `CheckForError` `UpdateList` . Coloque-os após ProcessDialogChar e antes do final do arquivo.

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     O método chamará um método que tem o mesmo nome no objeto pai e esse método verificará se ocorreram erros e os tratará `CheckForError` corretamente. O `UpdateList` método atualizará a ListBox no controle pai; o método é chamado quando as propriedades `Name` e nesta classe `DueDate` mudam. Eles serão implementados posteriormente.

## <a name="integrate-into-the-properties-window"></a>Integrar-se ao janela Propriedades
 Agora, escreva o código que gerencia a ListBox, que será vinculada à **janela** Propriedades.

 Você deve alterar o manipulador de cliques do botão para ler a TextBox, criar um TodoItem e adiciona-o à ListBox.

1. Substitua a função existente `button1_Click` pelo código que cria um novo TodoItem e a adiciona à ListBox. Ele chama `TrackSelection()` , que será definido posteriormente.

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

2. No modo de exibição de Design selecione o controle ListBox. Na janela **Propriedades,** clique no **botão Manipuladores de eventos** e encontre o evento **SelectionChanged.** Preencha a caixa de texto com **listBox_SelectionChanged**. Isso adiciona um stub para um manipulador SelectionChanged e o atribui ao evento .

3. Implementar o método de `TrackSelection()` . Como você precisará obter os serviços, você precisará tornar o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> acessível pelo TodoWindowControl. Adicione o seguinte método à classe `TodoWindow`:

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. Adicione o seguinte usando diretivas a *TodoWindowControl.xaml.cs*:

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. Preencha o manipulador SelectionChanged da seguinte forma:

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. Agora, preencha a função TrackSelection, que fornecerá integração com a **janela** Propriedades. Essa função é chamada quando o usuário adiciona um item à ListBox ou clica em um item na ListBox. Ele adiciona o conteúdo da ListBox a um SelectionContainer e  passa o SelectionContainer para o manipulador de eventos da janela <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> Propriedades. O serviço TrackSelection rastreia objetos selecionados na interface do usuário e exibe suas propriedades

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

     Agora que você tem uma classe que a **janela Propriedades** pode usar, você pode integrar a **janela** Propriedades à janela de ferramentas. Quando o usuário clica em um item na ListBox na janela de ferramentas, a **janela** Propriedades deve ser atualizada de acordo. Da mesma forma, quando o usuário altera um item ToDo na **janela Propriedades,** o item associado deve ser atualizado.

7. Agora, adicione o restante do código da função UpdateList em *TodoWindowControl.xaml.cs.* Ele deve soltar e adicionar o TodoItem modificado da ListBox.

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

9. Abra a **página**  >  **Opções de** Ferramentas. Você deverá ver a categoria ToDo no painel esquerdo. As categorias são listadas em ordem alfabética, portanto, procure nos Ts.

10. Na página **Opções** de todo, você deverá ver a `DaysAhead` propriedade definida como **0**. Altere-o **para 2**.

11. No menu **Exibir/Outras Janelas,** abra **TodoWindow.** Digite **EndDate** na caixa de texto e clique em **Adicionar**.

12. Na caixa de listagem, você deverá ver uma data dois dias mais tarde do que hoje.

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>Adicione texto à janela Saída e itens ao Lista de Tarefas
 Para o **Lista de Tarefas**, você cria um novo objeto do tipo Tarefa  e, em seguida, adiciona esse objeto Task ao Lista de Tarefas chamando seu `Add` método . Para gravar na janela **Saída,** chame seu método para obter um objeto de painel e, em seguida, chame o método `GetPane` do objeto do `OutputString` painel.

1. Em *TodoWindowControl.xaml.cs*, no método , adicione código para obter o painel Geral da janela Saída (que é o padrão) e gravar `button1_Click` nele.   O método deverá ter esta aparência:

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

2. Para adicionar itens ao Lista de Tarefas, você precisa de um para adicionar uma classe aninhada à classe TodoWindowControl. A classe aninhada precisa derivar de <xref:Microsoft.VisualStudio.Shell.TaskProvider> . Adicione o código a seguir ao final da `TodoWindowControl` classe .

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

3. Em seguida, adicione uma referência privada `TodoTaskProvider` a e um método à classe `CreateProvider()` `TodoWindowControl` . Seu código deve ficar assim:

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

4. Adicione , que limpa o Lista de Tarefas, e , que adiciona uma entrada ao `ClearError()` `ReportError()` Lista de Tarefas, à `TodoWindowControl` classe .

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

5. Agora implemente `CheckForErrors` o método , da seguinte forma.

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

2. Abra **TodoWindow** ( Exibir  >  **Outros Windows**  >  **TodoWindow).**

3. Digite algo na caixa de texto e clique em **Adicionar**.

     Uma data de vencimento 2 dias após hoje é adicionada à caixa de listagem. Nenhum erro é gerado e o **Lista de Tarefas** (**Exibir**  >  **Lista de Tarefas**) não deve ter entradas.

4. Agora, altere a configuração **na página** Opções  >  **de** Ferramentas  >  **ToDo** de **2** para **0.**

5. Digite outra coisa no **TodoWindow** e clique em **Adicionar** novamente. Isso dispara um erro e também uma entrada no **Lista de Tarefas**.

     Conforme você adiciona itens, a data inicial é definida como agora mais 2 dias.

6. No menu **Exibir,** clique em **Saída para** abrir a **janela** Saída.

     Observe que sempre que você adiciona um item, uma mensagem é exibida no **painel Lista de Tarefas** dados.

7. Clique em um dos itens na ListBox.

     A **janela** Propriedades exibe as duas propriedades do item.

8. Altere uma das propriedades e pressione **Enter**.

     O item é atualizado na ListBox.
