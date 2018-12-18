---
title: Criar um aplicativo de dados simples usando o ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
caps.latest.revision: 46
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4754cad05858ed48fd421301b4b0f1d2c569a926
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49824276"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>Criar um aplicativo de dados simples usando o ADO.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você cria um aplicativo que manipule dados em um banco de dados, executar tarefas básicas, tais definindo cadeias de conexão, inserção de dados e executar procedimentos armazenados. Ao seguir este tópico, você pode descobrir como interagir com um banco de dados de dentro de um aplicativo simples de "formulários sobre dados" do Windows Forms usando o Visual c# ou Visual Basic e ADO.NET.  Todas as tecnologias de dados do .NET — inclusive conjuntos de dados, o LINQ to SQL e Entity Framework —, por fim, execute as etapas que são muito semelhantes às mostradas neste artigo.  
  
 Este artigo demonstra uma maneira simples de obter dados para fora de um banco de dados de uma maneira muito rápida. Se seu aplicativo precisa modificar dados de maneiras não triviais e atualizar o banco de dados, você deve considerar usando o Entity Framework e usando a associação de dados para sincronizar automaticamente os controles de interface do usuário para as alterações nos dados subjacentes.  
  
> [!IMPORTANT]
>  Para manter o código simples, ele não inclui tratamento de exceção pronta para produção.  
  
 **Neste tópico**  
  
-   [Configurar o banco de dados de exemplo](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_setupthesampledatabase)  
  
-   [Criar os formulários e adicionar controles](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_createtheformsandaddcontrols)  
  
-   [A cadeia de caracteres de conexão da Store](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_storetheconnectionstring)  
  
-   [Recuperar a cadeia de conexão](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_retrievetheconnectionstring)  
  
-   [Escreva o código para os formulários](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_writethecodefortheforms)  
  
-   [Teste seu aplicativo](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_testyourapplication)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para criar o aplicativo, você precisará de:  
  
- Visual Studio Community Edition.  
  
- SQL Server Express LocalDB.  
  
- O banco de dados de exemplo pequeno que você criar seguindo as etapas em [criar um banco de dados SQL usando um script](../data-tools/create-a-sql-database-by-using-a-script.md).  
  
- A cadeia de conexão para o banco de dados depois de você configurá-lo. Você pode encontrar esse valor abrindo **Pesquisador de objetos do SQL Server**, abrindo o menu de atalho para o banco de dados, selecionando **Properties**e, em seguida, rolando até o **ConnectionString** propriedade.  
  
  Este tópico pressupõe que você está familiarizado com a funcionalidade básica do IDE do Visual Studio e pode criar um aplicativo Windows Forms, adicionar formulários a esse projeto, colocar botões e outros controles em formulários, definem as propriedades desses controles e codificar eventos simples . Se você não estiver confortável com essas tarefas, sugerimos que você conclua a [Introdução ao Visual c# e Visual Basic](../ide/getting-started-with-visual-csharp-and-visual-basic.md) antes de iniciar este tópico.  
  
##  <a name="BKMK_setupthesampledatabase"></a> Configurar o banco de dados de exemplo  
 O banco de dados de exemplo para este passo a passo consiste nas tabelas clientes e pedidos. As tabelas não contêm dados inicialmente, mas você adicionará dados ao executar o aplicativo que você vai criar. O banco de dados também tem cinco procedimentos armazenados simples. [Criar um banco de dados SQL usando um script](../data-tools/create-a-sql-database-by-using-a-script.md) contém um script Transact-SQL que cria as tabelas, as chaves primária e estrangeiras, restrições e os procedimentos armazenados.  
  
##  <a name="BKMK_createtheformsandaddcontrols"></a> Criar os formulários e adicionar controles  
  
1. Criar um projeto para um aplicativo do Windows Forms e nomeie-a como SimpleDataApp.  
  
    Visual Studio cria o projeto e vários arquivos, incluindo um formulário vazio do Windows que é denominado Form1.  
  
2. Adicione dois formulários do Windows ao seu projeto para que ele tenha três formulários e forneça a eles os seguintes nomes:  
  
   -   Navegação  
  
   -   NewCustomer  
  
   -   FillOrCancel  
  
3. Para cada formulário, adicione as caixas de texto, botões e outros controles que aparecem nas ilustrações a seguir. Para cada controle, defina as propriedades que descrevem as tabelas.  
  
   > [!NOTE]
   >  A caixa de grupo e os controles de rótulo adicionam clareza mas não são usados no código.  
  
   **Formulário de navegação**  
  
   ![Caixa de diálogo de navegação](../data-tools/media/simpleappnav.png "SimpleAppNav")  
  
|Controles para o formulário de navegação|Propriedades|  
|--------------------------------------|----------------|  
|Botão|Nome = btnGoToAdd|  
|Botão|Nome = btnGoToFillOrCancel|  
|Botão|Nome = btnExit|  
  
 **Formulário NewCustomer**  
  
 ![Adicionar um novo cliente e fazer um pedido](../data-tools/media/simpleappnewcust.png "SimpleAppNewCust")  
  
|Controles para o formulário NewCustomer|Propriedades|  
|---------------------------------------|----------------|  
|TextBox|Nome = txtCustomerName|  
|TextBox|Nome = txtCustomerID<br /><br /> ReadOnly = True|  
|Botão|Name = btnCreateAccount|  
|NumericUpdown|DecimalPlaces = 0<br /><br /> Máximo = 5000<br /><br /> Nome = numOrderAmount|  
|DateTimePicker|Formato = abreviado<br /><br /> Nome = dtpOrderDate|  
|Botão|Nome = btnPlaceOrder|  
|Botão|Name = btnAddAnotherAccount|  
|Botão|Nome = btnAddFinish|  
  
 **Formulário FillOrCancel**  
  
 ![preencher ou Cancelar ordens](../data-tools/media/simpleappcancelfill.png "SimpleAppCancelFill")  
  
|Controles para o formulário FillOrCancel|Propriedades|  
|----------------------------------------|----------------|  
|TextBox|Nome = txtOrderID|  
|Botão|Name = btnFindByOrderID|  
|DateTimePicker|Formato = abreviado<br /><br /> Nome = dtpFillDate|  
|DataGridView|Nome = dgvCustomerOrders<br /><br /> ReadOnly = True<br /><br /> RowHeadersVisible = False|  
|Botão|Nome = btnCancelOrder|  
|Botão|Nome = btnFillOrder|  
|Botão|Nome = btnFinishUpdates|  
  
##  <a name="BKMK_storetheconnectionstring"></a> A cadeia de caracteres de conexão da Store  
 Quando seu aplicativo tenta abrir uma conexão ao banco de dados, seu aplicativo deve ter acesso à cadeia de conexão. Para evitar inserir a cadeia de caracteres manualmente em cada formulário, armazenar a cadeia de caracteres no arquivo de configuração de aplicativo em seu projeto e crie um método que retorna a cadeia de caracteres quando o método é chamado de qualquer formulário em seu aplicativo.  
  
 Você pode encontrar a cadeia de conexão no **Pesquisador de objetos do SQL Server** por clicando duas vezes o banco de dados, selecionando **propriedades**e, em seguida, localizando a propriedade ConnectionString. Use Ctrl + A para selecionar a cadeia de caracteres.  
  
1.  Na **Gerenciador de soluções**, selecione o **Properties** nó sob o projeto e, em seguida, selecione **Settings**.  
  
2.  No **nome** coluna, digite `connString`.  
  
3.  No **tipo** lista, selecione **(cadeia de caracteres de Conexão)**.  
  
4.  No **escopo** lista, selecione **aplicativo**.  
  
5.  No **valor** coluna, insira sua cadeia de conexão (sem qualquer fora de aspas) e, em seguida, salve suas alterações.  
  
> [!NOTE]
>  Em um aplicativo real, você deve armazenar a cadeia de caracteres de conexão com segurança, conforme descrito em [cadeias de caracteres de Conexão e arquivos de configuração](http://msdn.microsoft.com/library/37df2641-661e-407a-a3fb-7bf9540f01e8).  
  
##  <a name="BKMK_retrievetheconnectionstring"></a> Recuperar a cadeia de conexão  
  
1.  Na barra de menus, selecione **Project** > **Add Reference**e, em seguida, adicione uma referência à dll.  
  
2.  Na barra de menus, selecione **Project** > **Add Class** para adicionar um arquivo de classe ao seu projeto e, em seguida, nomeie o arquivo `Utility`.  
  
     Visual Studio cria o arquivo e exibe-o em **Gerenciador de soluções**.  
  
3.  No arquivo de utilitário, substitua o código de espaço reservado com o código a seguir. Observe os comentários numerados (prefixados com o Util-) que identificam seções do código. A tabela que segue o código chama pontos chave.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    //Util-1 More namespaces.  
    using System.Configuration;   
  
    namespace SimpleDataApp  
    {  
        internal class Utility  
        {  
  
            //Get the connection string from App config file.  
            internal static string GetConnectionString()  
            {  
                //Util-2 Assume failure.  
                string returnValue = null;  
  
                //Util-3 Look for the name in the connectionStrings section.  
                ConnectionStringSettings settings =  
                ConfigurationManager.ConnectionStrings["SimpleDataApp.Properties.Settings.connString"];  
  
                //If found, return the connection string.  
                if (settings != null)  
                    returnValue = settings.ConnectionString;  
  
                return returnValue;  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.Linq  
    Imports System.Text  
    Imports System.Threading.Tasks  
    ' Util-1 More namespaces.  
    Imports System.Configuration  
  
    Namespace SimpleDataApp  
        Friend Class Utility  
  
            ' Get connection string from App config file.  
            Friend Shared Function GetConnectionString() As String  
  
                ' Util-2 Assume failure.  
                Dim returnValue As String = Nothing  
  
                ' Util-3 Look for the name in the connectionStrings section.  
                Dim settings As ConnectionStringSettings = ConfigurationManager.ConnectionStrings("SimpleDataApp.My.MySettings.connString")  
  
                ' If found, return the connection string.  
                If settings IsNot Nothing Then  
                    returnValue = settings.ConnectionString  
                End If  
  
                Return returnValue  
            End Function  
        End Class  
    End Namespace  
    ```  
  
    |Comentário|Descrição|  
    |-------------|-----------------|  
    |Util-1|Adicionar o `System.Configuration` namespace.|  
    |Util-2|Defina uma variável `returnValue`e inicializá-lo para `null` (c#) ou `Nothing` (Visual Basic).|  
    |Util-3|Mesmo que você inseriu `connString` como o nome da cadeia de caracteres de conexão na **Properties** janela, você deve especificar `"SimpleDataApp.Properties.Settings.connString"` (c#) ou `"SimpleDataApp.My.MySettings.connString"` (Visual Basic) no código.|  
  
##  <a name="BKMK_writethecodefortheforms"></a> Escreva o código para os formulários  
 Esta seção contém visões gerais breves das quais cada formulário faz e mostra o código que cria os formulários. Comentários numerados identificam seções do código.  
  
### <a name="navigation-form"></a>Formulário de navegação  
 O formulário navegação abre quando você executar o aplicativo. O **adicionar uma conta** botão abre o formulário NewCustomer. O **preencher ou Cancelar ordens** botão abre o formulário FillOrCancel. O **Exit** botão fecha o aplicativo.  
  
#### <a name="make-the-navigation-form-the-startup-form"></a>Tornar a navegação formam o formulário de inicialização  
 Se você estiver usando c#, em **Gerenciador de soluções**, abra Program.cs e altere o `Application.Run` linha a esta: `Application.Run(new Navigation());`  
  
 Se você estiver usando Visual Basic, em **Gerenciador de soluções**, abra o **Properties** janela, selecione o **aplicativo** guia e, em seguida, selecione  **Simpledataapp** no **formulário de inicialização** lista.  
  
#### <a name="create-event-handlers"></a>Criar manipuladores de eventos  
 Clique duas vezes em três botões no formulário para criar métodos de manipulador de eventos vazio.  
  
#### <a name="create-code-for-navigation"></a>Criar o código para navegação  
 No formulário de navegação, substitua o código existente pelo código a seguir.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
  
namespace SimpleDataApp  
{  
    public partial class Navigation : Form  
    {  
        public Navigation()  
        {  
            InitializeComponent();  
        }  
  
        //Open the NewCustomer form as a dialog box, which will return focus to the calling form when it closes.  
        private void btnGoToAdd_Click(object sender, EventArgs e)  
        {  
            Form frm = new NewCustomer();  
            frm.Show();  
        }  
  
        //Open the FillorCancel form as a dialog box.  
        private void btnGoToFillOrCancel_Click(object sender, EventArgs e)  
        {  
            Form frm = new FillOrCancel();  
            frm.ShowDialog();  
        }  
  
        //Close the application, not just the Navigation form.  
        private void btnExit_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
  
Namespace SimpleDataApp  
    Partial Public Class Navigation  
        Inherits Form  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' Open the NewCustomer form as a dialog box, which will return focus to the calling form when it closes.  
        Private Sub btnGoToAdd_Click() Handles btnGoToAdd.Click  
            Dim frm As Form = New NewCustomer()  
            frm.Show()  
        End Sub  
  
        ' Open the FillorCancel form as a dialog box.  
        Private Sub btnGoToFillOrCancel_Click() Handles btnGoToFillOrCancel.Click  
            Dim frm As Form = New FillOrCancel()  
            frm.ShowDialog()  
        End Sub  
  
        ' Close the application, not just the Navigation form.  
        Private Sub btnExit_Click() Handles btnExit.Click  
            Me.Close()  
        End Sub  
    End Class  
End Namespace  
  
```  
  
### <a name="newcustomer-form"></a>Formulário NewCustomer  
 Quando você inserir um nome de cliente e, em seguida, selecione a **criar conta** botão, o formulário de NewCustomer cria uma conta de cliente e do SQL Server retorna um valor de identidade como o novo número da conta. Você, em seguida, fazer um pedido para a nova conta especificando um valor e uma data do pedido e selecionando o **fazer pedido** botão.  
  
#### <a name="create-event-handlers"></a>Criar manipuladores de eventos  
 Criar um vazio, clique em manipulador de eventos para cada botão no formulário.  
  
#### <a name="create-code-for-newcustomer"></a>Criar o código para NewCustomer  
 Adicione o seguinte código ao formulário de NewCustomer. Repasse cada bloco de código usando os comentários numerados e a tabela após o código.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
//NC-1 More namespaces.  
using System.Data.SqlClient;  
using System.Configuration;  
  
namespace SimpleDataApp  
{  
    public partial class NewCustomer : Form  
    {  
        //NC-2 Storage for IDENTITY values returned from database.  
        private int parsedCustomerID;  
        private int orderID;  
  
        //NC-3 Specify a connection string.  
        string connstr = SimpleDataApp.Utility.GetConnectionString();  
  
        public NewCustomer()  
        {  
            InitializeComponent();  
        }  
  
        //NC-4 Create account.  
        private void btnCreateAccount_Click(object sender, EventArgs e)  
        {  
            //NC-5 Set up and run stored procedure only if Customer Name is present.  
            if (isCustomerName())  
            {  
  
                //NC-6 Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //NC-7 Create a SqlCommand, and identify it as a stored procedure.  
                SqlCommand cmdNewCustomer = new SqlCommand("Sales.uspNewCustomer", conn);  
                cmdNewCustomer.CommandType = CommandType.StoredProcedure;  
  
                //NC-8 Add input parameter from the stored procedure and specify what to use as its value.  
                cmdNewCustomer.Parameters.Add(new SqlParameter("@CustomerName", SqlDbType.NVarChar, 40));  
                cmdNewCustomer.Parameters["@CustomerName"].Value = txtCustomerName.Text;  
  
                //NC-9 Add output parameter.  
                cmdNewCustomer.Parameters.Add(new SqlParameter("@CustomerID", SqlDbType.Int));  
                cmdNewCustomer.Parameters["@CustomerID"].Direction = ParameterDirection.Output;  
  
                //NC-10 try-catch-finally  
                try  
                {  
                    //NC-11 Open the connection.  
                    conn.Open();  
  
                    //NC-12 Run the stored procedure.  
                    cmdNewCustomer.ExecuteNonQuery();  
  
                    //NC-13 Customer ID is an IDENTITY value from the database.   
                    this.parsedCustomerID = (int)cmdNewCustomer.Parameters["@CustomerID"].Value;  
                    this.txtCustomerID.Text = Convert.ToString(parsedCustomerID);  
  
                }  
                catch  
                {  
                    //NC-14 A simple catch.  
  
                    MessageBox.Show("Customer ID was not returned. Account could not be created.");  
                }  
                finally  
                {  
                    //NC-15 Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //NC-16 Verify that Customer Name is present.  
        private bool isCustomerName()  
        {  
            if (txtCustomerName.Text == "")  
            {  
                MessageBox.Show("Please enter a name.");  
                return false;  
            }  
            else  
            {  
                return true;  
            }  
        }  
  
        //NC-17 Place order.  
        private void btnPlaceOrder_Click(object sender, EventArgs e)  
        {  
            //NC-18 Set up and run stored procedure only if required input is present.  
            if (isPlaceOrderReady())  
            {  
                // Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //NC-19 Create SqlCommand and identify it as a stored procedure.  
                SqlCommand cmdNewOrder = new SqlCommand("Sales.uspPlaceNewOrder", conn);  
                cmdNewOrder.CommandType = CommandType.StoredProcedure;  
  
                //NC-20 @CustomerID, which was an output parameter from uspNewCustomer.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@CustomerID", SqlDbType.Int));  
                cmdNewOrder.Parameters["@CustomerID"].Value = this.parsedCustomerID;  
  
                //NC-21 @OrderDate.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@OrderDate", SqlDbType.DateTime, 8));  
                cmdNewOrder.Parameters["@OrderDate"].Value = dtpOrderDate.Value;  
  
                //NC-22 @Amount.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@Amount", SqlDbType.Int));  
                cmdNewOrder.Parameters["@Amount"].Value = numOrderAmount.Value;  
  
                //NC-23 @Status. For a new order, the status is always O (open).  
                cmdNewOrder.Parameters.Add(new SqlParameter("@Status", SqlDbType.Char, 1));  
                cmdNewOrder.Parameters["@Status"].Value = "O";  
  
                //NC-24 Add return value for stored procedure, which is orderID.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@RC", SqlDbType.Int));  
                cmdNewOrder.Parameters["@RC"].Direction = ParameterDirection.ReturnValue;  
  
                //try-catch-finally  
                try  
                {  
                    //Open connection.  
                    conn.Open();  
  
                    //Run the stored procedure.  
                    cmdNewOrder.ExecuteNonQuery();  
  
                    //NC-25 Display the order number.  
                    this.orderID = (int)cmdNewOrder.Parameters["@RC"].Value;  
                    MessageBox.Show("Order number " + this.orderID + " has been submitted.");  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("Order could not be placed.");  
                }  
                finally  
                {  
                    //Close connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //NC-26 Verify that order data is ready.  
        private bool isPlaceOrderReady()  
        {  
            // Verify that CustomerID is present.  
            if (txtCustomerID.Text == "")  
            {  
                MessageBox.Show("Please create customer account before placing order.");  
                return false;  
            }  
  
            // Verify that Amount isn't 0.   
            else if ((numOrderAmount.Value < 1))  
            {  
                MessageBox.Show("Please specify an order amount.");  
                return false;  
            }  
            else  
            {  
                // Order can be submitted.  
                return true;  
            }  
        }  
  
        //NC-27 Reset the form for another new account.  
        private void btnAddAnotherAccount_Click(object sender, EventArgs e)  
        {  
            this.ClearForm();  
        }  
  
        //NC-28 Clear values from controls.  
        private void ClearForm()  
        {  
            txtCustomerName.Clear();  
            txtCustomerID.Clear();  
            dtpOrderDate.Value = DateTime.Now;  
            numOrderAmount.Value = 0;  
            this.parsedCustomerID = 0;  
        }  
  
        //NC-29 Close the form.  
        private void btnAddFinish_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
  
    }  
}  
  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
' NC-1 More namespaces.  
Imports System.Data.SqlClient  
Imports System.Configuration  
  
Namespace SimpleDataApp  
    Partial Public Class NewCustomer  
        Inherits Form  
  
        ' NC-2 Storage for IDENTITY values returned from database.  
        Private parsedCustomerID As Integer  
        Private orderID As Integer  
  
        ' NC-3 Specify a connection string.  
        Private connstr As String = SimpleDataApp.Utility.GetConnectionString()  
  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' NC-4 Create account.  
        Private Sub btnCreateAccount_Click() Handles btnCreateAccount.Click  
  
            ' NC-5 Set up and run stored procedure only if Customer Name is present.  
            If isCustomerName() Then  
  
                ' NC-6 Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' NC-7 Create a SqlCommand, and identify it as a stored procedure.  
                Dim cmdNewCustomer As New SqlCommand("Sales.uspNewCustomer", conn)  
                cmdNewCustomer.CommandType = CommandType.StoredProcedure  
  
                ' NC-8 Add input parameter from the stored procedure and specify what to use as its value.  
                cmdNewCustomer.Parameters.Add(New SqlParameter("@CustomerName", SqlDbType.NVarChar, 40))  
                cmdNewCustomer.Parameters("@CustomerName").Value = txtCustomerName.Text  
  
                ' NC-9 Add output parameter.  
                cmdNewCustomer.Parameters.Add(New SqlParameter("@CustomerID", SqlDbType.Int))  
                cmdNewCustomer.Parameters("@CustomerID").Direction = ParameterDirection.Output  
  
                ' NC-10 try-catch-finally  
                Try  
                    ' NC-11 Open the connection.  
                    conn.Open()  
  
                    ' NC-12 Run the stored procedure.  
                    cmdNewCustomer.ExecuteNonQuery()  
  
                    ' NC-13 Customer ID is an IDENTITY value from the database.   
                    Me.parsedCustomerID = CInt(cmdNewCustomer.Parameters("@CustomerID").Value)  
                    Me.txtCustomerID.Text = Convert.ToString(parsedCustomerID)  
  
                Catch  
                    ' NC-14 A simple catch.  
                    MessageBox.Show("Customer ID was not returned. Account could not be created.")  
                Finally  
                    ' NC-15 Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' NC-16 Verify that Customer Name is present.  
        Private Function isCustomerName() As Boolean  
            If txtCustomerName.Text = "" Then  
                MessageBox.Show("Please enter a name.")  
                Return False  
            Else  
                Return True  
            End If  
        End Function  
  
        ' NC-17 Place order.  
        Private Sub btnPlaceOrder_Click() Handles btnPlaceOrder.Click  
  
            ' NC-18 Set up and run stored procedure only if necessary input is present.  
            If isPlaceOrderReady() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' NC-19 Create SqlCommand and identify it as a stored procedure.  
                Dim cmdNewOrder As New SqlCommand("Sales.uspPlaceNewOrder", conn)  
                cmdNewOrder.CommandType = CommandType.StoredProcedure  
  
                ' NC-20 @CustomerID, which was an output parameter from uspNewCustomer.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@CustomerID", SqlDbType.Int))  
                cmdNewOrder.Parameters("@CustomerID").Value = Me.parsedCustomerID  
  
                ' NC-21 @OrderDate.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@OrderDate", SqlDbType.DateTime, 8))  
                cmdNewOrder.Parameters("@OrderDate").Value = dtpOrderDate.Value  
  
                ' NC-22 @Amount.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@Amount", SqlDbType.Int))  
                cmdNewOrder.Parameters("@Amount").Value = numOrderAmount.Value  
  
                ' NC-23 @Status. For a new order, the status is always O (open).  
                cmdNewOrder.Parameters.Add(New SqlParameter("@Status", SqlDbType.[Char], 1))  
                cmdNewOrder.Parameters("@Status").Value = "O"  
  
                ' NC-24 Add return value for stored procedure, which is orderID.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@RC", SqlDbType.Int))  
                cmdNewOrder.Parameters("@RC").Direction = ParameterDirection.ReturnValue  
  
                ' try-catch-finally  
                Try  
                    ' Open connection.  
                    conn.Open()  
  
                    ' Run the stored procedure.  
                    cmdNewOrder.ExecuteNonQuery()  
  
                    ' NC-25 Display the order number.  
                    Me.orderID = CInt(cmdNewOrder.Parameters("@RC").Value)  
                    MessageBox.Show("Order number " & (Me.orderID).ToString & " has been submitted.")  
  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("Order could  not be placed.")  
  
                Finally  
                    ' Close connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' NC-26 Verify that order data is ready.  
        Private Function isPlaceOrderReady() As Boolean  
  
            ' Verify that CustomerID is present.  
            If txtCustomerID.Text = "" Then  
                MessageBox.Show("Please create customer account before placing order.")  
                Return False  
  
                ' Verify that Amount isn't 0.   
            ElseIf (numOrderAmount.Value < 1) Then  
  
                MessageBox.Show("Please specify an order amount.")  
                Return False  
            Else  
                ' Order can be submitted.  
                Return True  
            End If  
        End Function  
  
        ' NC-27 Reset the form for another new account.  
        Private Sub btnAddAnotherAccount_Click() Handles btnAddAnotherAccount.Click  
            Me.ClearForm()  
        End Sub  
  
        ' NC-28 Clear values from controls.  
        Private Sub ClearForm()  
            txtCustomerName.Clear()  
            txtCustomerID.Clear()  
            dtpOrderDate.Value = DateTime.Now  
            numOrderAmount.Value = 0  
            Me.parsedCustomerID = 0  
        End Sub  
  
        ' NC-29 Close the form.  
        Private Sub btnAddFinish_Click() Handles btnAddFinish.Click  
            Me.Close()  
        End Sub  
  
    End Class  
End Namespace  
```  
  
|Comentário|Descrição|  
|-------------|-----------------|  
|NC-1|Adicione `System.Data.SqlClient` e `System.Configuration` à lista de namespaces.|  
|NC-2|Declare a `parsedCustomerID` e `orderID` variáveis, que você usará mais tarde.|  
|NC-3|Chame o `GetConnectionString` método para obter a cadeia de conexão no arquivo de configuração de aplicativo e armazenar o valor no `connstr` variável de cadeia de caracteres.|  
|NC-4|Adicione código para o manipulador de eventos para o `btnCreateAccount` botão.|  
|NC-5|Coloque a chamada para `isCustomerName` em torno do código de evento de clique, de modo que `uspNewCustomer` seja executado somente se um nome de cliente está presente.|  
|NC-6|Criar uma `SqlConnection` objeto (`conn`) e passe a cadeia de conexão no `connstr`.|  
|NC-7|Criar uma `SqlCommand` objeto, `cmdNewCustomer`.<br /><br /> -Especifique `Sales.uspNewCustomer` como o procedimento armazenado para executar.<br />– Use o `CommandType` propriedade para especificar que o comando é um procedimento armazenado.|  
|NC-8|Adicionar o `@CustomerName` parâmetro de entrada do procedimento armazenado.<br /><br /> -Adicionar o parâmetro para o `Parameters` coleção.<br />– Use o `SqlDbType` enumeração para especificar o tipo de parâmetro como nvarchar(40).<br />-Especifique `txtCustomerName.Text` como a origem.|  
|NC-9|Adicione o parâmetro de saída do procedimento armazenado.<br /><br /> -Adicionar o parâmetro para o `Parameters` coleção.<br />-Use `ParameterDirection.Output` para identificar o parâmetro como saída.|  
|NC-10|Adicione um bloco Try-Catch-Finally para abrir a conexão, execute o procedimento armazenado, lidar com exceções e, em seguida, feche a conexão.|  
|NC-11|Abra a conexão (`conn`) que você criou em NC-6.|  
|NC-12|Use o `ExecuteNonQuery` método para `cmdNewCustomer` para executar o `Sales.uspNewCustomer` procedimento armazenado. Esse procedimento armazenado é executado um `INSERT` instrução, não uma consulta.|  
|NC-13|O `@CustomerID` valor é retornado como um valor de identidade do banco de dados. Porque ele é um número inteiro, você precisará convertê-lo em uma cadeia de caracteres para exibi-lo na **Customer ID** caixa de texto.<br /><br /> -Você declarou `parsedCustomerID` em NC-2.<br />-Store a `@CustomerID` valor em `parsedCustomerID` para uso posterior.<br />-Converter a ID do cliente retornada em uma cadeia de caracteres e inseri-la em `txtCustomerID.Text`.|  
|NC-14|Para este exemplo, adicione uma cláusula catch (não-qualidade de produção) simples.|  
|NC-15|Sempre feche uma conexão depois de terminar de usá-la, para que ele possa ser liberado para o pool de conexão. Ver [Conexão do SQL Server Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca\(l=en-us,v=VS.110\).aspx).|  
|NC-16|Defina um método para verificar se um nome de cliente está presente.<br /><br /> -Se a caixa de texto está vazia, exibir uma mensagem e retornar `false`, porque é necessário um nome para criar a conta.<br />-Se a caixa de texto não estiver vazia, retorne `true`.|  
|NC-17|Adicione código para o manipulador de eventos para o `btnPlaceOrder` botão.|  
|NC-18|Encapsular a chamada para `isPlaceOrderReady` em torno de `btnPlaceOrder_Click` código de evento, de modo que `uspPlaceNewOrder` não será executado se a entrada necessária não estiver presente.|  
|NC-19 até NC-25|Essas seções de código lembram o código que você adicionou para a `btnCreateAccount_Click` manipulador de eventos.<br /><br /> -NC-19. Criar o `SqlCommand` objeto, `cmdNewOrder`e especifique `Sales.uspPlaceOrder` como o procedimento armazenado.<br />-NC-20 até NC-23 são parâmetros de entrada para o procedimento armazenado.<br />-NC-24. `@RC` conterá um valor de retorno que é a ID da ordem gerada do banco de dados. Direção desse parâmetro é especificada como `ReturnValue`.<br />-NC-25. Store o valor da ID do pedido no `orderID` variável que você declarou em NC-2 e exibir o valor em uma caixa de mensagem.|  
|NC-26|Defina um método para verificar se uma ID de cliente existe e que foi especificado um valor em `numOrderAmount`.|  
|NC-27|Chame o `ClearForm` método no `btnAddAnotherAccount` manipulador de eventos de clique.|  
|NC-28|Criar o `ClearForm` método para limpar os valores do formulário se você quiser adicionar outro cliente.|  
|NC29|Feche o formulário NewCustomer e retornar o foco para o formulário de navegação.|  
  
### <a name="fillorcancel-form"></a>Formulário FillOrCancel  
 O formulário FillorCancel executa uma consulta para retornar uma ordem quando você inserir uma ID de pedido e selecione o **localizar ordem** botão. A linha retornada aparece em uma grade de dados somente leitura. Você pode marcar a ordem como cancelada (X), se você selecionar o **Cancelar pedido** botão, ou você pode marcar a ordem como preenchida (F) se você selecionar a **preencher ordem** botão. Se você selecionar o **localizar ordem** novamente no botão, a linha atualizada aparecerá.  
  
#### <a name="create-event-handlers"></a>Criar manipuladores de eventos  
 Criar vazio clique manipuladores de eventos para os quatro botões no formulário.  
  
#### <a name="create-code-for-fillorcancel"></a>Criar o código para FillOrCancel  
 Adicione o seguinte código ao formulário de FillOrCancel. Percorra os blocos de código usando os comentários numerados e a tabela que segue o código.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
//FC-1 More namespaces.  
using System.Text.RegularExpressions;  
using System.Data.SqlClient;  
using System.Configuration;  
  
namespace SimpleDataApp  
{  
    public partial class FillOrCancel : Form  
    {  
        //FC-2 Storage for OrderID.  
        private int parsedOrderID;  
  
        //FC-3 Specify a connection string.  
        string connstr = SimpleDataApp.Utility.GetConnectionString();  
  
        public FillOrCancel()  
        {  
            InitializeComponent();  
        }  
  
        //FC-4 Find an order.  
        private void btnFindByOrderID_Click(object sender, EventArgs e)  
        {  
            //FC-5 Prepare the connection and the command.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //Define a query string that has a parameter for orderID.  
                string sql = "select * from Sales.Orders where orderID = @orderID";  
  
                //Create a SqlCommand object.  
                SqlCommand cmdOrderID = new SqlCommand(sql, conn);  
  
                //Define the @orderID parameter and its value.  
                cmdOrderID.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdOrderID.Parameters["@orderID"].Value = parsedOrderID;  
  
                //try-catch-finally  
                try  
                {  
                    //FC-6 Run the command and display the results.  
                    //Open the connection.  
                    conn.Open();  
  
                    //Run the command by using SqlDataReader.  
                    SqlDataReader rdr = cmdOrderID.ExecuteReader();  
  
                    //Create a data table to hold the retrieved data.  
                    DataTable dataTable = new DataTable();  
  
                    //Load the data from SqlDataReader into the data table.  
                    dataTable.Load(rdr);  
  
                    //Display the data from the data table in the data grid view.  
                    this.dgvCustomerOrders.DataSource = dataTable;  
  
                    //Close the SqlDataReader.  
                    rdr.Close();  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("The requested order could not be loaded into the form.");  
                }  
                finally  
                {  
                    //Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-7 Cancel an order.  
        private void btnCancelOrder_Click(object sender, EventArgs e)  
        {  
            //Set up and run stored procedure only if OrderID is ready.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                // Create command and identify it as a stored procedure.  
                SqlCommand cmdCancelOrder = new SqlCommand("Sales.uspCancelOrder", conn);  
                cmdCancelOrder.CommandType = CommandType.StoredProcedure;  
  
                cmdCancelOrder.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdCancelOrder.Parameters["@orderID"].Value = parsedOrderID;  
  
                // try-catch-finally  
                try  
                {  
                    // Open the connection.  
                    conn.Open();  
  
                    // Run the cmdCancelOrder command.  
                    cmdCancelOrder.ExecuteNonQuery();  
                }  
                // A simple catch.  
                catch  
                {  
                    MessageBox.Show("The cancel operation was not completed.");  
                }  
                finally  
                {  
                    //Close connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-8 Fill an order.  
        private void btnFillOrder_Click(object sender, EventArgs e)  
        {  
            //Set up and run stored procedure only if OrderID is ready.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //Create command and identify it as a stored procedure.  
                SqlCommand cmdFillOrder = new SqlCommand("Sales.uspFillOrder", conn);  
                cmdFillOrder.CommandType = CommandType.StoredProcedure;  
  
                // Add input parameter from the stored procedure.  
                cmdFillOrder.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdFillOrder.Parameters["@orderID"].Value = parsedOrderID;  
  
                //Add the second input parameter.  
                cmdFillOrder.Parameters.Add(new SqlParameter("@FilledDate", SqlDbType.DateTime, 8));  
                cmdFillOrder.Parameters["@FilledDate"].Value = dtpFillDate.Value;  
  
                //try-catch-finally  
                try  
                {  
                    //Open the connection.  
                    conn.Open();  
  
                    //Run the cmdFillOrder command.  
                    cmdFillOrder.ExecuteNonQuery();  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("The fill operation was not completed.");  
                }  
                finally  
                {  
                    //Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-9 Verify that OrderID is ready.  
        private bool isOrderID()  
        {  
  
            //Check for input in the Order ID text box.  
            if (txtOrderID.Text == "")  
            {  
                MessageBox.Show("Please specify the Order ID.");  
                return false;  
            }  
  
            // Check for characters other than integers.  
            else if (Regex.IsMatch(txtOrderID.Text, @"^\D*$"))  
            {  
               //Show message and clear input.  
                MessageBox.Show("Please specify integers only.");  
                txtOrderID.Clear();  
                return false;  
            }  
            else  
            {  
                //Convert the text in the text box to an integer to send to the database.  
                parsedOrderID = Int32.Parse(txtOrderID.Text);  
                return true;  
            }  
        }  
  
        //Close the form.  
        private void btnFinishUpdates_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
' FC-1 More namespaces.  
Imports System.Text.RegularExpressions  
Imports System.Data.SqlClient  
Imports System.Configuration  
  
Namespace SimpleDataApp  
    Partial Public Class FillOrCancel  
        Inherits Form  
        ' FC-2 Storage for OrderID.  
        Private parsedOrderID As Integer  
  
        ' FC-3 Specify a connection string.  
        Private connstr As String = SimpleDataApp.Utility.GetConnectionString()  
  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' FC-4 Find an order.  
        Private Sub btnFindByOrderID_Click() Handles btnFindByOrderID.Click  
  
            ' FC-5 Prepare the connection and the command.  
  
            If isOrderID() Then  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Define the query string that has a parameter for orderID.  
                Dim sql As String = "select * from Sales.Orders where orderID = @orderID"  
  
                ' Create a SqlCommand object.  
                Dim cmdOrderID As New SqlCommand(sql, conn)  
  
                ' Define the @orderID parameter and its value.  
                cmdOrderID.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdOrderID.Parameters("@orderID").Value = parsedOrderID  
  
                ' try-catch-finally  
                Try  
                    ' FC-6 Run the command and display the results.  
                    ' Open connection.  
                    conn.Open()  
  
                    ' Run the command by using SqlDataReader.  
                    Dim rdr As SqlDataReader = cmdOrderID.ExecuteReader()  
  
                    ' Create a data table to hold the retrieved data.  
                    Dim dataTable As New DataTable()  
  
                    ' Load the data from SqlDataReader into the data table.  
                    dataTable.Load(rdr)  
  
                    ' Display the data from the data table in the data grid view.  
                    Me.dgvCustomerOrders.DataSource = dataTable  
  
                    ' Close the SqlDataReader.  
                    rdr.Close()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The requested order could not be loaded into the form.")  
                Finally  
                    ' Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-7 Cancel an order.  
        Private Sub btnCancelOrder_Click() Handles btnCancelOrder.Click  
  
            ' Set up and run stored procedure only if OrderID is ready.  
            If isOrderID() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Create the command and identify it as a stored procedure.  
                Dim cmdCancelOrder As New SqlCommand("Sales.uspCancelOrder", conn)  
                cmdCancelOrder.CommandType = CommandType.StoredProcedure  
  
                ' Add input parameter from the stored procedure.  
                cmdCancelOrder.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdCancelOrder.Parameters("@orderID").Value = parsedOrderID  
  
                ' try-catch-finally  
                Try  
                    ' Open the connection.  
                    conn.Open()  
  
                    ' Run the cmdCancelOrder command.  
                    cmdCancelOrder.ExecuteNonQuery()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The cancel operation was not completed.")  
                Finally  
                    ' Close connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-8 Fill an order.  
        Private Sub btnFillOrder_Click() Handles btnFillOrder.Click  
  
            ' Set up and run stored procedure only if OrderID is ready.  
            If isOrderID() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Create command and identify it as a stored procedure.  
                Dim cmdFillOrder As New SqlCommand("Sales.uspFillOrder", conn)  
                cmdFillOrder.CommandType = CommandType.StoredProcedure  
  
                ' Add input parameter from the stored procedure.  
                cmdFillOrder.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdFillOrder.Parameters("@orderID").Value = parsedOrderID  
  
                ' Add second input parameter.  
                cmdFillOrder.Parameters.Add(New SqlParameter("@FilledDate", SqlDbType.DateTime, 8))  
                cmdFillOrder.Parameters("@FilledDate").Value = dtpFillDate.Value  
  
                ' try-catch-finally  
                Try  
                    ' Open the connection.  
                    conn.Open()  
  
                    ' Run the cmdFillOrder command.   
                    cmdFillOrder.ExecuteNonQuery()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The fill operation was not completed.")  
                Finally  
                    ' Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-9 Verify that OrderID is ready.  
        Private Function isOrderID() As Boolean  
  
            ' Check for input in the Order ID text box.  
            If txtOrderID.Text = "" Then  
                MessageBox.Show("Please specify the Order ID.")  
                Return False  
  
                ' Check for characters other than integers.  
            ElseIf Regex.IsMatch(txtOrderID.Text, "^\D*$") Then  
  
                ' Show message and clear input.  
                MessageBox.Show("Please specify integers only.")  
                txtOrderID.Clear()  
                Return False  
  
            Else  
                ' Convert the text in the text box to an integer to send to the database.  
                parsedOrderID = Int32.Parse(txtOrderID.Text)  
                Return True  
  
            End If  
        End Function  
  
        ' Close the form.  
        Private Sub btnFinishUpdates_Click() Handles btnFinishUpdates.Click  
            Me.Close()  
        End Sub  
    End Class  
End Namespace  
```  
  
|Comentário|Descrição|  
|-------------|-----------------|  
|FC-1|Adicione `System.Data.SqlClient`, `System.Configuration`, e `System.Text.RegularExpressions` à lista de namespaces.|  
|FC-2|Declare o `parsedOrderID` variável.|  
|FC-3|Chame o `GetConnectionString` método para obter a cadeia de conexão no arquivo de configuração de aplicativo e armazenar o valor no `connstr` variável de cadeia de caracteres.|  
|FC-4|Adicione código ao manipulador de eventos Click para `btnFindOrderByID`.|  
|FC-5|Essas tarefas são necessárias antes de tentar executar uma instrução SQL ou um procedimento armazenado.<br /><br /> -Criar um `SqlConnection` objeto.<br />-Definir a instrução SQL ou especifique o nome do procedimento armazenado. (Nesse caso, você executará um `SELECT` instrução.)<br />-Criar um `SqlCommand` objeto.<br />-Defina quaisquer parâmetros para a instrução SQL ou procedimento armazenado.|  
|FC-6|Esse código usa `SqlDataReader` e `DataTable` para recuperar e exibir o resultado da consulta.<br /><br /> -Abra a conexão.<br />-Criar uma `SqlDataReader` objeto, `rdr`, executando o `ExecuteReader` método para `cmdOrderID`.<br />-Criar um `DataTable` objeto para manter os dados recuperados.<br />-Carregar os dados do `SqlDataReader` do objeto para o `DataTable` objeto.<br />-Exibe os dados na exibição de grade de dados, especificando `DataTable` como `DataSource` para a exibição de grade de dados.<br />-Feche `SqlDataReader`.|  
|FC-7|Adicione código ao manipulador de eventos Click para `btnCancelOrder`. Esse código é executado o `Sales.uspCancelOrder` procedimento armazenado.|  
|FC-8|Adicione código ao manipulador de eventos Click para `btnFillOrder`. Esse código é executado o `Sales.uspFillOrder` procedimento armazenado.|  
|FC-9|Crie um método para verificar se `OrderID` está pronto para enviar como um parâmetro para o `SqlCommand` objeto.<br /><br /> -Certifique-se de que uma ID foi inserida no `txtOrderID`.<br />-Use `Regex.IsMatch` para definir uma verificação simples para caracteres não inteiro.<br />-Você declarou o `parsedOrderID` variável em FC-2.<br />-Se a entrada é válida, converta o texto em um inteiro e armazenar o valor no `parsedOrderID` variável.<br />-Encapsular o `isOrderID` método ao redor de `btnFindByOrderID`, `btnCancelOrder`, e `btnFillOrder` manipuladores de eventos de clique.|  
  
##  <a name="BKMK_testyourapplication"></a> Teste seu aplicativo  
 Selecione a tecla F5 para compilar e testar seu aplicativo depois que você codifica cada manipulador de eventos de clique e, em seguida, depois de concluir a codificação.

