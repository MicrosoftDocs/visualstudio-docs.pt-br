---
title: 'Passo a passo: Criar seu primeiro suplemento VSTO para PowerPoint'
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
- PowerPoint [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cea6e61a1afd734ca0ae52a704a2d881371f5817
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882581"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-powerpoint"></a>Passo a passo: Criar seu primeiro suplemento VSTO para PowerPoint
  Este passo a passo mostra como criar um suplemento do VSTO para PowerPoint do Microsoft Office. Os recursos que você criar nesse tipo de solução estão disponíveis para o aplicativo em si, independentemente de qual apresentações estão abertas. Para obter mais informações, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um projeto de suplemento do VSTO do PowerPoint para o PowerPoint.  
  
- Escrevendo código que usa o modelo de objeto do PowerPoint para adicionar uma caixa de texto para cada novo slide.  
  
- Criando e executando o projeto para testá-lo.  
  
- Limpando o projeto para que o suplemento do VSTO não seja executado automaticamente em seu computador de desenvolvimento.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   PowerPoint  
  
## <a name="create-the-project"></a>Criar o projeto  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, expanda **Office/SharePoint**.  
  
4.  Sob o expandida **Office/SharePoint** nó, selecione o **suplementos do Office** nó.  
  
5.  Na lista de modelos de projeto, selecione um projeto de suplemento do VSTO do PowerPoint.  
  
6.  No **nome** , digite **FirstPowerPointAddIn**.  
  
7.  Clique em **OK**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o **FirstPowerPointAddIn** projeto e abrirá o **ThisAddIn** arquivo de código no editor.  
  
## <a name="write-code-that-adds-text-to-each-new-slide"></a>Escrever um código que adiciona o texto para cada novo slide  
 Em seguida, adicione código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do PowerPoint para adicionar uma caixa de texto para cada novo slide. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:  
  
-   Uma definição parcial do `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do PowerPoint. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md). O restante do `ThisAddIn` classe é definida em um arquivo de código oculto que você não deve modificar.  
  
-   O `ThisAddIn_Startup` e `ThisAddIn_Shutdown` manipuladores de eventos. Esses manipuladores de eventos são chamados quando o PowerPoint carrega e descarrega o suplemento do VSTO. Use esses manipuladores de eventos para inicializar o suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ela for descarregada. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="to-add-a-text-box-to-each-new-slide"></a>Para adicionar uma caixa de texto para cada novo slide  
  
1. No arquivo de código ThisAddIn, adicione o seguinte código para o `ThisAddIn` classe. Esse código define um manipulador de eventos para o [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) evento do <xref:Microsoft.Office.Interop.PowerPoint.Application> objeto.  
  
    Quando o usuário adiciona um novo slide na apresentação ativa, esse manipulador de eventos adiciona uma caixa de texto na parte superior do novo slide, e adiciona algum texto à caixa de texto.  
  
    [!code-vb[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_PowerPointAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#1)]  
  
2. Se você estiver usando c#, adicione o seguinte código para o `ThisAddIn_Startup` manipulador de eventos. Esse código é necessária para conectar o `Application_PresentationNewSlide` manipulador de eventos com o [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) eventos.  
  
    [!code-csharp[Trin_PowerPointAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#2)]  
  
   Para modificar cada novo slide, os exemplos de código anterior usam os seguintes objetos:  
  
-   O `Application` campo do `ThisAddIn` classe. O `Application` campo retorna um <xref:Microsoft.Office.Interop.PowerPoint.Application> objeto que representa a instância atual do PowerPoint.  
  
-   O `Sld` parâmetro do manipulador de eventos para o [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) eventos. O `Sld` parâmetro é um <xref:Microsoft.Office.Interop.PowerPoint.Slide> objeto que representa o novo slide. Para obter mais informações, consulte [soluções PowerPoint](../vsto/powerpoint-solutions.md).  
  
## <a name="test-the-project"></a>O projeto de teste  
 Quando você compila e executa o projeto, verifique se a caixa de texto aparece em novos slides que você adiciona a uma apresentação.  
  
### <a name="to-test-the-project"></a>Para testar o projeto  
  
1.  Pressione **F5** para compilar e executar seu projeto.  
  
     Quando você compila o projeto, o código é compilado em um assembly que é colocado na pasta de saída de compilação para o projeto. Visual Studio também cria um conjunto de entradas do registro que permitem descobrir e carregar o suplemento do VSTO no PowerPoint, e ele define as configurações de segurança no computador de desenvolvimento para habilitar o suplemento do VSTO ser executado. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
2.  No PowerPoint, adicione um novo slide na apresentação ativa.  
  
3.  Verifique se o texto a seguir é adicionado a uma nova caixa de texto na parte superior do slide.  
  
     **Este texto foi adicionado por meio de código.**  
  
4.  Feche o PowerPoint.  
  
## <a name="clean-up-the-project"></a>Limpar o projeto  
 Quando você concluir o desenvolvimento de um projeto, remova o suplemento do VSTO assembly, as entradas do registro e as configurações de segurança de seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO será executado sempre que você abrir o PowerPoint no computador de desenvolvimento.  
  
### <a name="to-clean-up-your-project"></a>Para limpar seu projeto  
  
1.  No Visual Studio, sobre o **construir** menu, clique em **limpar solução**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você criou um básico suplemento VSTO para PowerPoint, você pode aprender mais sobre como desenvolver suplementos do VSTO nesses tópicos:  
  
-   Tarefas de programação gerais que você pode executar nos suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
-   Usando o modelo de objeto do PowerPoint. Para obter mais informações, consulte [soluções PowerPoint](../vsto/powerpoint-solutions.md).  
  
-   Personalizando a interface do usuário do PowerPoint, por exemplo, adicionando uma guia personalizada à faixa de opções ou criando seu próprio painel de tarefas personalizado. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
-   Compilação e depuração de suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
-   Implantação de suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Soluções PowerPoint](../vsto/powerpoint-solutions.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)  
  
  