---
title: Criar Web Part do Silverlight exibindo OData para SharePoint
ms.date: 02/22/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 75653f0357bcc605e666ee271a527b616985b641
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017166"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>Walkthrough: criar uma Web Part do Silverlight que exibe o OData para SharePoint
  O SharePoint 2010 expõe seus dados de lista por meio do OData. No SharePoint, o serviço OData é implementado pelo serviço RESTful ListData. svc. Este tutorial mostra como criar uma Web Part do SharePoint que hospeda um aplicativo do Silverlight. O aplicativo do Silverlight exibe informações da lista de anúncios do SharePoint usando ListData. svc. Para obter mais informações, consulte [interface REST do SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/ff521587(v=office.14)) e [protocolo Open Data](https://www.odata.org/).

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Microsoft Windows e do SharePoint.

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>Criar um aplicativo Silverlight e uma Web Part do Silverlight
 Primeiro, crie um aplicativo do Silverlight no Visual Studio. O aplicativo do Silverlight recupera dados da lista de anúncios do SharePoint usando o serviço ListData. svc.

> [!NOTE]
> Nenhuma versão do Silverlight antes de 4,0 dá suporte às interfaces necessárias para referenciar dados da lista do SharePoint.

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>Para criar um aplicativo do Silverlight e uma Web Part do Silverlight

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. No painel modelos, escolha o modelo de **Web Part do Silverlight do SharePoint 2010** .

4. Na caixa **nome** , digite **SLWebPartTest** e, em seguida, escolha o botão **OK** .

    A caixa de diálogo **Assistente para personalização do SharePoint** é exibida.

5. Na página **especificar o site e o nível de segurança para depuração** , insira a URL para o site do SharePoint Server em que você deseja depurar a definição do site ou use o local padrão (<em>nome do sistema</em>http:///).

6. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** .

    Embora este exemplo use uma solução de farm, os projetos de Web Part do Silverlight podem ser implantados como soluções de farm ou de área restrita. Para obter mais informações sobre soluções de área restrita e soluções de farm, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7. Na seção **como você deseja associar a Web Part do Silverlight** da página **especificar informações de configuração do Silverlight** , escolha o botão de opção **criar um novo projeto do Silverlight e associá-lo ao Web Part** .

8. Altere o **nome** para **SLApplication**, defina **Language** para **Visual Basic** ou **Visual C#** e, em seguida, defina a **versão do Silverlight** para o **Silverlight 4,0**.

9. Escolha o botão **Concluir**. Os projetos aparecem em **Gerenciador de soluções**.

     A solução contém dois projetos: um aplicativo do Silverlight e uma Web Part do Silverlight. O aplicativo do Silverlight recupera e exibe os dados da lista do SharePoint, e a Web Part do Silverlight hospeda o aplicativo do Silverlight, permitindo que você o exiba no SharePoint.

## <a name="customize-the-silverlight-application"></a>Personalizar o aplicativo do Silverlight
 Adicione código e elementos de design ao aplicativo do Silverlight.

#### <a name="to-customize-the-silverlight-application"></a>Para personalizar o aplicativo do Silverlight

1. Adicione uma referência de assembly a System. Windows. Data no aplicativo do Silverlight. Para obter mais informações, consulte [como: Adicionar ou remover referências usando a caixa de diálogo Adicionar referência](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9).

2. Em **Gerenciador de soluções**, abra o menu de atalho para **referências**e, em seguida, escolha **Adicionar referência de serviço**.

    > [!NOTE]
    > Se você estiver usando Visual Basic, deverá escolher o ícone **Mostrar todos os arquivos** na parte superior da **Gerenciador de soluções** para exibir o nó **referências** .

3. Na caixa endereço da caixa de diálogo **Adicionar referência de serviço** , insira a URL do seu site do SharePoint, como **http://MySPSite** e, em seguida, escolha o botão **ir** .

     Quando o Silverlight localiza o serviço OData do SharePoint ListData. svc, ele substitui o endereço pela URL de serviço completa. Para este exemplo, http://myserver torna-se http://myserver/_vti_bin/ListData.svc .

4. Escolha o botão **OK** para adicionar a referência de serviço ao projeto e use o nome do serviço padrão, ServiceReference1.

5. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

6. Adicione uma nova fonte de dados ao projeto com base no serviço do SharePoint. Para fazer isso, na barra de menus, escolha **Exibir**  >  **outras**  >  **fontes de dados**do Windows.

     A janela **fontes de dados** mostra todos os dados de lista do SharePoint disponíveis, como tarefas, anúncios e calendário.

7. Adicione os dados da lista de anúncios ao aplicativo do Silverlight. Você pode arrastar "anúncios" da janela **fontes de dados** para o designer do Silverlight.

     Isso cria um controle de grade associado à lista de anúncios do site do SharePoint.

8. Redimensione o controle de grade para ajustá-lo à página do Silverlight.

9. No arquivo de código MainPage. XAML (*MainPage.XAML.cs* para Visual C# ou *MainPage. XAML. vb* para Visual Basic), adicione as seguintes referências de namespace.

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using directives.
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

11. Substitua o `UserControl_Loaded` procedimento pelo seguinte.

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

     Certifique-se de substituir o espaço reservado *ServerName* pelo nome do servidor que está executando o SharePoint.

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

## <a name="modify-the-silverlight-web-part"></a>Modificar a Web Part do Silverlight
 Altere uma propriedade no projeto de Web Part do Silverlight para habilitar a depuração do Silverlight.

#### <a name="to-modify-the-silverlight-web-part"></a>Para modificar a Web Part do Silverlight

1. Abra o menu de atalho do projeto de Web Part do Silverlight (**SLWebPartTest**) e escolha **Propriedades**.

2. Na janela **Propriedades** , escolha a guia **SharePoint** .

3. Se ainda não estiver selecionado, marque a caixa de seleção **Habilitar depuração do Silverlight (em vez de depuração de script)** .

4. Salve o projeto.

## <a name="test-the-silverlight-web-part"></a>Testar a Web Part do Silverlight
 Teste a nova Web Part do Silverlight no SharePoint para garantir que ela exiba os dados da lista do SharePoint corretamente.

#### <a name="to-test-the-silverlight-web-part"></a>Para testar a Web Part do Silverlight

1. Escolha a tecla **F5** para compilar e executar a solução do SharePoint.

2. No SharePoint, no menu **ações do site** , escolha **nova página**.

3. Na caixa de diálogo **nova página** , insira um título, como o **teste de Web Part SL**, e escolha o botão **criar** .

4. No designer de página, na guia **ferramentas de edição** , escolha **Inserir**.

5. Na faixa de guias, escolha **Web Part**.

6. Na caixa **categorias** , escolha a pasta **personalizada** .

7. Na lista **Web Parts** , escolha a Web Part do Silverlight e, em seguida, escolha o botão **Adicionar** para adicionar a Web Part ao designer.

8. Depois de ter feito todas as adições à página da Web desejada, escolha a guia **página** e, em seguida, escolha o botão **salvar & fechar** na barra de ferramentas.

     A Web Part do Silverlight agora deve exibir dados de comunicado do site do SharePoint. Por padrão, a página é armazenada na lista páginas do site no SharePoint.

    > [!NOTE]
    > Ao acessar dados no Silverlight entre domínios, o Silverlight protege contra vulnerabilidades de segurança que podem ser usadas para explorar aplicativos Web. Se você encontrar problemas ao acessar dados remotos no Silverlight, consulte [disponibilizando um serviço entre limites de domínio](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc197955(v=vs.95)).

## <a name="see-also"></a>Consulte também
- [Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)
- [Implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)
