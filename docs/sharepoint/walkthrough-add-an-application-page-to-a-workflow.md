---
title: 'Passo a passo: Adicionar uma página de aplicativo a um fluxo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4bdb01e5cbb45b9986e61a99e18b5984e92d37dd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49866890"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>Passo a passo: Adicionar uma página de aplicativo a um fluxo de trabalho
  Este passo a passo demonstra como adicionar uma página de aplicativo que exibe dados derivados de um fluxo de trabalho a um projeto de fluxo de trabalho. Ele se baseia no projeto descrito no tópico [instruções passo a passo: criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).

 Este passo a passo demonstra as seguintes tarefas:

- Adicionando uma página ASPX de aplicativo para um projeto de fluxo de trabalho do SharePoint.

- Obtendo dados do projeto de fluxo de trabalho e manipulá-los.

- Exibindo dados em uma tabela na página do aplicativo.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

-   Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e do SharePoint.

-   Visual Studio.

-   Você também tem que concluir o projeto no tópico [instruções passo a passo: criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).

## <a name="ammend-the-workflow-code"></a>Ammend o código de fluxo de trabalho
 Primeiro, adicione uma linha de código para o fluxo de trabalho para definir o valor da coluna de resultado para a quantidade do relatório de despesas. Esse valor é usado posteriormente o cálculo de resumo de relatório de despesas.

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>Para definir o valor da coluna de resultado no fluxo de trabalho

1.  Carregar o projeto concluído do tópico [instruções passo a passo: Criando um fluxo de trabalho com associação e formulários de iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2.  Abra o código para *Workflow1.cs* ou *Workflow1.vb* (dependendo da sua linguagem de programação).

3.  Na parte inferior do `createTask1_MethodInvoking` método, adicione o seguinte código:

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>Criar uma página de aplicativo
 Em seguida, adicione um formulário ASPX ao projeto. Este formulário exibirá os dados obtidos do projeto de fluxo de trabalho de relatório de despesas. Para fazer isso, você adicionará uma página de aplicativo. Uma página de aplicativo usa a mesma página mestra como outras páginas do SharePoint, que significa que ele será semelhante a outras páginas no site do SharePoint.

#### <a name="to-add-an-application-page-to-the-project"></a>Para adicionar uma página de aplicativo ao projeto

1.  Escolha o projeto ExpenseReport e, em seguida, na barra de menus, escolha **Project** > **Adicionar Novo Item**.

2.  No **modelos** painel, escolha o **página de aplicativo** modelo, use o nome padrão para o item de projeto (**ApplicationPage1.aspx**) e escolha o **Adicionar** botão.

3.  No [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ApplicationPage1.aspx, substitua o `PlaceHolderMain` seção com o seguinte:

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     Este código adiciona uma tabela para a página junto com um título.

4.  Adicionar um título para a página de aplicativo, substituindo o `PlaceHolderPageTitleInTitleArea` seção com o seguinte:

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>O aplicativo de página de código
 Em seguida, adicione o código para a página de resumo do aplicativo de relatório de despesas. Quando você abre a página, o código examina a lista de tarefas no SharePoint para despesas que excederam o limite de gasto alocado. O relatório lista cada item junto com a soma das despesas.

#### <a name="to-code-the-application-page"></a>Para o aplicativo de página de código

1.  Escolha o **ApplicationPage1.aspx** nó e em seguida, na barra de menus, escolha **exibição** > **código** para exibir o código por trás da página de aplicativo.

2.  Substitua os **usando** ou **importação** instruções (dependendo da sua linguagem de programação) na parte superior da classe com o seguinte:

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

3.  Adicione o seguinte código ao método `Page_Load`:

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
    >  Certifique-se de substituir "TestServer" no código com o nome de um servidor válido que está executando o SharePoint.

## <a name="test-the-application-page"></a>Testar a página de aplicativo
 Em seguida, determine se a página de aplicativo exibe corretamente os dados de despesas.

#### <a name="to-test-the-application-page"></a>Para testar a página do aplicativo

1. Escolha o **F5** tecla para executar e implantar o projeto do SharePoint.

2. Escolha o **página inicial** botão e, em seguida, escolha o **documentos compartilhados** link na barra QuickLaunch para exibir a lista de documentos compartilhados no site do SharePoint.

3. Para representar os relatórios de despesas para este exemplo, carregar alguns novos documentos em lista de documentos, escolhendo o **documentos** no link a **LibraryTools** guia na parte superior da página e, em seguida, escolhendo o  **Carregar documento** botão na faixa de opções da ferramenta.

4. Depois de carregar alguns documentos, criar uma instância de fluxo de trabalho escolhendo a **biblioteca** no link a **LibraryTools** guia na parte superior da página e, em seguida, escolhendo o **configurações da biblioteca**botão na faixa de opções da ferramenta.

5. No **Document Library Settings** , escolha o **configurações de fluxo de trabalho** link no **permissões e gerenciamento** seção.

6. No **configurações de fluxo de trabalho** , escolha o **adicionar um fluxo de trabalho** link.

7. No **adicionar um fluxo de trabalho** , escolha o **ExpenseReport - Workflow1** fluxo de trabalho, insira um nome para o fluxo de trabalho, como **ExpenseTest**e, em seguida, escolha o **Próxima** botão.

    O formulário de associação de fluxo de trabalho é exibida. Usá-lo para relatar o valor de limite de gastos.

8. No formulário de associação, insira **1000** para o **limite de aprovação automática** caixa e, em seguida, escolha o **associar o fluxo de trabalho** botão.

9. Escolha o **doméstica** botão para retornar à home page do SharePoint.

10. Escolha o **documentos compartilhados** link na barra de início rápido.

11. Escolha um dos documentos carregados para exibir uma seta suspensa, escolha-o e, em seguida, escolha o **fluxos de trabalho** item.

12. Escolha a imagem ao lado de ExpenseTest para exibir o formulário de iniciação do fluxo de trabalho.

13. No **Total de despesa** caixa de texto, insira um valor que é maior que 1000 e, em seguida, escolha o **Iniciar fluxo de trabalho** botão.

     Quando uma despesa relatada excede a quantidade de despesas alocado, uma tarefa é adicionada à lista de tarefas. Uma coluna denominada **ExpenseTest** com o valor **concluído** também é adicionado ao item de relatório de despesas na lista de documentos compartilhados.

14. Repita as etapas 11 a 13 com outros documentos na lista de documentos compartilhados. (O número exato de documentos não é importante.)

15. Exibir a página de resumo do aplicativo de relatório de despesas, abrindo a seguinte URL em um navegador da Web: **http://**<em>SystemName</em>**/_layouts/ExpenseReport/ApplicationPage1.aspx**.

     A página Resumo do relatório de despesas lista todos os relatórios de despesas que excedeu a quantidade alocada, a quantidade que foi excedido pelo e o valor total para todos os relatórios.

## <a name="next-steps"></a>Próximas etapas
 Para obter mais informações sobre páginas de aplicativo do SharePoint, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

 Você pode aprender mais sobre como projetar o conteúdo da página do SharePoint usando o Visual Web Designer no Visual Studio com estes tópicos:

-   [Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md).

-   [Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md).

## <a name="see-also"></a>Consulte também

- [Passo a passo: Criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [Como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md)
- [Criar páginas de aplicativo do SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)