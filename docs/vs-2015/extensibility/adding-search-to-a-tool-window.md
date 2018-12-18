---
title: Adicionando pesquisa a uma janela de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tool windows, adding search
ms.assetid: f78c4892-8060-49c4-8ecd-4360f1b4d133
caps.latest.revision: 39
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cd5331e433c4790a51dfb7c42b5b0b50eb26c1a6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794147"
---
# <a name="adding-search-to-a-tool-window"></a>Adicionando a pesquisa a uma janela de ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você cria ou atualiza uma janela de ferramentas em sua extensão, você pode adicionar a mesma funcionalidade de pesquisa que aparece em outro lugar no Visual Studio. Essa funcionalidade inclui os seguintes recursos:  
  
- Uma caixa de pesquisa que está sempre localizada em uma área personalizada da barra de ferramentas.  
  
- Um indicador de progresso é sobreposto na caixa de pesquisa em si.  
  
- A capacidade de Mostrar resultados assim que você insere cada caractere (pesquisa instantânea) ou somente depois que você escolhe a tecla Enter (pesquisa sob demanda).  
  
- Uma lista que mostra os termos para os quais você pesquisou mais recentemente.  
  
- A capacidade de filtrar pesquisas por campos específicos ou aspectos dos destinos de pesquisa.  
  
  Seguindo este passo a passo, você aprenderá a executar as seguintes tarefas:  
  
1.  Crie um projeto de VSPackage.  
  
2.  Crie uma janela de ferramenta que contém um UserControl com uma caixa de texto somente leitura.  
  
3.  Adicione uma caixa de pesquisa para a janela da ferramenta.  
  
4.  Adicione a implementação de pesquisa.  
  
5.  Habilite a pesquisa instantânea e a exibição de uma barra de progresso.  
  
6.  Adicionar um **diferenciar maiusculas de minúsculas** opção.  
  
7.  Adicionar um **pesquisar somente as linhas até mesma** filtro.  
  
## <a name="to-create-a-vsix-project"></a>Para criar um projeto do VSIX  
  
1.  Crie um projeto do VSIX chamado `TestToolWindowSearch` com uma janela de ferramenta chamada **TestSearch**. Se você precisar de ajuda para fazer isso, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
## <a name="to-create-a-tool-window"></a>Para criar uma janela de ferramentas  
  
1.  No `TestToolWindowSearch` do projeto, abra o arquivo TestSearchControl.xaml.  
  
2.  Substitua a `<StackPanel>` bloco com o seguinte bloco, que adiciona um somente leitura <xref:System.Windows.Controls.TextBox> para o <xref:System.Windows.Controls.UserControl> na janela da ferramenta.  
  
    ```xaml  
    <StackPanel Orientation="Vertical">  
        <TextBox Name="resultsTextBox" Height="800.0"  
            Width="800.0"  
            IsReadOnly="True">  
        </TextBox>  
    </StackPanel>  
    ```  
  
3.  No arquivo TestSearchControl.xaml.cs, adicione a seguinte instrução using:  
  
    ```csharp  
    using System.Text;  
    ```  
  
4.  Remover o `button1_Click()` método.  
  
     No **TestSearchControl** , adicione o código a seguir.  
  
     Esse código adiciona uma pública <xref:System.Windows.Controls.TextBox> propriedade nomeada **SearchResultsTextBox** e uma propriedade de cadeia de caracteres pública chamada **SearchContent**. No construtor, SearchResultsTextBox é definido como a caixa de texto e SearchContent é inicializado como um conjunto delimitado por nova linha de cadeias de caracteres. O conteúdo da caixa de texto também é inicializado para o conjunto de cadeias de caracteres.  
  
    ```csharp  
    public partial class TestSearchControl : UserControl  
    {  
        public TextBox SearchResultsTextBox { get; set; }  
        public string SearchContent { get; set; }  
  
        public TestSearchControl()  
        {  
            InitializeComponent();  
  
            this.SearchResultsTextBox = resultsTextBox;  
            this.SearchContent = BuildContent();  
  
            this.SearchResultsTextBox.Text = this.SearchContent;  
        }  
  
        private string BuildContent()  
        {  
            StringBuilder sb = new StringBuilder();  
            sb.AppendLine("1 go");  
            sb.AppendLine("2 good");  
            sb.AppendLine("3 Go");  
            sb.AppendLine("4 Good");  
            sb.AppendLine("5 goodbye");  
            sb.AppendLine("6 Goodbye");  
  
            return sb.ToString();  
        }  
    }  
    ```  
  
     [!code-csharp[ToolWindowSearch#1](../snippets/csharp/VS_Snippets_VBCSharp/toolwindowsearch/cs/mycontrol.xaml.cs#1)]
     [!code-vb[ToolWindowSearch#1](../snippets/visualbasic/VS_Snippets_VBCSharp/toolwindowsearch/vb/mycontrol.xaml.vb#1)]  
  
5.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.  
  
6.  Na barra de menus, escolha **modo de exibição**, **Other Windows**, **TestSearch**.  
  
     A janela de ferramenta é exibida, mas o controle de pesquisa ainda não aparecer.  
  
## <a name="to-add-a-search-box-to-the-tool-window"></a>Para adicionar uma caixa de pesquisa para a janela da ferramenta  
  
1.  No arquivo TestSearch.cs, adicione o seguinte código para o `TestSearch` classe. O código substitui o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> propriedade para que o acessador get retorna `true`.  
  
     Para habilitar a pesquisa, você deve substituir o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> propriedade. O <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> implementos de classe <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch> e fornece uma implementação padrão que não permite a pesquisa.  
  
    ```csharp  
    public override bool SearchEnabled  
    {  
        get { return true; }  
    }  
    ```  
  
2.  Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
3.  Na instância experimental do Visual Studio, abra **TestSearch**.  
  
     Na parte superior da janela de ferramentas, um controle de pesquisa é exibida com uma **pesquisa** marca d'água e um ícone de Lente de aumento. No entanto, a pesquisa não funciona ainda porque o processo de pesquisa não foi implementado.  
  
## <a name="to-add-the-search-implementation"></a>Para adicionar a implementação de pesquisa  
 Quando você habilita a pesquisa em um <xref:Microsoft.VisualStudio.Shell.ToolWindowPane>, como no procedimento anterior, a janela da ferramenta cria um host de pesquisa. Esse host configura e gerencia os processos de pesquisa, que sempre ocorrem em um thread em segundo plano. Porque o <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> classe gerencia a criação de host de pesquisa e a configuração de backup da pesquisa, você só precisa criar uma tarefa de pesquisa e fornecer o método de pesquisa. O processo de pesquisa ocorre em um thread em segundo plano, e chamadas para o controle de janela da ferramenta ocorrerem no thread da interface do usuário. Portanto, você deve usar o <xref:Microsoft.VisualStudio.Shell.ThreadHelper.Invoke%2A> método para gerenciar todas as chamadas feitas ao lidar com o controle.  
  
1.  No arquivo TestSearch.cs, adicione o seguinte `using` instruções:  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Runtime.InteropServices;  
    using System.Text;  
    using System.Windows.Controls;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.PlatformUI;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
2.  No `TestSearch` de classe, adicione o código a seguir, que executa as seguintes ações:  
  
    -   Substitui o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A> método para criar uma tarefa de pesquisa.  
  
    -   Substitui o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> método para restaurar o estado da caixa de texto. Esse método é chamado quando um usuário cancela uma tarefa de pesquisa e quando um usuário define ou cancela a definição de opções ou filtros. Ambos <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> são chamados no thread da interface do usuário. Portanto, não é necessário acessar a caixa de texto por meio do <xref:Microsoft.VisualStudio.Shell.ThreadHelper.Invoke%2A> método.  
  
    -   Cria uma classe chamada `TestSearchTask` que herda de <xref:Microsoft.VisualStudio.Shell.VsSearchTask>, que fornece uma implementação padrão de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask>.  
  
         No `TestSearchTask`, o construtor define um campo particular que faz referência a janela da ferramenta. Para fornecer o método de pesquisa, você deve substituir a <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A> e <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A> métodos. O <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A> método é onde você implementa o processo de pesquisa. Esse processo inclui executar a pesquisa, exibindo os resultados da pesquisa na caixa de texto e chamar a implementação da classe base desse método para relatar que a pesquisa foi concluída.  
  
    ```csharp  
    public override IVsSearchTask CreateSearch(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback)  
    {  
        if (pSearchQuery == null || pSearchCallback == null)  
            return null;  
         return new TestSearchTask(dwCookie, pSearchQuery, pSearchCallback, this);  
    }  
  
    public override void ClearSearch()  
    {  
        TestSearchControl control = (TestSearchControl)this.Content;  
        control.SearchResultsTextBox.Text = control.SearchContent;  
    }  
  
    internal class TestSearchTask : VsSearchTask  
    {  
        private TestSearch m_toolWindow;  
  
        public TestSearchTask(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback, TestSearch toolwindow)  
            : base(dwCookie, pSearchQuery, pSearchCallback)  
        {  
            m_toolWindow = toolwindow;  
        }  
  
        protected override void OnStartSearch()  
        {  
            // Use the original content of the text box as the target of the search.   
            var separator = new string[] { Environment.NewLine };  
            TestSearchControl control = (TestSearchControl)m_toolWindow.Content;  
            string[] contentArr = control.SearchContent.Split(separator, StringSplitOptions.None);  
  
            // Get the search option.   
            bool matchCase = false;  
            // matchCase = m_toolWindow.MatchCaseOption.Value;   
  
                // Set variables that are used in the finally block.  
                StringBuilder sb = new StringBuilder("");  
                uint resultCount = 0;  
                this.ErrorCode = VSConstants.S_OK;  
  
                try  
                {  
                    string searchString = this.SearchQuery.SearchString;  
  
                    // Determine the results.   
                    uint progress = 0;  
                    foreach (string line in contentArr)  
                    {  
                        if (matchCase == true)  
                        {  
                            if (line.Contains(searchString))  
                            {  
                                sb.AppendLine(line);  
                                resultCount++;  
                            }  
                        }  
                        else  
                            {  
                                if (line.ToLower().Contains(searchString.ToLower()))  
                                {  
                                    sb.AppendLine(line);  
                                    resultCount++;  
                                }  
                            }  
  
                            // SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));   
  
                            // Uncomment the following line to demonstrate the progress bar.   
                            // System.Threading.Thread.Sleep(100);  
                        }  
                    }  
                    catch (Exception e)  
                    {  
                        this.ErrorCode = VSConstants.E_FAIL;  
                    }  
                    finally  
                    {  
                        ThreadHelper.Generic.Invoke(() =>  
                        { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });  
  
                        this.SearchResults = resultCount;  
                    }  
  
            // Call the implementation of this method in the base class.   
            // This sets the task status to complete and reports task completion.   
            base.OnStartSearch();  
        }  
  
        protected override void OnStopSearch()  
        {  
            this.SearchResults = 0;  
        }  
    }  
    ```  
  
3.  Teste a implementação de pesquisa, executando as seguintes etapas:  
  
    1.  Recompilar o projeto e iniciar a depuração.  
  
    2.  Na instância experimental do Visual Studio, abra a janela da ferramenta novamente, digite algum texto de pesquisa na janela de pesquisa e clique em ENTER.  
  
         Os resultados corretos devem aparecer.  
  
## <a name="to-customize-the-search-behavior"></a>Para personalizar o comportamento de pesquisa  
 Alterando as configurações de pesquisa, você pode executar uma variedade de alterações na aparência do controle de pesquisa e como a pesquisa é realizada. Por exemplo, você pode alterar a marca d'água (o texto padrão que aparece na caixa de pesquisa), o mínimo e a largura máxima do controle de pesquisa e se deseja mostrar uma barra de progresso. Você também pode alterar o ponto no quais resultados da pesquisa comecem a aparecer (sob demanda ou a pesquisa instantânea) e se deseja mostrar uma lista de termos para os quais você pesquisou recentemente. Você pode encontrar a lista completa de configurações no <xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource> classe.  
  
1.  No arquivo TestSearch.cs, adicione o seguinte código para o `TestSearch` classe. Esse código permite que a pesquisa instantânea, em vez de sob demanda pesquisa (isto é, o usuário não precisa clicar em ENTER). O código substitui o `ProvideSearchSettings` método no `TestSearch` classe, que é necessário alterar as configurações padrão.  
  
    ```csharp  
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)  
    {  
        Utilities.SetValue(pSearchSettings,   
            SearchSettingsDataSource.SearchStartTypeProperty.Name,   
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}  
    ```  
  
2.  Testar a nova configuração, recriar a solução e reiniciar o depurador.  
  
     Resultados da pesquisa exibidos toda vez que você inserir um caractere na caixa de pesquisa.  
  
3.  No `ProvideSearchSettings` método, adicione a seguinte linha, que permite a exibição de uma barra de progresso.  
  
    ```csharp  
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)  
    {  
        Utilities.SetValue(pSearchSettings,   
            SearchSettingsDataSource.SearchStartTypeProperty.Name,   
             (uint)VSSEARCHSTARTTYPE.SST_INSTANT);  
        Utilities.SetValue(pSearchSettings,   
            SearchSettingsDataSource.SearchProgressTypeProperty.Name,   
             (uint)VSSEARCHPROGRESSTYPE.SPT_DETERMINATE);  
    }  
    ```  
  
     Para a barra de progresso seja exibida, o progresso deve ser relatado. Para relatar o progresso, descomente o código a seguir na `OnStartSearch` método da `TestSearchTask` classe:  
  
    ```csharp  
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));  
    ```  
  
4.  Diminuir o progresso de processamento suficiente para que a barra está visível, remova a seguinte linha na `OnStartSearch` método da `TestSearchTask` classe:  
  
    ```csharp  
    System.Threading.Thread.Sleep(100);  
    ```  
  
5.  Teste as novas configurações de recriar a solução e começando a debugb.  
  
     A barra de progresso aparece na janela de pesquisa (como uma linha azul abaixo da caixa de texto de pesquisa) toda vez que você realiza uma pesquisa.  
  
## <a name="to-enable-users-to-refine-their-searches"></a>Para habilitar usuários a refinar suas pesquisas  
 Você pode permitir que os usuários refinar as pesquisas por meio de opções, como **diferenciar maiusculas de minúsculas** ou **coincidir palavra inteira**. Opções podem ser boolianos, que aparecem como caixas de seleção ou comandos, que são exibidos como botões. Para este passo a passo, você criará uma opção de booliana.  
  
1.  No arquivo TestSearch.cs, adicione o seguinte código para o `TestSearch` classe. O código substitui o `SearchOptionsEnum` método, que permite a implementação de pesquisa detectar se uma determinada opção está ativada ou desativada. O código na `SearchOptionsEnum` adiciona uma opção para diferenciar maiusculas de minúsculas para uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions> enumerador. A opção para diferenciar maiusculas de minúsculas também se torna disponível como o `MatchCaseOption` propriedade.  
  
    ```csharp  
    private IVsEnumWindowSearchOptions m_optionsEnum;  
    public override IVsEnumWindowSearchOptions SearchOptionsEnum  
    {  
        get  
        {  
            if (m_optionsEnum == null)  
            {  
                List<IVsWindowSearchOption> list = new List<IVsWindowSearchOption>();  
  
                list.Add(this.MatchCaseOption);  
  
                m_optionsEnum = new WindowSearchOptionEnumerator(list) as IVsEnumWindowSearchOptions;  
            }  
            return m_optionsEnum;  
        }  
    }  
  
    private WindowSearchBooleanOption m_matchCaseOption;  
    public WindowSearchBooleanOption MatchCaseOption  
    {  
        get  
        {  
            if (m_matchCaseOption == null)  
            {  
                m_matchCaseOption = new WindowSearchBooleanOption("Match case", "Match case", false);  
            }  
            return m_matchCaseOption;  
        }  
    }  
    ```  
  
2.  No `TestSearchTask` classe, remova a linha matchCase no `OnStartSearch` método:  
  
    ```csharp  
    private IVsEnumWindowSearchOptions m_optionsEnum;  
    public override IVsEnumWindowSearchOptions SearchOptionsEnum  
    {  
        get  
        {  
            if (m_optionsEnum == null)  
            {  
                List<IVsWindowSearchOption> list = new List<IVsWindowSearchOption>();  
  
                list.Add(this.MatchCaseOption);  
  
                m_optionsEnum = new WindowSearchOptionEnumerator(list) as IVsEnumWindowSearchOptions;  
            }  
            return m_optionsEnum;  
        }  
    }  
  
    private WindowSearchBooleanOption m_matchCaseOption;  
    public WindowSearchBooleanOption MatchCaseOption  
    {  
        get  
         {  
            if (m_matchCaseOption == null)  
            {  
                m_matchCaseOption = new WindowSearchBooleanOption("Match case", "Match case", false);  
            }  
            return m_matchCaseOption;  
        }  
    }  
    ```  
  
3.  A opção de teste:  
  
    1.  Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
    2.  Na janela da ferramenta, escolha a seta para baixo no lado direito da caixa de texto.  
  
         O **diferenciar maiusculas de minúsculas** caixa de seleção é exibida.  
  
    3.  Selecione o **diferenciar maiusculas de minúsculas** caixa de seleção e, em seguida, executará algumas pesquisas.  
  
## <a name="to-add-a-search-filter"></a>Para adicionar um filtro de pesquisa  
 Você pode adicionar filtros de pesquisa que permitem aos usuários refinar o conjunto de destinos de pesquisa. Por exemplo, você pode filtrar os arquivos no Explorador de arquivos, as datas em que eles foram modificados mais recentemente e extensões de nome de arquivo. Neste passo a passo, você adicionará um filtro até mesmo apenas para linhas. Quando o usuário escolhe o filtro, o host de pesquisa adiciona as cadeias de caracteres que você especificar para a consulta de pesquisa. Em seguida, você pode identificar essas cadeias de caracteres dentro de seu método de pesquisa e filtrar os destinos de pesquisa de acordo.  
  
1.  No arquivo TestSearch.cs, adicione o seguinte código para o `TestSearch` classe. O código implementa `SearchFiltersEnum` adicionando um <xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter> que especifica para filtrar os resultados da pesquisa para que sejam exibidos apenas linhas pares.  
  
    ```csharp  
    public override IVsEnumWindowSearchFilters SearchFiltersEnum  
    {  
        get  
        {  
            List<IVsWindowSearchFilter> list = new List<IVsWindowSearchFilter>();  
            list.Add(new WindowSearchSimpleFilter("Search even lines only", "Search even lines only", "lines", "even"));  
            return new WindowSearchFilterEnumerator(list) as IVsEnumWindowSearchFilters;  
        }  
    }  
  
    ```  
  
     Agora o controle de pesquisa exibe o filtro de pesquisa `Search even lines only`. Quando o usuário escolhe o filtro, a cadeia de caracteres `lines:"even"` aparece na caixa de pesquisa. Outros critérios de pesquisa podem aparecer ao mesmo tempo como o filtro. Cadeias de caracteres de pesquisa podem aparecer antes do filtro, após o filtro, ou ambos.  
  
2.  No arquivo TestSearch.cs, adicione os seguintes métodos para o `TestSearchTask` classe, que está no `TestSearch` classe. Esses métodos aceitam o `OnStartSearch` método, que na próxima etapa, você modificará.  
  
    ```csharp  
    private string RemoveFromString(string origString, string stringToRemove)  
    {  
        int index = origString.IndexOf(stringToRemove);  
        if (index == -1)  
            return origString;  
        else   
             return (origString.Substring(0, index) + origString.Substring(index + stringToRemove.Length)).Trim();  
    }  
  
    private string[] GetEvenItems(string[] contentArr)  
    {  
        int length = contentArr.Length / 2;  
        string[] evenContentArr = new string[length];  
  
        int indexB = 0;  
        for (int index = 1; index < contentArr.Length; index += 2)  
        {  
            evenContentArr[indexB] = contentArr[index];  
            indexB++;  
        }  
  
        return evenContentArr;  
    }  
    ```  
  
3.  No `TestSearchTask` classe, atualize o `OnStartSearch` método com o código a seguir. Essa alteração atualiza o código para dar suporte ao filtro.  
  
    ```csharp  
    protected override void OnStartSearch()  
    {  
        // Use the original content of the text box as the target of the search.   
        var separator = new string[] { Environment.NewLine };  
        string[] contentArr = ((TestSearchControl)m_toolWindow.Content).SearchContent.Split(separator, StringSplitOptions.None);  
  
        // Get the search option.   
        bool matchCase = false;  
        matchCase = m_toolWindow.MatchCaseOption.Value;  
  
        // Set variables that are used in the finally block.  
        StringBuilder sb = new StringBuilder("");  
        uint resultCount = 0;  
        this.ErrorCode = VSConstants.S_OK;  
  
        try  
        {  
            string searchString = this.SearchQuery.SearchString;  
  
            // If the search string contains the filter string, filter the content array.   
            string filterString = "lines:\"even\"";  
  
            if (this.SearchQuery.SearchString.Contains(filterString))  
            {  
                // Retain only the even items in the array.  
                contentArr = GetEvenItems(contentArr);  
  
                // Remove 'lines:"even"' from the search string.  
                searchString = RemoveFromString(searchString, filterString);  
            }  
  
            // Determine the results.   
            uint progress = 0;  
            foreach (string line in contentArr)  
            {  
                if (matchCase == true)  
                {  
                    if (line.Contains(searchString))  
                    {  
                        sb.AppendLine(line);  
                        resultCount++;  
                    }  
                }  
                else  
                {  
                    if (line.ToLower().Contains(searchString.ToLower()))  
                    {  
                        sb.AppendLine(line);  
                        resultCount++;  
                    }  
                }  
  
                SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));  
  
                // Uncomment the following line to demonstrate the progress bar.   
                // System.Threading.Thread.Sleep(100);  
            }  
        }  
        catch (Exception e)  
        {  
            this.ErrorCode = VSConstants.E_FAIL;  
        }  
        finally  
        {  
            ThreadHelper.Generic.Invoke(() =>  
            { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });  
  
            this.SearchResults = resultCount;  
        }  
  
        // Call the implementation of this method in the base class.   
        // This sets the task status to complete and reports task completion.   
        base.OnStartSearch();  
    }  
    ```  
  
4.  Teste seu código.  
  
5.  Compile o projeto e comece a depuração. Na instância experimental do Visual Studio, abra a janela de ferramentas e, em seguida, escolha a seta para baixo no controle de pesquisa.  
  
     O **diferenciar maiusculas de minúsculas** caixa de seleção e o **pesquisar somente as linhas até mesma** filtro são exibidos.  
  
6.  Escolha o filtro.  
  
     A caixa de pesquisa contém **linhas: "mesmo"**, e os seguintes resultados são exibidos:  
  
     2 BOM  
  
     4 BOM  
  
     Adeus 6  
  
7.  Exclua `lines:"even"` da caixa de pesquisa, selecione o **diferenciar maiusculas de minúsculas** caixa de seleção e, em seguida, insira `g` na caixa de pesquisa.  
  
     Os seguintes resultados são exibidos:  
  
     ir de 1  
  
     2 BOM  
  
     adeus 5  
  
8.  Escolha o X no lado direito da caixa de pesquisa.  
  
     A pesquisa está desmarcada e o conteúdo original aparecerá. No entanto, o **diferenciar maiusculas de minúsculas** caixa de seleção ainda está selecionada.

