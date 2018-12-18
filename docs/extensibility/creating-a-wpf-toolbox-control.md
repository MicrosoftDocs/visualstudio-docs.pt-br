---
title: Criar um controle de caixa de ferramentas do WPF | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 43734720a4e86f9f1e214285df1873b39b67fa01
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500326"
---
# <a name="create-a-wpf-toolbox-control"></a>Criar um controle de caixa de ferramentas do WPF
O modelo de controle de caixa de ferramentas do WPF (Windows Presentation Framework) permite que você crie controles WPF que são adicionados automaticamente para o **caixa de ferramentas** quando a extensão está instalada. Este tópico mostra como usar o modelo para criar uma **caixa de ferramentas** controle que você pode distribuir a outros usuários.  
  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-wpf-toolbox-control"></a>Criar um controle de caixa de ferramentas do WPF  
  
### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>Criar uma extensão com um controle de caixa de ferramentas do WPF  
  
1.  Crie um projeto do VSIX chamado `MyToolboxControl`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c#** > **extensibilidade**.  
  
2.  Quando o projeto aberto, adicione uma **controle de caixa de ferramentas do WPF** modelo de item chamado `MyToolboxControl`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** > **Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **controle de caixa de ferramentas do WPF**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para *MyToolboxControl.cs*.  
  
     A solução agora contém um controle de usuário, uma `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> que adiciona o controle para o **caixa de ferramentas**e um **Microsoft.VisualStudio.ToolboxControl** entrada de ativo no manifesto do VSIX para  implantação.  
  
#### <a name="to-create-the-control-ui"></a>Para criar o controle da interface do usuário  
  
1.  Abra *MyToolboxControl.xaml* no designer.  
  
     O designer mostra uma <xref:System.Windows.Controls.Grid> controle que contém um <xref:System.Windows.Controls.Button> controle.  
  
2.  Organize o layout de grade. Quando você seleciona o <xref:System.Windows.Controls.Grid> controlar, barras de controle azul aparecem nas bordas superior e esquerdas da grade. Você pode adicionar linhas e colunas à grade clicando nas barras.  
  
3.  Adicione controles filho à grade. Você pode posicionar um controle filho, arrastando-o do **caixa de ferramentas** para uma seção da grade, ou definindo sua `Grid.Row` e `Grid.Column` atributos em que o XAML. O exemplo a seguir adiciona dois rótulos na linha superior da grade e um botão na segunda linha.  
  
    ```xaml  
    <Grid>  
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />  
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />  
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />  
    </Grid>  
    ```  
  
## <a name="renaming-the-control"></a>Renomear o controle  
 Por padrão, o controle será exibido na **caixa de ferramentas** como **MyToolboxControl** em um grupo denominado **MyToolboxControl.MyToolboxControl**. Você pode alterar esses nomes na *MyToolboxControl.xaml.cs* arquivo.  
  
1.  Abra *MyToolboxControl.xaml.cs* na exibição de código.  
  
2.  Encontre o `MyToolboxControl` de classe e renomeie-o para TestControl. (A maneira mais rápida de fazer isso é renomear a classe, em seguida, selecione **Renomear** no menu de contexto e conclua as etapas. (Para obter mais informações sobre o **renomeie** de comando, consulte [renomear refatoração (c#)](../ide/reference/rename.md).)
  
3.  Vá para o `ProvideToolboxControl` de atributo e altere o valor do primeiro parâmetro para **teste**. Esse é o nome do grupo que contém o controle na **caixa de ferramentas**.  
  
     O código resultante deve ter esta aparência:  
  
    ```csharp  
    [ProvideToolboxControl("Test", true)]  
    public partial class TestControl : UserControl  
    {  
        public TestControl()  
        {  
            InitializeComponent();  
        }  
    }  
    ```  
  
## <a name="build-test-and-deployment"></a>Compilação, teste e implantação  
 Quando você depurar o projeto, você deve encontrar o controle instalado na **caixa de ferramentas** da instância experimental do Visual Studio.  
  
### <a name="to-build-and-test-the-control"></a>Para compilar e testar o controle  
  
1.  Recompilar o projeto e iniciar a depuração.  
  
2.  Na nova instância do Visual Studio, crie um projeto de aplicativo do WPF. Verifique se que o Designer XAML é aberto.  
  
3.  Localizar seu controle na **caixa de ferramentas** e arraste-o para a superfície de design.  
  
4.  Inicie a depuração de aplicativo do WPF.  
  
5.  Verifique se o controle for exibido.  
  
### <a name="to-deploy-the-control"></a>Para implantar o controle  
  
1.  Depois de compilar o projeto testado, você pode encontrar o *. VSIX* arquivo no * \bin\debug\* pasta do projeto.  
  
2.  Você pode instalá-lo em um computador local clicando duas vezes o *VSIX* arquivo e seguindo o procedimento de instalação. Para desinstalar o controle, vá para **ferramentas** > **extensões e atualizações** e procure a extensão de controle e clique em **desinstalação**.  
  
3.  Carregar o *VSIX* arquivo a uma rede ou para um site da Web.  
  
     Se você carregar o arquivo para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web, outros usuários podem usar **ferramentas** > **extensões e atualizações** no Visual Studio para localizar o controle online e instalá-lo.