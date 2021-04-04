---
title: Como adicionar um método de atualizador | Microsoft Docs
description: Saiba como permitir que os usuários atualizem dados corporativos em uma lista externa do SharePoint adicionando um método de atualizador.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d6337ac237c2a030593b90b29af5e8474052de99
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216729"
---
# <a name="how-to-add-an-updater-method"></a>Como adicionar um método de atualizador
  Você pode permitir que os usuários atualizem dados corporativos em uma lista externa do SharePoint criando um método de *atualizador* . Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-an-updater-method"></a>Para criar um método de atualizador

1. No BDC designer, escolha uma entidade.

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método** do Windows BDC.

    A janela detalhes do método BDC é aberta. Para obter mais informações sobre essa janela, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar método de atualizador**.

    O Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na janela detalhes do método BDC.

   - Um método chamado **Update**.

   - Um parâmetro de entrada para o método.

   - Um descritor de tipo para o parâmetro. Por padrão, o Visual Studio usa o descritor de tipo de entidade que você definiu para o método Finder (por exemplo: contact).

   - Uma instância de método para o método.

     Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

   > [!NOTE]
   > Se o identificador do tipo de entidade representa um campo em uma tabela de banco de dados que não é gerada automaticamente, defina a propriedade de **campo de pré-atualização** como **true**.

4. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**.

    O arquivo de código do serviço de entidade é aberto no **Editor de código**. Para obter mais informações sobre esse arquivo, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

5. Adicione o código ao método Update para atualizar os dados. O exemplo a seguir atualiza as informações de um contato no banco de dados de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet5":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet5":::

## <a name="see-also"></a>Confira também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador](../sharepoint/how-to-add-a-finder-method.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
