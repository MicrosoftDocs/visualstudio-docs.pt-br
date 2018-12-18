---
title: Criando uma página de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9b9d61b4a57e0255577fdb0621dafd4263fc127c
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607764"
---
# <a name="create-an-options-page"></a>Criar uma página de opções
Este passo a passo cria uma página Ferramentas/opções simples que usa uma grade de propriedade para examinar e definir propriedades.  
  
 Para salvar essas propriedades para e restaurá-los de um arquivo de configurações, siga estas etapas e, em seguida, consulte [criar uma categoria de configurações](../extensibility/creating-a-settings-category.md).  
  
 MPF fornece classes para ajudá-lo a criar páginas de opções de ferramentas, o <xref:Microsoft.VisualStudio.Shell.Package> classe e o <xref:Microsoft.VisualStudio.Shell.DialogPage> classe. Criar um VSPackage para fornecer um contêiner para essas páginas Subclassificando o `Package` classe. Criar cada página de opções de ferramentas, derivando do `DialogPage` classe.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-tools-options-grid-page"></a>Criar uma página de grade de opções de ferramentas  
 Nesta seção, você criará uma grade de propriedades Opções de ferramentas simple. Você usa essa grade para exibir e alterar o valor de uma propriedade.  
  
### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>Para criar o projeto do VSIX e adicione um VSPackage  
  
1. Cada extensão do Visual Studio inicia com um projeto de implantação do VSIX que conterá os ativos de extensão. Criar uma [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto do VSIX chamado `MyToolsOptionsExtension`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c#** > **extensibilidade**.  
  
2. Adicionar um VSPackage adicionando um modelo de item de pacote do Visual Studio chamado `MyToolsOptionsPackage`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** > **Novo Item**. No **caixa de diálogo Adicionar Novo Item**, acesse **itens do Visual c#** > **extensibilidade** e selecione **Visual Studio Package**. No **nome** campo na parte inferior da caixa de diálogo, altere o nome de arquivo para `MyToolsOptionsPackage.cs`. Para obter mais informações sobre como criar um VSPackage, consulte [criar uma extensão com um VSPackage](../extensibility/creating-an-extension-with-a-vspackage.md).  
  
### <a name="to-create-the-tools-options-property-grid"></a>Para criar a grade de propriedades Opções de ferramentas  
  
1.  Abra o *MyToolsOptionsPackage* arquivo no editor de códigos.  
  
2.  Adicione a seguinte instrução using.  
  
    ```csharp  
    using System.ComponentModel;  
    ```  
  
3.  Declarar uma `OptionPageGrid` de classe e derive-a da <xref:Microsoft.VisualStudio.Shell.DialogPage>.  
  
    ```csharp  
    public class OptionPageGrid : DialogPage  
    {  }  
    ```  
  
4.  Aplicar uma <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> para o `VSPackage` classe a ser atribuído à classe uma categoria de opções e o nome de página de opções para o OptionPageGrid. O resultado deve ter esta aparência:  
  
    ```csharp  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [Guid(GuidList.guidMyToolsOptionsPkgString)]  
    [ProvideOptionPage(typeof(OptionPageGrid),  
        "My Category", "My Grid Page", 0, 0, true)]  
    public sealed class MyToolsOptionsPackage : Package  
    ```  
  
5.  Adicionar um `OptionInteger` propriedade para o `OptionPageGrid` classe.  
  
    -   Aplicar um <xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName> atribuir à propriedade de uma categoria de grade de propriedade.  
  
    -   Aplicar um <xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName> atribuir à propriedade um nome.  
  
    -   Aplicar um <xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName> atribuir à propriedade de uma descrição.  
  
    ```csharp  
    public class OptionPageGrid : DialogPage  
    {  
        private int optionInt = 256;  
  
        [Category("My Category")]  
        [DisplayName("My Integer Option")]  
        [Description("My integer option")]  
        public int OptionInteger  
        {  
            get { return optionInt; }  
            set { optionInt = value; }  
        }  
    }  
    ```  
  
    > [!NOTE]
    >  A implementação padrão de <xref:Microsoft.VisualStudio.Shell.DialogPage> dá suporte às propriedades que têm conversores apropriados ou que são estruturas ou matrizes que podem ser expandidos em propriedades que têm conversores apropriados. Para obter uma lista de conversores, consulte o <xref:System.ComponentModel> namespace.  
  
6.  Compile o projeto e comece a depuração.  
  
7.  Na instância experimental do Visual Studio, sobre o **ferramentas** menu, clique em **opções**.  
  
     No painel esquerdo, você deve ver **My Category**. (Categorias de opções são listadas em ordem alfabética, portanto, ele deve aparecer sobre na metade para baixo na lista.) Abra **My Category** e, em seguida, clique em **minha página de grade**. A grade de opções é exibida no painel direito. A categoria de propriedade é **minhas opções**, e é o nome da propriedade **minha opção de inteiro**. A descrição da propriedade **minha opção inteiro**, aparece na parte inferior do painel. Altere o valor do seu valor inicial de 256 para algo diferente. Clique em **Okey**e, em seguida, reabra **minha página de grade**. Você pode ver que o novo valor persiste.  
  
     Sua página de opções também está disponível por meio de início rápido do Visual Studio. Na janela de início rápido no canto superior direito do IDE, digite **My Category** e você verá **My Category -> minha página de grade** listados na lista suspensa.  
  
## <a name="create-a-tools-options-custom-page"></a>Criar uma página de opções de ferramentas personalizada  
 Nesta seção, você pode criar uma página de opções de ferramentas com uma interface do usuário personalizada. Use esta página para exibir e alterar o valor de uma propriedade.  
  
1.  Abra o *MyToolsOptionsPackage* arquivo no editor de códigos.  
  
2.  Adicione a seguinte instrução using.  
  
    ```csharp  
    using System.Windows.Forms;  
    ```  
  
3.  Adicionar um `OptionPageCustom` classe, imediatamente antes o `OptionPageGrid` classe. Derive a classe nova do `DialogPage`.  
  
    ```csharp  
    public class OptionPageCustom : DialogPage  
    {  
        private string optionValue = "alpha";  
  
        public string OptionString  
        {  
            get { return optionValue; }  
            set { optionValue = value; }  
        }  
    }  
    ```  
  
4.  Adicione um atributo GUID. Adicione uma propriedade OptionString:  
  
    ```csharp  
    [Guid("00000000-0000-0000-0000-000000000000")]  
    public class OptionPageCustom : DialogPage  
    {  
        private string optionValue = "alpha";  
  
        public string OptionString  
        {  
            get { return optionValue; }  
            set { optionValue = value; }  
        }  
    }  
    ```  
  
5.  Aplicar um segundo <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> à classe VSPackage. Esse atributo atribui a classe de uma categoria de opções e o nome da página de opções.  
  
    ```csharp  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]  
    [ProvideMenuResource("Menus.ctmenu", 1)]  
    [Guid(GuidList.guidMyToolsOptionsPkgString)]  
    [ProvideOptionPage(typeof(OptionPageGrid),  
        "My Category", "My Grid Page", 0, 0, true)]  
    [ProvideOptionPage(typeof(OptionPageCustom),  
        "My Category", "My Custom Page", 0, 0, true)]  
    public sealed class MyToolsOptionsPackage : Package  
    ```  
  
6.  Adicione um novo **controle de usuário** chamado MyUserControl ao projeto.  
  
7.  Adicionar um **caixa de texto** controle para o controle de usuário.  
  
     No **propriedades** janela, na barra de ferramentas, clique no **eventos** botão e, em seguida, clique duas vezes o **deixe** eventos. O novo manipulador de eventos aparece na *MyUserControl.cs* código.  
  
8.  Adicionar um público `OptionsPage` campo, um `Initialize` método para a classe de controle e a atualização para o manipulador de eventos para definir a opção de valor para o conteúdo da caixa de texto:  
  
    ```csharp  
    public partial class MyUserControl : UserControl  
    {  
        public MyUserControl()  
        {  
            InitializeComponent();  
        }  
  
        internal OptionPageCustom optionsPage;  
  
        public void Initialize()  
        {  
            textBox1.Text = optionsPage.OptionString;  
        }  
  
        private void textBox1_Leave(object sender, EventArgs e)  
        {  
            optionsPage.OptionString = textBox1.Text;  
        }  
    }  
    ```  
  
     O `optionsPage` campo contém uma referência ao pai `OptionPageCustom` instância. O `Initialize` método exibe `OptionString` na **caixa de texto**. O manipulador de eventos grava o valor atual do **caixa de texto** para o `OptionString` ao focalizar deixa o **caixa de texto**.  
  
9. No arquivo de código do pacote, adicione uma substituição para o `OptionPageCustom.Window` propriedade para o `OptionPageCustom` classe para criar, inicializar e retornar uma instância de `MyUserControl`. Agora, a classe deve ser assim:  
  
    ```csharp  
    [Guid("00000000-0000-0000-0000-000000000000")]  
    public class OptionPageCustom : DialogPage  
    {  
        private string optionValue = "alpha";  
  
        public string OptionString  
        {  
            get { return optionValue; }  
            set { optionValue = value; }  
        }  
  
        protected override IWin32Window Window  
        {  
            get  
            {  
                MyUserControl page = new MyUserControl();  
                page.optionsPage = this;  
                page.Initialize();  
                return page;  
            }  
        }  
    }  
    ```  
  
10. Compile e execute o projeto.  
  
11. Na instância experimental, clique em **ferramentas** > **opções**.  
  
12. Encontre **minha categoria** e, em seguida **meu personalizado página**.  
  
13. Altere o valor de **OptionString**. Clique em **Okey**e, em seguida, reabra **minha página personalizada**. Você pode ver que o novo valor tem persistente.  
  
## <a name="access-options"></a>Opções de acesso  
 Nesta seção, você pode obter o valor de uma opção de VSPackage que hospeda a página de opções de ferramentas associada. A mesma técnica pode ser usada para obter o valor de qualquer propriedade pública.  
  
1.  No arquivo de código do pacote, adicionar uma propriedade pública denominada **OptionInteger** para o **MyToolsOptionsPackage** classe.  
  
    ```csharp  
    public int OptionInteger  
    {  
        get  
        {  
            OptionPageGrid page = (OptionPageGrid)GetDialogPage(typeof(OptionPageGrid));  
            return page.OptionInteger;  
        }  
    }  
  
    ```  
  
     Esse código chama <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> para criar ou recuperar um `OptionPageGrid` instância. `OptionPageGrid` chamadas <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A> para carregar suas opções, que são propriedades públicas.  
  
2.  Agora, adicione um modelo de item de comando personalizado chamado **MyToolsOptionsCommand** para exibir o valor. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **comando personalizado**. No **nome** campo na parte inferior da janela, altere o nome do arquivo de comando para *MyToolsOptionsCommand.cs*.  
  
3.  No *MyToolsOptionsCommand* do arquivo, substitua o corpo do comando `ShowMessageBox` método com o seguinte:  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;  
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));  
    }  
  
    ```  
  
4.  Compile o projeto e comece a depuração.  
  
5.  Na instância experimental, sobre o **ferramentas** menu, clique em **MyToolsOptionsCommand invocar**.  
  
     Uma caixa de mensagem exibe o valor atual de `OptionInteger`.  
  
## <a name="see-also"></a>Consulte também  
 [Opções e páginas de opções](../extensibility/internals/options-and-options-pages.md)
