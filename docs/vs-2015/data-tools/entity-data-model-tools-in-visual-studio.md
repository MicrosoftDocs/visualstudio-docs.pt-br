---
title: Ferramentas do Visual Studio de modelo de dados de entidade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8a3fffb36d7070701b99382c320e3a2d23b9a2b8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49893390"
---
# <a name="entity-data-model-tools-in-visual-studio"></a>Ferramentas de modelo de dados de entidade no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Entity Framework é uma tecnologia de mapeamento relacional de objeto que permite aos desenvolvedores de .NET trabalhar com dados relacionais usando objetos específicos de domínio. Elimina a necessidade da maioria do código de acesso a dados que os desenvolvedores geralmente precisam gravar. O Entity Framework é o mapeamento relacional de objeto recomendado (ORM) tecnologia para novos aplicativos do .NET de modelagem.  
  
 A partir de março de 2016, é a versão lançada mais recente [Entity Framework 6](https://msdn.microsoft.com/data/ef) . [Entity Framework 7](https://docs.efproject.net/en/latest/) está em pré-lançamento.  
  
 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] Ferramentas foram projetadas para ajudar você a criar [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] aplicativos. Para obter a documentação completa [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ferramentas está aqui: [Entity Framework](https://msdn.microsoft.com/data/jj590134).  
  
 Com o [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ferramentas, você pode criar um *modelo conceitual* de uma já existente de banco de dados e, em seguida, graficamente visualizar e editar seu modelo conceitual. Ou, você pode criar graficamente um modelo conceitual primeiro e, em seguida, gerar um banco de dados que dá suporte a seu modelo. Em ambos os casos, você pode atualizar automaticamente seu modelo quando subjacente alterações de banco de dados e gerar automaticamente o código da camada de objeto para o seu aplicativo. Geração de banco de dados e geração de código da camada de objeto são personalizáveis.  
  
 Estas são as ferramentas específicas que constituem ferramentas de modelo de dados de entidade no Visual Studio 2015:  
  
- Você pode usar o [!INCLUDE[vstecado](../includes/vstecado-md.md)]  **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] Designer** (**Entity Designer**) para criar visualmente e modificar entidades, associações, mapeamentos e relações de herança. O **Entity Designer** também gera [!INCLUDE[TLA#tla_cshrp](../includes/tlasharptla-cshrp-md.md)] ou [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] código da camada de objeto.  
  
- Você pode usar o  **[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] assistente** para gerar um modelo conceitual de um banco de dados existente e adicionar informações de conexão de banco de dados ao seu aplicativo.  
  
- Você pode usar o **Assistente para criação de banco de dados** para criar um modelo conceitual primeiro e, em seguida, criar um banco de dados que oferece suporte ao modelo.  
  
- Você pode usar o **Assistente de atualização de modelo** para atualizar seu modelo conceitual, o modelo de armazenamento e a mapeamentos de quando foram feitas alterações no banco de dados subjacente.  
  
  > [!NOTE]
  >  Começando com o Visual Studio 2010, [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] as ferramentas não suportam [!INCLUDE[ss2k](../includes/ss2k-md.md)].  
  
  As ferramentas de geram ou modificar um arquivo. edmx. Esse arquivo contém informações que descrevem o modelo conceitual, o modelo de armazenamento e os mapeamentos entre eles. Para obter mais informações, consulte [EDMX](https://msdn.microsoft.com/data/jj650889.aspx).  
  
  Entity Framework Power Tools ajudam você a criar aplicativos que usam o modelo de dados de entidade. As ferramentas podem gerar um modelo conceitual, validar um modelo existente, produzir arquivos de código-fonte que contêm classes de objeto com base no modelo conceitual e produzem arquivos de código-fonte que contêm modos de exibição que gera o modelo. Para obter informações detalhadas, consulte [modos de exibição de mapeamento Pre-Generated](https://msdn.microsoft.com/data/dn469601.aspx).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Entity Framework do ADO.NET](http://msdn.microsoft.com/library/a437041f-6899-4ae7-96ce-aabf528d7205)|Descreve como usar [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ferramentas, que [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] fornece para criar aplicativos.|  
|[Modelo de Dados de Entidade](http://msdn.microsoft.com/library/2dda3d5b-4582-4ba0-a91d-fcd7a1498137)|Fornece links e informações sobre como trabalhar com dados que são usados por aplicativos criados no [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)].|  
|[Introdução ao .NET completo (Console, WinForms, WPF etc.)](https://docs.efproject.net/en/latest/platforms/full-dotnet/getting-started.html)|Fornece tutoriais sobre como criar aplicativos de área de trabalho do .NET que usam o Entity Framework 7.|  
|[O ASP.NET 5 aplicativo para o novo banco de dados](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html)|Descreve como criar um novo aplicativo ASP.NET 5 usando o Entity Framework 7.|  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)

