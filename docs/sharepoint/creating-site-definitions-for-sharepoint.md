---
title: Criando definições de site para o SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0f1a512218c3c1b7af179cfaba3e231a90941fe0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015058"
---
# <a name="create-site-definitions-for-sharepoint"></a>Criar definições de site para o SharePoint
  O projeto de definição de site do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] permite que você crie uma *definição de site*, que serve como base para um novo site do SharePoint. Essas definições não apenas determinam a aparência e o comportamento do site do SharePoint, mas também seu conteúdo e funcionalidade padrão. Na definição, você pode colocar listas pré-configuradas, tipos de conteúdo, receptores de eventos, imagens e outros itens. O SharePoint inclui algumas definições de site, como BLOG, por exemplo. Quando você cria um site com base na definição do site do BLOG, o site contém as listas, Web Parts e outros itens que um site de Blogs requer.

 Para obter mais informações sobre definições de site, consulte [definições e modelos de site](/previous-versions/office/developer/sharepoint-2010/ms434313(v=office.14)).

## <a name="site-definition-projects"></a>Projetos de definição de site
 Os projetos de definição de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fornecem apenas os arquivos básicos de que um site do SharePoint precisa; eles não fornecem nenhuma funcionalidade padrão. Você deve adicionar arquivos e conteúdo para fornecer a funcionalidade desejada. Você pode criar o site manualmente, criando e adicionando os arquivos necessários.

## <a name="feature-stapling"></a>Grampeamento de recursos
 Um benefício de criar definições de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] é que elas usam automaticamente o *grampeamento de recursos*. O grampeamento de recursos anexa um recurso a uma definição de site em vez de inserir sua funcionalidade na própria definição de site. Isso permite que você adicione o recurso a qualquer site criado usando a definição de site sem modificar a definição de site original. Para obter mais informações, consulte [grampeamento de recursos](/previous-versions/office/developer/sharepoint-2007/bb861862(v=office.12)).

## <a name="site-definition-project-components"></a>Componentes do projeto de definição de site
 Quando você cria uma solução de definição de site, os seguintes arquivos padrão são adicionados ao seu nó **SiteDefinition** .

|Nome do Arquivo|Descrição|
|---------------|-----------------|
|*default. aspx*|O home page ASPX padrão para o novo site do SharePoint.|
|*onet.xml*|Especifica a configuração do novo site, os componentes do modelo de definição de site e o comportamento padrão. Essas configurações podem incluir atributos como os tipos de conteúdo habilitados, as exibições de lista padrão, os arquivos de modelo de documento e as Web Parts incluídas no site. Por padrão, a `Modules` seção lista os arquivos a serem adicionados ao site do SharePoint e como eles são configurados.|
|*webtemp_ \<SiteDefinitionName> . xml*|Especifica as configurações de definição de site que aparecem na seção **seleção de modelo** da página **novo site do SharePoint** .|

 Por padrão, todas as definições de site são armazenadas na pasta * \<drive:> \Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates* Cada definição de site tem sua própria subpasta.

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Passo a passo: Criar um projeto de definição de site básico](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|O conduz passo a passo por meio da criação de um projeto básico de definição de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .|
|[Como criar uma definição e configuração de site personalizados](/previous-versions/office/developer/sharepoint-2010/ms454677(v=office.14))|Descreve como criar uma definição de site personalizada no SharePoint copiando uma definição de site existente e, em seguida, modificando a cópia.|
|[*WebTemp.xml*](/previous-versions/office/developer/sharepoint-2010/ms447717(v=office.14))|Descreve o arquivo original que especifica as definições de site disponíveis na seção **seleção de modelo** da página **novo site do SharePoint** .|
|[Localizar soluções do SharePoint](../sharepoint/localizing-sharepoint-solutions.md)|Descreve como preparar suas soluções do SharePoint para uso global.|
|[Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)|Descreve como você pode criar partes de uma página do SharePoint que os usuários podem modificar.|
|[Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|Descreve como você pode criar controles reutilizáveis que são executados em páginas de aplicativo e Web Parts.|
|[Visual Web Developer](/previous-versions/visualstudio/visual-studio-2010/ms178093(v=vs.100))|Descreve como usar o designer que aparece quando você abre uma página da Web em seu projeto.|
|[Visão geral de Páginas da Web do ASP.NET](/previous-versions/aspnet/428509ah(v=vs.100))|Fornece informações gerais sobre a estrutura de [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas da Web, como as páginas são processadas pelo [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] e como as [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas exibem a marcação que está em conformidade com os padrões XHTML.|
|[Sintaxe da página da Web do ASP.NET](/previous-versions/aspnet/k33801s3(v=vs.100))|Descreve os elementos de marcação que compõem uma página ASP.NET.|
|[Páginas da Web do ASP.NET de programação](/previous-versions/aspnet/0yt4zca8(v=vs.100))|Fornece informações sobre como criar manipuladores de eventos em [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] páginas e como trabalhar com o script de cliente.|
|[Programação no Windows SharePoint Services](/previous-versions/office/developer/sharepoint-services/ms430674(v=office.12))|Descreve como usar o modelo de objeto gerenciado que é fornecido no [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] .|

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
