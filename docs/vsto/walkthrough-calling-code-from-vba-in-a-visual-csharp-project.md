---
title: 'Walkthrough: chamar código do VBA em um projeto do Visual C#'
description: Saiba como chamar um método em uma personalização em nível de documento para o Microsoft Excel do código Visual Basic for Applications (VBA) na pasta de trabalho.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 260872096f36f91a2618f636e297d3c48b3fe51b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824465"
---
# <a name="walkthrough-call-code-from-vba-in-a-visual-c-project"></a>Walkthrough: chamar código do VBA em um projeto do Visual C#
  Este tutorial demonstra como chamar um método em uma personalização em nível de documento para Microsoft Office o Excel do código Visual Basic for Applications (VBA) na pasta de trabalho. O procedimento envolve três etapas básicas: adicionar um método à `Sheet1` classe de item de host, expor o método ao código VBA na pasta de trabalho e, em seguida, chamar o método do código VBA na pasta de trabalho.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Embora este passo a passos use o Excel especificamente, os conceitos demonstrados pelo passo a passos também são aplicáveis a projetos de nível de documento para o Word.

 Este passo a passo ilustra as seguintes tarefas:

- Criar uma pasta de trabalho que contém código VBA.

- Confiar no local da pasta de trabalho usando a central de confiabilidade no Excel.

- Adicionando um método à `Sheet1` classe de item de host.

- Extraindo uma interface para a `Sheet1` classe de item de host.

- Expondo o método ao código VBA.

- Chamar o método do código VBA.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-a-workbook-that-contains-vba-code"></a>Criar uma pasta de trabalho que contém código VBA
 A primeira etapa é criar uma pasta de trabalho habilitada para macro que contenha uma macro simples do VBA. Antes que você possa expor código em uma personalização para o VBA, a pasta de trabalho já deve conter código VBA. Caso contrário, o Visual Studio não pode modificar o projeto do VBA para habilitar o código VBA para chamar o assembly de personalização.

 Se você já tiver uma pasta de trabalho que contenha código VBA que deseja usar, ignore esta etapa.

### <a name="to-create-a-workbook-that-contains-vba-code"></a>Para criar uma pasta de trabalho que contém código VBA

1. Inicie o Excel.

2. Salve o documento ativo como uma **pasta de trabalho do Excel Macro-Enabled ( \* . xlsm)** com o nome **WorkbookWithVBA**. Salve-o em um local conveniente, como o desktop.

3. Na faixa de faixas, clique na guia **desenvolvedor** .

    > [!NOTE]
    > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

4. No grupo de **códigos** , clique em **Visual Basic**.

     O Editor do Visual Basic é aberto.

5. Na janela do **projeto** , clique duas vezes em **ThisWorkbook**.

     O arquivo de código para o `ThisWorkbook` objeto é aberto.

6. Adicione o código VBA a seguir ao arquivo de código. Esse código define uma função simples que não faz nada. A única finalidade dessa função é garantir que exista um projeto do VBA na pasta de trabalho. Isso é necessário para etapas posteriores neste passo a passos.

    ```vb
    Sub EmptySub()
    End Sub
    ```

7. Salve o documento e saia do Excel.

## <a name="create-the-project"></a>Criar o projeto
 Agora você pode criar um projeto de nível de documento para o Excel que usa a pasta de trabalho habilitada para macro criada anteriormente.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** e, em seguida, expanda **Office/SharePoint**.

4. Selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, selecione a **pasta de trabalho do excel 2010** ou o projeto de **pasta de trabalho do Excel 2013** .

6. Na caixa **nome** , digite **CallingCodeFromVBA**.

7. Clique em **OK**.

     O **Assistente de ferramentas do Visual Studio para o Office Project** é aberto.

8. Selecione **copiar um documento existente** e, na caixa **caminho completo do documento existente** , especifique o local da pasta de trabalho **WorkbookWithVBA** que você criou anteriormente. Se você estiver usando sua própria pasta de trabalho habilitada para macro, especifique o local dessa pasta de trabalho.

9. Clique em **Concluir**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre a pasta de trabalho **WorkbookWithVBA** no designer e adiciona o projeto **CallingCodeFromVBA** ao **Gerenciador de soluções**.

## <a name="trust-the-location-of-the-workbook"></a>Confiar no local da pasta de trabalho
 Antes de expor o código em sua solução para o código VBA na pasta de trabalho, você deve confiar no VBA na pasta de trabalho a ser executada. Há várias maneiras de fazer isso. Neste tutorial, você executará essa tarefa confiando no local da pasta de trabalho na central de **confiabilidade** no Excel.

### <a name="to-trust-the-location-of-the-workbook"></a>Para confiar no local da pasta de trabalho

1. Inicie o Excel.

2. Clique na guia **arquivo** .

3. Clique no botão **Opções do Excel** .

4. No painel categorias, clique em **central de confiabilidade**.

5. No painel de detalhes, clique em **configurações da central de confiabilidade**.

6. No painel categorias, clique em **locais confiáveis**.

7. No painel de detalhes, clique em **Adicionar novo local**.

8. Na caixa de diálogo **Microsoft Office local confiável** , navegue até a pasta que contém o projeto **CallingCodeFromVBA** .

9. Selecione as **subpastas deste local também são confiáveis**.

10. Na caixa de diálogo **Microsoft Office local confiável** , clique em **OK**.

11. Na caixa de diálogo **central de confiabilidade** , clique em **OK**.

12. Na caixa de diálogo **Opções do Excel** , clique em **OK**.

13. Saia do **Excel**.

## <a name="add-a-method-to-the-sheet1-class"></a>Adicionar um método à classe Plan1
 Agora que o projeto do VBA está configurado, adicione um método público à `Sheet1` classe de item de host que você pode chamar a partir do código VBA.

### <a name="to-add-a-method-to-the-sheet1-class"></a>Para adicionar um método à classe Plan1

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1. cs** e clique em **Exibir código**.

     O arquivo **Plan1. cs** é aberto no editor de código.

2. Adicione o código a seguir à classe `Sheet1` . O `CreateVstoNamedRange` método cria um novo <xref:Microsoft.Office.Tools.Excel.NamedRange> objeto no intervalo especificado. Esse método também cria um manipulador de eventos para o <xref:Microsoft.Office.Tools.Excel.NamedRange.Selected> evento do <xref:Microsoft.Office.Tools.Excel.NamedRange> . Mais adiante neste tutorial, você chamará o `CreateVstoNamedRange` método do código VBA no documento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet2":::

3. Adicione o método a seguir à classe `Sheet1`. Esse método substitui o <xref:Microsoft.Office.Tools.Excel.WorksheetBase.GetAutomationObject%2A> método para retornar a instância atual da `Sheet1` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet3":::

4. Aplique os atributos a seguir antes da primeira linha da `Sheet1` declaração de classe. Esses atributos tornam a classe visível para COM, mas sem gerar uma interface de classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/Sheet1.cs" id="Snippet1":::

## <a name="extract-an-interface-for-the-sheet1-class"></a>Extrair uma interface para a classe Plan1
 Antes de expor o `CreateVstoNamedRange` método ao código VBA, você deve criar uma interface pública que defina esse método, e você deve expor essa interface para com.

### <a name="to-extract-an-interface-for-the-sheet1-class"></a>Para extrair uma interface para a classe Plan1

1. No arquivo de código **Plan1. cs** , clique em qualquer lugar na `Sheet1` classe.

2. No menu **refatorar** , clique em **extrair interface**.

3. Na caixa de diálogo **extrair interface** , na caixa **selecionar interface de membros públicos para formulário** , clique na entrada do `CreateVstoNamedRange` método.

4. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] gera uma nova interface chamada `ISheet1` e modifica a definição da `Sheet1` classe para que ela implemente a `ISheet1` interface. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] também abre o arquivo **ISheet1. cs** no editor de código.

5. No arquivo **ISheet1. cs** , substitua a `ISheet1` declaração de interface pelo código a seguir. Esse código torna a `ISheet1` interface pública e aplica o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo para tornar a interface visível para com.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/CallingCodeFromVBA/ISheet1.cs" id="Snippet4":::

6. Compile o projeto.

## <a name="expose-the-method-to-vba-code"></a>Expor o método ao código VBA
 Para expor o `CreateVstoNamedRange` método ao código VBA na pasta de trabalho, defina a propriedade **ReferenceAssemblyFromVbaProject** para o `Sheet1` item de host como **true**.

### <a name="to-expose-the-method-to-vba-code"></a>Para expor o método ao código VBA

1. Em **Gerenciador de soluções**, clique duas vezes em **Plan1. cs**.

     O arquivo **WorkbookWithVBA** é aberto no designer, com Sheet1 visível.

2. Na janela **Propriedades** , selecione a propriedade **ReferenceAssemblyFromVbaProject** e altere o valor para **true**.

3. Clique em **OK** na mensagem que é exibida.

4. Compile o projeto.

## <a name="call-the-method-from-vba-code"></a>Chamar o método do código VBA
 Agora você pode chamar o `CreateVstoNamedRange` método do código VBA na pasta de trabalho.

> [!NOTE]
> Neste tutorial, você adicionará código VBA à pasta de trabalho durante a depuração do projeto. O código VBA que você adicionar a este documento será substituído na próxima vez que você compilar o projeto, pois o Visual Studio substitui o documento na pasta de saída da compilação por uma cópia do documento da pasta principal do projeto. Se você quiser salvar o código VBA, poderá copiá-lo para o documento na pasta do projeto. Para obter mais informações, consulte [combinar VBA e personalizações em nível de documento](../vsto/combining-vba-and-document-level-customizations.md).

### <a name="to-call-the-method-from-vba-code"></a>Para chamar o método do código VBA

1. Pressione **F5** para executar o projeto.

2. Na guia **desenvolvedor** , no grupo **código** , clique em **Visual Basic**.

     O Editor do Visual Basic é aberto.

3. No menu **Inserir** , clique em **módulo**.

4. Adicione o código a seguir ao novo módulo.

     Esse código chama o `CreateTable` método no assembly de personalização. A macro acessa esse método usando o `GetManagedClass` método global para acessar a classe de `Sheet1` item de host que você expôs ao código VBA. O `GetManagedClass` método foi gerado automaticamente quando você define a propriedade **ReferenceAssemblyFromVbaProject** anteriormente neste passo a passos.

    ```vb
    Sub CallVSTOMethod()
        Dim VSTOSheet1 As CallingCodeFromVBA.Sheet1
        Set VSTOSheet1 = GetManagedClass(Sheet1)
        Call VSTOSheet1.CreateVstoNamedRange(Sheet1.Range("A1"), "VstoNamedRange")
    End Sub
    ```

5. Pressione **F5**.

6. Na pasta de trabalho aberta, clique na célula **a1** em **Sheet1**. Verifique se a caixa de mensagem é exibida.

7. Saia do Excel sem salvar as alterações.

## <a name="next-steps"></a>Próximas etapas
 Você pode saber mais sobre como chamar código em soluções do Office do VBA nestes tópicos:

- Chame o código em um item de host em uma Visual Basic personalização do VBA. Esse processo é diferente do processo do Visual C#. Para obter mais informações, consulte [Walkthrough: chamar código do VBA em um projeto Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md).

- Chame o código em um suplemento do VSTO do VBA. Para obter mais informações, consulte [Walkthrough: chamar código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).

## <a name="see-also"></a>Consulte também
- [Combine personalizações do VBA e no nível do documento](../vsto/combining-vba-and-document-level-customizations.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Como: expor código ao VBA em um projeto Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
- [Como: expor código ao VBA em um projeto do Visual C&#35;](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
- [Walkthrough: chamar o código do VBA em um projeto Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
