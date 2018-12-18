---
title: Inspecione as propriedades XAML durante a depuração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 390edde4-7b8d-4c89-8d69-55106b7e6b11
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: fcb2877a79afc310985102972d870caae560b393
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31480209"
---
# <a name="inspect-xaml-properties-while-debugging"></a>Inspecione as propriedades XAML durante a depuração
Você pode obter uma exibição em tempo real do seu código XAML em execução com o **árvore Visual dinâmica** e **Live propriedade Explorer**. Essas ferramentas oferecem um modo de exibição de árvore dos elementos de interface do usuário de seu aplicativo em execução do XAML e mostram as propriedades de tempo de execução de qualquer elemento de interface do usuário selecionado.  
  
 Você pode usar essas ferramentas nas seguintes configurações:  
  
|Tipo de aplicativo|Sistema operacional e ferramentas|  
|-----------------|--------------------------------|  
|Aplicativos de Windows Presentation Foundation (4.0 e posterior)|Windows 7 e posterior|  
|Aplicativos Universais do Windows|Windows 10 e acima, com o [Windows 10 SDK](https://dev.windows.com/en-us/downloads/windows-10-sdk)|  
  
## <a name="looking-at-elements-in-the-live-visual-tree"></a>Examinando os elementos na árvore Visual dinâmica  
 Vamos começar com um aplicativo do WPF muito simple que tem um botão e uma exibição de lista. Toda vez que você clicar no botão, o outro item é adicionado à lista. Par itens aparecem em cinza e itens ímpares são coloridos de amarelos.  
  
 Criar um novo aplicativo c# WPF (arquivo > Novo > projeto, em seguida, selecione c# e localizar o aplicativo do WPF). Nomeie- **TestXAML**.  
  
 Altere MainWindow. XAML para o seguinte:  
  
```xaml  
<Window x:Class="TestXAML.MainWindow"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    xmlns:local="clr-namespace:TestXAML"  
    mc:Ignorable="d"  
     Title="MainWindow" Height="350" Width="525">  
    <Grid>  
        <Button x:Name="button" Background="LightBlue" Content="Add Item" HorizontalAlignment="Left" Margin="216,206,0,0" VerticalAlignment="Top" Width="75" Click="button_Click"/>  
        <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="100" VerticalAlignment="Top" Width="100" Margin="205,80,0,0"/>  
    </Grid>  
</Window>  
```  
  
 Adicione o manipulador de comando a seguir ao arquivo MainWindow.xaml.cs:  
  
```csharp 
int count;

private void button_Click(object sender, RoutedEventArgs e)  
{  
    ListBoxItem item = new ListBoxItem();  
    item.Content = "Item" + ++count;  
    if (count % 2 == 0)  
    {  
        item.Background = Brushes.LightGray;  
    }  
    else  
    {  
        item.Background = Brushes.LightYellow;  
    }  
    listBox.Items.Add(item);  
}  
```  
  
 Compile o projeto e comece a depuração. (A configuração de compilação deve ser não a versão de depuração. Para obter mais informações sobre configurações de compilação, consulte [Noções básicas sobre configurações de compilação](../ide/understanding-build-configurations.md).)  
  
 Quando a janela é exibida, clique no **Adicionar Item** botão algumas vezes. Você deve ver algo parecido com isso:  
  
 ![Janela principal do aplicativo](../debugger/media/livevisualtree-app.png "LiveVIsualTree aplicativo")  
  
 Agora, abra o **árvore Visual dinâmica** janela (**Depurar > Windows > Árvore Visual dinâmica**, ou que localizá-lo no lado esquerdo do IDE). Arraste-a para fora de sua posição de encaixe para que possamos pesquisar esta janela e **propriedades Live** janela lado a lado. No **árvore Visual dinâmica** janela, expanda o **ContentPresenter** nó. Ela deve conter nós para o botão e a caixa de listagem. Expanda a caixa de listagem (e, em seguida, o **ScrollContentPresenter** e **ItemsPresenter**) para localizar a lista de itens de caixa. A janela deve ter esta aparência:  
  
 ![ListBoxItems na árvore Visual dinâmica](../debugger/media/livevisualtree-listboxitems.png "LiveVisualTree ListBoxItems")  
  
 Volte à janela do aplicativo e adicione alguns itens. Você deverá ver mais itens de caixa de lista no **árvore Visual dinâmica**.  
  
 Agora vamos examinar as propriedades de um dos itens da caixa de lista. Selecione o primeiro item de caixa de lista no **árvore Visual dinâmica** e clique no **Mostrar propriedades** ícone na barra de ferramentas. O **Live propriedade Explorer** devem aparecer. Observe que o **conteúdo** campo é "1" e o **em segundo plano** campo é **#FFFFFFE0** (amarelo-claro). Volte para o **árvore Visual dinâmica** e selecione o segundo item de caixa de listagem. O **Live propriedade Explorer** deve mostrar que o **conteúdo** campo é "2" e o **em segundo plano** campo é **#FFD3D3D3** (cinza claro ).  
  
 A estrutura real do XAML tem muitos elementos que você provavelmente não está interessado diretamente, e se você não souber o código também pode ter dificuldade para navegar na árvore para localizar o que você está procurando. Portanto, o **árvore Visual dinâmica** possui duas maneiras que permitem a você usar a interface do usuário do aplicativo para ajudá-lo a localizar o elemento que você deseja examinar.  
  
 **Habilitar seleção no aplicativo em execução**. Você pode habilitar esse modo quando você seleciona o botão mais à esquerda no **árvore Visual dinâmica** barra de ferramentas. Com esse modo em, você pode selecionar um elemento de interface do usuário no aplicativo e o **árvore Visual dinâmica** (e o **Live Visualizador de propriedade**) é atualizado automaticamente para mostrar o nó da árvore correspondente a esse elemento e suas propriedades.  
  
 **Exibir adornos de layout no aplicativo em execução**. Você pode habilitar esse modo quando você selecionar o botão que está imediatamente à direita do botão de seleção Habilitar. Quando **exibir adornos de layout** está ativado, ele faz com que a janela do aplicativo mostrar as linhas horizontais e verticais ao longo dos limites do objeto selecionado para que possa ver o que ele alinha, bem como retângulos mostrando as margens. Por exemplo, ativar ambos **Habilitar seleção** e **layout de exibição** em e selecione o **Adicionar Item** bloco de texto no aplicativo. Você verá o nó de bloco de texto no **árvore Visual dinâmica** e propriedades de bloco de texto no **Live Visualizador de propriedade**, bem como as linhas horizontais e verticais dos limites do bloco de texto.  
  
 ![LivePropertyViewer em DisplayLayout](../debugger/media/livevisualtreelivepropertyviewer-displaylayout.png "LiveVisualTreeLivePropertyViewer DisplayLayout")  
  
 **Visualizar seleção**. Você pode habilitar esse modo, selecionando o terceiro botão à esquerda na barra de ferramentas da árvore Visual dinâmica. Esse modo não mostra o XAML em que o elemento foi declarado, se você tiver acesso ao código-fonte do aplicativo. Selecione **Habilitar seleção** e **visualizar seleção**, e, em seguida, selecione o botão no nosso aplicativo de teste. O arquivo de MainWindow. XAML é aberto no Visual Studio e o cursor é colocado na linha em que o botão está definido.  
  
## <a name="using-xaml-tools-with-running-applications"></a>Usando ferramentas XAML com a execução de aplicativos  
 Você pode usar essas ferramentas XAML, mesmo quando você não tiver o código-fonte. Quando você anexa a um aplicativo em execução de XAML, você pode usar o **árvore Visual dinâmica** nos elementos da interface do usuário do aplicativo muito. Aqui está um exemplo, usando o mesmo aplicativo de teste do WPF que usamos antes.  
  
1.  Iniciar o **TestXaml** aplicativo na versão de configuração. Você não pode anexar a um processo que está sendo executado em um **depurar** configuração.  
  
2.  Abra uma segunda instância do Visual Studio e clique em **Depurar > Anexar ao processo**. Localizar **TestXaml.exe** na lista de processos disponíveis e clique em **Attach**.  
  
3.  O aplicativo começa a ser executado.  
  
4.  Na segunda instância do Visual Studio, abra o **árvore Visual dinâmica** (**Depurar > Windows > Árvore Visual dinâmica**). Você deve ver o **TestXaml** elementos de interface do usuário e você deve ser capaz de manipulá-los como você enquanto estiver depurando o aplicativo diretamente.