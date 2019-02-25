---
title: 'Como: Adicionar um método Updater | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], updating data
- BDC [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating data
- Business Data Connectivity service [SharePoint development in Visual Studio], Updater
- Business Data Connectivity service [SharePoint development in Visual Studio], updating entity instances
- BDC [SharePoint development in Visual Studio], updating entity instances
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26b917b04314c99ba6575842b8e102113b22b469
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56596953"
---
# <a name="how-to-add-an-updater-method"></a>Como: Adicionar um método Updater
  Você pode habilitar os usuários atualizem dados comerciais em uma lista externa do SharePoint com a criação de um *atualizador* método. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-an-updater-method"></a>Para criar um método Updater

1. No designer de BDC, escolha uma entidade.

2. Na barra de menus, escolha **modo de exibição** > **Other Windows** > **detalhes do método BDC**.

    Abre a janela de detalhes do método BDC. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. No **adicionar um método** , escolha **criar método de atualizador**.

    Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos são exibidos na janela de detalhes do método BDC.

   - Um método chamado **atualização**.

   - Um parâmetro de entrada para o método.

   - Um descritor de tipo para o parâmetro. Por padrão, o Visual Studio usa descritor de tipo de entidade que você definiu para o método Finder (por exemplo: Entre em contato com).

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

   > [!NOTE]
   >  Se o identificador do tipo de entidade representa um campo em uma tabela de banco de dados que é gerado automaticamente, defina a **campo do pré-atualizador** propriedade **verdadeiro**.

4. Na **Gerenciador de soluções**, abra o menu de atalho do serviço arquivo de código que foi gerado para a entidade e, em seguida, escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto na **Editor de códigos**. Para obter mais informações sobre esse arquivo, consulte [criar um modelo de conectividade de dados de negócios](../sharepoint/creating-a-business-data-connectivity-model.md).

5. Adicione código para o método de atualização para atualizar dados. O exemplo a seguir atualiza as informações de um contato do banco de dados de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   >  Substitua o valor da `ServerName` campo com o nome do seu servidor.

    [!code-csharp[SP_BDC#5](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#5)]
    [!code-vb[SP_BDC#5](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#5)]

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como: Adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)
- [Como: Adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: Adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)
- [Como: Adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)
- [Como: Adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)
- [Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: Adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como: Definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
