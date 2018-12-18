---
title: Soluções do Outlook
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], Outlook
- Office projects [Office development in Visual Studio], Outlook
- Office solutions [Office development in Visual Studio], Outlook
- templates [Office development in Visual Studio], Outlook
- projects [Office development in Visual Studio], Outlook
- Outlook [Office development in Visual Studio]
- e-mail [Office development in Visual Studio], Outlook solutions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7d0a79d48b8ff054e4c7bdb9151f3eefbf287b24
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831231"
---
# <a name="outlook-solutions"></a>Soluções do Outlook
  Visual Studio fornece modelos de projeto, que você pode usar para criar suplementos do VSTO para o Microsoft Office Outlook. Você pode usar suplementos do VSTO para automatizar o Outlook, estender os recursos do Outlook ou personalizar a interface de usuário (IU) do Outlook. Para obter mais informações sobre o VSTO Add-ins, consulte [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="create-an-outlook-vsto-add-in-project"></a>Criar um projeto de suplemento do VSTO Outlook  
 Criar projetos do Outlook usando o **do suplemento do Outlook** modelo de projeto na **novo projeto** caixa de diálogo. Esse modelo inclui referências de assembly necessárias e os arquivos de projeto.  
  
 Para obter mais informações sobre como criar um projeto de suplemento do VSTO, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md). Para obter mais informações sobre os modelos de projeto, consulte [visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md).  
  
## <a name="outlook-vsto-add-in-programming-model"></a>Outlook do suplemento do VSTO modelo de programação  
 Quando você cria um projeto de suplemento do VSTO do Outlook, o Visual Studio gera uma classe, chamada `ThisAddIn`, que é a base da sua solução. Essa classe fornece um ponto de partida para escrever seu código, e ele também expõe o modelo de objeto do Outlook para o suplemento do VSTO.  
  
 Para obter mais informações sobre o `ThisAddIn` classe e outros recursos que você pode usar em um suplemento VSTO, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
## <a name="automate-outlook-by-using-the-outlook-object-model"></a>Automatizar o Outlook por meio do modelo de objeto do Outlook  
 O modelo de objeto do Outlook expõe vários tipos que você pode usar para automatizar o Outlook. Esses tipos permitem que você escreva código para realizar tarefas comuns:  
  
- Programaticamente, criar e enviar mensagens de email.  
  
- Envie novas solicitações de reunião.  
  
- Procurar itens nas pastas do Outlook.  
  
  Para obter mais informações, consulte [visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md).  
  
## <a name="customize-the-user-interface-of-an-outlook-application"></a>Personalizar a interface do usuário de um aplicativo do Outlook  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Adicione guias personalizadas à faixa de opções de um inspetor do Outlook.|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
|Adicione grupos personalizados a uma guia interna em um inspetor do Outlook.|[Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)|  
|Adicionar um painel de tarefas personalizado que aparece em um inspetor do Outlook|[Painéis de tarefas personalizados](../vsto/custom-task-panes.md).|  
|Adicione uma região de formulário que estende ou substitui formulários existentes do Outlook.|[Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)|  
  
 Para obter mais informações sobre como personalizar a interface do usuário do Outlook e outros aplicativos do Microsoft Office, consulte [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Visão geral de modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)|Fornece uma visão geral dos objetos que são fornecidos pelo modelo de objeto do Outlook.|  
|[Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)|Explica as ferramentas fornecidas pelo Visual Studio que tornam mais fácil para você projetar, desenvolver e depurar as regiões do formulário.|  
|[Passo a passo: Criar seu primeiro suplemento VSTO para Outlook](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)|Mostra como criar um suplemento do VSTO para o Microsoft Office Outlook.|  
|[Outlook 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199013)|A área da biblioteca MSDN onde você pode encontrar artigos e consultar a documentação sobre como desenvolver soluções do Outlook (não específicas para desenvolvimento do Office usando o Visual Studio).|  
  
  