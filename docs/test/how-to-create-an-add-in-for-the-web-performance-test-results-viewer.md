---
title: Criar um suplemento para o Visualizador de Resultados do Teste de Desempenho Web
ms.date: 10/20/2016
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, Visual Studio Add-in
- Visual Studio Add-in, Web performance tests
ms.assetid: 1118c604-4b1b-4b21-a04e-45995b676fa8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 736c43a83a956c02b760b4909a427a82c6fa9e4c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287825"
---
# <a name="how-to-create-an-add-in-for-the-web-performance-test-results-viewer"></a>Como: criar um suplemento para o Visualizador de Resultados de Teste de desempenho da Web

Você pode estender a interface do usuário para o **Visualizador de Testes de Desempenho Web** usando os seguintes namespaces:

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>

Além disso, você precisa adicionar uma referência ao LoadTestPackage DLL, que está localizado na pasta *% ProgramFiles (x86)% \ Microsoft Visual Studio \\ \<version> \Enterprise\Common7\IDE\PrivateAssemblies*

Para estender a interface do usuário do **Visualizador de Testes de Desempenho Web**, você precisa criar um suplemento do Visual Studio e um controle de usuário. Os procedimentos a seguir explicam como criar o suplemento, o controle de usuário e como implementar as classes necessárias para estender interface de usuário do **Visualizador de Testes de Desempenho Web**.

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="create-or-open-a-solution-that-contains-an-aspnet-web-application-and-a-web-performance-and-load-test-project"></a>Criar ou abrir uma solução que contém um aplicativo Web ASP.NET e um projeto de teste de desempenho Web e de carga

### <a name="to-prepare-for-extending-the-web-performance-test-results-viewer"></a>Para se preparar para estender o Visualizador de Resultados de Teste de Desempenho na Web

Crie ou abra uma solução de não produção com a qual você poderá fazer experiências e que contenha um aplicativo Web do ASP.NET e um projeto de desempenho na Web, além de carregar o projeto de teste com um ou mais testes de desempenho na Web para o aplicativo Web do ASP.NET.

> [!NOTE]
> Você pode criar um aplicativo Web ASP.NET e um projeto de teste de carga e desempenho na Web que contém testes de desempenho da Web seguindo os procedimentos em [como criar um teste de serviço Web](../test/how-to-create-a-web-service-test.md) e [gerar e executar um teste de desempenho da Web codificado](../test/generate-and-run-a-coded-web-performance-test.md).

## <a name="create-a-visual-studio-add-in"></a>Criar um suplemento do Visual Studio

Um suplemento é uma DLL compilada executada no IDE (ambiente de desenvolvimento integrado) do Visual Studio. A compilação ajuda a proteger sua propriedade intelectual e melhora o desempenho. Embora você possa criar suplementos manualmente, talvez você ache mais fácil usar o **Assistente de Suplemento**. O assistente cria um suplemento funcional, mas básico, que você poderá executar imediatamente depois de criá-lo. Depois que o **Assistente de Suplemento** gerar o programa básico, você poderá adicionar um código a ele e personalizá-lo.

O **Assistente de Suplemento** permite fornecer um nome de exibição e uma descrição para o suplemento. Ambos serão exibidos no **Gerenciador de Suplementos**. Também é possível fazer o assistente gerar um código que seja adicionado ao menu **Ferramentas** para abrir o suplemento. Você também pode optar por exibir uma caixa de diálogo personalizada **Sobre** para seu suplemento. Quando o assistente terminar, você terá um novo projeto com apenas uma classe que implementa o suplemento. Essa classe é chamada de Conectar.

Você usará o **Gerenciador de Suplementos** ao final deste artigo.

### <a name="to-create-an-add-in-by-using-the-add-in-wizard"></a>Para criar um suplemento usando o Assistente de Suplemento

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução, escolha **Adicionar**e, em seguida, selecione **novo projeto**.

2. Criar um projeto de **suplemento do Visual Studio**.

    O **Assistente de Suplemento** do Visual Studio é iniciado.

3. Escolha **Próxima**.

4. Na página **Selecione uma Linguagem de Programação**, selecione a linguagem de programação que deseja usar para gravar o suplemento.

   > [!NOTE]
   > Este tópico usa o Visual C# no código de exemplo.

5. Na página **Selecione um Aplicativo Host**, selecione **Visual Studio** e desmarque **Macros do Visual Studio**.

6. Escolha **Próxima**.

7. Digite um nome e uma descrição para o suplemento na página **Digite um Nome e uma Descrição**.

     Após o suplemento ser criado, seu nome e sua descrição serão exibidos na lista **Suplementos Disponíveis** no **Gerenciador de Suplementos**. Adicione detalhes o suficiente à descrição do suplemento de modo que os usuários possam saber o que o suplemento faz, como funciona etc.

8. Escolha **Próxima**.

9. Na página **Escolha Opções de Suplemento**, selecione **Desejo que o suplemento seja carregado quando o aplicativo host for iniciado**.

10. Desmarque as caixas de seleção restantes.

11. Na página **Escolhendo Informações de “Ajuda Sobre”**, você pode especificar se deseja que as informações sobre o suplemento sejam exibidas em uma caixa de diálogo **Sobre**. Se você quiser que as informações sejam exibidas, marque a caixa de seleção **Sim, desejo que o suplemento ofereça informações da caixa “Sobre”**.

     As informações que podem ser adicionadas à caixa de diálogo **Sobre** do Visual Studio incluem o número de versão, os detalhes de suporte, os dados de licenciamento etc.

12. Escolha **Próxima**.

13. As opções que você selecionou são exibidas na página **Resumo** para análise. Se você estiver satisfeito, escolha **Finalizar** para criar o suplemento. Se quiser alterar algo, escolha o botão **Voltar**.

     A nova solução e o projeto são criados, e o arquivo *Connect.cs* do novo suplemento é exibido no **Editor de Códigos**.

     Você adicionará o código ao arquivo *Connect.cs* após o procedimento a seguir, que cria um controle de usuário que será referenciado por este projeto WebPerfTestResultsViewerAddin.

    Após um suplemento ser criado, será necessário registrá-lo no Visual Studio para que ele possa ser ativado no **Gerenciador de Suplementos**. Faça isso usando um arquivo XML que tenha uma extensão de nome de arquivo *.addin*.

    O arquivo *. AddIn* descreve as informações que o Visual Studio exige para exibir o suplemento no **Gerenciador de suplementos**. Quando o Visual Studio é iniciado, ele procura no local do arquivo *. AddIn* quaisquer arquivos *. AddIn* disponíveis. Se encontrar algum, ele lerá o arquivo XML e fornecerá ao **Gerenciador de Suplementos** as informações necessárias para iniciar o suplemento quando clicado.

    O arquivo *.addin* é criado automaticamente quando você cria um suplemento usando o **Assistente de Suplemento**.

### <a name="add-in-file-locations"></a>Locais de arquivo de suplemento

Duas cópias do arquivo *.addin* são criadas automaticamente pelo **Assistente de Suplemento**, da seguinte forma:

|**Local do arquivo .addin**|**Descrição**|
|-|----------------------------|-|
|Pasta raiz do projeto|Usado na implantação do projeto de suplemento. Incluído no projeto para facilitar a edição e tem o caminho local para a implantação de XCopy-style.|
|Pasta do suplemento|Usado para executar o suplemento no ambiente de depuração. Ela deve sempre apontar para o caminho de saída da configuração da compilação atual.|

## <a name="create-a-windows-form-control-library-project"></a>Criar um projeto da Biblioteca de Controles do Windows Forms

O suplemento do Visual Studio criado no procedimento anterior referencia um projeto da Biblioteca de Controle Windows Forms para criar uma instância de uma classe <xref:System.Windows.Forms.UserControl>.

### <a name="to-create-a-control-to-be-used-in-the-web-test-results-viewer"></a>Para criar um controle a ser usado no Visualizador de Resultados de Teste de Desempenho na Web

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução, escolha **Adicionar**e, em seguida, selecione **novo projeto**.

2. Crie um projeto da **Biblioteca de Controle do Windows Forms**.

3. Na **Caixa de Ferramentas**, arraste um <xref:System.Windows.Forms.DataGridView> para a superfície de userControl1.

4. Clique no glifo de marcação de ação (![Glifo de marcação inteligente](../test/media/vs_winformsmttagglyph.gif)) no canto superior direito do <xref:System.Windows.Forms.DataGridView> e siga estas etapas:

    1. Escolha **Encaixar no Contêiner Pai**.

    2. Desmarque as caixas de seleção de **Habilitar Inclusão**, **Habilitar Edição**, **Habilitar Exclusão** e **Habilitar Reorganização de Colunas**.

    3. Escolha **Adicionar Coluna**.

         A caixa de diálogo **Adicionar Coluna** é exibida.

    4. Na lista suspensa **Tipo**, selecione **DataGridViewTextBoxColumn**.

    5. Limpe o texto "Column1" em **Texto do cabeçalho**.

    6. Escolha **Adicionar**.

    7. Escolha **Fechar**.

5. Na janela **Propriedades** , altere a propriedade **(Name)** de <xref:System.Windows.Forms.DataGridView> para **resultControlDataGridView**.

6. Clique com o botão direito do mouse na superfície de design e selecione **Exibir Código**.

     O arquivo *UserControl1.cs* é exibido no **Editor de Códigos**.

7. Altere o nome da classe instanciada <xref:System.Windows.Forms.UserControl> de UserContro1 para resultControl:

    ```csharp
    namespace WebPerfTestResultsViewerControl
    {
        public partial class resultControl : UserControl
        {
            public resultControl()
            {
                InitializeComponent();
            }
    ```

     No próximo procedimento, você adicionará o código ao arquivo *Connect.cs* do projeto WebPerfTestResultsViewerAddin, que referenciará a classe resultControl.

     Você adicionará um código extra ao arquivo *Connect.cs* depois.

## <a name="add-code-to-the-webperftestresultsvieweraddin"></a>Adicionar um código ao WebPerfTestResultsViewerAddin

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó **referências** no projeto WebPerfTestResultsViewerAddin e selecione **Adicionar referência**.

2. Na caixa de diálogo **Adicionar Referência**, escolha a guia **.NET**.

3. Role para baixo e selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework** e **System.Windows.Forms**.

4. Escolha **OK**.

5. Clique com o botão direito do mouse no nó **Referências** novamente e selecione **Adicionar Referência**.

6. Na caixa de diálogo **Adicionar Referência**, clique na guia **Procurar**.

7. Escolha a lista suspensa para **examinar** e navegue até *% ProgramFiles (x86)% \ Microsoft Visual Studio\2017\Enterprise\Common7\IDE\PrivateAssemblies* e selecione o arquivo *Microsoft.VisualStudio.QualityTools.LoadTestPackage.dll* .

8. Escolha **OK**.

9. Clique com o botão direito do mouse no nó do projeto WebPerfTestResultsViewerAddin e selecione **Adicionar Referência**.

10. Na caixa de diálogo **Adicionar Referência**, clique na guia **Projetos**.

11. Em **Nome do Projeto,** selecione o projeto **WebPerfTestResultsViewerControl** e escolha **OK**.

12. Se o arquivo *Connect.cs* ainda não estiver aberto, em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo **Connect.cs** no projeto WebPerfTestResultsViewerAddin e selecione **Exibir código**.

13. No arquivo *Connect.cs*, adicione as seguintes instruções Using:

    ```csharp
    using System.IO;
    using System.Windows.Forms;
    using System.Collections.Generic;
    using Microsoft.VisualStudio.TestTools.LoadTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using WebPerfTestResultsViewerControl;
    ```

14. Role para baixo até a parte inferior do arquivo *Connect.cs*. Você precisa adicionar uma lista de GUIDs do <xref:System.Windows.Forms.UserControl>, caso mais de uma instância do **Visualizador de Testes de Desempenho Web** seja aberta. Você adicionará um código depois que usa essa lista.

     Uma segunda lista de cadeias de caracteres é usada no método OnDiscconection, que você codificará mais tarde.

    ```csharp
    private DTE2 _applicationObject;
    private AddIn _addInInstance;

    private Dictionary<Guid, List<UserControl>> m_controls = new Dictionary<Guid, List<UserControl>>();        private List<string> temporaryFilePaths = new List<string>();
    ```

15. O arquivo *Connect.cs* instancia uma classe chamada Connect da <xref:Extensibility.IDTExtensibility2> classe e também inclui alguns métodos para implementar o suplemento do Visual Studio. Um dos métodos é o método OnConnection, que recebe a notificação de que o suplemento está sendo carregado. No método OnConnection, você usará a classe LoadTestPackageExt para criar seu pacote de extensibilidade para o **Visualizador de Testes de Desempenho Web**. Adicione o seguinte código ao método OnConnection:

    ```csharp
    public void OnConnection(object application, ext_ConnectMode connectMode, object addInInst, ref Array custom)
                {
                _applicationObject = (DTE2)application;
                _addInInstance = (AddIn)addInInst;

                // Create a load test packge extensibility class.            LoadTestPackageExt loadTestPackageExt = _applicationObject.GetObject("Microsoft.VisualStudio.TestTools.LoadTesting.LoadTestPackageExt") as LoadTestPackageExt;            // Process open windows.            foreach (WebTestResultViewer webTestResultViewer in loadTestPackageExt.WebTestResultViewerExt.ResultWindows)            {                WindowCreated(webTestResultViewer);            }            // Create event handlers.            loadTestPackageExt.WebTestResultViewerExt.WindowCreated += new EventHandler<WebTestResultViewerExt.WindowCreatedEventArgs>(WebTestResultViewerExt_WindowCreated);            loadTestPackageExt.WebTestResultViewerExt.WindowClosed += new EventHandler<WebTestResultViewerExt.WindowClosedEventArgs>(WebTesResultViewer_WindowClosed);            loadTestPackageExt.WebTestResultViewerExt.SelectionChanged += new EventHandler<WebTestResultViewerExt.SelectionChangedEventArgs>(WebTestResultViewer_SelectedChanged);
            }
    ```

16. Adicione o seguinte código à classe de conexão para criar o método WebTestResultViewerExt_WindowCreated do manipulador de eventos loadTestPackageExt.WebTestResultViewerExt.WindowCreated que você adicionou no método OnConnection e para o método WindowCreated que o método WebTestResultViewerExt_WindowCreated chama.

    ```csharp
            void WebTestResultViewerExt_WindowCreated(object sender, WebTestResultViewerExt.WindowCreatedEventArgs e)
            {
                // New control added to new result viewer window.
                WindowCreated(e.WebTestResultViewer);
            }

    private void WindowCreated(WebTestResultViewer viewer)        {            // Instantiate an instance of the resultControl referenced in the WebPerfTestResultsViewerControl project.
                resultControl resultControl = new resultControl();            // Add to the dictionary of open playback windows.            System.Diagnostics.Debug.Assert(!m_controls.ContainsKey(viewer.TestResultId));            List<UserControl> userControls = new List<UserControl>();            userControls.Add(resultControl);            // Add Guid to the m_control List to manage Result viewers and controls.            m_controls.Add(viewer.TestResultId, userControls);            // Add tabs to the playback control.            resultControl.Dock = DockStyle.Fill;            viewer.AddResultPage(new Guid(), "Sample", resultControl);        }
    ```

17. Adicione o seguinte código à classe de conexão para criar o método WebTestResultViewer_SelectedChanged do manipulador de eventos loadTestPackageExt.WebTestResultViewerExt.SelectionChanged que você adicionou no método OnConnection:

    ```csharp
    void WebTestResultViewer_SelectedChanged(object sender, WebTestResultViewerExt.SelectionChangedEventArgs e)
    {
        foreach (UserControl userControl in m_controls[e.TestResultId])            {                // Update the userControl in each result viewer.                resultControl resultControl = userControl as resultControl;                if (resultControl != null)                    // Call the resultControl's Update method (This will be added in the next procedure).                    resultControl.Update(e.WebTestRequestResult);            }
    }
    ```

18. Adicione o seguinte código à classe de conexão para criar o método WebTesResultViewer_WindowClosed do manipulador de eventos loadTestPackageExt.WebTestResultViewerExt.WindowClosed que você adicionou no método OnConnection:

    ```csharp
    void WebTesResultViewer_WindowClosed(object sender, WebTestResultViewerExt.WindowClosedEventArgs e)
    {
        if (m_controls.ContainsKey(e.WebTestResultViewer.TestResultId))
        {
            m_controls.Remove(e.WebTestResultViewer.TestResultId);
        }
    }
    ```

     Agora que o código foi concluído para o suplemento do Visual Studio, você precisa adicionar o método Update ao resultControl no projeto WebPerfTestResultsViewerControl.

## <a name="add-code-to-the-webperftestresultsviewercontrol"></a>Adicionar código ao WebPerfTestResultsViewerControl

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto WebPerfTestResultsViewerControl e selecione **Propriedades**.

2. Selecione a guia **Aplicativo** e, em seguida, escolha a lista suspensa **Estrutura de destino** e selecione **.NET Framework 4** (ou posterior). Feche a janela **Propriedades** .

   Isso é necessário para dar suporte às referências de DLL necessárias para estender o **Visualizador de Testes de Desempenho Web**.

3. Em **Gerenciador de soluções**, no projeto WebPerfTestResultsViewerControl, clique com o botão direito do mouse no nó **referências** e selecione **Adicionar referência**.

4. Na caixa de diálogo **Adicionar Referência**, clique na guia **.NET**.

5. Role para baixo e selecione **Microsoft.VisualStudio.QualityTools.WebTestFramework**.

6. Escolha **OK**.

7. No arquivo *UserControl1.cs*, adicione as seguintes instruções Using:

    ```csharp
    using Microsoft.VisualStudio.TestTools.WebTesting;
    using Microsoft.VisualStudio.TestTools.WebTesting.Rules;
    ```

8. Adicione o método Update que é chamado e passado para um WebTestRequestResult do método WebPerfTestResultsViewerAddin WebTestResultViewer_SelectedChanged no arquivo *Connect.cs*. O método Atualização popula o DataGridView com diversas propriedades passadas para ele no WebTestRequestResult.

    ```csharp
    public void Update(WebTestRequestResult WebTestResults)
            {
                // Clear the DataGridView when a request is selected.
                resultControlDataGridView.Rows.Clear();
                // Populate the DataGridControl with properties from the WebTestResults.
                this.resultControlDataGridView.Rows.Add("Request: " + WebTestResults.Request.Url.ToString());
                this.resultControlDataGridView.Rows.Add("Response: " + WebTestResults.Response.ResponseUri.ToString());
                foreach (RuleResult ruleResult in WebTestResults.ExtractionRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Extraction rule results: " + ruleResult.Message.ToString());
                }
                foreach (RuleResult ruleResult in WebTestResults.ValidationRuleResults)
                {
                    this.resultControlDataGridView.Rows.Add("Validation rule results: " + ruleResult.Message.ToString());
                }
                foreach (WebTestError webTestError in WebTestResults.Errors)
                {
                    this.resultControlDataGridView.Rows.Add("Error: " + webTestError.ErrorType.ToString() + " " + webTestError.ErrorSubtype.ToString() + " " + webTestError.ExceptionText.ToString());
                }
            }
    ```

## <a name="build-the-solution"></a>Compilar a solução

- No menu **Build**, selecione **Compilar Solução**.

## <a name="register-the-webperftestresultsvieweraddin-add-in"></a>Registrar o suplemento WebPerfTestResultsViewerAddin

1. No menu **Ferramentas**, selecione **Gerenciador de Suplementos**.

2. A caixa de diálogo **Gerenciador de Suplementos** é exibida.

3. Marque a caixa de seleção do suplemento WebPerfTestResultsViewerAddin na coluna **Suplementos Disponíveis** e desmarque as caixas de seleção sob as colunas **Inicialização** e **Linha de Comando**.

4. Escolha **OK**.

## <a name="run-the-web-performance-test-using-the-web-test-results-viewer"></a>Executar o teste de desempenho Web usando o Visualizador de Resultados de Teste na Web

1. Execute seu teste de desempenho na Web e você verá a nova guia do suplemento WebPerfTestResultsViewerAddin chamada Exemplo, exibida no **Visualizador de Testes de Desempenho Web**.

2. Escolha a guia para ver as propriedades apresentadas no DataGridView.

## <a name="net-security"></a>Segurança do .NET

Para melhorar a segurança impedindo que suplementos mal-intencionados sejam ativados automaticamente, o Visual Studio fornece configurações em uma página de **Opções de Ferramentas** chamada **Segurança de Macros/Suplemento**.

Além disso, essa página de opções permite que você especifique as pastas nas quais o Visual Studio procura *. *Arquivos de registro do suplemento. Isso melhora a segurança, permitindo que você limite os locais em que os arquivos de registro *.AddIn* podem ser lidos. Isso ajuda a impedir que arquivos *.AddIn* mal-intencionados sejam usados acidentalmente.

**Configurações de Segurança do Suplemento**

As configurações no Visual Studio relacionadas à segurança do suplemento são:

- **Permitir que os componentes do suplemento sejam carregados.** Selecionadas por padrão. Quando selecionado, os suplementos têm permissão para serem carregados no Visual Studio. Quando não selecionados, os suplementos são proibidos de serem carregados no Visual Studio.

- **Permitir carregamento de componentes de Suplemento de uma URL.** Não é selecionado por padrão. Quando forem selecionados, os suplementos poderão ser carregados de sites externos. Quando não selecionados, os suplementos remotos são proibidos de serem carregados no Visual Studio. Se um suplemento não puder ser carregado por algum motivo, ele não poderá ser carregado na Web. Essa configuração controla somente o carregamento da DLL do suplemento. Os arquivos de registro *.Addin* precisam estar sempre localizados no sistema local.

## <a name="see-also"></a>Veja também

- <xref:System.Windows.Forms.UserControl>
- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.DataGrid>
- [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md)
