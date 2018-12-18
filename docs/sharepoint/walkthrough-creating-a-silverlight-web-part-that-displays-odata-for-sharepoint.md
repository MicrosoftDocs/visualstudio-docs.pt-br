---
title: 'Passo a passo: Criando uma Web Part do Silverlight que exiba OData para o SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/22/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 67742078cefcd0608d1cff9a5bab609053544392
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296106"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>Passo a passo: Criar uma web part do Silverlight que exiba OData para o SharePoint
  SharePoint 2010 expõe seus dados de lista por meio do OData. No SharePoint, o serviço OData é implementado pelo serviço RESTful ListData.svc. Este passo a passo mostra como criar uma web part do SharePoint que hospeda um aplicativo do Silverlight. O aplicativo do Silverlight exibe informações da lista de lançamento do SharePoint usando ListData.svc. Para obter mais informações, consulte [Interface REST do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=225999) e [Open Data Protocol](http://go.microsoft.com/fwlink/?LinkId=226000).  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do Microsoft Windows e do SharePoint.
  
-   [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].  
  
## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>Criar um aplicativo do Silverlight e a web part do Silverlight
 Primeiro, crie um aplicativo do Silverlight no Visual Studio. O aplicativo do Silverlight recupera dados da lista de anúncios do SharePoint usando o serviço ListData.svc.  
  
> [!NOTE]  
>  Nenhuma versão do Silverlight 4.0 antes de dar suporte as interfaces necessárias para fazer referência a dados de lista do SharePoint.  
  
#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>Para criar um aplicativo do Silverlight e a web part do Silverlight
  
1. Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.  
  
2. Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3. No painel modelos, escolha o **Web Part do SharePoint 2010 Silverlight** modelo.  
  
4. No **nome** , digite **SLWebPartTest** e, em seguida, escolha o **Okey** botão.  
  
    O **Assistente para personalização do SharePoint** caixa de diálogo é exibida.  
  
5. Sobre o **especificar o nível de site e segurança para depuração** página, insira a URL do servidor do site do SharePoint onde você deseja depurar a definição de site ou usar o local padrão (http://<em>nome do sistema</em>/) .  
  
6. No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção.  
  
    Embora este exemplo usa uma solução de farm, os projetos do Silverlight na web part podem ser implantados como farm ou soluções em área restrita. Para obter mais informações sobre as soluções em área restrita e soluções de farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
7. No **como você deseja associar a Web Part Silverlight** seção o **especificar informações de configuração do Silverlight** , escolha o **criar um novo projeto do Silverlight e associá-la com a web part** botão de opção.  
  
8. Alterar o **nome** para **SLApplication**, defina **idioma** como **Visual Basic** ou **Visual c#**, e, em seguida, defina **versão do Silverlight** à **Silverlight 4.0**.  
  
9. Escolha o **concluir** botão. Os projetos são exibidos na **Gerenciador de soluções**.  
  
     A solução contém dois projetos: um aplicativo do Silverlight e uma web part do Silverlight. O aplicativo do Silverlight recupera e exibe os dados da lista do SharePoint, e a web part Silverlight hospeda o aplicativo do Silverlight, permitindo que você exibi-lo no SharePoint.  
  
## <a name="customize-the-silverlight-application"></a>Personalizar o aplicativo do Silverlight
 Adicione elementos de código e design para o aplicativo do Silverlight.  
  
#### <a name="to-customize-the-silverlight-application"></a>Para personalizar o aplicativo do Silverlight
  
1.  Adicione uma referência de assembly a System no aplicativo do Silverlight. Para obter mais informações, consulte [como: Adicionar ou remover referências usando a caixa de diálogo Adicionar referência](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9).  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho **referências**e, em seguida, escolha **Add Service Reference**.  
  
    > [!NOTE]  
    >  Se você estiver usando Visual Basic, você deve escolher o **Show All Files** ícone na parte superior da **Gerenciador de soluções** para exibir o **referências** nó.  
  
3.  Na caixa de endereço a **adicionar referência de serviço** caixa de diálogo, digite a URL do site do SharePoint, como **http://MySPSite**e, em seguida, escolha o **vá** botão.  
  
     Quando o Silverlight localiza o serviço de OData de SharePoint ListData.svc, ele substitui o endereço com a URL do serviço completo. Neste exemplo, http://myserver torna-se http://myserver/_vti_bin/ListData.svc.  
  
4.  Escolha o **Okey** botão para adicionar a referência de serviço ao projeto e, em seguida, use o nome de serviço padrão, ServiceReference1.  
  
5.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
6.  Adicione uma nova fonte de dados para o projeto baseado no serviço do SharePoint. Para fazer isso, na barra de menus, escolha **modo de exibição** > **Other Windows** > **fontes de dados**.  
  
     O **fontes de dados** janela mostra todos os dados de lista do SharePoint disponíveis, como tarefas, anúncios e calendário.  
  
7.  Adicione os dados de lista de anúncios ao aplicativo do Silverlight. Você pode arrastar "Anúncios" das **fontes de dados** janela para o Silverlight designer.  
  
     Isso cria um controle de grade associado à lista de anúncios do site do SharePoint.  
  
8.  Redimensione o controle de grade para caber na página do Silverlight.  
  
9. No arquivo de código de MainPage. XAML (*MainPage.xaml.cs* do Visual c# ou *MainPage* para o Visual Basic), adicione as seguintes referências de namespace.  
  
    ```vb  
    ' Add the following three Imports statements.  
    Imports SLApplication.ServiceReference1  
    Imports System.Windows.Data  
    Imports System.Data.Services.Client  
    ```  
  
    ```csharp  
    // Add the following three using statements.  
    using SLApplication.ServiceReference1;  
    using System.Windows.Data;  
    using System.Data.Services.Client;  
    ```  
  
10. Adicione as seguintes declarações de variável na parte superior da classe.  
  
    ```vb  
    Private context As TeamSiteDataContext  
    Private myCollectionViewSource As CollectionViewSource  
    Private announcements As New DataServiceCollection(Of AnnouncementsItem)()  
    ```  
  
    ```csharp  
    private TeamSiteDataContext context;  
    private CollectionViewSource myCollectionViewSource;  
    DataServiceCollection<AnnouncementsItem> announcements = new DataServiceCollection<AnnouncementsItem>();  
    ```  
   
11. Substitua o `UserControl_Loaded` procedimento com o seguinte.  
  
    ```vb  
    Private Sub UserControl_Loaded_1(sender As Object, e As RoutedEventArgs)  
        ' The URL for the OData service.  
        ' Replace <server name> in the next line with the name of your SharePoint server.  
        context = New TeamSiteDataContext(New Uri("http://<server name>/_vti_bin/ListData.svc"))  
  
        ' Do not load your data at design time.  
        If Not System.ComponentModel.DesignerProperties.GetIsInDesignMode(Me) Then  
            'Load your data here and assign the results to the CollectionViewSource.  
            myCollectionViewSource =   DirectCast(Me.Resources("announcementsViewSource"), System.Windows.Data.CollectionViewSource)  
            announcements.LoadCompleted += New EventHandler(Of LoadCompletedEventArgs)(AddressOf announcements_LoadCompleted)  
            announcements.LoadAsync(context.Announcements)  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    private void UserControl_Loaded_1(object sender, RoutedEventArgs e)  
    {  
        // The URL for the OData service.  
        // Replace <server name> in the next line with the name of your   
        // SharePoint server.  
        context = new TeamSiteDataContext(new Uri("http://ServerName>/_vti_bin/ListData.svc"));  
  
        // Do not load your data at design time.  
        if (!System.ComponentModel.DesignerProperties.GetIsInDesignMode(this))  
        {  
            //Load your data here and assign the results to the CollectionViewSource.  
            myCollectionViewSource = (System.Windows.Data.CollectionViewSource)this.Resources["announcementsViewSource"];  
            announcements.LoadCompleted += new EventHandler<LoadCompletedEventArgs>(announcements_LoadCompleted);  
            announcements.LoadAsync(context.Announcements);  
        }  
    }  
    ```  
     Certifique-se de substituir os *ServerName* espaço reservado com o nome do servidor que está executando o SharePoint.  
  
12. Adicione o seguinte procedimento de tratamento de erros.  
  
    ```vb  
    Private Sub announcements_LoadCompleted(sender As Object, e As LoadCompletedEventArgs)  
        ' Handle any errors.  
        If e.[Error] Is Nothing Then  
            myCollectionViewSource.Source = announcements  
        Else  
            MessageBox.Show(String.Format("ERROR: {0}", e.[Error].Message))  
        End If  
    End Sub  
  
    ```  
  
    ```csharp  
    void announcements_LoadCompleted(object sender, LoadCompletedEventArgs e)  
    {  
        // Handle any errors.  
        if (e.Error == null)  
        {  
            myCollectionViewSource.Source = announcements;  
        }  
        else  
        {  
            MessageBox.Show(string.Format("ERROR: {0}", e.Error.Message));  
        }  
    }  
    ```  
       
## <a name="modify-the-silverlight-web-part"></a>Modificar a web part do Silverlight
 Altere uma propriedade em que o projeto de web part do Silverlight para habilitar a depuração do Silverlight.  
  
#### <a name="to-modify-the-silverlight-web-part"></a>Para modificar a web part do Silverlight  
  
1.  Abra o menu de atalho para o projeto de web part do Silverlight (**SLWebPartTest**) e, em seguida, escolha **propriedades**.  
  
2.  No **propriedades** janela, escolha o **SharePoint** guia.  
  
3.  Se ele ainda não estiver selecionado, selecione a **Silverlight Habilitar depuração (em vez de depuração de Script)** caixa de seleção.  
  
4.  Salvar o projeto.  
  
## <a name="test-the-silverlight-web-part"></a>Testar a web part do Silverlight
 Teste a nova web part do Silverlight no SharePoint para garantir que ele exibe corretamente os dados de lista do SharePoint.  
  
#### <a name="to-test-the-silverlight-web-part"></a>Para testar a web part do Silverlight  
  
1.  Escolha o **F5** chave para compilar e executar a solução do SharePoint.  
  
2.  No SharePoint, sobre o **ações do Site** menu, escolha **nova página**.  
  
3.  No **nova página** caixa de diálogo, insira um título, como **SL de teste na Web Part**e, em seguida, escolha o **criar** botão.  
  
4.  No designer de página, sobre o **ferramentas de edição** guia, escolha **inserir**.  
  
5.  Na faixa de guias, escolha **Web Part**.  
  
6.  No **categorias** , escolha o **personalizado** pasta.  
  
7.  No **Web Parts** lista, escolha a web part do Silverlight e, em seguida, escolha o **Add** botão para adicionar a web part para o designer.  
  
8.  Depois de ter feito todas as adições à página da web que você deseja, escolha o **página** guia e, em seguida, escolha o **salvar e fechar** botão na barra de ferramentas.  
  
     A web part Silverlight agora deve exibir dados de anúncio do site do SharePoint. Por padrão, a página é armazenada na lista de páginas do Site no SharePoint.  
  
    > [!NOTE]  
    >  Ao acessar dados no Silverlight entre domínios, o Silverlight protege contra vulnerabilidades de segurança que podem ser usadas para explorar os aplicativos da web. Se você encontrar problemas ao acessar dados remotos no Silverlight, consulte [tornando um serviço disponível entre limites de domínio](http://go.microsoft.com/fwlink/?LinkId=223276).  
  
## <a name="see-also"></a>Consulte também
 [Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)   
 [Implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)  
  
  
