---
title: 'Passo a passo: Criar seu primeiro suplemento VSTO para o projeto'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- Project [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7fb6ece309fb0c5e7c67abf039d2b27a9f04236d
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671411"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-project"></a>Passo a passo: Criar seu primeiro suplemento VSTO para o projeto
  Este passo a passo mostra como criar um suplemento do VSTO para o Microsoft Office Project. Os recursos que você criar nesse tipo de solução estão disponíveis para o aplicativo em si, independentemente de qual projeto estiver aberto. Para obter mais informações, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um projeto de suplemento do VSTO do projeto.  
  
- Escrevendo código que usa o modelo de objeto do projeto para adicionar uma tarefa a um novo projeto.  
  
- Criando e executando o projeto para testá-lo.  
  
- Limpando o projeto concluído para que o suplemento do VSTO não seja executado automaticamente em seu computador de desenvolvimento.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Project_15_short](../vsto/includes/project-15-short-md.md)] ou [!INCLUDE[Project_14_short](../vsto/includes/project-14-short-md.md)].  
  
## <a name="create-the-project"></a>Criar o projeto  
  
### <a name="to-create-a-new-project-in-visual-studio"></a>Para criar um novo projeto no Visual Studio  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, expanda **Office/SharePoint**.  
  
4.  Sob o expandida **Office/SharePoint** nó, selecione o **suplementos do Office** nó.  
  
5.  Na lista de modelos de projeto, selecione **suplemento do Project 2010** ou **suplemento do Project 2013**.  
  
6.  No **nome** , digite **FirstProjectAddIn**.  
  
7.  Clique em **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o **FirstProjectAddIn** projeto e abrirá o **ThisAddIn** arquivo de código no editor.  
  
## <a name="write-code-that-adds-a-new-task-to-a-project"></a>Escrever um código que adiciona uma nova tarefa a um projeto  
 Em seguida, adicione código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do projeto para adicionar uma nova tarefa a um projeto. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:  
  
-   Uma definição parcial do `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do projeto. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md). O restante do `ThisAddIn` classe é definida em um arquivo de código oculto que você não deve modificar.  
  
-   O `ThisAddIn_Startup` e `ThisAddIn_Shutdown` manipuladores de eventos. Esses manipuladores de eventos são chamados quando o projeto carrega e descarrega o suplemento do VSTO. Use esses manipuladores de eventos para inicializar o suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ela for descarregada. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="to-add-a-task-to-a-new-project"></a>Para adicionar uma tarefa a um novo projeto  
  
1. No arquivo de código ThisAddIn, adicione o seguinte código para o `ThisAddIn` classe. Esse código define um manipulador de eventos para o `NewProject` eventos do `Microsoft.Office.Interop.MSProject.Application` classe.  
  
    Quando o usuário cria um novo projeto, esse manipulador de eventos adiciona uma tarefa ao projeto.  
  
    [!code-vb[Trin_ProjectAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_ProjectAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_ProjectAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs#1)]  
  
   Para modificar o projeto, este exemplo de código usa os seguintes objetos:  
  
-   O `Application` campo do `ThisAddIn` classe. O `Application` campo retorna um `Microsoft.Office.Interop.MSProject.Application` objeto que representa a instância atual do projeto.  
  
-   O `pj` parâmetro do manipulador de eventos para o evento NewProject. O `pj` parâmetro é um `Microsoft.Office.Interop.MSProject.Project` objeto que representa o projeto. Para obter mais informações, consulte [soluções de projeto](../vsto/project-solutions.md).  
  
1.  Se você estiver usando c#, adicione o seguinte código para o `ThisAddIn_Startup` manipulador de eventos. Esse código se conecta a `Application_Newproject` manipulador de eventos com o evento NewProject.  
  
     [!code-csharp[Trin_ProjectAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs#2)]  
  
  
## <a name="test-the-project"></a>O projeto de teste  
 Quando você compila e executa o projeto, verifique se a nova tarefa aparece no novo projeto resultante.  
  
### <a name="to-test-the-project"></a>Para testar o projeto  
  
1.  Pressione **F5** para compilar e executar seu projeto. Microsoft Project é iniciado e abre automaticamente um novo projeto em branco.  
  
     Quando você compila o projeto, o código é compilado em um assembly que está incluído na pasta de saída de compilação para o projeto. Visual Studio também cria um conjunto de entradas do registro que permitem que o projeto descobrir e carregar o suplemento do VSTO e ela define as configurações de segurança no computador de desenvolvimento para habilitar o suplemento do VSTO ser executado. Para obter mais informações, consulte [visão geral do processo de compilação solução Office](/previous-versions/visualstudio/visual-studio-2010/h2c9cdc0(v=vs.100)).  
  
2.  Verifique se que uma nova tarefa é adicionada ao projeto em branco.  
  
3.  Verifique se o texto a seguir aparece na **nome da tarefa** campo da tarefa.  
  
     **Este texto foi adicionado por meio de código.**  
  
4.  Feche o Microsoft Project.  
  
## <a name="clean-up-the-project"></a>Limpar o projeto  
 Quando você concluir o desenvolvimento de um projeto, remova o suplemento do VSTO assembly, as entradas do registro e as configurações de segurança de seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO será executado sempre que você abrir o Microsoft Project no computador de desenvolvimento.  
  
### <a name="to-clean-up-your-project"></a>Para limpar seu projeto  
  
1.  No Visual Studio, sobre o **construir** menu, clique em **limpar solução**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você criou um básico suplemento VSTO para o projeto, você pode aprender mais sobre como desenvolver suplementos do VSTO nesses tópicos:  
  
-   Tarefas gerais de programação que você pode executar no VSTO Add-ins para o projeto: [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
-   Usando o modelo de objeto do projeto: [soluções de projeto](../vsto/project-solutions.md).  
  
-   Compilar e depurar o VSTO Add-ins para o projeto: [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
-   Implantando o VSTO Add-ins para o projeto: [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Soluções de projeto](../vsto/project-solutions.md)   
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)  
  
  