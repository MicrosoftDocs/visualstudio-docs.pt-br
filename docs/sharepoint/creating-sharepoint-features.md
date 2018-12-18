---
title: Criando funcionalidades do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
- features [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 56bc4dbd50bedc15fcf6c69cbc334fe09c6094cc
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36325593"
---
# <a name="create-sharepoint-features"></a>Criar recursos do SharePoint
  Você pode usar um recurso do SharePoint para agrupar itens de projeto do SharePoint relacionados para facilitar a implantação. Você pode criar recursos, definir escopos e marcar outros recursos como dependências usando o Designer de recursos do SharePoint. O designer também gera um manifesto, que é um arquivo XML que descreve cada recurso.  
  
## <a name="add-features-to-the-sharepoint-solution"></a>Adicionar recursos à solução do SharePoint
 Você pode adicionar um recurso à solução do SharePoint usando o Gerenciador de soluções ou o Packaging Explorer. Você pode usar um dos métodos a seguir para adicionar um recurso.  
  
-   Na **Gerenciador de soluções**, abra o menu de atalho **recursos**e, em seguida, escolha **adicionar recurso**.  
  
-   Na **Packaging Explorer**, abra o menu de atalho para o pacote e, em seguida, escolha **adicionar recurso**.  
  
## <a name="using-the-feature-designer"></a>Usando o designer de recursos
 Uma solução do SharePoint pode conter um ou mais recursos do SharePoint, que são agrupadas sob o nó de recurso no Gerenciador de soluções. Cada recurso tem seu próprio **Designer de recursos** que você pode usar para personalizar as propriedades de recurso. Para obter mais informações, consulte [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md). Para diferenciar recursos uns dos outros, você pode configurar as propriedades de recurso, como o título, descrição, versão e escopo.  
  
### <a name="feature-designer-options"></a>Opções de designer de recursos
 Depois de criar um recurso, você pode usar o Designer de recursos para personalizá-lo.  
  
 A tabela a seguir descreve as propriedades de recurso que são exibidas no Designer de recurso.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|Título|Opcional. O título padrão do recurso é definido como *SolutionName* *FeatureName*.|  
|Descrição|Opcional. A descrição do recurso do SharePoint.|  
|Escopo|Necessário. Se um recurso é criado usando **Gerenciador de soluções**, o escopo é definido na Web por padrão.<br /><br /> -Farm: Ative um recurso para um farm de servidores inteiro.<br /><br /> -Site: Ative um recurso para todos os sites em um conjunto de sites.<br /><br /> -Web: Ative um recurso para um site específico.<br /><br /> -WebApplication: Ative um recurso para todos os sites da web em um aplicativo web.|  
|Itens da solução|Todos os itens do SharePoint que pode ser adicionado ao recurso.|  
|Itens no recurso|Os itens de projeto do SharePoint que foram adicionados ao recurso.|  
  
## <a name="add-and-remove-sharepoint-project-items"></a>Adicionar e remover itens de projeto do SharePoint
 Você pode selecionar quais itens de projeto do SharePoint que você deseja adicionar um recurso do SharePoint para implantação. Use o **Designer de recursos** adicionar e remover itens de recursos e exibir o manifesto de recurso. Para obter mais informações, consulte [como: adicionar e remover itens de recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md).  
  
## <a name="add-feature-dependencies"></a>Adicionar dependências de recurso
 Você pode configurar o manifesto de recurso para que o servidor do SharePoint ativa certos recursos antes que o recurso é ativado. Por exemplo, se seu recurso do SharePoint depende de outros recursos de funcionalidade ou dados, o servidor do SharePoint pode primeiro tentar ativar qualquer um dos recursos que seu recurso depende. Para obter mais informações, consulte [como: adicionar e remover dependências de recurso](../sharepoint/how-to-add-and-remove-feature-dependencies.md).  
  
## <a name="see-also"></a>Consulte também
 [Como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)   
 [Como: adicionar e remover itens de recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)   
 [Como: adicionar e remover dependências de recurso](../sharepoint/how-to-add-and-remove-feature-dependencies.md)  
  
  
