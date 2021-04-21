---
title: 'Walkthrough: criar seu primeiro suplemento do VSTO para o projeto'
description: Crie um suplemento em nível de aplicativo para o Microsoft Project. Esse recurso está disponível para o próprio aplicativo, independentemente de quais projetos estão abertos.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- Project [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 48d7baf9605947818ffd79eb7312c0dbefe581ac
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824257"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-project"></a>Walkthrough: criar seu primeiro suplemento do VSTO para o projeto
  Este tutorial mostra como criar um suplemento do VSTO para Microsoft Office projeto. Os recursos que você cria nesse tipo de solução estão disponíveis para o próprio aplicativo, independentemente de quais projetos estão abertos. Para obter mais informações, consulte [visão geral do desenvolvimento de soluções do Office &#40;&#41;do VSTO ](../vsto/office-solutions-development-overview-vsto.md).

 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de suplemento do VSTO do projeto.

- Escrever código que usa o modelo de objeto do projeto para adicionar uma tarefa a um novo projeto.

- Compilando e executando o projeto para testá-lo.

- Limpando o projeto concluído para que o suplemento do VSTO não seja mais executado automaticamente no seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Project_15_short](../vsto/includes/project-15-short-md.md)] ou [!INCLUDE[Project_14_short](../vsto/includes/project-14-short-md.md)].

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-project-in-visual-studio"></a>Para criar um novo projeto no Visual Studio

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, selecione o **suplemento project 2010** ou o **suplemento 2013 do projeto**.

6. Na caixa **nome** , digite **FirstProjectAddIn**.

7. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstProjectAddIn** e abre o arquivo de código **ThisAddIn** no editor.

## <a name="write-code-that-adds-a-new-task-to-a-project"></a>Escrever código que adiciona uma nova tarefa a um projeto
 Em seguida, adicione o código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do projeto para adicionar uma nova tarefa a um projeto. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:

- Uma definição parcial da `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do projeto. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md). O restante da `ThisAddIn` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `ThisAddIn_Startup` `ThisAddIn_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o projeto carrega e descarrega seu suplemento do VSTO. Use esses manipuladores de eventos para inicializar seu suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ele for descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-a-task-to-a-new-project"></a>Para adicionar uma tarefa a um novo projeto

1. No arquivo de código ThisAddIn, adicione o código a seguir à `ThisAddIn` classe. Esse código define um manipulador de eventos para o `NewProject` evento da `Microsoft.Office.Interop.MSProject.Application` classe.

    Quando o usuário cria um novo projeto, esse manipulador de eventos adiciona uma tarefa ao projeto.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ProjectAddInTutorial/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs" id="Snippet1":::

   Para modificar o projeto, este exemplo de código usa os seguintes objetos:

- O `Application` campo da `ThisAddIn` classe. O `Application` campo retorna um `Microsoft.Office.Interop.MSProject.Application` objeto, que representa a instância atual do projeto.

- O `pj` parâmetro do manipulador de eventos para o evento NewProject. O `pj` parâmetro é um `Microsoft.Office.Interop.MSProject.Project` objeto, que representa o projeto. Para obter mais informações, consulte [Project Solutions](../vsto/project-solutions.md).

1. Se você estiver usando C#, adicione o código a seguir ao `ThisAddIn_Startup` manipulador de eventos. Esse código conecta o `Application_Newproject` manipulador de eventos ao evento NewProject.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs" id="Snippet2":::

## <a name="test-the-project"></a>Testar o projeto
 Ao compilar e executar o projeto, verifique se a nova tarefa aparece no novo projeto resultante.

### <a name="to-test-the-project"></a>Para testar o projeto

1. Pressione **F5** para compilar e executar o projeto. O Microsoft Project é iniciado e abre automaticamente um novo projeto em branco.

     Quando você cria o projeto, o código é compilado em um assembly que é incluído na pasta de saída de compilação para o projeto. O Visual Studio também cria um conjunto de entradas do registro que habilitam o Project a descobrir e carregar o suplemento do VSTO e define as configurações de segurança no computador de desenvolvimento para permitir que o suplemento do VSTO seja executado. Para obter mais informações, consulte [visão geral do processo de criação de soluções do Office](/previous-versions/visualstudio/visual-studio-2010/h2c9cdc0(v=vs.100)).

2. Verifique se uma nova tarefa foi adicionada ao projeto em branco.

3. Verifique se o texto a seguir aparece no campo **nome da tarefa** da tarefa.

     **Esse texto foi adicionado usando código.**

4. Feche o Microsoft Project.

## <a name="clean-up-the-project"></a>Limpar o projeto
 Quando você terminar de desenvolver um projeto, remova o assembly do suplemento do VSTO, as entradas do registro e as configurações de segurança do seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO será executado toda vez que você abrir o Microsoft Project no computador de desenvolvimento.

### <a name="to-clean-up-your-project"></a>Para limpar seu projeto

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas
 Agora que você criou um suplemento do VSTO básico para o Project, você pode aprender mais sobre como desenvolver suplementos do VSTO a partir destes tópicos:

- Tarefas gerais de programação que você pode executar em suplementos do VSTO para projetos: [programa suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

- Usando o modelo de objeto do projeto: [soluções de projeto](../vsto/project-solutions.md).

- Criando e Depurando suplementos do VSTO para o projeto: [criar soluções do Office](../vsto/building-office-solutions.md).

- Implantando suplementos do VSTO para o projeto: [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Soluções de projeto](../vsto/project-solutions.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
