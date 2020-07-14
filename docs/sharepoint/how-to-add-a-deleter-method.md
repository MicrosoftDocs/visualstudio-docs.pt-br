---
title: Como adicionar um método excluidor | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], removing data
- BDC [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], removing data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: dd97d28936e9f0cc50e9064fdc1a6a64bb20fc77
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017036"
---
# <a name="how-to-add-a-deleter-method"></a>Como adicionar um método excluidor
  Você pode habilitar um usuário final para excluir um registro de dados de uma lista externa em um site do SharePoint adicionando um método excluidor ao modelo. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-a-deleter-method"></a>Para criar um método excluidor

1. No **BDC designer**, escolha uma entidade.

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método**do Windows BDC.

    A janela **detalhes do método BDC** é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar um método excluidor**.

    O Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na janela **detalhes do método BDC** .

   - Um método chamado **delete**.

   - Um parâmetro de entrada para o método.

   - Um descritor de tipo para o parâmetro.

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

4. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto no editor de código. Para obter mais informações sobre o arquivo de código do serviço de entidade, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

5. Adicione o código ao método excluidor para excluir um registro. O exemplo a seguir exclui um item de linha de um pedido de vendas usando o banco de dados de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > O método neste exemplo usa dois parâmetros de entrada.

   > [!NOTE]
   > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

    [!code-csharp[SP_BDC#6](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs#6)]
    [!code-vb[SP_BDC#6](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb#6)]

## <a name="see-also"></a>Consulte também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
