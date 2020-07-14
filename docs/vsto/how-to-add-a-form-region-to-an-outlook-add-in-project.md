---
title: 'Como: adicionar uma região de formulário a um projeto de suplemento do Outlook'
ms.date: 02/02/2017
ms.topic: how-to
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
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a03ba05226720913d48dc1828dcb849bee72d17e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538392"
---
# <a name="how-to-add-a-form-region-to-an-outlook-add-in-project"></a>Como: adicionar uma região de formulário a um projeto de suplemento do Outlook
  Crie uma região de formulário para estender um formulário Microsoft Office do Outlook padrão ou personalizado usando o novo assistente de **área de formulário do Outlook** . Você pode criar uma nova região de formulário e criar a interface do usuário no Visual Studio, ou pode importar uma região de formulário que foi desenvolvida no Outlook e adicionar Visual Basic ou código C#.

 Se você tiver uma região de formulário do Outlook que você usou em outro projeto do Outlook, poderá reutilizá-la em seu projeto de suplemento do VSTO do Outlook atual usando a caixa de diálogo **Adicionar item existente** . Para obter mais informações, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

### <a name="to-add-a-new-form-region-to-an-outlook-project"></a>Para adicionar uma nova região de formulário a um projeto do Outlook

1. Abra ou crie um projeto de suplemento do VSTO do Outlook no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. Em **Gerenciador de soluções**, selecione o nó do projeto de suplemento do VSTO do Outlook.

3. No menu **Projeto** , clique em **Adicionar Novo Item**.

4. Na caixa de diálogo **Adicionar novo item** , selecione **região de formulário do Outlook**.

5. Digite um nome para a região de formulário na caixa **nome** e clique em **Adicionar**.

     O assistente de **região de formulário NewOutlook** é iniciado.

6. Na página **Selecione como você deseja criar a região de formulário** , selecione se deseja projetar a região de formulário arrastando controles gerenciados para um designer visual ou importe uma região de formulário que foi desenvolvida no Outlook.

    > [!NOTE]
    > Se você optar por importar uma região de formulário que foi criada no Outlook, deverá especificar o local de um arquivo de armazenamento de formulário do Outlook (*. OFS*). Você não pode adicionar controles gerenciados a uma região de formulário que você cria no Outlook; Você só pode adicionar código por trás da interface do usuário existente. Para obter mais informações, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

7. Na página **selecionar o tipo de região de formulário que você deseja criar** , examine os tipos de região de formulário e selecione um e clique em **Avançar**. Para obter mais informações sobre tipos de região de formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

8. No **texto descritivo de fornecimento e selecione sua página preferências de exibição** , na caixa **nome** , digite um nome para a região de formulário. Para os tipos de região de formulário substituição e substituir, as caixas **título** e **Descrição** também estão disponíveis.

     Para obter informações sobre onde o nome, o título e a descrição aparecem no Outlook quando você implanta a região do formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

9. Selecione um ou mais modos de exibição nos quais você deseja que a região do formulário apareça.

     Todos os tipos de região de formulário podem aparecer nos inspetores, no modo de composição (para criar itens) e no modo de leitura (para exibir itens). Os tipos de região de formulário adjacente, substituição e substituição – também podem aparecer no painel de leitura.

10. Clique em **Próximo**.

11. Na página **identificar as classes de mensagem que exibirão esta região de formulário** , selecione as classes de mensagem padrão do Outlook ou digite os nomes de uma ou mais classes de mensagem personalizadas e clique em **concluir**. Para obter mais informações, consulte [associar uma região de formulário a uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md).

## <a name="see-also"></a>Confira também
- [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)
- [Soluções do Outlook](../vsto/outlook-solutions.md)
- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Walkthrough: importar uma região de formulário projetada no Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [Ações personalizadas nas regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)
