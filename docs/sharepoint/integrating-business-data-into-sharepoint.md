---
title: Integrando dados corporativos ao SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
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
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b4bbfb681a0dac0825bf7af4f1f27ab1c1b50053
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016306"
---
# <a name="integrate-business-data-into-sharepoint"></a>Integre dados corporativos ao SharePoint
  Você pode integrar dados corporativos ao SharePoint. Os dados de negócios podem vir de aplicativos de servidor back-end, como o [!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)] Siebel e o SAP, ou um serviço Web. Os usuários podem exibir, adicionar, atualizar ou excluir dados corporativos usando listas externas ou Web Parts de dados corporativos no SharePoint.  Os usuários também podem acessar esses dados offline em um aplicativo Microsoft Office, como o Microsoft Outlook. Para obter mais informações, consulte [onde você pode mostrar dados externos](/previous-versions/office/developer/sharepoint-2010/ee558737(v=office.14)).

 Para integrar dados no SharePoint, crie um modelo para o serviço corporativo de conectividade de dados (BDC). O serviço do BDC é um aplicativo no SharePoint que armazena informações sobre dados em aplicativos de negócios. Para obter mais informações, consulte [serviço corporativo de conectividade de dados (BDC)](/previous-versions/office/developer/sharepoint-2010/ee556407(v=office.14)).

## <a name="models-in-visual-studio"></a>Modelos no Visual Studio
 Os modelos no Visual Studio permitem que você escreva código personalizado para recuperar e atualizar dados de fontes de dados de back-end. Você também pode agregar dados de várias fontes de dados. Por exemplo, você pode exibir uma lista de clientes que contêm dados de um [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] banco de dado e um serviço Web.

 Você também pode importar modelos que já foram implantados no SharePoint. Depois de importar um modelo, você pode adicionar código personalizado ou apenas usar o Visual Studio para empacotar e implantar o modelo em vários farms de servidores do SharePoint. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md).

## <a name="design-a-model-in-visual-studio"></a>Criar um modelo no Visual Studio
 Você pode criar um modelo usando um designer e várias janelas de ferramentas. À medida que você cria o modelo, o Visual Studio gera o modelo XML. Para obter mais informações, consulte [visão geral das ferramentas de design de modelo do BDC](../sharepoint/bdc-model-design-tools-overview.md).

 Um modelo contém entidades e métodos.

### <a name="entities"></a>Entidades
 Uma entidade descreve uma coleção de campos. Por exemplo, uma entidade pode representar uma tabela em um banco de dados. Uma entidade aparece como um tipo de conteúdo externo no SharePoint. Para obter mais informações sobre tipos de conteúdo externo, consulte [o que são tipos de conteúdo externo?](/previous-versions/office/developer/sharepoint-2010/ee556391(v=office.14))

### <a name="methods"></a>Métodos
 Um método permite que os consumidores de um tipo de conteúdo externo executem uma ação nos campos de uma entidade. Por exemplo, um método de atualizador pode permitir que os usuários alterem o endereço e a data de nascimento de um cliente onde `Address` e `BirthDate` são os campos da `Customer` entidade.

 O Visual Studio gera um arquivo de código de serviço para cada entidade em seu modelo. Quando você adiciona um método ao seu modelo, o Visual Studio gera um método correspondente no arquivo de código de serviço. Adicione código a cada método para executar a tarefa apropriada. Por exemplo, se você adicionar um método de criador ao modelo, o Visual Studio gerará um método de criador em seu arquivo de código de serviço. Esse método é chamado pelo serviço BDC quando um usuário clica no botão **novo item** em uma lista com base no modelo. Portanto, adicione o código ao método Creator que adiciona novos dados a uma fonte de dados. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)|Mostra como criar um novo modelo ou importar um modelo que você exporta do SharePoint.|
|[Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)|Explica como projetar os elementos de um modelo usando as ferramentas de design do Visual Studio.|
|[Quando usar o SharePoint Designer versus o Visual Studio ao criar soluções usando o BCS](/previous-versions/office/developer/sharepoint-2010/ee558875(v=office.14))|Ajuda a decidir se deseja usar o Visual Studio ou usar o SharePoint Designer para criar um modelo para o BDC.|
