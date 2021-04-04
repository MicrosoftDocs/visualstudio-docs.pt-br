---
title: Como adicionar um método localizador | Microsoft Docs
description: Adicione um método localizador no Visual Studio, que permite que o serviço BDC (conectividade de dados corporativos) exiba uma lista de entidades em uma Web Part ou lista do SharePoint.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6bd75c94e2f0f557b85d945d141f952950abb2eb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216339"
---
# <a name="how-to-add-a-finder-method"></a>Como adicionar um método localizador
  Para habilitar o serviço BDC (conectividade de dados corporativos) para exibir uma lista de entidades em uma Web Part ou lista, você deve criar um método *localizador* . Um método Finder é um método especial que retorna uma coleção de instâncias de entidade. Para obter mais informações, consulte [criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

### <a name="to-create-a-finder-method"></a>Para criar um método localizador

1. No **BDC designer**, escolha uma entidade.

    Para obter mais informações, consulte [como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método** do Windows BDC.

    A janela **detalhes do método BDC** é aberta. Para obter mais informações sobre a janela **detalhes do método BDC** , consulte [visão geral das ferramentas de design do modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

3. Na lista **Adicionar um método** , escolha **criar método localizador**.

    O Visual Studio adiciona um método, um parâmetro de retorno e um descritor de tipo.

4. Configure o descritor de tipo como um descritor de tipo de coleção de entidade. Para obter mais informações sobre como criar um descritor de tipo de coleção de entidades, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).

   > [!NOTE]
   > Você não precisará executar esta etapa se tiver adicionado um método localizador específico à entidade. O Visual Studio usa o descritor de tipo que você definiu no método localizador específico.

5. No **Gerenciador de soluções**, abra o menu de atalho do arquivo de código de serviço que foi gerado para a entidade e escolha **Exibir código**. Para obter mais informações sobre o arquivo de código de serviço, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

6. Adicione o código ao método Finder. Esse código executa as seguintes tarefas:

   - Recupera dados de uma fonte de dados.

   - Retorna uma lista de entidades para o serviço BDC.

     O exemplo a seguir retorna uma coleção de `Contact` entidades usando dados do banco de dado de exemplo AdventureWorks para SQL Server.

   > [!NOTE]
   > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="see-also"></a>Confira também
- [Visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como adicionar um método localizador específico](../sharepoint/how-to-add-a-specific-finder-method.md)
- [Como: adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md)
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md)
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md)
- [Como: adicionar um parâmetro a um método](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [Como definir uma instância de método](../sharepoint/how-to-define-a-method-instance.md)
