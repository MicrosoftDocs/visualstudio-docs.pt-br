---
title: 'Walkthrough: criar seu primeiro suplemento do VSTO para PowerPoint'
description: Crie um suplemento em nível de aplicativo para o Microsoft PowerPoint. Esse recurso está disponível para o próprio aplicativo, independentemente de quais apresentações estão abertas.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- PowerPoint [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a5adf37c6d55d4704ee370052646e620cbe716c3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824244"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-powerpoint"></a>Walkthrough: criar seu primeiro suplemento do VSTO para PowerPoint
  Este tutorial mostra como criar um suplemento do VSTO para Microsoft Office PowerPoint. Os recursos que você cria nesse tipo de solução estão disponíveis para o próprio aplicativo, independentemente de quais apresentações estão abertas. Para obter mais informações, consulte [visão geral do desenvolvimento de soluções do Office &#40;&#41;do VSTO ](../vsto/office-solutions-development-overview-vsto.md).

 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto de suplemento do VSTO do PowerPoint para PowerPoint.

- Escrever código que usa o modelo de objeto do PowerPoint para adicionar uma caixa de texto a cada novo slide.

- Compilando e executando o projeto para testá-lo.

- Limpar o projeto para que o suplemento do VSTO não seja mais executado automaticamente no seu computador de desenvolvimento.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- PowerPoint

## <a name="create-the-project"></a>Criar o projeto

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

4. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do Office** .

5. Na lista de modelos de projeto, selecione um projeto de suplemento do VSTO do PowerPoint.

6. Na caixa **nome** , digite **FirstPowerPointAddIn**.

7. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto **FirstPowerPointAddIn** e abre o arquivo de código **ThisAddIn** no editor.

## <a name="write-code-that-adds-text-to-each-new-slide"></a>Escrever código que adiciona texto a cada novo slide
 Em seguida, adicione o código ao arquivo de código ThisAddIn. O novo código usa o modelo de objeto do PowerPoint para adicionar uma caixa de texto a cada novo slide. Por padrão, o arquivo de código ThisAddIn contém o seguinte código gerado:

- Uma definição parcial da `ThisAddIn` classe. Essa classe fornece um ponto de entrada para seu código e fornece acesso ao modelo de objeto do PowerPoint. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md). O restante da `ThisAddIn` classe é definido em um arquivo de código oculto que você não deve modificar.

- Os `ThisAddIn_Startup` `ThisAddIn_Shutdown` manipuladores de eventos e. Esses manipuladores de eventos são chamados quando o PowerPoint carrega e descarrega seu suplemento do VSTO. Use esses manipuladores de eventos para inicializar seu suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo seu suplemento do VSTO quando ele for descarregado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

### <a name="to-add-a-text-box-to-each-new-slide"></a>Para adicionar uma caixa de texto a cada novo slide

1. No arquivo de código ThisAddIn, adicione o código a seguir à `ThisAddIn` classe. Esse código define um manipulador de eventos para o evento [Microsoft.Office.Interop.PowerPoint.EApplication_Event. PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) do objeto [Application](/previous-versions/office/developer/office-2010/ff764034(v=office.14)) .

    Quando o usuário adiciona um novo slide à apresentação ativa, esse manipulador de eventos adiciona uma caixa de texto à parte superior do novo slide e adiciona um texto à caixa de texto.

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_PowerPointAddInTutorial/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs" id="Snippet1":::

2. Se você estiver usando C#, adicione o código a seguir ao `ThisAddIn_Startup` manipulador de eventos. Esse código é necessário para conectar o `Application_PresentationNewSlide` manipulador de eventos com o evento [Microsoft.Office.Interop.PowerPoint.EApplication_Event. PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) .

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs" id="Snippet2":::

   Para modificar cada novo slide, os exemplos de código anteriores usam os seguintes objetos:

- O `Application` campo da `ThisAddIn` classe. O `Application` campo retorna um objeto [Application](/previous-versions/office/developer/office-2010/ff764034(v=office.14)) , que representa a instância atual do PowerPoint.

- O `Sld` parâmetro do manipulador de eventos para o evento [Microsoft.Office.Interop.PowerPoint.EApplication_Event. PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14)) . O `Sld` parâmetro é um objeto de [Slide](/previous-versions/office/developer/office-2010/ff763417(v=office.14)) , que representa o novo slide. Para obter mais informações, consulte [soluções do PowerPoint](../vsto/powerpoint-solutions.md).

## <a name="test-the-project"></a>Testar o projeto
 Ao compilar e executar o projeto, verifique se a caixa de texto aparece em novos slides que você adiciona a uma apresentação.

### <a name="to-test-the-project"></a>Para testar o projeto

1. Pressione **F5** para compilar e executar o projeto.

     Quando você cria o projeto, o código é compilado em um assembly que é colocado na pasta de saída de compilação para o projeto. O Visual Studio também cria um conjunto de entradas de registro que permitem que o PowerPoint descubra e carregue o suplemento do VSTO e define as configurações de segurança no computador de desenvolvimento para permitir que o suplemento do VSTO seja executado. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

2. No PowerPoint, adicione um novo slide à apresentação ativa.

3. Verifique se o texto a seguir é adicionado a uma nova caixa de texto na parte superior do slide.

     **Esse texto foi adicionado usando código.**

4. Feche o PowerPoint.

## <a name="clean-up-the-project"></a>Limpar o projeto
 Quando você terminar de desenvolver um projeto, remova o assembly do suplemento do VSTO, as entradas do registro e as configurações de segurança do seu computador de desenvolvimento. Caso contrário, o suplemento do VSTO será executado toda vez que você abrir o PowerPoint no computador de desenvolvimento.

### <a name="to-clean-up-your-project"></a>Para limpar seu projeto

1. No Visual Studio, no menu **Compilar** , clique em **limpar solução**.

## <a name="next-steps"></a>Próximas etapas
 Agora que você criou um suplemento do VSTO básico para o PowerPoint, você pode aprender mais sobre como desenvolver suplementos do VSTO a partir destes tópicos:

- Tarefas gerais de programação que você pode executar em suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

- Usando o modelo de objeto do PowerPoint. Para obter mais informações, consulte [soluções do PowerPoint](../vsto/powerpoint-solutions.md).

- Personalizando a interface do usuário do PowerPoint, por exemplo, adicionando uma guia personalizada à faixa de faixas ou criando seu próprio painel de tarefas personalizado. Para obter mais informações, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).

- Criando e Depurando suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [criar soluções do Office](../vsto/building-office-solutions.md).

- Implantando suplementos do VSTO para PowerPoint. Para obter mais informações, consulte [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Soluções do PowerPoint](../vsto/powerpoint-solutions.md)
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Criar soluções do Office](../vsto/building-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Visão geral dos modelos do Office Project](../vsto/office-project-templates-overview.md)
