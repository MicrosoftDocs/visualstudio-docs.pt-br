---
title: Criar um modelo de conectividade de dados de negócios | Microsoft Docs
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
- Business Data Connectivity service [SharePoint development in Visual Studio], model
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- SharePoint development in Visual Studio, Business Data Connectivity service
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 68940d6e48f1f3a3e51017e1cc838976735de104
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49930200"
---
# <a name="create-a-business-data-connectivity-model"></a>Criar um modelo de conectividade de dados corporativos
  Você pode criar um modelo de conectividade de dados comerciais (BDC) ou personalizar um modelo BDC existente usando o Visual Studio. Cada projeto do SharePoint pode conter apenas um modelo. Para obter mais informações, consulte [Integre dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md).  
  
## <a name="create-a-new-model"></a>Criar um novo modelo
 Para criar um novo modelo, crie um **modelo de conectividade de dados corporativos** do projeto ou adicione um **modelo de conectividade de dados corporativos** item a um **projeto vazio do SharePoint**.  
  
> [!NOTE]  
>  Você deve ter [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] instalado em seu computador.  
  
 Visual Studio adiciona uma pasta para o projeto. Esta pasta tem o nome que você especificar para o **modelo de conectividade de dados corporativos** item o **Adicionar Novo Item** caixa de diálogo. Se você criar um novo **modelo de conectividade de dados corporativos** nomes de projeto, o Visual Studio na pasta **BdcModel1**.  
  
 Visual Studio adiciona os seguintes arquivos para a nova pasta:  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|Arquivo de definição de modelo|Contém XML que define as entidades, métodos, objetos do sistema de linha de negócios (LOB) e outros metadados que descreve o modelo.<br /><br /> Modificar os metadados nesse arquivo usando o Designer de BDC **BDC Explorer**, **detalhes do método BDC** janela, e **propriedades** janela.|  
|Arquivo de código do serviço de entidade|Contém métodos que recuperam, atualizar e excluir instâncias da entidade padrão.|  
  
 Para definir as propriedades de uma entidade, edite o arquivo de código de entidade. Para obter mais informações, consulte [como: adicionar uma entidade a um modelo](../sharepoint/how-to-add-an-entity-to-a-model.md).  
  
 Para recuperar, atualizar e excluir instâncias de uma entidade, adicione código ao arquivo de código do serviço de entidade. Para obter mais informações, consulte [criando um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).  
  
 Quando você compila o projeto, o Visual Studio cria um assembly. Certifique-se de que você não adicione outros itens para o projeto que adicione código ao assembly do projeto (por exemplo: uma **fluxo de trabalho sequencial** item ou uma **Web Part** item). O código para esse item não será executado quando você implanta a solução porque o pacote de solução não copia o assembly no cache de assembly global.  O pacote de solução implanta o assembly para o BDC somente banco de dados no SharePoint.  
  
> [!NOTE]  
>  Visual Studio copia o assembly em ambos os locais em seu computador local quando você depura o projeto.  
  
## <a name="add-an-existing-model"></a>Adicionar um modelo existente
 Você pode importar um modelo que foi criado usando outras ferramentas como o SharePoint Designer. Você pode optar por importar um modelo existente ao seu projeto nas seguintes situações:  
  
- Para personalizar um modelo que já é implantado em um farm de servidores do SharePoint.  
  
- Para empacotar e implantar um modelo existente em vários farms de servidores do SharePoint.  
  
  Em ambos os casos, os sistemas LOB definidos no modelo que você importar não são afetados em continuarão a funcionar conforme o esperado. Para adicionar um modelo existente para um projeto do SharePoint, use o Visual Studio **Add Existing Item** caixa de diálogo. Para obter mais informações, consulte [como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md).  
  
  Você pode adicionar um sistema LOB do assembly do tipo .NET Framework para o modelo importado selecionando uma opção na **LobSystem de assembly .NET adicionar**. Isso permite que você escreva código personalizado e usar um designer para definir os metadados para o modelo importado.  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Como: criar um modelo BDC](../sharepoint/how-to-create-a-bdc-model.md)|Mostra como criar um novo modelo BDC.|  
|[Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|Mostra como importar um modelo existente para um projeto do SharePoint.|  
|[Como: usar um arquivo de recurso para especificar nomes localizados, propriedades e permissões](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|Descreve como fornecer cadeias de caracteres que são mescladas com os metadados de modelo quando o modelo é consumido por um Web Part ou página da Web.|  
|[Como: incluir um assembly personalizado em uma recurso BDC](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|Mostra como incluir um assembly personalizado no recurso.|  
  
 
