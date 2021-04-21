---
title: 'Walkthrough: criar seu primeiro suplemento do VSTO para Outlook'
description: Crie um suplemento de nível de aplicativo para o Microsoft Outlook. Esse recurso está disponível para o próprio aplicativo, independentemente de qual item do Outlook está aberto.
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Outlook [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a6bcc134096284579e1097edf0e958105f48cfcb
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824271"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-outlook"></a>Walkthrough: criar seu primeiro suplemento do VSTO para Outlook
  Este tutorial mostra como criar um suplemento do VSTO para Microsoft Office Outlook. Os recursos que você cria nesse tipo de solução estão disponíveis para o próprio aplicativo, independentemente de qual item do Outlook está aberto. Para obter mais informações, consulte [visão geral do desenvolvimento de soluções do Office &#40;&#41;do VSTO ](../vsto/office-solutions-development-overview-vsto.md).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de suplemento do VSTO do Outlook para Outlook.

- Escrever código que usa o modelo de objeto do Outlook para adicionar texto ao assunto e ao corpo de uma nova mensagem de email.

- Compilando e executando o projeto para testá-lo.

- Limpando o projeto concluído para que o suplemento do VSTO não seja mais executado automaticamente no seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-outlook-project-in-visual-studio"></a>Para criar um novo projeto do Outlook no Visual Studio

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, escolha um projeto de suplemento do VSTO do Outlook.

6. Na caixa **nome** , digite **FirstOutlookAddIn**.

7. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstOutlookAddIn** e abre o arquivo de código **ThisAddIn** no editor.

## <a name="write-code-that-adds-text-to-each-new-mail-message"></a>Escrever código que adiciona texto a cada nova mensagem de email
 Em seguida, adicione o código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do Outlook para adicionar texto a cada nova mensagem de email. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:

- Uma definição parcial da `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do Outlook. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md). O restante da `ThisAddIn` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `ThisAddIn_Startup` `ThisAddIn_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o Outlook carrega e descarrega o suplemento do VSTO. Use esses manipuladores de eventos para inicializar seu suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ele for descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-text-to-the-subject-and-body-of-each-new-mail-message"></a>Para adicionar texto ao assunto e ao corpo de cada nova mensagem de email

1. No arquivo de código ThisAddIn, declare um campo chamado `inspectors` na `ThisAddIn` classe. O `inspectors` campo mantém uma referência à coleção de janelas de Inspetor na instância atual do Outlook. Essa referência impede que o coletor de lixo libere a memória que contém o manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs" id="Snippet1":::

2. Substitua o método `ThisAddIn_Startup` pelo seguinte código. Esse código anexa um manipulador de eventos ao <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb" id="Snippet2":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs" id="Snippet2":::

3. No arquivo de código ThisAddIn, adicione o código a seguir à `ThisAddIn` classe. Esse código define um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento.

    Quando o usuário cria uma nova mensagem de email, esse manipulador de eventos adiciona texto à linha de assunto e ao corpo da mensagem.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb" id="Snippet3":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs" id="Snippet3":::

   Para modificar cada nova mensagem de email, os exemplos de código anteriores usam os seguintes objetos:

- O `Application` campo da `ThisAddIn` classe. O `Application` campo retorna um <xref:Microsoft.Office.Interop.Outlook.Application> objeto, que representa a instância atual do Outlook.

- O `Inspector` parâmetro do manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento. O `Inspector` parâmetro é um <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto, que representa a janela do inspetor da nova mensagem de email. Para obter mais informações, consulte [soluções do Outlook](../vsto/outlook-solutions.md).

## <a name="test-the-project"></a>Testar o projeto
 Ao compilar e executar o projeto, verifique se o texto aparece na linha de assunto e no corpo de uma nova mensagem de email.

### <a name="to-test-the-project"></a>Para testar o projeto

1. Pressione **F5** para compilar e executar o projeto.

     Quando você cria o projeto, o código é compilado em um assembly que é incluído na pasta de saída de compilação para o projeto. O Visual Studio também cria um conjunto de entradas do registro que permitem que o Outlook descubra e carregue o suplemento do VSTO e define as configurações de segurança no computador de desenvolvimento para permitir que o suplemento do VSTO seja executado. Para obter mais informações, consulte [visão geral do processo de criação de soluções do Office](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md).

2. No Outlook, crie uma nova mensagem de email.

3. Verifique se o texto a seguir é adicionado à linha de assunto e ao corpo da mensagem.

     **Esse texto foi adicionado usando código.**

4. Feche o Outlook.

## <a name="clean-up-the-project"></a>Limpar o projeto
 Quando você terminar de desenvolver um projeto, remova o assembly do suplemento do VSTO, as entradas do registro e as configurações de segurança do seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO será executado toda vez que você abrir o Outlook no computador de desenvolvimento.

### <a name="to-clean-up-your-project"></a>Para limpar seu projeto

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas
 Agora que você criou um suplemento do VSTO básico para o Outlook, você pode aprender mais sobre como desenvolver suplementos do VSTO a partir destes tópicos:

- Tarefas de programação gerais que você pode executar usando suplementos do VSTO para Outlook. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

- Usando o modelo de objeto do Outlook. Para obter mais informações, consulte [soluções do Outlook](../vsto/outlook-solutions.md).

- Personalizando a interface do usuário do Outlook, por exemplo, adicionando uma guia personalizada à faixa de faixas ou criando seu próprio painel de tarefas personalizado. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

- Criando e Depurando suplementos do VSTO para Outlook. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

- Implantando suplementos do VSTO para Outlook. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Soluções do Outlook](../vsto/outlook-solutions.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
