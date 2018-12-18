---
title: 'Passo a passo: Chamar o código do VBA em um projeto do Visual c#'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], calling code from VBA
- Word [Office development in Visual Studio], calling code from VBA
- Visual C# [Office development in Visual Studio], calling code from VBA
- workbooks [Office development in Visual Studio], calling code from VBA
- VBA [Office development in Visual Studio], calling code in document-level customizations
- Office documents [Office development in Visual Studio, Visual Basic for Applications and
- calling code from VBA
- document-level customizations [Office development in Visual Studio], calling code
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e2803ef31ec1009215d4490ac527c42cbdc90571
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38781683"
---
# <a name="walkthrough-call-code-from-vba-in-a-visual-c-project"></a>Passo a passo: Chamar o código do VBA em um projeto do Visual c#
  Este passo a passo demonstra como chamar um método em uma personalização no nível de documento do Microsoft Office Excel no Visual Basic para código Applications (VBA) na pasta de trabalho. O procedimento envolve três etapas básicas: adicionar um método para o `Sheet1` classe de item de host, expõem o método ao código VBA na pasta de trabalho e, em seguida, chame o método do código VBA na pasta de trabalho.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Embora este passo a passo usa o Excel especificamente, os conceitos demonstrados pelo passo a passo se aplicam a projetos no nível de documento para Word.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Criando uma pasta de trabalho que contém o código do VBA.  
  
-   Confiando o local da pasta de trabalho usando a Central de confiabilidade no Excel.  
  
-   Adicionando um método para o `Sheet1` classe de item de host.  
  
-   Extrair uma interface para o `Sheet1` classe de item de host.  
  
-   Expondo o método ao código VBA.  
  
-   Chamando o método do código do VBA.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Excel  
  
## <a name="create-a-workbook-that-contains-vba-code"></a>Criar uma pasta de trabalho que contenha código VBA  
 A primeira etapa é criar uma pasta de trabalho habilitada para macro que contém uma macro do VBA simples. Antes de você pode expor o código em uma personalização ao VBA, a pasta de trabalho já deve conter o código do VBA. Caso contrário, o Visual Studio não pode modificar o projeto do VBA para habilitar o código do VBA chamar o assembly de personalização.  
  
 Se você já tiver uma pasta de trabalho que contenha código VBA que você deseja usar, você pode ignorar esta etapa.  
  
### <a name="to-create-a-workbook-that-contains-vba-code"></a>Para criar uma pasta de trabalho que contenha código VBA  
  
1.  Inicie o Excel.  
  
2.  Salvar o documento ativo como uma **pasta de trabalho (\*. xlsm)** com o nome **WorkbookWithVBA**. Salve-o em um local conveniente, como a área de trabalho.  
  
3.  Na faixa de opções, clique no **desenvolvedor** guia.  
  
    > [!NOTE]  
    >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
4.  No **código** , clique em **Visual Basic**.  
  
     Abre o Editor do Visual Basic.  
  
5.  No **Project** janela, clique duas vezes em **ThisWorkbook**.  
  
     O arquivo de código para o `ThisWorkbook` do objeto é aberta.  
  
6.  Adicione o seguinte código do VBA para o arquivo de código. Esse código define uma função simples que não faz nada. A única finalidade dessa função é garantir a existência de um projeto do VBA na pasta de trabalho. Isso é necessário para etapas posteriores neste passo a passo.  
  
    ```vb  
    Sub EmptySub()  
    End Sub  
    ```  
  
7.  Salve o documento e saia do Excel.  
  
## <a name="create-the-project"></a>Criar o projeto  
 Agora você pode criar um projeto de nível de documento para Excel que usa a pasta de trabalho habilitada para macro criado anteriormente.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  No painel de modelos, expanda **Visual c#** e, em seguida, expanda **Office/SharePoint**.  
  
4.  Selecione o **suplementos do Office** nó.  
  
5.  Na lista de modelos de projeto, selecione a **pasta de trabalho do Excel 2010** ou **pasta de trabalho do Excel 2013** projeto.  
  
6.  No **nome** , digite **CallingCodeFromVBA**.  
  
7.  Clique em **OK**.  
  
     O **Visual Studio Tools for Office Project Wizard** é aberta.  
  
8.  Selecione **copiar um documento existente**e, na **caminho completo do documento existente** , especifique o local do **WorkbookWithVBA** pasta de trabalho que você criou anteriormente . Se você estiver usando sua própria pasta de trabalho habilitada para macro, especifique o local dessa pasta de trabalho em vez disso.  
  
9. Clique em **Finalizar**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **WorkbookWithVBA** pasta de trabalho no designer e adiciona os **CallingCodeFromVBA** projeto ao **Gerenciador de soluções**.  
  
## <a name="trust-the-location-of-the-workbook"></a>Confiar no local da pasta de trabalho  
 Antes de expor o código em sua solução ao código VBA na pasta de trabalho, você deve confiar em VBA na pasta de trabalho para ser executado. Há várias maneiras de fazer isso. Neste passo a passo, você irá realizar essa tarefa confiando o local da pasta de trabalho na **Central de confiabilidade** no Excel.  
  
### <a name="to-trust-the-location-of-the-workbook"></a>Para confiar no local da pasta de trabalho  
  
1.  Inicie o Excel.  
  
2.  Clique o **arquivo** guia.  
  
3.  Clique o **opções do Excel** botão.  
  
4.  No painel de categorias, clique em **Central de confiabilidade**.  
  
5.  No painel de detalhes, clique em **configurações da Central de confiabilidade**.  
  
6.  No painel de categorias, clique em **locais confiáveis**.  
  
7.  No painel de detalhes, clique em **adicionar novo local**.  
  
8.  No **local confiável do Microsoft Office** caixa de diálogo, navegue até a pasta que contém o **CallingCodeFromVBA** projeto.  
  
9. Selecione **as subpastas deste local também são confiáveis**.  
  
10. No **local confiável do Microsoft Office** caixa de diálogo, clique em **Okey**.  
  
11. No **Central de confiabilidade** caixa de diálogo, clique em **Okey**.  
  
12. No **opções do Excel** caixa de diálogo, clique em **Okey**.  
  
13. Exit **Excel**.  
  
## <a name="add-a-method-to-the-sheet1-class"></a>Adicione um método à classe Sheet1  
 Agora que o projeto do VBA é definido, adicione um método público para o `Sheet1` hospedar a classe do item que você pode chamar de código do VBA.  
  
### <a name="to-add-a-method-to-the-sheet1-class"></a>Para adicionar um método à classe Sheet1  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **Sheet1.cs**e, em seguida, clique em **Exibir código**.  
  
     O **Sheet1.cs** arquivo é aberto no Editor de códigos.  
  
2.  Adicione o seguinte código para o `Sheet1` classe. O `CreateVstoNamedRange` método cria um novo <xref:Microsoft.Office.Tools.Excel.NamedRange> objeto no intervalo especificado. Esse método cria um manipulador de eventos para o <xref:Microsoft.Office.Tools.Excel.NamedRange.Selected> eventos do <xref:Microsoft.Office.Tools.Excel.NamedRange>. Posteriormente neste passo a passo, você chamará o `CreateVstoNamedRange` método do código do VBA no documento.  
  
     [!code-csharp[Trin_CallingCSCustomizationFromVBA#2](../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs#2)]  
  
3.  Adicione o seguinte método à classe `Sheet1`. Esse método substitui o <xref:Microsoft.Office.Tools.Excel.Worksheet.GetAutomationObject%2A> método para retornar a instância atual do `Sheet1` classe.  
  
     [!code-csharp[Trin_CallingCSCustomizationFromVBA#3](../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs#3)]  
  
4.  Aplicar os atributos a seguir antes da primeira linha do `Sheet1` declaração de classe. Esses atributos torná-la visível para COM, mas sem gerar uma interface de classe.  
  
     [!code-csharp[Trin_CallingCSCustomizationFromVBA#1](../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs#1)]  
  
## <a name="extract-an-interface-for-the-sheet1-class"></a>Extrair uma interface para a classe Sheet1  
 Antes de você pode expor o `CreateVstoNamedRange` método ao código VBA, você deve criar uma interface pública que define esse método, e você deve expor essa interface a com.&lt;1}  
  
### <a name="to-extract-an-interface-for-the-sheet1-class"></a>Para extrair uma interface para a classe Sheet1  
  
1.  No **Sheet1.cs** arquivo de código, clique em qualquer lugar a `Sheet1` classe.  
  
2.  Sobre o **refatorar** menu, clique em **extrair Interface**.  
  
3.  No **extrair Interface** na caixa de **selecionar membros públicos para formar a interface** caixa, clique na entrada para o `CreateVstoNamedRange` método.  
  
4.  Clique em **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] gera uma nova interface chamada `ISheet1`, e ele modifica a definição do `Sheet1` classe para que ele implementa o `ISheet1` interface. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] também abre a **ISheet1.cs** arquivo no Editor de códigos.  
  
5.  No **ISheet1.cs** do arquivo, substitua o `ISheet1` declaração com o seguinte código de interface. Este código faz o `ISheet1` da interface pública, e isso se aplica a <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributos para tornar a interface visível para COM.  
  
     [!code-csharp[Trin_CallingCSCustomizationFromVBA#4](../vsto/codesnippet/CSharp/CallingCodeFromVBA/ISheet1.cs#4)]  
  
6.  Compile o projeto.  
  
## <a name="expose-the-method-to-vba-code"></a>Expor o método ao código VBA  
 Para expor os `CreateVstoNamedRange` método ao código VBA na pasta de trabalho, defina a **ReferenceAssemblyFromVbaProject** propriedade para o `Sheet1` item de host para **verdadeiro**.  
  
### <a name="to-expose-the-method-to-vba-code"></a>Para expor o método ao código VBA  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em **Sheet1.cs**.  
  
     O **WorkbookWithVBA** arquivo é aberto no designer, com Sheet1 visível.  
  
2.  No **propriedades** janela, selecione a **ReferenceAssemblyFromVbaProject** propriedade e altere o valor para **verdadeiro**.  
  
3.  Clique em **Okey** na mensagem que é exibida.  
  
4.  Compile o projeto.  
  
## <a name="call-the-method-from-vba-code"></a>Chame o método do código do VBA  
 Agora você pode chamar o `CreateVstoNamedRange` método do código VBA na pasta de trabalho.  
  
> [!NOTE]  
>  Neste passo a passo, você adicionará código VBA na pasta de trabalho durante a depuração do projeto. O código do VBA que você adicionar a este documento será substituído na próxima vez que você compila o projeto, porque o Visual Studio substitui o documento na pasta de saída de compilação com uma cópia do documento da pasta do projeto principal. Se você deseja salvar o código do VBA, você pode copiar no documento na pasta do projeto. Para obter mais informações, consulte [combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md).  
  
### <a name="to-call-the-method-from-vba-code"></a>Para chamar o método do código do VBA  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  No **desenvolvedor** guia, o **código** , clique em **Visual Basic**.  
  
     Abre o Editor do Visual Basic.  
  
3.  Sobre o **inserir** menu, clique em **módulo**.  
  
4.  Adicione o seguinte código para o novo módulo.  
  
     Esse código chama o `CreateTable` método no assembly de personalização. A macro acessa esse método por meio global `GetManagedClass` método para acessar o `Sheet1` hospedar a classe do item que é exposta ao código VBA. O `GetManagedClass` método foi gerado automaticamente quando você define o **ReferenceAssemblyFromVbaProject** propriedade no início deste passo a passo.  
  
    ```vb  
    Sub CallVSTOMethod()  
        Dim VSTOSheet1 As CallingCodeFromVBA.Sheet1  
        Set VSTOSheet1 = GetManagedClass(Sheet1)  
        Call VSTOSheet1.CreateVstoNamedRange(Sheet1.Range("A1"), "VstoNamedRange")  
    End Sub  
    ```  
  
5.  Pressione **F5**.  
  
6.  Na pasta de trabalho aberta, clique na célula **A1** nos **Sheet1**. Verifique se a caixa de mensagem aparece.  
  
7.  Saia do Excel sem salvar suas alterações.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como chamar o código em soluções do Office do VBA nestes tópicos:  
  
-   Chame o código em um item de host em uma personalização no Visual Basic do VBA. Esse processo é diferente do processo Visual c#. Para obter mais informações, consulte [instruções passo a passo: chamar o código do VBA em um projeto do Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md).  
  
-   Chame o código em um suplemento do VSTO do VBA. Para obter mais informações, consulte [instruções passo a passo: chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).  
  
## <a name="see-also"></a>Consulte também  
 [Combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Como: expor o código para VBA em um projeto do Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)   
 [Como: expor o código para VBA em um Visual C&#35; projeto](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)   
 [Passo a passo: Chamar o código do VBA em um projeto do Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)  
  