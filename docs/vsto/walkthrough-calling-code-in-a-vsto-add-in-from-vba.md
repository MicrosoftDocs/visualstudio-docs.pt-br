---
title: 'Walkthrough: chamar o código em um suplemento do VSTO do VBA'
description: Saiba como expor um objeto em um suplemento do VSTO a outras soluções de Microsoft Office, incluindo Visual Basic for Applications (VBA) e suplementos do VSTO COM.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- Video How tos, Office development in Visual Studio
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 21e0928396327911ea794c6270340c6efd27a43e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824595"
---
# <a name="walkthrough-call-code-in-a-vsto-add-in-from-vba"></a>Walkthrough: chamar o código em um suplemento do VSTO do VBA
  Este tutorial demonstra como expor um objeto em um suplemento do VSTO para outras soluções de Microsoft Office, incluindo Visual Basic for Applications (VBA) e suplementos do VSTO COM.

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 Embora este passo a passos use o Excel especificamente, os conceitos demonstrados por instruções são aplicáveis a qualquer modelo de projeto de suplemento do VSTO fornecido pelo Visual Studio.

 Este passo a passo ilustra as seguintes tarefas:

- Definição de uma classe que pode ser exposta a outras soluções do Office.

- Expondo a classe a outras soluções do Office.

- Chamar um método da classe a partir do código VBA.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-the-vsto-add-in-project"></a>Criar o projeto de suplemento do VSTO
 A primeira etapa é criar um projeto de suplemento do VSTO para o Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de suplemento do VSTO do Excel com o nome **ExcelImportData**, usando o modelo de projeto de suplemento do VSTO do Excel. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo de código **ThisAddIn. cs** ou **ThisAddIn. vb** e adiciona o projeto **ExcelImportData** ao **Gerenciador de soluções**.

## <a name="define-a-class-that-you-can-expose-to-other-office-solutions"></a>Definir uma classe que você pode expor a outras soluções do Office
 A finalidade deste passo a passos é chamar o `ImportData` método de uma classe chamada `AddInUtilities` em seu suplemento do VSTO do código do VBA. Esse método grava uma cadeia de caracteres na célula a1 da planilha ativa.

 Para expor a `AddInUtilities` classe a outras soluções do Office, você deve tornar a classe pública e visível para com. Você também deve expor a interface [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) na classe. O código no procedimento a seguir demonstra uma maneira de atender a esses requisitos. Para obter mais informações, consulte [chamando código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).

### <a name="to-define-a-class-that-you-can-expose-to-other-office-solutions"></a>Para definir uma classe que você pode expor a outras soluções do Office

1. No menu **projeto** , clique em **Adicionar classe**.

2. Na caixa de diálogo **Adicionar novo item** , altere o nome da nova classe para **AddInUtilities** e clique em **Adicionar**.

     O arquivo **AddInUtilities. cs** ou **AddInUtilities. vb** é aberto no editor de código.

3. Adicione as seguintes diretivas à parte superior do arquivo.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb" id="Snippet2":::

4. Substitua a `AddInUtilities` classe pelo código a seguir.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb" id="Snippet3":::

     Esse código torna a `AddInUtilities` classe visível para com e adiciona o `ImportData` método à classe. Para expor a interface [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) , a `AddInUtilities` classe também tem o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo e implementa uma interface que é visível para com.

## <a name="expose-the-class-to-other-office-solutions"></a>Expor a classe a outras soluções do Office
 Para expor a `AddInUtilities` classe a outras soluções do Office, substitua o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método na `ThisAddIn` classe. Em sua substituição, retorne uma instância da `AddInUtilities` classe.

### <a name="to-expose-the-addinutilities-class-to-other-office-solutions"></a>Para expor a classe AddInUtilities a outras soluções do Office

1. Em **Gerenciador de soluções**, expanda **Excel**.

2. Clique com o botão direito do mouse em **ThisAddIn. cs** ou em **ThisAddIn. vb** e clique em **Exibir código**.

3. Adicione o código a seguir à classe `ThisAddIn` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb" id="Snippet1":::

4. No menu **Compilar**, clique em **Compilar Solução**.

     Verifique se a solução é compilada sem erros.

## <a name="test-the-vsto-add-in"></a>Testar o suplemento do VSTO
 Você pode chamar a `AddInUtilities` classe de vários tipos diferentes de soluções do Office. Neste tutorial, você usará o código VBA em uma pasta de trabalho do Excel. Para obter mais informações sobre os outros tipos de soluções do Office que você também pode usar, consulte [chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).

### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5** para executar o projeto.

2. No Excel, salve a pasta de trabalho ativa como uma pasta de trabalho do Excel Macro-Enabled (*. xlsm). Salve-o em um local conveniente, como o desktop.

3. Na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

4. No grupo de **códigos** , clique em **Visual Basic**.

     O Editor do Visual Basic é aberto.

5. Na janela do **projeto** , clique duas vezes em **ThisWorkbook**.

     O arquivo de código para o `ThisWorkbook` objeto é aberto.

6. Adicione o código VBA a seguir ao arquivo de código. Esse código obtém primeiro um objeto COMAddIn que representa o suplemento do VSTO **ExcelImportData** . Em seguida, o código usa a propriedade Object do objeto COMAddIn para chamar o `ImportData` método.

    ```vb
    Sub CallVSTOMethod()
        Dim addIn As COMAddIn
        Dim automationObject As Object
        Set addIn = Application.COMAddIns("ExcelImportData")
        Set automationObject = addIn.Object
        automationObject.ImportData
    End Sub
    ```

7. Pressione **F5**.

8. Verifique se uma nova folha de **dados importada** foi adicionada à pasta de trabalho. Verifique também se a célula a1 contém a cadeia de caracteres que trata de **meus dados**.

9. Saia do Excel.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre a programação de suplementos do VSTO a partir destes tópicos:

- Use a `ThisAddIn` classe para automatizar o aplicativo host e executar outras tarefas em projetos de suplemento do VSTO. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

- Crie um painel de tarefas personalizado em um suplemento do VSTO. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md) e [como adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md).

- Personalize a faixa de bits em um suplemento do VSTO. Para obter mais informações, consulte [visão geral da faixa](../vsto/ribbon-overview.md) de e [como: introdução à personalização da faixa de faixas](../vsto/how-to-get-started-customizing-the-ribbon.md).

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Chamar código em suplementos do VSTO de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)
- [Personalizar recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
