---
title: Integrando dados corporativos ao SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data
- BDC [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], business data
- Business Data Connectivity service [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], data
- BDC [SharePoint development in Visual Studio], data
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: e75367844a3a62e044a98f9d52c567fcfca3590e
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118543"
---
# <a name="integrate-business-data-into-sharepoint"></a>Integre dados corporativos no SharePoint
  Você pode integrar dados de negócios no SharePoint. Dados de negócios podem vir de aplicativos de servidor back-end, como [!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)], Siebel e SAP, ou um serviço Web. Os usuários podem exibir, adicionar, atualizar ou excluir dados de negócios usando listas externas ou Web Parts de dados de negócios no SharePoint.  Usuários também podem acessar esses dados offline em um aplicativo do Microsoft Office, como o Microsoft Outlook. Para obter mais informações, consulte [onde pode você mostrar dados externos](http://go.microsoft.com/fwlink/?LinkId=169295).  
  
 Para integrar dados ao SharePoint, crie um modelo para o serviço de conectividade de dados comerciais (BDC). O serviço de BDC é um aplicativo no SharePoint que armazena informações sobre os dados em aplicativos de negócios. Para obter mais informações, consulte [serviço de conectividade de dados comerciais (BDC)](http://go.microsoft.com/fwlink/?LinkID=169276).  
  
## <a name="models-in-visual-studio"></a>Modelos no Visual Studio  
 Modelos no Visual Studio permitem que você escrever código personalizado para recuperar e atualizar dados de fontes de dados back-end. Você também pode agregar dados de várias fontes de dados. Por exemplo, você pode exibir uma lista de clientes que contém dados de um [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] banco de dados e um serviço Web.  
  
 Você também pode importar modelos que já foram implantados no SharePoint. Depois de importar um modelo, você pode adicionar código personalizado ou usar apenas o Visual Studio para empacotar e implantar o modelo em vários farms de servidores do SharePoint. Para obter mais informações, consulte [criar um modelo de conectividade de dados de negócios](../sharepoint/creating-a-business-data-connectivity-model.md).  
  
## <a name="design-a-model-in-visual-studio"></a>Criar um modelo no Visual Studio
 Você pode criar um modelo usando um designer e várias janelas de ferramentas. Ao projetar o modelo, o Visual Studio gera o modelo XML. Para obter mais informações, consulte [visão geral das ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md).  
  
 Um modelo contém entidades e métodos.  
  
### <a name="entities"></a>Entidades  
 Uma entidade descreve uma coleção de campos. Por exemplo, uma entidade pode representar uma tabela em um banco de dados. Uma entidade é exibido como um tipo de conteúdo externo no SharePoint. Para obter mais informações sobre tipos de conteúdo externo, consulte [quais são os tipos de conteúdo externos?](http://go.microsoft.com/fwlink/?LinkId=169293)  
  
### <a name="methods"></a>Métodos  
 Um método permite que os consumidores de um tipo de conteúdo externo para executar uma ação nos campos de uma entidade. Por exemplo, um método Updater pode permitir que os usuários alterar o endereço e a data de um cliente de nascimento onde `Address` e `BirthDate` são os campos do `Customer` entidade.  
  
 Visual Studio gera um arquivo de código de serviço para cada entidade em seu modelo. Quando você adiciona um método ao seu modelo, o Visual Studio gera um método correspondente no arquivo de código de serviço. Adicione código para cada método para executar a tarefa apropriada. Por exemplo, se você adicionar um método Creator para o modelo, o Visual Studio gera um método Creator em seu arquivo de código de serviço. Esse método é chamado pelo serviço de BDC, quando um usuário clica o **Novo Item** botão em uma lista que é baseada no modelo. Portanto, adicione código ao método criador que adiciona novos dados a uma fonte de dados. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)|Mostra como criar um novo modelo ou importar um modelo que você exportar do SharePoint.|  
|[Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)|Explica como os elementos de um modelo de design usando ferramentas de design do Visual Studio.|  
|[Quando usar o SharePoint Designer vs. Soluções do Visual Studio quando criamos usando o BCS](http://go.microsoft.com/fwlink/?LinkID=183448)|Ajuda a decidir se deseja usar o Visual Studio ou usar o SharePoint Designer para criar um modelo para o BDC.|  
  
