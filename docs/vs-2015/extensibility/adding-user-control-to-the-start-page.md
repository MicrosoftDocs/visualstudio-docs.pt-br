---
title: Adicionando o controle de usuário para a página inicial | Microsoft Docs
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
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 01510eabcb4d2d3605f38b8bb574ed3e21efebac
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736716"
---
# <a name="adding-user-control-to-the-start-page"></a>Adicionando um controle de usuário à página inicial
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como adicionar uma referência DLL para uma página inicial personalizada. O exemplo adiciona um controle de usuário para a solução, compila o controle de usuário e, em seguida, faz referência ao assembly compilado do arquivo Start Page. XAML. Uma nova guia hospeda o controle de usuário, que funciona como um navegador da Web básico.  
  
 Você pode usar o mesmo processo para adicionar qualquer assembly que pode ser chamado de um arquivo. XAML.  
  
## <a name="adding-a-wpf-user-control-to-the-solution"></a>Adicionando um controle de usuário do WPF à solução  
 Primeiro, adicione um controle de usuário do Windows Presentation Foundation (WPF) para a solução de página inicial.  
  
1.  Criar uma página inicial usando criamos na [criando uma página de início personalizado](../extensibility/creating-a-custom-start-page.md).  
  
2.  Na **Gerenciador de soluções**, a solução com o botão direito, clique em **Add**e, em seguida, clique em **novo projeto**.  
  
3.  No painel esquerdo do **novo projeto** diálogo caixa, expanda o a **Visual Basic** ou **Visual c#** nó e clique em **Windows**. No painel central, selecione **biblioteca de controle de usuário do WPF**.  
  
4.  Nomeie o controle `WebUserControl` e, em seguida, clique em **Okey**.  
  
## <a name="implementing-the-user-control"></a>Implementando o controle de usuário  
 Para implementar um controle de usuário do WPF, crie a interface do usuário (IU) no XAML e, em seguida, gravar os eventos de lógica em c# ou outra linguagem .NET.  
  
#### <a name="to-write-the-xaml-for-the-user-control"></a>Para gravar o XAML para o controle de usuário  
  
1.  Abra o arquivo XAML para o controle de usuário. No \<grade > elemento, adicione as seguintes definições de linha para o controle.  
  
    ```vb  
    <Grid.RowDefinitions>  
        <RowDefinition Height="Auto"/>  
        <RowDefinition Height="*" />  
    </Grid.RowDefinitions>  
  
    ```  
  
2.  No principal `Grid` elemento, adicione a seguinte nova `Grid` elemento, que contém uma caixa de texto para digitar endereços da Web e um botão para definir o novo endereço.  
  
    ```xml  
    <Grid Grid.Row="0">  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="*" />  
            <ColumnDefinition Width="Auto" />  
        </Grid.ColumnDefinitions>  
        <TextBox x:Name="UserSource" Grid.Column="0" />  
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />  
    </Grid>  
    ```  
  
3.  Adicionar o quadro a seguir para o nível superior `Grid` elemento logo após o `Grid` elemento que contém o botão e a caixa de texto.  
  
    ```vb  
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />  
    ```  
  
4.  O exemplo a seguir mostra o XAML concluído para o controle de usuário.  
  
    ```xml  
    <UserControl x:Class="WebUserControl.UserControl1"  
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"   
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"   
                 mc:Ignorable="d"   
                 d:DesignHeight="300" d:DesignWidth="300">  
        <Grid>  
            <Grid.RowDefinitions>  
                <RowDefinition Height="Auto"/>  
                <RowDefinition Height="*" />  
            </Grid.RowDefinitions>  
            <Grid Grid.Row="0">  
                <Grid.ColumnDefinitions>  
                    <ColumnDefinition Width="*" />  
                    <ColumnDefinition Width="Auto" />  
                </Grid.ColumnDefinitions>  
                <TextBox x:Name="UserSource" Grid.Column="0" />  
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />  
            </Grid>  
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />  
        </Grid>  
    </UserControl>  
  
    ```  
  
#### <a name="to-write-the-code-behind-events-for-the-user-control"></a>Para gravar os eventos de lógica do controle de usuário  
  
1.  No designer XAML, clique duas vezes o **endereço definido** adicionada ao controle de botão.  
  
     O arquivo UserControl1.cs é aberto no editor de códigos.  
  
2.  Preencha o manipulador de eventos SetButton_Click da seguinte maneira.  
  
    ```csharp  
    private void SetButton_Click(object sender, RoutedEventArgs e)  
    {  
        try  
        {  
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);  
        }  
        catch (Exception error)  
        {  
            MessageBox.Show(error.Message);  
        }  
    }  
    ```  
  
     Esse código define o endereço da Web que é digitado na caixa de texto como o destino para o navegador da Web. Se o endereço não é válido, o código gera um erro.  
  
3.  Você também deve tratar o evento WebFrame_Navigated:  
  
    ```csharp  
    private void WebFrame_Navigated(object sender, EventArgs e)  
    { }  
    ```  
  
4.  Compile a solução.  
  
## <a name="adding-the-user-control-to-the-start-page"></a>Adicionando o controle de usuário para a página inicial  
 Para disponibilizar esse controle para o projeto de página inicial, no arquivo de página de início do projeto, adicione uma referência para a nova biblioteca de controle. Em seguida, você pode adicionar o controle para a marcação de XAML de página de início.  
  
1. Na **Gerenciador de soluções**, no projeto de página inicial, clique com botão direito **referências** e, em seguida, clique em **Add Reference**.  
  
2. Sobre o **projetos** guia, selecione **WebUserControl** e, em seguida, clique em **Okey**.  
  
3. No menu **Compilar**, clique em **Compilar Solução**.  
  
    Compilando a solução disponibiliza o controle de usuário para o IntelliSense para outros arquivos na solução.  
  
   Para adicionar o controle para a marcação de XAML de página Iniciar, adicionar uma referência ao namespace para o assembly e, em seguida, colocar o controle na página.  
  
#### <a name="to-add-the-control-to-the-markup"></a>Para adicionar o controle à marcação  
  
1. Na **Gerenciador de soluções**, abra o arquivo. XAML de página inicial.  
  
2. No **XAML** painel, adicione a seguinte declaração de namespace para o nível superior <xref:System.Windows.Controls.Grid> elemento.  
  
   ```xml  
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
   ```  
  
3. No **XAML** painel, role até a \<grade > seção.  
  
    A seção contém um <xref:System.Windows.Controls.TabControl> elemento em um <xref:System.Windows.Controls.Grid> elemento.  
  
4. Adicionar um \<TabControl > elemento que contém um \<TabItem > que contém uma referência ao controle de usuário.  
  
   ```xml  
  
   <TabItem Header="Web" Height="Auto">  
       <vsc:UserControl1 />  
   </TabItem>  
  
   ```  
  
   Agora você pode testar o controle.  
  
## <a name="testing-a-manually-created-custom-start-page"></a>Testando uma página de início personalizados criados manualmente  
  
1.  Copie seu arquivo XAML e quaisquer arquivos de texto de suporte ou marcação arquivos, como o **%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\**  pasta.  
  
2.  Se sua página inicial faz referência a quaisquer controles ou tipos em assemblies que não estão instalados pelo Visual Studio, copie os assemblies e, em seguida, cole-os nas _pasta de instalação do Visual Studio_**\Common7\IDE\ PrivateAssemblies\\**.  
  
3.  Em um prompt de comando do Visual Studio, digite **devenv /rootsuffix Exp** para abrir uma instância experimental do Visual Studio.  
  
4.  Na instância experimental, vá para o **Ferramentas / opções / ambiente / inicialização** da página e selecione o arquivo XAML da **Personalizar página inicial** lista suspensa.  
  
5.  Sobre o **modo de exibição** menu, clique em **Start Page**.  
  
     Sua página inicial personalizada deve ser exibida. Se você deseja alterar todos os arquivos, você deve fechar a instância experimental, faça as alterações, copie e cole os arquivos alterados e, em seguida, reabra a instância experimental para exibir as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Controles de contêiner do WPF](http://msdn.microsoft.com/en-us/a0177167-d7db-4205-9607-8ae316952566)   
 [Adicionar XAML personalizado à página inicial](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)

