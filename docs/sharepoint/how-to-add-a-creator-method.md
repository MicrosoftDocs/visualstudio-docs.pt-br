---
title: 'Como: adicionar um método criador | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 962e353b5ae82f6dd3eccc2898385fd4b9ee30ee
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017070"
---
# <a name="how-to-add-a-creator-method"></a>Como: adicionar um método de criador
  Um método de criador adiciona novos dados à fonte de dados de uma entidade. O serviço BDC (conectividade de dados corporativos) chama esse método quando os usuários escolhem o botão **novo item** na **faixa de faixas** de uma lista baseada no modelo. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-add-a-creator-method"></a>Para adicionar um método de criador

1. No **BDC designer**, escolha uma entidade.

2. Na barra de menus, escolha **Exibir**  >  **outros**  > **detalhes do método**do Windows BDC.

    A janela **detalhes do método BDC** é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar método criador**.

    O Visual Studio adiciona os seguintes elementos ao modelo, e esses elementos aparecem na janela **detalhes do método BDC** .

   - Um método chamado **Create**.

   - Um parâmetro de entrada para o método.

   - Um parâmetro de retorno para o método.

   - Inscriprs de tipo para os parâmetros.

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

4. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto no editor de código. Para obter mais informações sobre o arquivo de código do serviço de entidade, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

5. Adicione código ao método criador que adiciona dados à fonte de dados. O exemplo a seguir adiciona um contato ao banco de dados de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

    [!code-csharp[SP_BDC#4](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#4)]
    [!code-vb[SP_BDC#4](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#4)]

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
