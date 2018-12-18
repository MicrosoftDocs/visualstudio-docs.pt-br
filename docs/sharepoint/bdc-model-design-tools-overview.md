---
title: Visão geral das ferramentas de Design de modelo BDC | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Method_Details
- VS.SharePointTools.BDC.Explorer
- VS.SharePointTools.BDC.Diagram
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], method details
- Business Data Connectivity service [SharePoint development in Visual Studio], designer
- Business Data Connectivity service [SharePoint development in Visual Studio], method details
- BDC [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], designer
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6c5a799a245d2149161809977446d0c005dbe293
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914496"
---
# <a name="bdc-model-design-tools-overview"></a>Visão geral de ferramentas de design de modelo BDC
  Você pode criar um modelo de conectividade de dados comerciais (BDC) usando o Designer de BDC, o **detalhes do método BDC** janela e o **BDC Explorer**.  
  
 O **BDC Explorer** lhe permite procurar o modelo, o modelo de pesquisa e definir os descritores de tipo.  
  
## <a name="bdc-designer"></a>Designer de BDC
 O Designer de BDC permite que você definir as entidades em seu modelo e organizar visualmente suas relações uns com os outros. Use o Designer de BDC para realizar as seguintes tarefas:  
  
- Adicione entidades no modelo.  
  
- Remova entidades do modelo.  
  
- Defina relações entre entidades.  
  
  Para abrir o Designer de BDC, duas vezes no arquivo de modelo em seu projeto, ou abra o menu de atalho para o arquivo de modelo e, em seguida, escolha **abrir**. Adicionar uma entidade no modelo arrastando ou copiando uma **Entity** da **caixa de ferramentas** para o designer. Para criar uma associação entre duas entidades, escolha o **associação** no controlar as **caixa de ferramentas**, escolha a primeira entidade e, em seguida, escolha a segunda entidade.  
  
## <a name="bdc-method-details-window"></a>Janela de detalhes do método BDC
 Use o **detalhes do método BDC** janela para definir os parâmetros, instâncias e descritores de um método de filtro.  
  
 Você pode gerar rapidamente os métodos Finder, localizador específico, criador, Updater e agente de exclusão na **detalhes do método BDC** janela. Quando você gera esses métodos, o Visual Studio adiciona metadados, como parâmetros, instâncias e descritores de tipo para o método. Você pode modificar esses metadados para satisfazer seu cenário específico.  
  
 Para abrir o **detalhes do método BDC** janela, na barra de menus, escolha **exibição** > **Other Windows** > **detalhes do método BDC** .  
  
 Para exibir os métodos de **detalhes do método BDC** janela, escolha a entidade no Designer de BDC. Os métodos da entidade selecionada aparecem na **detalhes do método BDC** janela. Se você não escolher uma entidade no Designer de BDC, o **detalhes do método BDC** janela não exibe nenhuma informação.  
  
 Expandir ou recolher nós os **detalhes do método BDC** janela para definir parâmetros, instâncias e descritores de filtro. Use o **BDC Explorer** para definir os descritores de tipo.  
  
## <a name="bdc-explorer"></a>BDC Explorer
 O **BDC Explorer** exibe os elementos que compõem o modelo. Para abrir o **BDC Explorer**, na barra de menus, escolha **exibição** > **Other Windows** > **BDC Explorer**. Para procurar o modelo, expanda os nós na **BDC Explorer**. Cada nó representa um elemento no XML do arquivo de modelo.  
  
 Conforme você escolher nós na **BDC Explorer**, as propriedades de cada nó que você escolher aparecem na **propriedades** janela. Muitas dessas propriedades correspondem aos atributos no arquivo de modelo. Você pode pesquisar o modelo, usando a caixa de pesquisa na parte superior do **BDC Explorer**.  
  
> [!NOTE]  
>  O **BDC Explorer** não exibe identificadores, propriedades personalizadas, cadeias de caracteres localizadas, grupos de associação, ações, os descritores de filtro, listas de controle de ação e valores de parâmetro padrão.  
  
### <a name="define-type-descriptors"></a>Defina os descritores de tipo
 Use o **BDC Explorer** para definir os descritores de tipo. O BDC Explorer permite que você definir um descritor de tipo de uma vez e, em seguida, reutilizar esse descritor de tipo em outro lugar no seu modelo. Para fazer isso, um descritor de tipo de copiar e colá-la em qualquer outro parâmetro ou descritor de tipo.  
  
> [!NOTE]  
>  As alterações a um descritor de tipo original não afetam as cópias desse descritor de tipo.  
  
 Para obter mais informações, consulte [como: definir o descritor de tipo de um parâmetro](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: criar um modelo BDC](../sharepoint/how-to-create-a-bdc-model.md)   
 [Como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md)   
 [Como: adicionar um método Finder](../sharepoint/how-to-add-a-finder-method.md)   
 [Como: adicionar um método Finder específico](../sharepoint/how-to-add-a-specific-finder-method.md)   
 [Como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md)   
 [Como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md)   
 [Como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md)   
 [Criar uma associação entre entidades](../sharepoint/creating-an-association-between-entities.md)   
 [Passo a passo: Criar uma lista externa no SharePoint usando dados corporativos](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)   
 [Integre dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)   
 [Criando um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)   
 [Criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)  
  
 
