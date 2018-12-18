---
title: Estendendo a propriedades, lista de tarefas, saída e as opções Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ebff9aaeb49d99b26b92d1908e22397b9ab0a20d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868684"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>Estender as janelas de propriedades, lista de tarefas, saída e opções
Você pode acessar qualquer janela de ferramentas no Visual Studio. Este passo a passo mostra como integrar informações sobre sua janela de ferramentas em uma nova **opções** página e uma nova configuração na **propriedades** página e também como gravar na **listadetarefas** e **saída** windows.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-an-extension-with-a-tool-window"></a>Criar uma extensão com uma janela de ferramentas  
  
1.  Crie um projeto chamado **TodoList** usando o modelo VSIX e adicionar um modelo de item da janela de ferramenta personalizada denominado **TodoWindow**.  
  
    > [!NOTE]
    >  Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
## <a name="set-up-the-tool-window"></a>Configurar a janela da ferramenta  
 Adicione uma caixa de texto no qual você pode digitar um novo item ToDo, um botão para adicionar o novo item à lista e uma caixa de listagem para exibir os itens na lista.  
  
1.  Na *TodoWindow.xaml*, excluir os controles de botão, a caixa de texto e o StackPanel de UserControl.  
  
    > [!NOTE]
    >  Isso não exclui os **button1_Click** manipulador de eventos, que serão reutilizados em uma etapa posterior.  
  
2.  Do **todos os controles do WPF** seção o **caixa de ferramentas**, arraste uma **tela** controle à grade.  
  
3.  Arraste uma **caixa de texto**, um **botão**e um **ListBox** à tela. Organize os elementos para que a caixa de texto e o botão estiverem no mesmo nível e a caixa de listagem preenche o restante da janela abaixo deles, como na imagem abaixo.  
  
     ![Concluída a janela de ferramentas](../extensibility/media/t5-toolwindow.png "ToolWindow T5")  
  
4.  No painel de XAML, localizar o botão e defina sua propriedade de conteúdo **adicionar**. Reconectar o manipulador de eventos do botão para o controle de botão, adicionando um `Click="button1_Click"` atributo. O bloco de tela deve ter esta aparência:  
  
    ```xml  
    <Canvas HorizontalAlignment="Left" Width="306">  
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>  
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>  
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>  
    </Canvas>  
    ```  
  
### <a name="customize-the-constructor"></a>Personalizar o construtor  
  
1.  No *TodoWindowControl.xaml.cs* de arquivo, adicione a seguinte instrução using:  
  
    ```csharp  
    using System;  
    ```  
  
2.  Adicione uma referência pública para o TodoWindow e tem o construtor TodoWindowControl utilizam um parâmetro TodoWindow. O código deve ter esta aparência:  
  
    ```csharp  
    public TodoWindow parent;  
  
    public TodoWindowControl(TodoWindow window)  
    {  
        InitializeComponent();  
        parent = window;  
    }  
    ```  
  
3.  Na *TodoWindow.cs*, altere o construtor TodoWindowControl para incluir o parâmetro TodoWindow. O código deve ter esta aparência:  
  
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
 Você pode fornecer uma página na **opções** caixa de diálogo para que os usuários podem alterar as configurações para a janela da ferramenta. Criar uma página de opções requer uma classe que descreve as opções e uma entrada na *TodoListPackage.cs* ou *TodoListPackage.vb* arquivo.  
  
1. Adicione uma classe chamada `ToolsOptions.cs`. Verifique as `ToolsOptions` classe herdar de <xref:Microsoft.VisualStudio.Shell.DialogPage>.  
  
   ```csharp  
   class ToolsOptions : DialogPage  
   {  
   }  
   ```  
  
2. Adicione a seguinte instrução using:  
  
   ```csharp  
   using Microsoft.VisualStudio.Shell;  
   ```  
  
3. A página de opções neste passo a passo fornece apenas uma opção chamada DaysAhead. Adicionar um campo privado chamado **daysAhead** e uma propriedade chamada **DaysAhead** para o `ToolsOptions` classe:  
  
   ```csharp  
   private double daysAhead;  
  
   public double DaysAhead  
   {  
       get { return daysAhead; }  
       set { daysAhead = value; }  
   }  
   ```  
  
   Agora você deve fazer o projeto ciente dessa página de opções.  
  
### <a name="make-the-options-page-available-to-users"></a>Tornar a página de opções disponíveis para usuários  
  
1.  Na *TodoWindowPackage.cs*, adicione uma <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> para o `TodoWindowPackage` classe:  
  
    ```csharp  
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]  
    ```  
  
2.  O primeiro parâmetro para o construtor ProvideOptionPage é o tipo da classe `ToolsOptions`, que você criou anteriormente. O segundo parâmetro, "ToDo", é o nome da categoria na **opções** caixa de diálogo. O terceiro parâmetro, "Geral", é o nome da subcategoria do **opções** caixa de diálogo em que a página de opções estarão disponível. Os próximos dois parâmetros são IDs de recurso para cadeias de caracteres; a primeira é o nome da categoria e o segundo é o nome da subcategoria. O parâmetro final determina se esta página pode ser acessada por meio de automação.  
  
     Quando um usuário abre sua página de opções, ele deve ser semelhante a figura a seguir.  
  
     ![Página de opções](../extensibility/media/t5optionspage.gif "T5OptionsPage")  
  
     Observe que a categoria **ToDo** e a subcategoria **geral**.  
  
## <a name="make-data-available-to-the-properties-window"></a>Disponibilizar dados para a janela Propriedades  
 Você pode disponibilizar informações da lista de tarefas, criando uma classe chamada `TodoItem` que armazena informações sobre os itens individuais na lista de tarefas.  
  
1.  Adicione uma classe chamada `TodoItem.cs`.  
  
     Quando a janela da ferramenta está disponível para os usuários, os itens na caixa de listagem serão representados por TodoItems. Quando o usuário seleciona um desses itens, na caixa de listagem, o **propriedades** janela exibirá informações sobre o item.  
  
     Para tornar dados disponíveis na **propriedades** janela, você transformar os dados em propriedades públicas que têm dois atributos especiais, `Description` e `Category`. `Description` é o texto que aparece na parte inferior a **propriedades** janela. `Category` determina onde a propriedade deve ser exibida quando o **propriedades** janela é exibida na **categorizado** modo de exibição. Na imagem a seguir, o **propriedades** janela está **categorizado** modo de exibição, o **nome** propriedade no **ToDo Fields** categoria é selecionado e a descrição de **nome** propriedade é exibida na parte inferior da janela.  
  
     ![Janela propriedades](../extensibility/media/t5properties.png "T5Properties")  
  
2.  Adicione as seguintes instruções using a *TodoItem.cs* arquivo.  
  
    ```csharp  
    using System.ComponentModel;  
    using System.Windows.Forms;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
3.  Adicionar o `public` modificador de acesso à declaração de classe.  
  
    ```csharp  
    public class TodoItem  
    {  
    }  
    ```  
  
     Adicione as duas propriedades, `Name` e `DueDate`. Vamos fazer a `UpdateList()` e `CheckForErrors()` mais tarde.  
  
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
  
4.  Adicione uma referência privada para o controle de usuário. Adicione um construtor que usa o controle de usuário e o nome para este item de tarefas pendentes. Para localizar o valor para `daysAhead`, ele obtém a propriedade da página de opções.  
  
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
  
5.  Porque instâncias do `TodoItem` classe será armazenado na caixa de listagem e a caixa de listagem chamará o `ToString` função, você deve sobrecarregar o `ToString` função. Adicione o seguinte código ao *TodoItem.cs*, após o construtor e antes do final da classe.  
  
    ```csharp  
    public override string ToString()  
    {  
        return name + " Due: " + dueDate.ToShortDateString();  
    }  
    ```  
  
6.  Na *TodoWindowControl.xaml.cs*, adicione métodos stub para o `TodoWindowControl` classe para o `CheckForError` e `UpdateList` métodos. Colocá-los após o ProcessDialogChar e antes do final do arquivo.  
  
    ```csharp  
    public void CheckForErrors()  
    {  
    }  
    public void UpdateList(TodoItem item)  
    {  
    }  
    ```  
  
     O `CheckForError` método chamará um método que tem o mesmo nome no objeto pai, e esse método verificará se quaisquer erros ocorreram e tratarão-los corretamente. O `UpdateList` método atualizará a caixa de listagem no controle pai; o método é chamado quando o `Name` e `DueDate` propriedades nessa alteração de classe. Eles serão implementados mais tarde.  
  
## <a name="integrate-into-the-properties-window"></a>Integrar a janela Propriedades  
 Agora escreva o código que gerencia a caixa de listagem, que será vinculada à **propriedades** janela.  
  
 Você deve alterar o botão de manipulador para ler a caixa de texto, crie um TodoItem de clique e o adiciona à caixa de listagem.  
  
1.  Substitua a `button1_Click` função com o código que cria um novo TodoItem e o adiciona à caixa de listagem. Ele chama `TrackSelection()`, que será definido posteriormente.  
  
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
  
2.  No modo Design, selecione o controle de caixa de listagem. No **propriedades** janela clique a **manipuladores de eventos** botão e encontre o **SelectionChanged** eventos. Preencha a caixa de texto com **listBox_SelectionChanged**. Isso adiciona um stub para um manipulador SelectionChanged e o atribui ao evento.  
  
3.  Implementar o método de `TrackSelection()` . Desde que você precisará obter o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> services, você precisa fazer o <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> acessível pelo TodoWindowControl. Adicione o seguinte método para o `TodoWindow` classe:  
  
    ```  
    internal object GetVsService(Type service)  
    {  
        return GetService(service);  
    }  
    ```  
  
4.  Adicione as seguintes instruções de uso *TodoWindowControl.xaml.cs*:  
  
    ```csharp  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio.Shell.Interop;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    ```  
  
5.  Preencha o manipulador SelectionChanged da seguinte maneira:  
  
    ```  
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)  
    {  
        TrackSelection();  
    }  
    ```  
  
6.  Agora, preencha a função TrackSelection, que fornece integração com o **propriedades** janela. Essa função é chamada quando o usuário adiciona um item à caixa de listagem ou clica em um item na caixa de listagem. Ele adiciona o conteúdo da caixa de listagem para um SelectionContainer e passa o SelectionContainer para o **propriedades** da janela <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> manipulador de eventos. O serviço TrackSelection controla objetos selecionados na interface do usuário (UI) e exibe suas propriedades  
  
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
  
     Agora que você tem uma classe que o **propriedades** pode usar a janela, você pode integrar o **propriedades** janela com a janela da ferramenta. Quando o usuário clica em um item na caixa de listagem na janela da ferramenta, o **propriedades** janela deve ser atualizada adequadamente. Da mesma forma, quando o usuário altera um item de tarefas na **propriedades** janela, o item associado deve ser atualizado.  
  
7.  Agora, adicione o restante do código na função AtualizarLista *TodoWindowControl.xaml.cs*. Ele deve descartar e adicione novamente o TodoItem modificado na caixa de listagem.  
  
    ```csharp  
    public void UpdateList(TodoItem item)  
    {  
        var index = listBox.SelectedIndex;  
        listBox.Items.RemoveAt(index);  
        listBox.Items.Insert(index, item);  
        listBox.SelectedItem = index;  
    }  
    ```  
  
8.  Teste seu código. Compile o projeto e comece a depuração. A instância experimental deve aparecer.  
  
9. Abra o **ferramentas** > **opções** página. Você deve ver a categoria de tarefas no painel esquerdo. Categorias são listadas em ordem alfabética, portanto, procure em Ts.  
  
10. Sobre o **Todo** página de opções, você deverá ver a `DaysAhead` propriedade definida como **0**. Altere-o para **2**.  
  
11. Sobre o **exibição / Windows outras** menu, abrir **TodoWindow**. Tipo de **EndDate** na caixa de texto e clique **Add**.  
  
12. Na caixa de listagem, você deve ver uma data dois dias depois da data atual.  
  
## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>Adicionar texto na janela de saída e os itens à lista de tarefas  
 Para o **lista de tarefas**, você criar um novo objeto do tipo de tarefa e, em seguida, adicionar esse objeto de tarefa para o **lista de tarefas** chamando seu `Add` método. Para gravar o **saída** janela, você chama seu `GetPane` método para obter um objeto de painel e, em seguida, chamar o `OutputString` método do objeto de painel.  
  
1.  Na *TodoWindowControl.xaml.cs*, no `button1_Click` método, adicione código para obter o **geral** painel da **saída** janela (que é o padrão) e gravar nele. O método deve ter esta aparência:  
  
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
  
2.  Para adicionar itens à lista de tarefas, é necessário um para adicionar uma classe aninhada à classe TodoWindowControl. A classe aninhada precisa ser derivada de <xref:Microsoft.VisualStudio.Shell.TaskProvider>. Adicione o seguinte código ao final do `TodoWindowControl` classe.  
  
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
  
3.  Em seguida, adicione uma referência privada à `TodoTaskProvider` e uma `CreateProvider()` método para o `TodoWindowControl` classe. O código deve ter esta aparência:  
  
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
  
4.  Adicione `ClearError()`, que limpa a lista de tarefas, e `ReportError()`, que adiciona uma entrada à lista de tarefas, como o `TodoWindowControl` classe.  
  
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
  
5.  Agora, implemente o `CheckForErrors` método, da seguinte maneira.  
  
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
  
1.  Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
2.  Abra o **TodoWindow** (**exibição** > **outros Windows** > **TodoWindow**).  
  
3.  Digite algo na caixa de texto e, em seguida, clique em **adicionar**.  
  
     Uma data de vencimento 2 dias depois que hoje é adicionado à caixa de listagem. Nenhum erro é gerado e o **lista de tarefas** (**exibição** > **lista de tarefas**) não deve ter nenhuma entrada.  
  
4.  Agora, altere a configuração na **ferramentas** > **opções** > **ToDo** página de **2** para **0**.  
  
5.  Digite algo diferente na **TodoWindow** e, em seguida, clique em **Add** novamente. Isso dispara um erro e também uma entrada na **lista de tarefas**.  
  
     Como adicionar itens, a data inicial é definida como now além de 2 dias.  
  
6.  Sobre o **modo de exibição** menu, clique em **saída** para abrir o **saída** janela.  
  
     Observe que toda vez que você adicionar um item, será exibida uma mensagem na **lista de tarefas** painel.  
  
7.  Clique em um dos itens na caixa de listagem.  
  
     O **propriedades** janela exibe as duas propriedades para o item.  
  
8.  Altere uma das propriedades e, em seguida, pressione **Enter**.  
  
     O item é atualizado na caixa de listagem.