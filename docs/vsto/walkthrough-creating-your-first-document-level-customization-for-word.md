---
title: Crie sua primeira personalização em nível de documento para o Word
description: Crie uma personalização em nível de documento para o Microsoft Word. Os recursos que você cria nesse tipo de solução estão disponíveis somente quando um documento específico está aberto.
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Word [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 71051c6255f9035079a7888fb3a4c7df2f5eab59
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827546"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-word"></a>Walkthrough: criar sua primeira personalização em nível de documento para o Word

  Este guia introdutório mostra como criar uma personalização em nível de documento para Microsoft Office Word. Os recursos que você cria nesse tipo de solução estão disponíveis somente quando um documento específico está aberto. Você não pode usar uma personalização em nível de documento para fazer alterações em todo o aplicativo, por exemplo, exibindo uma nova guia da faixa de bits quando qualquer documento está aberto.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de documento do Word.

- Adicionar texto ao documento hospedado no Visual Studio Designer.

- Escrever código que usa o modelo de objeto do Word para adicionar texto ao documento personalizado quando ele é aberto.

- Compilando e executando o projeto para testá-lo.

- Limpando o projeto para remover os arquivos de compilação desnecessários e as configurações de segurança do seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-word-document-project-in-visual-studio"></a>Para criar um novo projeto de documento do Word no Visual Studio

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.
::: moniker range="vs-2017"
3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do VSTO** .

5. Na lista de modelos de projeto, selecione um projeto de documento do Word VSTO.

6. Na caixa **nome** , digite **FirstDocumentCustomization**.

7. Clique em **OK**.

8. Selecione **criar um novo documento** no **Assistente do ferramentas do Visual Studio para Office Project** e clique em **OK**.
::: moniker-end
::: moniker range=">=vs-2019"
3. Na caixa de diálogo **criar um novo projeto** , selecione o projeto de **documento do Word VSTO** .

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. Clique em **Próximo**.

5. Digite **FirstWorkbookCustomization** na caixa **nome** do diálogo **configurar seu novo projeto** e clique em **criar**.

6. Selecione **criar um novo documento** no **Assistente do ferramentas do Visual Studio para Office Project** e clique em **OK**.
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstDocumentCustomization** e adiciona o documento **FirstDocumentCustomization** e o arquivo de código ThisDocument ao projeto. O documento **FirstDocumentCustomization** é aberto automaticamente no designer.

## <a name="close-and-reopen-the-document-in-the-designer"></a>Fechar e reabrir o documento no designer

 Se você fechar deliberadamente ou acidentalmente o documento no designer enquanto estiver desenvolvendo seu projeto, você poderá reabri-lo.

### <a name="to-close-and-reopen-the-document-in-the-designer"></a>Para fechar e reabrir o documento no designer

1. Feche o documento clicando no botão **fechar** (X) para a janela do designer.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo de código **ThisDocument** e clique em **Designer de exibição**.

     \- ou –

     Em **Gerenciador de soluções**, clique duas vezes no arquivo de código **ThisDocument** .

## <a name="add-text-to-the-document-in-the-designer"></a>Adicionar texto ao documento no designer

 Você pode criar a interface do usuário da sua personalização modificando o documento que está aberto no designer. Por exemplo, você pode adicionar texto, tabelas ou controles do Word. Para obter mais informações sobre como usar o designer, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md).

### <a name="to-add-text-to-your-document-by-using-the-designer"></a>Para adicionar texto ao documento usando o designer

1. No documento que está aberto no designer, digite o texto a seguir.

     **Esse texto foi adicionado usando o designer.**

## <a name="add-text-to-the-document-programmatically"></a>Adicionar texto ao documento programaticamente

 Em seguida, adicione o código ao arquivo de código ThisDocument. O novo código usa o modelo de objeto do Word para adicionar um segundo parágrafo de texto ao documento. Por padrão, o arquivo de código ThisDocument contém o seguinte código gerado:

- Uma definição parcial da `ThisDocument` classe, que representa o modelo de programação do documento e fornece acesso ao modelo de objeto do Word. Para obter mais informações, consulte [visão geral](../vsto/word-object-model-overview.md)de [item de host de documento](../vsto/document-host-item.md) e modelo de objeto do Word. O restante da `ThisDocument` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `ThisDocument_Startup` `ThisDocument_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o documento é aberto e fechado. Use esses manipuladores de eventos para inicializar sua personalização quando o documento for aberto e para limpar os recursos usados pela sua personalização quando o documento for fechado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-a-second-paragraph-of-text-to-the-document-by-using-code"></a>Para adicionar um segundo parágrafo de texto ao documento usando código

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisDocument** e clique em **Exibir código**.

     O arquivo de código é aberto no Visual Studio.

2. Substitua o `ThisDocument_Startup` manipulador de eventos pelo código a seguir. Quando o documento é aberto, esse código adiciona um segundo parágrafo de texto ao documento.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/FirstDocumentCustomization/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstDocumentCustomization/ThisDocument.cs" id="Snippet1":::

    > [!NOTE]
    > Esse código usa o valor de índice 1 para acessar o primeiro parágrafo na <xref:Microsoft.Office.Tools.Word.Document.Paragraphs%2A> propriedade. Embora Visual Basic e o Visual C# usem matrizes baseadas em 0, os limites de matriz inferiores da maioria das coleções no modelo de objeto do Word são 1. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).

## <a name="test-the-project"></a>Testar o projeto

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para compilar e executar o projeto.

     Quando você cria o projeto, o código é compilado em um assembly associado ao documento. O Visual Studio coloca uma cópia do documento e o assembly na pasta de saída do projeto e define as configurações de segurança no computador de desenvolvimento para permitir que a personalização seja executada. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

2. No documento, verifique se você vê o texto a seguir.

     **Esse texto foi adicionado usando o designer.**

     **Esse texto foi adicionado usando código.**

3. Feche o documento.

## <a name="clean-up-the-project"></a>Limpar o projeto

 Ao concluir o desenvolvimento de um projeto, você deve remover os arquivos na pasta de saída da compilação e as configurações de segurança criadas pelo processo de compilação.

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>Para limpar o projeto concluído em seu computador de desenvolvimento

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas

 Agora que você criou uma personalização básica no nível do documento para o Word, você pode aprender mais sobre como desenvolver personalizações a partir destes tópicos:

- Tarefas gerais de programação que você pode executar em personalizações em nível de documento: [programa personalizações em nível de documento](../vsto/programming-document-level-customizations.md).

- Tarefas de programação específicas para personalizações em nível de documento para Word: [Word Solutions](../vsto/word-solutions.md).

- Usando o modelo de objeto do Word: [visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md).

- Personalizando a interface do usuário do Word, por exemplo, adicionando uma guia personalizada à faixa de faixas ou criando seu próprio painel de ações: [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

- Usando objetos de palavra estendidos fornecidos pelas soluções do Office no Visual Studio para executar tarefas que não são possíveis com o uso do modelo de objeto do Word (por exemplo, Hospedagem de controles gerenciados em documentos e Associação de controles de texto a dados usando o modelo de associação de dados Windows Forms): [Automatize a palavra usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md).

- Criando e Depurando personalizações em nível de documento para o Word: [crie soluções do Office](../vsto/building-office-solutions.md).

- Implantando personalizações em nível de documento para [o Word: implante uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também

- [Visão geral do desenvolvimento de soluções do Office &#40;&#41;VSTO ](../vsto/office-solutions-development-overview-vsto.md)
- [Soluções do Word](../vsto/word-solutions.md)
- [Programar personalizações em nível de documento](../vsto/programming-document-level-customizations.md)
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
