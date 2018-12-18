---
title: Criando definições de Site do SharePoint | Microsoft Docs
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
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0e43cfa7c9fa78722639053c572280cbaad912bf
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36325336"
---
# <a name="create-site-definitions-for-sharepoint"></a>Criar definições de site do SharePoint
  O projeto de definição de Site do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] permite que você crie uma *definição de site*, que serve como base para um novo site do SharePoint. Essas definições não apenas determinam a aparência e comportamento de site do SharePoint, mas também seu conteúdo padrão e funcionalidade. Na definição, você pode colocar pré-configurada listas, tipos de conteúdo, receptores de eventos, imagens e outros itens. O SharePoint inclui algumas definições de site, como de BLOG, por exemplo. Quando você cria um site com base na definição do site BLOG, o site contém as listas, Web parts e outros itens que exige que um site de blog.  
  
 Para obter mais informações sobre definições de site, consulte [modelos de Site e definições](http://go.microsoft.com/fwlink/?LinkId=179134).  
  
## <a name="site-definition-projects"></a>Projetos de definição de site
 Projetos de definição de site [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fornecer apenas os arquivos básicos que precisa de um site do SharePoint; eles não fornecem nenhuma funcionalidade padrão. Você deve adicionar os arquivos e conteúdo para fornecer a funcionalidade que você deseja. Você pode criar o site manualmente, criando e adicionando os arquivos que você precisa.  
  
## <a name="feature-stapling"></a>Grampeamento do recurso
 Um dos benefícios da criação de definições de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] é que eles usam automaticamente *grampeamento do recurso*. Grampeamento do recurso anexa um recurso a uma definição de site em vez de inserir sua funcionalidade na definição de site em si. Fazer isso permite que você adicionar o recurso para qualquer site criado usando a definição de site sem modificar a definição do site original. Para obter mais informações, consulte [grampeamento do recurso](http://go.microsoft.com/fwlink/?LinkID=119283).  
  
## <a name="site-definition-project-components"></a>Componentes de projeto de definição de site
 Quando você cria uma solução de definição de site, os arquivos de padrão a seguir são adicionados ao seu **SiteDefinition** nó.  
  
|Nome do Arquivo|Descrição|  
|---------------|-----------------|  
|*Default. aspx*|Página inicial à página ASPX padrão para o novo site do SharePoint.|  
|*onet*|Especifica a configuração do novo site, os componentes do modelo de definição de site e o comportamento padrão. Essas configurações podem incluir atributos como os tipos de conteúdo que estiverem habilitados, modos de exibição de lista padrão, arquivos de modelo de documento e Web parts incluídas com o site. Por padrão, o `Modules` seção lista os arquivos a serem adicionados ao site do SharePoint e como eles são configurados.|  
|*webtemp_\<SiteDefinitionName >. XML*|Especifica as configurações de definição de site que aparece na **seleção de modelo** seção o **novo Site do SharePoint** página.|  
  
 Por padrão, todas as definições de site são armazenadas na  *\<unidade: > \Program Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates* pasta. Cada definição de site tem sua própria subpasta.  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Passo a passo: criar um projeto de definição de site básico](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|Orienta você passo a passo durante a criação de um projeto de definição de site básico em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].|  
|[Como: criar uma definição de Site personalizada e configuração](http://go.microsoft.com/fwlink/?LinkId=183309)|Descreve como criar uma definição de site personalizada no SharePoint, copiando uma definição de site existente e, em seguida, modificar a cópia.|  
|[*Webtemp*](http://go.microsoft.com/fwlink/?LinkId=183310)|Descreve o arquivo original que especifica as definições de site disponíveis na **seleção de modelo** seção o **novo Site do SharePoint** página.|  
|[Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)|Descreve como preparar suas soluções do SharePoint para uso global.|  
|[Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)|Descreve como você pode criar partes de uma página do SharePoint que os usuários podem modificar.|  
|[Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|Descreve como você pode criar controles reutilizáveis que são executados em páginas de aplicativos e Web Parts.|  
|[Visual Web Developer](http://go.microsoft.com/fwlink/?LinkId=178725)|Descreve como usar o designer que aparece quando você abre uma página da Web em seu projeto.|  
|[Visão geral de páginas da Web do ASP.NET](http://go.microsoft.com/fwlink/?LinkId=178726)|Fornece informações gerais sobre a estrutura de [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas da Web, como as páginas são processadas pelo [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]e como [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] as páginas exibidas a marcação que está em conformidade com padrões XHTML.|  
|[Sintaxe de página da Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=178727)|Descreve os elementos de marcação que compõem uma página ASP.NET.|  
|[Páginas da Web ASP.NET de programação](http://go.microsoft.com/fwlink/?LinkId=178728)|Fornece informações sobre como criar manipuladores de eventos em [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas e como trabalhar com o script de cliente.|  
|[Programação no Windows SharePoint Services](http://go.microsoft.com/fwlink/?LinkId=178729)|Descreve como usar o modelo de objeto gerenciado que é fornecido no [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)].|  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
 
