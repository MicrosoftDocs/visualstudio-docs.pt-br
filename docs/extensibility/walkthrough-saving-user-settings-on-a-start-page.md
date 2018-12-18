---
title: 'Passo a passo: Salvando as configurações do usuário em uma página de início | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fa57fb8c4e0c85ff7a9c1b258f1c326a241442c3
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566711"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>Passo a passo: Salvar configurações do usuário em uma página inicial
Você pode manter as configurações do usuário para sua página inicial. Seguindo este passo a passo, você pode criar um controle que salva uma configuração no registro quando o usuário clica em um botão e, em seguida, recupera a configuração toda vez que carrega a página de início. Como o modelo de projeto de página inicial inclui um controle de usuário personalizável, e o XAML de página de início padrão chama esse controle, você não precisa modificar a página de início em si.  
  
 O repositório de configurações que é instanciado neste passo a passo é uma instância das <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> interface, que lê e grava no seguinte local do registro quando ele é chamado: **HKCU\Software\Microsoft\VisualStudio\14.0\\ \<CollectionName >**  
  
 Quando ele está em execução na instância experimental do Visual Studio, o repositório de configurações lê e grava **HKCU\Software\Microsoft\VisualStudio\14.0Exp\\\<CollectionName >.**  
  
 Para obter mais informações sobre como persistir configurações, consulte [opções e configurações do usuário estendendo](../extensibility/extending-user-settings-and-options.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
> [!NOTE]
>  Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
>   
>  Você pode baixar o modelo de projeto de página inicial usando **Extension Manager**.  
  
## <a name="setting-up-the-project"></a>Configuração do projeto  
  
### <a name="to-configure-the-project-for-this-walkthrough"></a>Para configurar o projeto para este passo a passo  
  
1.  Crie um projeto de página inicial, conforme descrito em [criar uma página inicial personalizada](creating-a-custom-start-page.md). Nomeie o projeto **SaveMySettings**.  
  
2.  Na **Gerenciador de soluções**, adicione as seguintes referências de assembly ao projeto StartPageControl:  
  
    -   EnvDTE  
  
    -   EnvDTE80  
  
    -   Microsoft.VisualStudio.OLE.Interop  
  
    -   Microsoft.VisualStudio.Shell.Interop.11.0  
  
3.  Abra *MyControl.xaml*.  
  
4.  No painel de XAML, do nível superior <xref:System.Windows.Controls.UserControl> definição de elemento, adicione a seguinte declaração de evento após as declarações de namespace.  
  
    ```xml 
    Loaded="OnLoaded"  
    ```  
  
5.  No painel de design, clique na área principal do controle e, em seguida, pressione **excluir**.  
  
     Essa etapa remove as <xref:System.Windows.Controls.Border> elemento e todo o conteúdo e deixa somente os primeiros nível <xref:System.Windows.Controls.Grid> elemento.  
  
6.  Dos **caixa de ferramentas**, arraste um <xref:System.Windows.Controls.StackPanel> controle à grade.  
  
7.  Agora, arraste uma <xref:System.Windows.Controls.TextBlock>, um <xref:System.Windows.Controls.TextBox>e um botão para o <xref:System.Windows.Controls.StackPanel>.  
  
8.  Adicionar um **X:Name** atributo para o <xref:System.Windows.Controls.TextBox>e uma `Click` eventos para o <xref:System.Windows.Controls.Button>, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">  
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>  
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />  
        <Button Click="Button_Click" Width="100">Save My Setting</Button>  
    </StackPanel>  
    ```  
  
## <a name="implement-the-user-control"></a>Implementar o controle de usuário  
  
### <a name="to-implement-the-user-control"></a>Para implementar o controle de usuário  
  
1.  No painel de XAML, clique com botão direito a `Click` atributo o <xref:System.Windows.Controls.Button> elemento e, em seguida, clique **navegar até manipulador de eventos**.  
  
     Essa etapa abre *MyControl.xaml.cs*e cria um manipulador de stub para o `Button_Click` eventos.  
  
2.  Adicione o seguinte `using` instruções na parte superior do arquivo.  
  
     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]  
  
3.  Adicionar uma privada `SettingsStore` propriedade, conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    private IVsWritableSettingsStore _settingsStore = null;  
    private IVsWritableSettingsStore SettingsStore  
    {  
        get  
        {  
            if (_settingsStore == null)  
            {  
                // Get a reference to the DTE from the DataContext.   
                var typeDescriptor = DataContext as ICustomTypeDescriptor;  
                var propertyCollection = typeDescriptor.GetProperties();  
                var dte = propertyCollection.Find("DTE", false).GetValue(  
                    DataContext) as DTE2;  
  
                // Get the settings manager from the DTE.   
                var serviceProvider = new ServiceProvider(  
                    (Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);  
                var settingsManager = serviceProvider.GetService(  
                    typeof(SVsSettingsManager)) as IVsSettingsManager;  
  
                // Write the user settings to _settingsStore.  
                settingsManager.GetWritableSettingsStore(  
                    (uint)__VsSettingsScope.SettingsScope_UserSettings,  
                    out _settingsStore);  
            }  
            return _settingsStore;  
        }  
    }  
    ```  
  
     Essa propriedade primeiro obtém uma referência para o <xref:EnvDTE80.DTE2> interface, que contém o modelo de objeto de automação do <xref:System.Windows.FrameworkElement.DataContext%2A> do controle de usuário e, em seguida, usa o DTE para obter uma instância do <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> interface. Em seguida, ele usa essa instância para retornar as configurações do usuário atual.  
  
4.  Preencha o `Button_Click` evento da seguinte maneira.  
  
    ```csharp  
    private void Button_Click(object sender, RoutedEventArgs e)  
    {  
        int exists = 0;  
        SettingsStore.CollectionExists("MySettings", out exists);  
        if (exists != 1)  
        {  
            SettingsStore.CreateCollection("MySettings");  
        }  
        SettingsStore.SetString("MySettings", "MySetting", txtblk.Text);  
    }  
    ```  
  
     Isso grava o conteúdo da caixa de texto em um campo de "MySetting" em uma coleção de "MySettings" no registro. Se a coleção não existir, ele é criado.  
  
5.  Adicione o seguinte manipulador para o `OnLoaded` eventos do controle de usuário.  
  
    ```csharp  
    private void OnLoaded(Object sender, RoutedEventArgs e)  
    {  
        string value;  
        SettingsStore.GetStringOrDefault(  
            "MySettings", "MySetting", "", out value);  
        txtblk.Text = value;  
    }  
    ```  
  
     Esse código define o texto da caixa de texto para o valor atual de "MySetting".  
  
6.  Compile o controle de usuário.  
  
7.  Na **Gerenciador de soluções**, abra *vsixmanifest*.  
  
8.  No editor de manifesto, defina **nome do produto** à **salvar minhas configurações Start Page**.  
  
     Este recurso define o nome da página início conforme aparece na **Personalizar página inicial** lista o **opções** caixa de diálogo.  
  
9. Crie *StartPage*.  
  
## <a name="test-the-control"></a>Testar o controle  
  
### <a name="to-test-the-user-control"></a>Para testar o controle de usuário  
  
1.  Pressione **F5**.  
  
     A instância experimental do Visual Studio é aberto.  
  
2.  Na instância experimental, sobre o **ferramentas** menu, clique em **opções**.  
  
3.  No **ambiente** nó, clique em **inicialização**e, em seguida, no **Personalizar página inicial** lista, selecione **[extensão instalada] salvar minhas configurações de página inicial** .  
  
     Clique em **OK**.  
  
4.  Feche a página de início se ele estiver aberto e, no **modo de exibição** menu, clique em **Start Page**.  
  
5.  Na página Iniciar, clique o **MyControl** guia.  
  
6.  Na caixa de texto, digite **Cat**e, em seguida, clique em **salvar minha configuração**.  
  
7.  Feche a página de início e, em seguida, abra-o novamente.  
  
     A palavra "Gato" deve ser exibido na caixa de texto.  
  
8.  Substitua a palavra "Gato" com a palavra "Cachorro". Não clique no botão.  
  
9. Feche a página de início e, em seguida, abra-o novamente.  
  
     A palavra "Cachorro" deve ser exibida na caixa de texto, mesmo que você não salvar a configuração porque o Visual Studio manterá as janelas de ferramentas na memória, mesmo se eles forem fechados, até que o próprio Visual Studio fecha.  
  
10. Feche a instância experimental do Visual Studio.  
  
11. Pressione **F5** para reabrir a instância experimental.  
  
12. A palavra "Gato" deve ser exibido na caixa de texto.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode modificar esse controle de usuário para salvar e recuperar qualquer número de configurações personalizadas, usando valores diferentes de manipuladores de eventos diferentes para obter e definir o `SettingsStore` propriedade. Desde que você usar outro `propertyName` parâmetro para cada chamada para <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A>, os valores não substituem uns aos outros no registro.  
  
## <a name="see-also"></a>Consulte também  
 <xref:EnvDTE80.DTE2?displayProperty=fullName>     
 [Adicionando comandos do Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md)