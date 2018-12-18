---
title: 'Como: adicionar uma região de formulário a um projeto de suplemento do Outlook'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.Page1
- VSTO.NewFormRegionWizard.Page3
- VSTO.NewFormRegionWizard.Page2
- VSTO.NewFormRegionWizard.Page0
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], adding
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 875644c10b07eb9c2b338b5a3cdfc827a76a7b34
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34549032"
---
# <a name="how-to-add-a-form-region-to-an-outlook-add-in-project"></a>Como: adicionar uma região de formulário a um projeto de suplemento do Outlook
  Criar uma região de formulário para estender um formulário personalizado ou padrão do Microsoft Office Outlook usando o **nova região de formulário do Outlook** assistente. Você pode criar uma nova região de formulário e criar a interface do usuário no Visual Studio, ou você pode importar uma região de formulário projetada no Outlook e adicione o código do Visual Basic ou c#.  
  
 Se você tiver uma região de formulário do Outlook usado em outro projeto do Outlook, você pode reutilizá-lo em seu projeto de suplemento do VSTO Outlook atual usando o **Add Existing Item** caixa de diálogo. Para obter mais informações, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
### <a name="to-add-a-new-form-region-to-an-outlook-project"></a>Para adicionar uma nova região de formulário a um projeto do Outlook  
  
1.  Abra ou crie um projeto de suplemento do VSTO do Outlook no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações, consulte [como: projetos do Office criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  Em **Solution Explorer**, selecione o nó do projeto do suplemento do VSTO do Outlook.  
  
3.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
4.  No **Adicionar Novo Item** caixa de diálogo, selecione **região de formulário do Outlook**.  
  
5.  Digite um nome para a região do formulário no **nome** caixa e, em seguida, clique em **adicionar**.  
  
     O **região do formulário NewOutlook** assistente é iniciado.  
  
6.  Sobre o **selecione como você deseja criar a região do formulário** , selecione se deseja criar a região de formulário por arrastar controles gerenciados em um designer visual ou importar uma região de formulário projetada no Outlook.  
  
    > [!NOTE]  
    >  Se você optar por importar uma região de formulário projetada no Outlook, você deve especificar o local de um armazenamento de formulário do Outlook (*. ofs*) arquivos. Você não pode adicionar controles gerenciados para uma região de formulário que você cria no Outlook; Você só pode adicionar código por trás da interface do usuário existente. Para obter mais informações, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
7.  Sobre o **selecione o tipo de região de formulário que você deseja criar** página, examine os tipos de região de formulário, selecione um e, em seguida, clique em **próximo**. Para obter mais informações sobre os tipos de região de formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
8.  No **fornecer um texto descritivo e selecione suas preferências de exibição** página, o **nome** , digite um nome para a região do formulário. Para os tipos de região de formulário Substituir tudo e a substituição de **título** e **descrição** caixas também estão disponíveis.  
  
     Para obter informações sobre onde o nome, o título e a descrição aparecerão no Outlook quando você implanta a região do formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
9. Selecione um ou mais modos de exibição no qual você deseja que a região de formulário apareça.  
  
     Todos os tipos de região de formulário podem aparecer no inspetores, no modo (para a criação de itens) de redação e no modo de leitura (para exibir itens). Adjacente à substituição e tipos de região de formulário de substituir tudo também podem ser exibido no painel de leitura.  
  
10. Clique em **Avançar**.  
  
11. Sobre o **identificar as classes de mensagem que exibição a região de formulário** página, selecione as classes de mensagem do Outlook padrão ou digite os nomes das classes de mensagem personalizada de um ou mais e, em seguida, clique em **concluir**. Para obter mais informações, consulte [associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)   
 [Soluções do Outlook](../vsto/outlook-solutions.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Diretrizes para criam regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Passo a passo: Importar uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)   
 [Ações personalizadas em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)  
  