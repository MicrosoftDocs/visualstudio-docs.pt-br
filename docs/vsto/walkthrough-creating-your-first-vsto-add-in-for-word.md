---
title: 'Walkthrough: criar seu primeiro suplemento do VSTO para Word'
description: Crie um suplemento de nível de aplicativo para o Microsoft Word. Esse recurso está disponível para o próprio aplicativo, independentemente de quais documentos estão abertos.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Word [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fd3509ab674faa220ed7bbea15a9762f52b1a525
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828274"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-word"></a>Walkthrough: criar seu primeiro suplemento do VSTO para Word
  Este guia introdutório mostra como criar um suplemento do VSTO para o Microsoft Office Word. Os recursos que você cria nesse tipo de solução estão disponíveis para o próprio aplicativo, independentemente de quais documentos estão abertos.

 [!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de suplemento do VSTO do Word.

- Escrever código que usa o modelo de objeto do Word para adicionar texto a um documento quando ele é salvo.

- Compilando e executando o projeto para testá-lo.

- Limpando o projeto concluído para que o suplemento do VSTO não seja mais executado automaticamente no seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-word-vsto-add-in-project-in-visual-studio"></a>Para criar um novo projeto de suplemento do VSTO do Word no Visual Studio

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, selecione um projeto de suplemento do VSTO do Word.

6. Na caixa **nome** , digite **FirstWordAddIn**.

7. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstWordAddIn** e abre o arquivo de código ThisAddIn no editor.

## <a name="write-code-to-add-text-to-the-saved-document"></a>Escreva o código para adicionar texto ao documento salvo
 Em seguida, adicione o código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do Word para adicionar texto clichê a cada documento salvo. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:

- Uma definição parcial da `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do Word. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md). O restante da `ThisAddIn` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `ThisAddIn_Startup` `ThisAddIn_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o Word carrega e descarrega o suplemento do VSTO. Use esses manipuladores de eventos para inicializar seu suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ele for descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-a-paragraph-of-text-to-the-saved-document"></a>Para adicionar um parágrafo de texto ao documento salvo

1. No arquivo de código ThisAddIn, adicione o código a seguir à `ThisAddIn` classe. O novo código define um manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento, que é gerado quando um documento é salvo.

    Quando o usuário salva um documento, o manipulador de eventos adiciona um novo texto no início do documento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/FirstWordAddIn/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstWordAddIn/ThisAddIn.cs" id="Snippet1":::

   > [!NOTE]
   > Esse código usa um valor de índice de 1 para acessar o primeiro parágrafo na <xref:Microsoft.Office.Interop.Word._Document.Paragraphs%2A> coleção. Embora Visual Basic e o Visual C# usem matrizes baseadas em 0, os limites de matriz inferiores da maioria das coleções no modelo de objeto do Word são 1. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).

2. Se você estiver usando C#, adicione o seguinte código necessário ao `ThisAddIn_Startup` manipulador de eventos. Esse código é usado para conectar o `Application_DocumentBeforeSave` manipulador de eventos ao <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstWordAddIn/ThisAddIn.cs" id="Snippet2":::

   Para modificar o documento quando ele é salvo, os exemplos de código anteriores usam os seguintes objetos:

- O `Application` campo da `ThisAddIn` classe. O `Application` campo retorna um <xref:Microsoft.Office.Interop.Word.Application> objeto, que representa a instância atual do Word.

- O `Doc` parâmetro do manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> evento. O `Doc` parâmetro é um <xref:Microsoft.Office.Interop.Word.Document> objeto, que representa o documento salvo. Para obter mais informações, consulte [visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md).

## <a name="test-the-project"></a>Testar o projeto

### <a name="to-test-the-project"></a>Para testar o projeto

1. Pressione **F5** para compilar e executar o projeto.

     Quando você cria o projeto, o código é compilado em um assembly que é incluído na pasta de saída de compilação para o projeto. O Visual Studio também cria um conjunto de entradas de registro que permitem que o Word descubra e carregue o suplemento do VSTO, e define as configurações de segurança no computador de desenvolvimento para habilitar o suplemento do VSTO para execução. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

2. No Word, salve o documento ativo.

3. Verifique se o texto a seguir foi adicionado ao documento.

     **Esse texto foi adicionado usando código.**

4. Feche o Word.

## <a name="clean-up-the-project"></a>Limpar o projeto
 Quando você terminar de desenvolver um projeto, remova o assembly do suplemento do VSTO, as entradas do registro e as configurações de segurança do seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO continuará a ser executado toda vez que você abrir o Word em seu computador de desenvolvimento.

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>Para limpar o projeto concluído em seu computador de desenvolvimento

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas
 Agora que você criou um suplemento do VSTO básico para o Word, você pode aprender mais sobre como desenvolver suplementos do VSTO a partir destes tópicos:

- Tarefas gerais de programação que você pode executar em suplementos do VSTO: [suplementos do programa VSTO](../vsto/programming-vsto-add-ins.md).

- Tarefas de programação específicas para os suplementos do VSTO do Word: [soluções do Word](../vsto/word-solutions.md).

- Usando o modelo de objeto do Word: [visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md).

- Personalizando a interface do usuário do Word, por exemplo, adicionando uma guia personalizada à faixa de faixas ou criando seu próprio painel de tarefas personalizado: [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

- Criando e Depurando suplementos do VSTO para Word: [criar soluções do Office](../vsto/building-office-solutions.md).

- Implantando suplementos do VSTO para Word: [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também
- [Visão geral do desenvolvimento de soluções do Office &#40;&#41;VSTO ](../vsto/office-solutions-development-overview-vsto.md)
- [Soluções do Word](../vsto/word-solutions.md)
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
