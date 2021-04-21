---
title: Criar sua primeira personalização em nível de documento para o Excel
description: Crie uma personalização em nível de documento para o Microsoft Excel. Os recursos que você cria nesse tipo de solução estão disponíveis somente quando uma pasta de trabalho específica está aberta.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Excel [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9254aa5fd465c14e24133df59bbcee46f3c1acf4
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826896"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-excel"></a>Walkthrough: criar sua primeira personalização em nível de documento para o Excel

  Este guia introdutório mostra como criar uma personalização em nível de documento para Microsoft Office Excel. Os recursos que você cria nesse tipo de solução estão disponíveis somente quando uma pasta de trabalho específica está aberta. Você não pode usar uma personalização em nível de documento para fazer alterações em todo o aplicativo, por exemplo, exibindo uma nova guia da faixa de bits quando qualquer pasta de trabalho estiver aberta.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de pasta de trabalho do Excel.

- Adicionar texto a uma planilha hospedada no Visual Studio Designer.

- Escrever código que usa o modelo de objeto do Excel para adicionar texto à planilha personalizada quando ela é aberta.

- Compilando e executando o projeto para testá-lo.

- Limpando o projeto concluído para remover os arquivos de compilação desnecessários e as configurações de segurança do seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-excel-workbook-project-in-visual-studio"></a>Para criar um novo projeto de pasta de trabalho do Excel no Visual Studio

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.
::: moniker range="vs-2017"
3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do VSTO** .

5. Na lista de modelos de projeto, escolha um projeto de pasta de trabalho do VSTO do Excel.

6. Na caixa **nome** , digite **FirstWorkbookCustomization**.

7. Clique em **OK**.

8. Selecione **criar um novo documento** no **Assistente do ferramentas do Visual Studio para Office Project** e clique em **OK**.
::: moniker-end
::: moniker range=">=vs-2019"
3. Na caixa de diálogo **criar um novo projeto** , selecione o projeto de **pasta de trabalho do VSTO do Excel** .

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. Clique em **Próximo**.

5. Digite **FirstWorkbookCustomization** na caixa **nome** do diálogo **configurar seu novo projeto** e clique em **criar**.

6. Selecione **criar um novo documento** no **Assistente do ferramentas do Visual Studio para Office Project** e clique em **OK**.
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstWorkbookCustomization** e adiciona os arquivos a seguir ao projeto.

   - *FirstWorkbookCustomization*. xlsx – representa a pasta de trabalho do Excel no projeto. Contém todas as planilhas e gráficos.

   - Plan1 (arquivo *. vb* para Visual Basic ou arquivo *. cs* para Visual C#) – uma planilha que fornece a superfície de design e o código para a primeira planilha na pasta de trabalho. Para obter mais informações, consulte [planilha de item de host](../vsto/worksheet-host-item.md).

   - Planilha2 (arquivo *. vb* para Visual Basic ou arquivo *. cs* para Visual C#) – uma planilha que fornece a superfície de design e o código para a segunda planilha na pasta de trabalho.

   - Sheet3 (arquivo *. vb* para Visual Basic ou arquivo *. cs* para Visual C#) – uma planilha que fornece a superfície de design e o código para a terceira planilha na pasta de trabalho.

   - ThisWorkbook (arquivo *. vb* para Visual Basic ou arquivo *. cs* para Visual C#) – contém a superfície de design e o código para personalizações em nível de pasta de trabalho. Para obter mais informações, veja [item de host da pasta de trabalho](../vsto/workbook-host-item.md).

     O arquivo de código Plan1 é aberto automaticamente no designer.

## <a name="close-and-reopen-worksheets-in-the-designer"></a>Fechar e reabrir planilhas no designer

 Se você fechar deliberadamente ou acidentalmente uma pasta de trabalho ou uma planilha no designer enquanto estiver desenvolvendo seu projeto, você poderá reabri-la.

### <a name="to-close-and-reopen-a-worksheet-in-the-designer"></a>Para fechar e reabrir uma planilha no designer

1. Feche a pasta de trabalho clicando no botão **fechar** (X) para a janela do designer.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo de código **Plan1** e clique em **Designer de exibição**.

     \- ou –

     Em **Gerenciador de soluções**, clique duas vezes no arquivo de código **Plan1** .

## <a name="add-text-to-a-worksheet-in-the-designer"></a>Adicionar texto a uma planilha no designer

 Você pode criar a interface do usuário da sua personalização modificando a planilha que está aberta no designer. Por exemplo, você pode adicionar texto a células, aplicar fórmulas ou adicionar controles do Excel. Para obter mais informações sobre como usar o designer, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md).

### <a name="to-add-text-to-a-worksheet-by-using-the-designer"></a>Para adicionar texto a uma planilha usando o designer

1. Na planilha que está aberta no designer, selecione a célula **a1** e digite o texto a seguir.

     **Esse texto foi adicionado usando o designer.**

> [!WARNING]
> Se você adicionar essa linha de texto à célula **a2**, ela será substituída por outro código neste exemplo.

## <a name="add-text-to-a-worksheet-programmatically"></a>Adicionar texto a uma planilha programaticamente

 Em seguida, adicione o código ao arquivo de código Plan1. O novo código usa o modelo de objeto do Excel para adicionar uma segunda linha de texto à pasta de trabalho. Por padrão, o arquivo de código Plan1 contém o seguinte código gerado:

- Uma definição parcial da `Sheet1` classe, que representa o modelo de programação da planilha e fornece acesso ao modelo de objeto do Excel. Para obter mais informações, [item de host de planilha](../vsto/worksheet-host-item.md) e [visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md). O restante da `Sheet1` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `Sheet1_Startup` `Sheet1_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o Excel carrega e descarrega sua personalização. Use esses manipuladores de eventos para inicializar sua personalização quando ele for carregado e para limpar os recursos usados pela sua personalização quando ele for descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-a-second-line-of-text-to-the-worksheet-by-using-code"></a>Para adicionar uma segunda linha de texto à planilha usando código

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **Plan1** e clique em **Exibir código**.

     O arquivo de código é aberto no Visual Studio.

2. Substitua o `Sheet1_Startup` manipulador de eventos pelo código a seguir. Quando Plan1 é aberto, esse código adiciona uma segunda linha de texto à planilha.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelWorkbookTutorial/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelWorkbookTutorial/Sheet1.vb" id="Snippet1":::

## <a name="test-the-project"></a>Testar o projeto

### <a name="to-test-your-workbook"></a>Para testar sua pasta de trabalho

1. Pressione **F5** para compilar e executar o projeto.

     Quando você cria o projeto, o código é compilado em um assembly associado à pasta de trabalho. O Visual Studio coloca uma cópia da pasta de trabalho e o assembly na pasta de saída da compilação para o projeto e define as configurações de segurança no computador de desenvolvimento para permitir que a personalização seja executada. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

2. Na pasta de trabalho, verifique se você vê o texto a seguir.

     **Esse texto foi adicionado usando o designer.**

     **Esse texto foi adicionado usando código.**

3. Feche a pasta de trabalho.

## <a name="clean-up-the-project"></a>Limpar o projeto

 Ao concluir o desenvolvimento de um projeto, você deve remover os arquivos na pasta de saída da compilação e as configurações de segurança criadas pelo processo de compilação.

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>Para limpar o projeto concluído em seu computador de desenvolvimento

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas

 Agora que você criou uma personalização básica no nível do documento para o Excel, você pode aprender mais sobre como desenvolver personalizações a partir destes tópicos:

- Tarefas gerais de programação que você pode executar em personalizações em nível de documento: [programa personalizações em nível de documento](../vsto/programming-document-level-customizations.md).

- Tarefas de programação específicas para personalizações em nível de documento para Excel: [soluções do Excel](../vsto/excel-solutions.md).

- Usando o modelo de objeto do Excel: [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).

- Personalizando a interface do usuário do Excel, por exemplo, adicionando uma guia personalizada à faixa de faixas ou criando seu próprio painel de ações: [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

- Usando objetos estendidos do Excel fornecidos pelas ferramentas de desenvolvimento do Office no Visual Studio para executar tarefas que não são possíveis com o uso do modelo de objeto do Excel (por exemplo, Hospedagem de controles gerenciados em documentos e Associação de controles do Excel a dados usando o modelo de associação de dados Windows Forms): [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md).

- Criando e Depurando personalizações em nível de documento para o Excel: [crie soluções do Office](../vsto/building-office-solutions.md).

- Implantando personalizações em nível de documento para [o Excel: implante uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também

- [Visão geral do desenvolvimento de soluções do Office &#40;&#41;VSTO ](../vsto/office-solutions-development-overview-vsto.md)
- [Soluções do Excel](../vsto/excel-solutions.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
