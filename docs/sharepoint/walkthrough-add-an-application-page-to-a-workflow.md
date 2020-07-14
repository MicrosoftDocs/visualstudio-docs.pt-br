---
title: 'Walkthrough: adicionar uma página de aplicativo a um fluxo de trabalho | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f54914e6676e0cc2400fa04ebb089fac08f58c3c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015494"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>Walkthrough: adicionar uma página de aplicativo a um fluxo de trabalho
  Este tutorial demonstra como adicionar uma página de aplicativo que exibe dados derivados de um fluxo de trabalho para um projeto de fluxo de trabalho. Ele baseia-se no projeto descrito no tópico [Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).

 Este tutorial demonstra as seguintes tarefas:

- Adicionando uma página de aplicativo ASPX a um projeto de fluxo de trabalho do SharePoint.

- Obtendo dados do projeto de fluxo de trabalho e manipulando-os.

- Exibindo dados em uma tabela na página do aplicativo.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

- Você também precisará concluir o projeto no tópico [Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).

## <a name="ammend-the-workflow-code"></a>Ammend o código do fluxo de trabalho
 Primeiro, adicione uma linha de código ao fluxo de trabalho para definir o valor da coluna resultado como o valor do relatório de despesas. Esse valor é usado posteriormente no cálculo do resumo do relatório de despesas.

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>Para definir o valor da coluna resultado no fluxo de trabalho

1. Carregue o projeto concluído do tópico [passo a passos: Criando um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

2. Abra o código para *Workflow1.cs* ou *Workflow1. vb* (dependendo da linguagem de programação).

3. Para a parte inferior do `createTask1_MethodInvoking` método, adicione o seguinte código:

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>Criar uma página de aplicativo
 Em seguida, adicione um formulário ASPX ao projeto. Este formulário exibirá os dados obtidos do projeto de fluxo de trabalho do relatório de despesas. Para fazer isso, você adicionará uma página de aplicativo. Uma página de aplicativo usa a mesma página mestra que outras páginas do SharePoint, o que significa que ela se assemelhará a outras páginas no site do SharePoint.

#### <a name="to-add-an-application-page-to-the-project"></a>Para adicionar uma página de aplicativo ao projeto

1. Escolha o projeto ExpenseReport e, na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

2. No painel **modelos** , escolha o modelo de **página de aplicativo** , use o nome padrão para o item de projeto (**ApplicationPage1. aspx**) e escolha o botão **Adicionar** .

3. No [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] de ApplicationPage1. aspx, substitua a `PlaceHolderMain` seção pelo seguinte:

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     Esse código adiciona uma tabela à página junto com um título.

4. Adicione um título à página do aplicativo, substituindo a `PlaceHolderPageTitleInTitleArea` seção pelo seguinte:

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>Codificar a página do aplicativo
 Em seguida, adicione o código à página do aplicativo de resumo do relatório de despesas. Quando você abre a página, o código examina a lista de tarefas no SharePoint em busca de despesas que excederam o limite de gastos alocado. O relatório lista cada item junto com a soma das despesas.

#### <a name="to-code-the-application-page"></a>Para codificar a página do aplicativo

1. Escolha o nó **ApplicationPage1. aspx** e, na barra de menus, escolha **Exibir**  >  **código** para exibir o código por trás da página do aplicativo.

2. Substitua as instruções **using** ou **Import** (dependendo da linguagem de programação) na parte superior da classe pelo seguinte:

    ```vb
    Imports System
    Imports Microsoft.SharePoint
    Imports Microsoft.SharePoint.WebControls
    Imports System.Collections
    Imports System.Data
    Imports System.Web.UI
    Imports System.Web.UI.WebControls
    Imports System.Web.UI.WebControls.WebParts
    Imports System.Drawing
    Imports Microsoft.SharePoint.Navigation
    ```

    ```csharp
    using System;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebControls;
    using System.Collections;
    using System.Data;
    using System.Web.UI;
    using System.Web.UI.WebControls;
    using System.Web.UI.WebControls.WebParts;
    using System.Drawing;
    using Microsoft.SharePoint.Navigation;
    ```

3. Adicione o seguinte código ao método `Page_Load`:

    ```vb
    Try
        ' Reference the Tasks list on the SharePoint site.
        ' Replace "TestServer" with a valid SharePoint server name.
        Dim site As SPSite = New SPSite("http://TestServer")
        Dim list As SPList = site.AllWebs(0).Lists("Tasks")
        ' string text = "";
        Dim sum As Integer = 0
        Table1.Rows.Clear()
        ' Add table headers.
        Dim hr As TableHeaderRow = New TableHeaderRow
        hr.BackColor = Color.LightBlue
        Dim hc1 As TableHeaderCell = New TableHeaderCell
        Dim hc2 As TableHeaderCell = New TableHeaderCell
        hc1.Text = "Expense Report Name"
        hc2.Text = "Amount Exceeded"
        hr.Cells.Add(hc1)
        hr.Cells.Add(hc2)
        ' Add the TableHeaderRow as the first item
        ' in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr)
        ' Iterate through the tasks in the Task list and collect those
        ' that have values in the "Related Content" and "Outcome" fields
        ' - the fields written to when expense approval is required.
        For Each item As SPListItem In list.Items
            Dim s_relContent As String = ""
            Dim s_outcome As String = ""
            Try
                ' Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related Content")
                s_outcome = item.GetFormattedValue("Outcome")
            Catch erx As System.Exception
                ' Task does not have fields - skip it.
                Continue For
            End Try
            ' Convert amount to an int and keep a running total.
            If (Not String.IsNullOrEmpty(s_relContent) And Not
              String.IsNullOrEmpty(s_outcome)) Then
                sum = (sum + Convert.ToInt32(s_outcome))
                Dim relContent As TableCell = New TableCell
                relContent.Text = s_relContent
                Dim outcome As TableCell = New TableCell
                outcome.Text = ("$" + s_outcome)
                Dim dataRow2 As TableRow = New TableRow
                dataRow2.Cells.Add(relContent)
                dataRow2.Cells.Add(outcome)
                Table1.Rows.Add(dataRow2)
            End If
        Next
        ' Report the sum of the reports in the table footer.
        Dim tfr As TableFooterRow = New TableFooterRow
        tfr.BackColor = Color.LightGreen
        ' Create a TableCell object to contain the
        ' text for the footer.
        Dim ftc1 As TableCell = New TableCell
        Dim ftc2 As TableCell = New TableCell
        ftc1.Text = "TOTAL: "
        ftc2.Text = ("$" + Convert.ToString(sum))
        ' Add the TableCell object to the Cells
        ' collection of the TableFooterRow.
        tfr.Cells.Add(ftc1)
        tfr.Cells.Add(ftc2)
        ' Add the TableFooterRow to the Rows
        ' collection of the table.
        Table1.Rows.Add(tfr)
    Catch errx As Exception
        System.Diagnostics.Debug.WriteLine(("Error: " + errx.ToString))
    End Try
    ```

    ```csharp
    try
    {
        // Reference the Tasks list on the SharePoint site.
        // Replace "TestServer" with a valid SharePoint server name.
        SPSite site = new SPSite("http://TestServer");
        SPList list = site.AllWebs[0].Lists["Tasks"];

        // string text = "";
        int sum = 0;

        Table1.Rows.Clear();

        // Add table headers.
        TableHeaderRow hr = new TableHeaderRow();
        hr.BackColor = Color.LightBlue;
        TableHeaderCell hc1 = new TableHeaderCell();
        TableHeaderCell hc2 = new TableHeaderCell();
        hc1.Text = "Expense Report Name";
        hc2.Text = "Amount Exceeded";
        hr.Cells.Add(hc1);
        hr.Cells.Add(hc2);
        // Add the TableHeaderRow as the first item
        // in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr);

        // Iterate through the tasks in the Task list and collect those
        // that have values in the "Related Content" and "Outcome"
        // fields - the fields written to when expense approval is
        // required.
        foreach (SPListItem item in list.Items)
        {
            string s_relContent = "";
            string s_outcome = "";

            try
            {
                // Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related
                  Content");
                s_outcome = item.GetFormattedValue("Outcome");
            }
            catch
            {
                // Task does not have fields - skip it.
                continue;
            }

            if (!String.IsNullOrEmpty(s_relContent) &&
              !String.IsNullOrEmpty(s_outcome))
            {
                // Convert amount to an int and keep a running total.
                sum += Convert.ToInt32(s_outcome);
                TableCell relContent = new TableCell();
                relContent.Text = s_relContent;
                TableCell outcome = new TableCell();
                outcome.Text = "$" + s_outcome;
                TableRow dataRow2 = new TableRow();
                dataRow2.Cells.Add(relContent);
                dataRow2.Cells.Add(outcome);
                Table1.Rows.Add(dataRow2);
            }
        }

        // Report the sum of the reports in the table footer.
           TableFooterRow tfr = new TableFooterRow();
        tfr.BackColor = Color.LightGreen;

        // Create a TableCell object to contain the
        // text for the footer.
        TableCell ftc1 = new TableCell();
        TableCell ftc2 = new TableCell();
        ftc1.Text = "TOTAL: ";
        ftc2.Text = "$" + Convert.ToString(sum);

        // Add the TableCell object to the Cells
        // collection of the TableFooterRow.
        tfr.Cells.Add(ftc1);
        tfr.Cells.Add(ftc2);

        // Add the TableFooterRow to the Rows
        // collection of the table.
        Table1.Rows.Add(tfr);
    }

    catch (Exception errx)
    {
        System.Diagnostics.Debug.WriteLine("Error: " + errx.ToString());
    }
    ```

    > [!WARNING]
    > Certifique-se de substituir "TestServer" no código pelo nome de um servidor válido que esteja executando o SharePoint.

## <a name="test-the-application-page"></a>Testar a página do aplicativo
 Em seguida, determine se a página do aplicativo exibe os dados de despesa corretamente.

#### <a name="to-test-the-application-page"></a>Para testar a página do aplicativo

1. Escolha a tecla **F5** para executar e implantar o projeto no SharePoint.

2. Escolha o botão **página inicial** e, em seguida, escolha o link **documentos compartilhados** na barra de início rápido para exibir a lista de documentos compartilhados no site do SharePoint.

3. Para representar relatórios de despesas para este exemplo, carregue alguns documentos novos na lista de documentos escolhendo o link **documentos** na guia **LibraryTools** na parte superior da página e, em seguida, escolhendo o botão **carregar documento** na faixa de ferramentas da ferramenta.

4. Depois de carregar alguns documentos, crie uma instância do fluxo de trabalho escolhendo o link da **biblioteca** na guia **LibraryTools** na parte superior da página e, em seguida, escolhendo o botão **configurações da biblioteca** na faixa de opções da ferramenta.

5. Na página **configurações da biblioteca de documentos** , escolha o link **configurações de fluxo de trabalho** na seção **permissões e gerenciamento** .

6. Na página **configurações de fluxo de trabalho** , escolha o link **Adicionar um fluxo de trabalho** .

7. Na página **Adicionar um fluxo de trabalho** , escolha o fluxo de trabalho **ExpenseReport-Workflow1** , insira um nome para o fluxo de trabalho, como **ExpenseTest**, e escolha o botão **Avançar** .

    O formulário Associação de fluxo de trabalho é exibido. Use-o para relatar o valor do limite de despesas.

8. No formulário associação, insira **1000** na caixa **limite de aprovação automática** e, em seguida, escolha o botão **associar fluxo de trabalho** .

9. Escolha o botão **página inicial** para retornar ao Home Page do SharePoint.

10. Escolha o link **documentos compartilhados** na barra de início rápido.

11. Escolha um dos documentos carregados para exibir uma seta suspensa, escolha-o e escolha o item **fluxos de trabalho** .

12. Escolha a imagem ao lado de ExpenseTest para exibir o formulário de inicialização do fluxo de trabalho.

13. Na caixa de texto **total de despesas** , insira um valor maior que 1000 e, em seguida, escolha o botão **Iniciar fluxo de trabalho** .

     Quando uma despesa relatada excede o valor de despesa alocado, uma tarefa é adicionada à Lista de Tarefas. Uma coluna denominada **ExpenseTest** com o valor **concluído** também é adicionada ao item de relatório de despesas na lista documentos compartilhados.

14. Repita as etapas 11-13 com outros documentos na lista de documentos compartilhados. (O número exato de documentos não é importante.)

15. Exiba a página do aplicativo de Resumo de relatórios de despesas abrindo a seguinte URL em um navegador da Web: **http://**<em>systemname</em>**/_layouts/ExpenseReport/ApplicationPage1.aspx**.

     A página Resumo do relatório de despesas lista todos os relatórios de despesas que excederam a quantidade alocada, o valor que ele excedeu e o valor total para todos os relatórios.

## <a name="next-steps"></a>Próximas etapas
 Para obter mais informações sobre páginas de aplicativo do SharePoint, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

 Você pode aprender mais sobre como projetar o conteúdo da página do SharePoint usando o Visual Web designer no Visual Studio a partir destes tópicos:

- [Crie Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md).

- [Crie controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md).

## <a name="see-also"></a>Consulte também

- [Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [Como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md)
- [Criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)