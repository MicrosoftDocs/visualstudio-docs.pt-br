---
title: 'Como: Adicionar um método Creator | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], Creator
- BDC [SharePoint development in Visual Studio], adding entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entity instances
- BDC [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Creator
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38312384c3e6ce51aa1b5b0b16df378286fc58b0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443586"
---
# <a name="how-to-add-a-creator-method"></a>Como: Adicionar um método Creator
  Um método Creator adiciona novos dados à fonte de dados de uma entidade. O serviço de conectividade de dados comerciais (BDC) chama esse método quando os usuários escolhem o **Novo Item** botão a **faixa de opções** de uma lista que é baseada no modelo. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-add-a-creator-method"></a>Para adicionar um método Creator

1. Sobre o **Designer de BDC**, escolha uma entidade.

2. Na barra de menus, escolha **modo de exibição** > **Other Windows** >**detalhes do método BDC**.

    O **detalhes do método BDC** janela é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. No **adicionar um método** , escolha **criar método de criador**.

    Visual Studio adiciona os seguintes elementos ao modelo, e esses elementos aparecem na **detalhes do método BDC** janela.

   - Um método chamado **criar**.

   - Um parâmetro de entrada para o método.

   - Um parâmetro de retorno do método.

   - Tipos de descritores para os parâmetros.

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

4. Na **Gerenciador de soluções**, abra o menu de atalho do serviço arquivo de código que foi gerado para a entidade e, em seguida, escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto no Editor de códigos. Para obter mais informações sobre o arquivo de código do serviço de entidade, consulte [criar um modelo de conectividade de dados de negócios](../sharepoint/creating-a-business-data-connectivity-model.md).

5. Adicione código ao método criador que adiciona dados à fonte de dados. O exemplo a seguir adiciona um contato para o banco de dados de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > Substitua o valor da `ServerName` campo com o nome do seu servidor.

    [!code-csharp[SP_BDC#4](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#4)]
    [!code-vb[SP_BDC#4](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#4)]

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como: Adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)
- [Como: Adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: Adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)
- [Como: Adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)
- [Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: Adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como: Definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
