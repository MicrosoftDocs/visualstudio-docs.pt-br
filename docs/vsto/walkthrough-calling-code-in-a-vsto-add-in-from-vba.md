---
title: 'Passo a passo: Chamar o código em um suplemento do VSTO do VBA'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9e46cf9032cae7d6400822be7d72394a7845314f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843815"
---
# <a name="walkthrough-call-code-in-a-vsto-add-in-from-vba"></a>Passo a passo: Chamar o código em um suplemento do VSTO do VBA
  Este passo a passo demonstra como expor um objeto em um suplemento do VSTO para outras soluções do Microsoft Office, incluindo o Visual Basic for Applications (VBA) e COM VSTO Add-ins.  
  
 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
 Embora este passo a passo usa o Excel especificamente, os conceitos demonstrados pelo passo a passo são aplicáveis a qualquer modelo de projeto do suplemento do VSTO fornecido pelo Visual Studio.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Definindo uma classe que pode ser exposta para outras soluções do Office.  
  
- Expondo a classe a outras soluções do Office.  
  
- Chamar um método da classe de código do VBA.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Excel  
  
## <a name="create-the-vsto-add-in-project"></a>Criar o projeto de suplemento do VSTO  
 A primeira etapa é criar um projeto de suplemento do VSTO para Excel.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de suplemento do VSTO do Excel com o nome **ExcelImportData**, usando o modelo de projeto do suplemento do VSTO do Excel. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **ThisAddIn.cs** ou **ThisAddIn. vb** arquivo de código e adiciona os **ExcelImportData** projeto ao **Gerenciador de soluções**.  
  
## <a name="define-a-class-that-you-can-expose-to-other-office-solutions"></a>Defina uma classe que você pode expor para outras soluções do Office  
 A finalidade deste passo a passo é chamar o `ImportData` método de uma classe chamada `AddInUtilities` no seu suplemento do VSTO do código do VBA. Esse método grava uma cadeia de caracteres na célula A1 da planilha ativa.  
  
 Para expor o `AddInUtilities` classe a outras soluções do Office, você deve tornar a classe pública e visível para COM. Você também deve expor as [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface na classe. O código no procedimento a seguir demonstra uma maneira de atender a esses requisitos. Para obter mais informações, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).  
  
### <a name="to-define-a-class-that-you-can-expose-to-other-office-solutions"></a>Para definir uma classe que você pode expor para outras soluções do Office  
  
1.  Sobre o **Project** menu, clique em **Adicionar classe**.  
  
2.  No **Adicionar Novo Item** diálogo caixa, altere o nome da nova classe para **AddInUtilities**e clique em **adicionar**.  
  
     O **AddInUtilities.cs** ou **AddInUtilities.vb** arquivo é aberto no Editor de códigos.  
  
3.  Adicione as seguintes instruções à parte superior do arquivo.  
  
     [!code-csharp[Trin_AddInInteropWalkthrough#2](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#2)]
     [!code-vb[Trin_AddInInteropWalkthrough#2](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#2)]  
  
4.  Substitua o `AddInUtilities` classe pelo código a seguir.  
  
     [!code-csharp[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#3)]
     [!code-vb[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#3)]  
  
     Este código faz o `AddInUtilities` classe visível para COM, e adiciona o `ImportData` método à classe. Para expor os [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface, o `AddInUtilities` classe também tem o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo e implementa uma interface que é visível para COM.  
  
## <a name="expose-the-class-to-other-office-solutions"></a>Expor a classe a outras soluções do Office  
 Para expor os `AddInUtilities` da classe a outras soluções do Office, substituir o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método no `ThisAddIn` classe. Em sua substituição, retornar uma instância do `AddInUtilities` classe.  
  
### <a name="to-expose-the-addinutilities-class-to-other-office-solutions"></a>Para expor a classe AddInUtilities para outras soluções do Office  
  
1.  Na **Gerenciador de soluções**, expanda **Excel**.  
  
2.  Clique com botão direito **ThisAddIn.cs** ou **ThisAddIn. vb**e, em seguida, clique em **Exibir código**.  
  
3.  Adicione o seguinte código para o `ThisAddIn` classe.  
  
     [!code-csharp[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs#1)]
     [!code-vb[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb#1)]  
  
4.  No menu **Compilar**, clique em **Compilar Solução**.  
  
     Verifique se a solução é compilada sem erros.  
  
## <a name="test-the-vsto-add-in"></a>Testar o suplemento do VSTO  
 Você pode chamar o `AddInUtilities` classe a partir de vários tipos diferentes de soluções do Office. Este passo a passo, você usará o código VBA em uma pasta de trabalho do Excel. Para obter mais informações sobre os outros tipos de soluções do Office você também pode usar, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).  
  
### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  No Excel, salve a pasta de trabalho ativa como uma pasta de trabalho (*. xlsm). Salve-o em um local conveniente, como a área de trabalho.  
  
3.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
4.  No **código** , clique em **Visual Basic**.  
  
     Abre o Editor do Visual Basic.  
  
5.  No **Project** janela, clique duas vezes em **ThisWorkbook**.  
  
     O arquivo de código para o `ThisWorkbook` do objeto é aberta.  
  
6.  Adicione o seguinte código do VBA para o arquivo de código. Esse código primeiro obtém um objeto COMAddIn que representa o **ExcelImportData** do suplemento do VSTO. Em seguida, o código usa a propriedade do objeto do objeto COMAddIn para chamar o `ImportData` método.  
  
    ```vb  
    Sub CallVSTOMethod()  
        Dim addIn As COMAddIn  
        Dim automationObject As Object  
        Set addIn = Application.COMAddIns("ExcelImportData")  
        Set automationObject = addIn.Object  
        automationObject.ImportData  
    End Sub  
    ```  
  
7.  Pressione **F5**.  
  
8.  Verificar se um novo **importado dados** folha foi adicionada à pasta de trabalho. Também verifique se essa célula A1 contém a cadeia de caracteres **esse é meu dados**.  
  
9. Saia do Excel.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre programação VSTO Add-ins com estes tópicos:  
  
-   Use o `ThisAddIn` classe para automatizar o aplicativo host e executar outras tarefas em projetos de suplemento do VSTO. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
-   Crie um painel de tarefas personalizado em um suplemento do VSTO. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md) e [como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md).  
  
-   Personalize a faixa de opções em um suplemento do VSTO. Para obter mais informações, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md) e [como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md).  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Personalizar os recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)  
  
  