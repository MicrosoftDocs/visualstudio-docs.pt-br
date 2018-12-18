---
title: Criar uma categoria de configurações | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 66667b97ef10d6b07bef3e8c1c3b19842a07482e
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388654"
---
# <a name="create-a-settings-category"></a>Criar uma categoria de configurações

Neste passo a passo, você cria uma categoria de configurações do Visual Studio e usá-lo para salvar os valores e restaurar os valores de um arquivo de configurações. Uma categoria de configurações é um grupo de propriedades relacionadas que são exibidos como um "ponto de configurações personalizadas"; ou seja, como uma caixa de seleção na **importação e exportação de configurações** assistente. (Você pode encontrá-lo sobre a **ferramentas** menu.) Configurações salvos ou restauradas como uma categoria e as configurações individuais não são exibidas no assistente. Para obter mais informações, consulte [as configurações de ambiente](../ide/environment-settings.md).

Criar uma categoria de configurações derivando-lo do <xref:Microsoft.VisualStudio.Shell.DialogPage> classe.

Para iniciar este passo a passo, você deve primeiro concluir a primeira seção do [criar uma página de opções](../extensibility/creating-an-options-page.md). A grade de propriedade opções resultante permite examinar e alterar as propriedades na categoria. Depois de salvar a categoria de propriedade em um arquivo de configurações, você pode examinar o arquivo para ver como os valores de propriedade são armazenados.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-settings-category"></a>Criar uma categoria de configurações
 Nesta seção, você pode usar um ponto de configurações personalizadas para salvar e restaurar os valores da categoria de configurações.

### <a name="to-create-a-settings-category"></a>Para criar uma categoria de configurações

1.  Conclua o [criar uma página de opções](../extensibility/creating-an-options-page.md).

2.  Abra o *VSPackage.resx* arquivo e adicione estes recursos de cadeia de caracteres de três:

    |Nome|Valor|
    |----------|-----------|
    |106|Minha categoria|
    |107|Minhas configurações|
    |108|OptionInteger e OptionFloat|

     Isso cria recursos esse nome de categoria "My Category", o objeto "My Settings" e a descrição da categoria "OptionInteger e OptionFloat".

    > [!NOTE]
    >  Esses três, apenas o nome da categoria não consta o **importar e exportar configurações** assistente.

3.  No *MyToolsOptionsPackage.cs*, adicione uma `float` propriedade denominada `OptionFloat` para o `OptionPageGrid` de classe, conforme mostrado no exemplo a seguir.

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;
        private float optionFloat = 3.14F;

        [Category("My Options")]
        [DisplayName("My Integer option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
        [Category("My Options")]
        [DisplayName("My Float option")]
        [Description("My float option")]
        public float OptionFloat
        {
            get { return optionFloat; }
            set { optionFloat = value; }
        }
    }
    ```

    > [!NOTE]
    >  O `OptionPageGrid` categoria chamada "My Category" agora consiste em duas propriedades, `OptionInteger` e `OptionFloat`.

4.  Adicionar um <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> para o `MyToolsOptionsPackage` de classe e dê a ele CategoryName "My Category", dê a ele o ObjectName "My Settings" e defina isToolsOptionPage como true. Defina o categoryResourceID, objectNameResourceID e DescriptionResourceID para o recurso de cadeia de caracteres correspondente que IDs criadas anteriormente.

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5.  Compile o projeto e comece a depuração. Na instância experimental, você deverá ver que **minha grade página** agora tem valores flutuantes e inteiros.

## <a name="examine-the-settings-file"></a>Examine o arquivo de configurações
 Nesta seção, você pode exportar os valores de categoria de propriedade para um arquivo de configurações. Examine o arquivo e, em seguida, importe os valores novamente para a categoria de propriedade.

1.  Inicie o projeto no modo de depuração pressionando **F5**. Isso inicia a instância experimental.

2.  Abra o **ferramentas** > **opções** caixa de diálogo.

3.  Na exibição de árvore no painel esquerdo, expanda **My Category** e, em seguida, clique em **minha página de grade**.

4.  Altere o valor de **OptionFloat** para 3.1416 e **OptionInteger** a 12. Clique em **OK**.

5.  Sobre o **ferramentas** menu, clique em **Import and Export Settings**.

     O **importar e exportar configurações** assistente é exibido.

6.  Certifique-se **exportar configurações de ambiente selecionadas** está selecionado e, em seguida, clique em **próxima**.

     O **escolher configurações para exportar** página será exibida.

7.  Clique em **minhas configurações**.

     O **descrição** alterações **OptionInteger e OptionFloat**.

8.  Certifique-se de que **minhas configurações** é a única categoria que está selecionada e, em seguida, clique em **próxima**.

     O **nome do seu arquivo de configurações** página será exibida.

9. Nomeie o novo arquivo de configurações *MySettings.vssettings* e salve-o em um diretório apropriado. Clique em **Finalizar**.

     O **Exportação concluída** página relatórios de que suas configurações foram exportadas com êxito.

10. Sobre o **arquivo** , aponte para **abra**e, em seguida, clique em **arquivo**. Localize *MySettings.vssettings* e abri-lo.

     Você pode encontrar a categoria de propriedade que você exportou na seção a seguir do arquivo (e seus GUIDs serão diferente).

    ```
    <Category name="My Category_My Settings"
          Category="{4802bc3e-3d9d-4591-8201-23d1a05216a6}"
          Package="{6bb6942e-014c-489e-a612-a935680f703d}"
          RegisteredName="My Category_My Settings">
          PackageName="MyToolsOptionsPackage">
       <PropertyValue name="OptionFloat">3.1416</PropertyValue>
       <PropertyValue name="OptionInteger">12</PropertyValue>
    </Category>
    ```

     Observe que o nome da categoria completo é formado pela adição de um caractere de sublinhado para o nome da categoria seguido pelo nome do objeto. OptionFloat e OptionInteger aparecem na categoria, junto com seus valores exportados.

11. Feche o arquivo de configurações sem alterá-lo.

12. No **ferramentas** menu, clique em **opções**, expanda **My Category**, clique em **minha página de grade** e, em seguida, altere o valor de  **OptionFloat** 1,0 e **OptionInteger** como 1. Clique em **OK**.

13. Sobre o **ferramentas** menu, clique em **importar e exportar configurações**, selecione **importar configurações de ambiente selecionadas**e, em seguida, clique em **Avançar**.

     O **salvar configurações atuais** página será exibida.

14. Selecione **não, apenas importe as novas configurações** e, em seguida, clique em **próxima**.

     O **escolha uma coleção de configurações a importar** página será exibida.

15. Selecione o *MySettings.vssettings* arquivo na **minhas configurações** nó do modo de exibição de árvore. Se o arquivo não aparecer na exibição de árvore, clique em **procurar** e encontrá-lo. Clique em **Avançar**.

     O **escolher configurações a importar** caixa de diálogo é exibida.

16. Certifique-se de que **minhas configurações** está selecionado e, em seguida, clique em **concluir**. Quando o **importação completa** página for exibida, clique em **fechar**.

17. Sobre o **ferramentas** menu, clique em **opções**, expanda **My Category**, clique em **minha página de grade** e verifique se os valores de categoria de propriedade tem foi restaurado.