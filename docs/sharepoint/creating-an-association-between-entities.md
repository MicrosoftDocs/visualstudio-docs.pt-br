---
title: Criando uma associação entre entidades | Microsoft Docs
description: Crie uma associação entre entidades em seu modelo de BDC (conectividade de dados corporativos). Saiba mais sobre os métodos de associação e tipos de associações.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Association_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associations between entities
- BDC [SharePoint development in Visual Studio], associations between entities
- Business Data Connectivity service [SharePoint development in Visual Studio], create an assocation
- Business Data Connectivity service [SharePoint development in Visual Studio], associate external content types
- Business Data Connectivity service [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], relate entities
- BDC [SharePoint development in Visual Studio], associate external content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d40c4e5c5d61b9da3cdbdd3fe96f45c4a0cff929
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213960"
---
# <a name="create-an-association-between-entities"></a>Criar uma associação entre entidades
  Você pode definir relações entre entidades em seu modelo de BDC (conectividade de dados corporativos) Criando associações. O Visual Studio gera métodos que fornecem aos consumidores do modelo informações sobre cada associação. Esses métodos podem ser consumidos por Web Parts do SharePoint, listas ou aplicativos personalizados para exibir relações de dados em uma interface do usuário.

## <a name="create-an-association"></a>Criar uma associação
 Crie uma associação escolhendo o controle de **Associação** na **caixa de ferramentas** do Visual Studio, escolhendo a primeira entidade (chamada de entidade de origem) e, em seguida, escolhendo a segunda entidade (chamada de entidade de destino). Você pode definir os detalhes da associação no editor de **Associação**. Para obter mais informações, consulte [como: criar uma associação entre entidades](../sharepoint/how-to-create-an-association-between-entities.md).

## <a name="association-methods"></a>Métodos de associação
 Aplicativos como Web Parts de dados comerciais do SharePoint consomem associações chamando métodos na classe de serviço de uma entidade. Você pode adicionar métodos à classe de serviço de uma entidade selecionando-as no **Editor de associação**.

 Por padrão, o **Editor de associação** adiciona um método de navegação de associação às entidades de origem e de destino. Um método de navegação de associação na entidade de origem permite que os consumidores recuperem uma lista de entidades de destino. Um método de navegação de associação na entidade de destino permite que os consumidores recuperem a entidade de origem relacionada a uma entidade de destino.

 Você deve adicionar o código a cada um desses métodos para retornar as informações apropriadas. Você também pode adicionar outros tipos de métodos para dar suporte a cenários mais avançados. Para obter mais informações sobre cada um desses métodos, consulte [operações com suporte](/previous-versions/office/developer/sharepoint-2010/ee557363(v=office.14)).

## <a name="types-of-associations"></a>Tipos de associações
 Você pode criar dois tipos de associações no designer do BDC: associações baseadas em chave estrangeira e associações de chaves estrangeiras externas.

### <a name="foreign-key-based-association"></a>Associação baseada em chave estrangeira
 Você pode criar uma associação baseada em chave estrangeira relacionando um identificador na entidade de origem aos descritores de tipo definidos na entidade de destino. Essa relação permite que os consumidores do modelo forneçam uma interface do usuário aprimorada para seus usuários. Por exemplo, um formulário no Outlook que permite que um usuário crie um pedido de vendas que possa exibir clientes em uma lista suspensa; ou uma lista de pedidos de vendas no SharePoint que permite aos usuários abrir uma página de perfil para um cliente.

 Para criar uma associação baseada em chave estrangeira, os identificadores relacionados e os descritores de tipo que compartilham o mesmo nome e tipo. Por exemplo, você pode criar uma associação baseada em chave estrangeira entre uma `Contact` entidade e uma `SalesOrder` entidade. A `SalesOrder` entidade retorna um `ContactID` descritor de tipo como parte do parâmetro de retorno do localizador ou métodos de localizador específicos. Os dois descritores de tipo aparecem no **Editor de associação**. Para criar uma relação baseada em chave estrangeira entre a `Contact` entidade e a `SalesOrder` entidade, escolha o `ContactID` identificador ao lado de cada um desses campos.

 Adicione código ao método de navegador de associação da entidade de origem que retorna uma coleção de entidades de destino. O exemplo a seguir retorna os pedidos de vendas de um contato.

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet7":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet7":::

 Adicione código ao método de navegador de associação da entidade de destino que retorna uma entidade de origem. O exemplo a seguir retorna o contato relacionado à ordem de venda.

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs" id="Snippet8":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb" id="Snippet8":::

### <a name="foreign-keyless-association"></a>Associação de subunidade estrangeira
 Você pode criar uma associação sem identificadores de mapeamento para descritores de tipo de campo. Crie esse tipo de associação quando a entidade de origem não tiver uma relação direta com a entidade de destino. Por exemplo, uma `SalesOrderDetail` tabela não tem uma chave estrangeira que mapeia para uma chave primária em uma `Contact` tabela.

 Se você quiser exibir informações na `SalesOrderDetail` tabela relacionada a um `Contact` , você poderá criar uma associação de um subunidade externo entre a `Contact` entidade e a `SalesOrderDetail` entidade.

 No método de navegação de associação da `Contact` entidade, retorne as `SalesOrderDetail` entidades Unindo tabelas ou chamando um procedimento armazenado.

 O exemplo a seguir retorna detalhes de todas as ordens de venda Unindo tabelas.

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet9":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet9":::

 No método de navegação de associação da `SalesOrderDetail` entidade, retorne o relacionado `Contact` . O exemplo a seguir demonstra isso.
                                                                            
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet10":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet10":::

## <a name="see-also"></a>Confira também
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
- [Como: criar uma associação entre entidades](../sharepoint/how-to-create-an-association-between-entities.md)
