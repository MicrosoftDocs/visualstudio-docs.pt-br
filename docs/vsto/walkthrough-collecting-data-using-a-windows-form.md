---
title: 'Walkthrough: coletar dados usando um formulário do Windows'
description: Abra um formulário do Windows de uma personalização em nível de documento para o Microsoft Excel, colete informações do usuário e grave essas informações em uma célula de planilha.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], Windows Forms
- Windows Forms [Office development in Visual Studio], collecting data
- forms [Office development in Visual Studio], walkthroughs
- worksheets [Office development in Visual Studio], collecting data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 62a49919522c5d4a88b6f4b6876b567c8d275dec
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826415"
---
# <a name="walkthrough-collect-data-by-using-a-windows-form"></a>Walkthrough: coletar dados usando um formulário do Windows
  Este tutorial demonstra como abrir um formulário do Windows de uma personalização em nível de documento para Microsoft Office Excel, coletar informações do usuário e gravar essas informações em uma célula de planilha.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Embora este passo a passos use um projeto de nível de documento para o Excel especificamente, os conceitos demonstrados pelo passo a passos são aplicáveis a outros projetos do Office.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="create-a-new-project"></a>Criar um novo projeto
 A primeira etapa é criar um projeto de pasta de trabalho do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **WinFormInput** e selecione **criar um novo documento** no assistente. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto **WinFormInput** ao **Gerenciador de soluções**.

## <a name="add-a-namedrange-control-to-the-worksheet"></a>Adicionar um controle NamedRange à planilha

### <a name="to-add-a-named-range-to-sheet1"></a>Para adicionar um intervalo nomeado a Sheet1

1. Selecione a célula **a1** em `Sheet1` .

2. Na caixa **nome** , digite **formInput**.

     A caixa **nome** está localizada à esquerda da barra de fórmulas, logo acima da **coluna a** da planilha.

3. Pressione **Enter**.

     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é adicionado à célula **a1**. Não há nenhuma indicação visível na planilha, mas **formInput** aparece na caixa **nome** (logo acima da planilha no lado esquerdo) e na janela **Propriedades** quando a célula **a1** é selecionada.

## <a name="add-a-windows-form-to-the-project"></a>Adicionar um formulário do Windows ao projeto
 Crie um formulário do Windows para solicitar informações ao usuário.

### <a name="to-add-a-windows-form"></a>Para adicionar um formulário do Windows

1. Selecione o projeto **WinFormInput** em **Gerenciador de soluções**.

2. No menu **projeto** , clique em **Adicionar Windows Form**.

3. Nomeie o formulário **GetInputString. vb** ou **GetInputString. cs** e clique em **Adicionar**.

    O novo formulário é aberto no designer.

4. Adicione um <xref:System.Windows.Forms.TextBox> e um <xref:System.Windows.Forms.Button> ao formulário.

5. Selecione o botão, localize o **texto** da propriedade na janela **Propriedades** e altere o texto para **OK**.

   Em seguida, adicione código para `ThisWorkbook.vb` ou `ThisWorkbook.cs` colete as informações do usuário.

## <a name="display-the-windows-form-and-collecting-information"></a>Exibir o formulário do Windows e coletar informações
 Crie uma instância do `GetInputString` Windows Form e exiba-a e, em seguida, grave as informações do usuário em uma célula da planilha.

#### <a name="to-display-the-form-and-collect-information"></a>Para exibir o formulário e coletar informações

1. Clique com o botão direito do mouse em **ThisWorkbook. vb** ou **ThisWorkbook. cs** em **Gerenciador de soluções** e clique em **Exibir código**.

2. No <xref:Microsoft.Office.Tools.Excel.Workbook.Open> manipulador de eventos do `ThisWorkbook` , adicione o código a seguir para declarar uma variável para o formulário `GetInputString` e, em seguida, mostrar o formulário.

   > [!NOTE]
   > No C#, você deve adicionar um manipulador de eventos, conforme mostrado no <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> evento abaixo. Para obter informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

    :::code language="csharp" source="../vsto/codesnippet/CSharp/WinFormInputCS/ThisWorkbook.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/WinFormInput/ThisWorkbook.vb" id="Snippet1":::

3. Crie um método chamado `WriteStringToCell` que grava o texto em um intervalo nomeado. Esse método é chamado no formulário, e a entrada do usuário é passada para o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle, `formInput` , na célula **a1**.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/WinFormInputCS/ThisWorkbook.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/WinFormInput/ThisWorkbook.vb" id="Snippet2":::

   Em seguida, adicione o código ao formulário para manipular o evento de clique do botão.

## <a name="send-information-to-the-worksheet"></a>Enviar informações para a planilha

### <a name="to-send-information-to-the-worksheet"></a>Para enviar informações para a planilha

1. Clique com o botão direito do mouse em **GetInputString** em **Gerenciador de soluções** e, em seguida, clique em **Designer de exibição**.

2. Clique duas vezes no botão para abrir o arquivo de código com o manipulador de eventos do botão <xref:System.Windows.Forms.Control.Click> adicionado.

3. Adicione código ao manipulador de eventos para obter a entrada da caixa de texto, enviá-la para a função `WriteStringToCell` e, em seguida, feche o formulário.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/WinFormInputCS/GetInputString.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/WinFormInput/GetInputString.vb" id="Snippet3":::

## <a name="test"></a>Teste
 Agora você pode executar o projeto. O formulário do Windows é exibido e sua entrada é exibida na planilha.

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para executar o projeto.

2. Confirme se o formulário do Windows é exibido.

3. Digite **Olá, mundo** na caixa de texto e clique em **OK**.

4. Confirme se **Olá, mundo** aparece na célula **a1** da planilha.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de mostrar um formulário do Windows e passar dados para uma planilha. Outras tarefas que você talvez queira executar incluem:

- Use Windows Forms controles em uma pasta de trabalho do Excel ou em um documento do Word. Para obter mais informações, consulte [visão geral dos controles de Windows Forms em documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md).

- Modifique a interface do usuário de um aplicativo Microsoft Office de uma personalização no nível do documento ou um suplemento do VSTO. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Passo a passos usando o Word](../vsto/walkthroughs-using-word.md)
- [Passo a passos usando o Excel](../vsto/walkthroughs-using-excel.md)
