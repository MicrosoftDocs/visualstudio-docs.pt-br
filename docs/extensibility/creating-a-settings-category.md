---
title: Criando uma categoria de configurações | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d50ca998efa034b1d4392c1fb7cecb8de8ed06
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904021"
---
# <a name="create-a-settings-category"></a>Criar uma categoria de configurações

Neste tutorial, você cria uma categoria de configurações do Visual Studio e a usa para salvar valores e restaurar valores de um arquivo de configurações. Uma categoria de configurações é um grupo de propriedades relacionadas que aparecem como um "ponto de configurações personalizadas"; ou seja, como uma caixa de seleção no assistente de **importação e exportação de configurações** . (Você pode encontrá-lo no menu **ferramentas** .) As configurações são salvas ou restauradas como uma categoria, e as configurações individuais não são exibidas no assistente. Para obter mais informações, confira [Configurações do ambiente](../ide/environment-settings.md).

Você cria uma categoria de configurações derivando-a da <xref:Microsoft.VisualStudio.Shell.DialogPage> classe.

Para iniciar este passo a passos, você deve primeiro concluir a primeira seção da [página criar uma opção](../extensibility/creating-an-options-page.md). A grade de propriedades de opções resultantes permite que você examine e altere as propriedades na categoria. Depois de salvar a categoria de propriedade em um arquivo de configurações, examine o arquivo para ver como os valores de propriedade são armazenados.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-settings-category"></a>Criar uma categoria de configurações
 Nesta seção, você usa um ponto de configurações personalizado para salvar e restaurar os valores da categoria configurações.

### <a name="to-create-a-settings-category"></a>Para criar uma categoria de configurações

1. Conclua a [página criar uma opção](../extensibility/creating-an-options-page.md).

2. Abra o arquivo *VSPackage. resx* e adicione estes três recursos de cadeia de caracteres:

    |Nome|Valor|
    |----------|-----------|
    |106|Minha categoria|
    |107|Minhas Configurações|
    |108|OptionInteger e OptionFloat|

     Isso cria recursos que nomeiem a categoria "minha categoria", o objeto "minhas configurações" e a descrição da categoria "OptionInteger e OptionFloat".

    > [!NOTE]
    > Desses três, somente o nome da categoria não aparece no assistente de **importação e exportação de configurações** .

3. No *MyToolsOptionsPackage.cs*, adicione uma `float` propriedade chamada `OptionFloat` à `OptionPageGrid` classe, conforme mostrado no exemplo a seguir.

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
    > A `OptionPageGrid` categoria denominada "minha categoria" agora consiste nas duas propriedades `OptionInteger` e `OptionFloat` .

4. Adicione uma <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> à `MyToolsOptionsPackage` classe e dê a ela o NomeDaCategoria "minha categoria", dê a ela o ObjectName "My Settings" e defina isToolsOptionPage como true. Defina categoryResourceID, objectNameResourceID e DescriptionResourceID como as IDs de recurso de cadeia de caracteres a serem criadas anteriormente.

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. Compile o projeto e comece a depuração. Na instância experimental, você deve ver que **a página de grade** agora tem valores inteiros e float.

## <a name="examine-the-settings-file"></a>Examinar o arquivo de configurações
 Nesta seção, você exporta valores de categoria de propriedade para um arquivo de configurações. Examine o arquivo e importe os valores de volta para a categoria de propriedade.

1. Inicie o projeto no modo de depuração pressionando **F5**. Isso inicia a instância experimental.

2. Abra a **Tools**  >  caixa de diálogo**Opções** de ferramentas.

3. No modo de exibição de árvore no painel esquerdo, expanda **minha categoria** e clique em **minha página de grade**.

4. Altere o valor de **OptionFloat** para 3,1416 e **OptionInteger** para 12. Clique em **OK**.

5. No menu, **Ferramentas**, clique em **Importar e Exportar Configurações**.

     O assistente de **importação e exportação de configurações** é exibido.

6. Verifique se a **Opções exportar configurações de ambiente selecionadas** está selecionada e clique em **Avançar**.

     A página **escolher configurações a serem exportadas** é exibida.

7. Clique em **minhas configurações**.

     A **Descrição** muda para **OptionInteger e OptionFloat**.

8. Verifique se **minhas configurações** é a única categoria selecionada e clique em **Avançar**.

     A página **nome do arquivo de configurações** é exibida.

9. Nomeie o novo arquivo de configurações MySettings *. vssettings* e salve-o em um diretório apropriado. Clique em **Concluir**.

     A página **Exportar completo** relata que suas configurações foram exportadas com êxito.

10. No menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo**. Localize *MySettings. vssettings* e abra-o.

     Você pode encontrar a categoria de propriedade exportada na seção a seguir do arquivo (seus GUIDs serão diferentes).

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

     Observe que o nome completo da categoria é formado pela adição de um sublinhado ao nome da categoria seguido pelo nome do objeto. OptionFloat e OptionInteger aparecem na categoria, junto com seus valores exportados.

11. Feche o arquivo de configurações sem alterá-lo.

12. No menu **ferramentas** , clique em **Opções**, expanda **minha categoria**, clique em **minha página de grade** e altere o valor de **OptionFloat** para 1,0 e **OptionInteger** para 1. Clique em **OK**.

13. No menu **ferramentas** , clique em **importar e exportar configurações**, selecione **Importar configurações de ambiente selecionadas**e clique em **Avançar**.

     A página **salvar configurações atuais** é exibida.

14. Selecione **não, apenas importe as novas configurações** e clique em **Avançar**.

     A página **escolher uma coleção de configurações a serem importadas** é exibida.

15. Selecione o arquivo MySettings *. vssettings* no nó **minhas configurações** do modo de exibição de árvore. Se o arquivo não aparecer no modo de exibição de árvore, clique em **procurar** e localize-o. Clique em **Próximo**.

     A caixa de diálogo **escolher configurações para importar** é exibida.

16. Verifique se **minhas configurações** está selecionada e clique em **concluir**. Quando a página **importação concluída** for exibida, clique em **fechar**.

17. No menu **ferramentas** , clique em **Opções**, expanda **minha categoria**, clique em **minha página de grade** e verifique se os valores da categoria de propriedade foram restaurados.
