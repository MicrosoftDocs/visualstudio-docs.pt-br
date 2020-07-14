---
title: 'Walkthrough: salvando configurações de usuário em uma página inicial | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8dd20513defd1db8848cf6a80a29e04c127c9dd4
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903159"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>Walkthrough: salvar as configurações do usuário em uma página inicial

Você pode manter as configurações de usuário para sua página inicial. Seguindo este passo a passos, você pode criar um controle que salva uma configuração no registro quando o usuário clica em um botão e, em seguida, recupera essa configuração toda vez que a página inicial é carregada. Como o modelo de projeto de página inicial inclui um controle de usuário personalizável e o XAML de página inicial padrão chama esse controle, você não precisa modificar a página inicial em si.

O armazenamento de configurações que é instanciado neste passo a passos é uma instância da <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> interface, que lê e grava no seguinte local do registro quando ele é chamado **: \\ \<CollectionName> HKCU\Software\Microsoft\VisualStudio\14.0**

Quando ele está em execução na instância experimental do Visual Studio, as configurações armazenam leituras e gravações em **HKCU\Software\Microsoft\VisualStudio\14.0Exp \\ \<CollectionName> .**

Para obter mais informações sobre como persistir configurações, consulte [estendendo configurações e opções de usuário](../extensibility/extending-user-settings-and-options.md).

## <a name="prerequisites"></a>Pré-requisitos

> [!NOTE]
> Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).
>
> Você pode baixar o modelo de projeto de página inicial usando o **Gerenciador de extensões**.

## <a name="set-up-the-project"></a>Configurar o projeto

1. Crie um projeto de página inicial conforme descrito em [criar uma página inicial personalizada](creating-a-custom-start-page.md). Nomeie o projeto **SaveMySettings**.

2. Em **Gerenciador de soluções**, adicione as seguintes referências de assembly ao projeto StartPageControl:

    - EnvDTE

    - EnvDTE80

    - Microsoft. VisualStudio. OLE. Interop

    - Microsoft. VisualStudio. Shell. Interop. 11.0

3. Abra *myControl. XAML*.

4. No painel XAML, na definição de elemento de nível superior <xref:System.Windows.Controls.UserControl> , adicione a seguinte declaração de evento após as declarações de namespace.

    ```xml
    Loaded="OnLoaded"
    ```

5. No painel Design, clique na área principal do controle e pressione **delete**.

     Essa etapa remove o <xref:System.Windows.Controls.Border> elemento e tudo nele e deixa apenas o elemento de nível superior <xref:System.Windows.Controls.Grid> .

6. Na **caixa de ferramentas**, arraste um <xref:System.Windows.Controls.StackPanel> controle para a grade.

7. Agora, arraste um <xref:System.Windows.Controls.TextBlock> , um <xref:System.Windows.Controls.TextBox> e um botão para o <xref:System.Windows.Controls.StackPanel> .

8. Adicione um atributo **x:Name** para o <xref:System.Windows.Controls.TextBox> e um `Click` evento para o <xref:System.Windows.Controls.Button> , conforme mostrado no exemplo a seguir.

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>Implementar o controle de usuário

1. No painel XAML, clique com o botão direito do mouse no `Click` atributo do <xref:System.Windows.Controls.Button> elemento e clique em **navegar até manipulador de eventos**.

     Essa etapa abre *myControl.XAML.cs*e cria um manipulador de stub para o `Button_Click` evento.

2. Adicione as seguintes `using` diretivas à parte superior do arquivo.

     [!code-csharp[StartPageDTE#11](../extensibility/codesnippet/CSharp/walkthrough-saving-user-settings-on-a-start-page_1.cs)]

3. Adicione uma `SettingsStore` propriedade privada, conforme mostrado no exemplo a seguir.

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

     Essa propriedade primeiro obtém uma referência à <xref:EnvDTE80.DTE2> interface, que contém o modelo de objeto de automação, do <xref:System.Windows.FrameworkElement.DataContext%2A> do controle de usuário e, em seguida, usa o DTE para obter uma instância da <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> interface. Em seguida, ele usa essa instância para retornar as configurações do usuário atual.

4. Preencha o `Button_Click` evento da seguinte maneira.

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

     Isso grava o conteúdo da caixa de texto em um campo "MySetting" em uma coleção "MySettings" no registro. Se a coleção não existir, ela será criada.

5. Adicione o manipulador a seguir ao `OnLoaded` evento do controle de usuário.

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     Esse código define o texto da caixa de texto como o valor atual de "MySetting".

6. Crie o controle de usuário.

7. No **Gerenciador de soluções**, abra *Source. Extension. vsixmanifest*.

8. No editor de manifesto, defina **nome do produto** para **salvar minha página inicial de configurações**.

     Esse recurso define o nome da página inicial como ela é exibida na lista **Personalizar página inicial** na caixa de diálogo **Opções** .

9. Compilar *Startpage. XAML*.

## <a name="test-the-control"></a>Testar o controle

1. Pressione **F5**.

     A instância experimental do Visual Studio é aberta.

2. Na instância experimental, no menu **ferramentas** , clique em **Opções**.

3. No nó **ambiente** , clique em **inicialização**e, em seguida, na lista **Personalizar página inicial** , selecione **[extensão instalada] salvar minha página inicial de configurações**.

     Clique em **OK**.

4. Feche a página inicial se ela estiver aberta e, no menu **Exibir** , clique em **página inicial**.

5. Na página inicial, clique na guia **MyControl** .

6. Na caixa de texto, digite **Cat**e clique em **salvar minha configuração**.

7. Feche a página inicial e abra-a novamente.

     A palavra "gato" deve ser exibida na caixa de texto.

8. Substitua a palavra "gato" pela palavra "cachorro". Não clique no botão.

9. Feche a página inicial e abra-a novamente.

     A palavra "cachorro" deve ser exibida na caixa de texto, mesmo que você não tenha salvo a configuração porque o Visual Studio mantém as janelas de ferramentas na memória, mesmo que elas sejam fechadas, até que o próprio Visual Studio seja fechado.

10. Feche a instância experimental do Visual Studio.

11. Pressione **F5** para reabrir a instância experimental.

12. A palavra "gato" deve ser exibida na caixa de texto.

## <a name="next-steps"></a>Próximas etapas

Você pode modificar esse controle de usuário para salvar e recuperar qualquer número de configurações personalizadas usando diferentes valores de manipuladores de eventos diferentes para obter e definir a `SettingsStore` propriedade. Contanto que você use um `propertyName` parâmetro diferente para cada chamada para <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> , os valores não substituem um ao outro no registro.

## <a name="see-also"></a>Confira também

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [Adicionando comandos do Visual Studio a uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
