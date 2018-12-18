---
title: Criando páginas para o SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, master pages
- SharePoint development in Visual Studio, page layouts
- SharePoint development in Visual Studio, content pages
- master pages[SharePoint development in Visual Studio], designing
- content pages[SharePoint development in Visual Studio], designing
- page layouts[SharePoint development in Visual Studio], designing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ecdbde69735f548b7ab70da132e9e2cc2080bbcb
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36326044"
---
# <a name="create-pages-for-sharepoint"></a>Criar páginas do SharePoint
  Você pode criar páginas de aplicativos, páginas do site, páginas mestras e layouts de página para um site do SharePoint.  
  
 Você pode criar páginas de aplicativo usando um modelo no Visual Studio. Crie páginas do site, páginas mestras e layouts de página, usando o SharePoint Designer. Em seguida, você pode importar essas páginas para o Visual Studio para usá-los em um projeto do SharePoint.  
  
 Você também pode modificar a aparência e comportamento de páginas usando as folhas de estilo em cascata, ECMAScript e temas.  
  
## <a name="types-of-sharepoint-pages"></a>Tipos de páginas do SharePoint
 A tabela a seguir descreve os quatro tipos principais de páginas que contém um site do SharePoint.  
  
|Tipo de página|Descrição|  
|---------------|-----------------|  
|Páginas de aplicativo|Crie uma página de aplicativo se você deseja que a página contêm código personalizado ou se desejar que a página seja compartilhado entre vários sites. Caso contrário, uma página de site pode ser a melhor opção.|  
|Páginas do site|Crie uma página do site se você quiser executar qualquer uma das seguintes tarefas:<br /><br /> -Adicione a página em uma biblioteca do SharePoint.<br />-Habilite a página de recursos de host como dinâmico de Web Parts e zonas de Web Parts.<br />-Habilite os usuários personalizem a página usando o SharePoint Designer.<br /><br /> Não crie uma página do site se você deseja que a página contêm código personalizado. Embora você possa adicionar código personalizado para uma página do site, o código de execução é interrompida quando o usuário personalizar a página usando o SharePoint Designer.|  
|Páginas mestras|Crie uma página mestra, se você quiser definir uma estrutura comum para páginas de sites e páginas de aplicativo.|  
|Layouts de página|Layouts de página são específicos para [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] e permitem que você definir mais de uma estrutura comum para páginas de sites e páginas de aplicativo.|  
  
 Para obter uma visão geral de cada tipo de página, consulte [bloco de construção: páginas e a Interface do usuário](http://go.microsoft.com/fwlink/?LinkID=182095), e [Layouts de página e páginas mestras](http://go.microsoft.com/fwlink/?LinkID=182096).  
  
## <a name="create-application-pages"></a>Criar páginas de aplicativo
 Você pode criar páginas de aplicativo no Visual Studio, adicionando um **página de aplicativo** item a um projeto do SharePoint. Você pode adicionar controles à página e, em seguida, manipular eventos de controle, adicionando código.  
  
 Você pode definir pontos de interrupção no arquivo de código da página, inicie o depurador e testar a página em um site do SharePoint local sem executar etapas adicionais de configuração. Para obter mais informações, consulte [criando páginas de aplicativo para SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).  
  
## <a name="create-site-pages-master-pages-and-page-layouts"></a>Criar páginas do site, páginas mestras e layouts de página
 Você pode criar páginas do site, páginas mestras e layouts de página, usando o SharePoint Designer. Em seguida, você pode importar essas páginas no Visual Studio. Importe suas páginas se você quiser tirar proveito da implantação ou recursos de controle do código-fonte que estão disponíveis no Visual Studio. Para obter mais informações, consulte [importação de itens de um Site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md).  
  
 Como é difícil de modificar essas páginas após a importação, você deve projetar essas páginas antes de importá-los.  
  
## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>Criar temas, ECMAScript e folhas de estilo em cascata
 Visual Studio fornece modelos para desenvolver folhas de estilo em cascata (CSS), ECMAScript (JavaScript, JScript) ou arquivos de tema para sites do SharePoint. Você pode criar esses arquivos usando as orientações disponíveis no SDK do SharePoint ou usando ferramentas como o SharePoint Designer.  
  
 Você pode adicionar esses arquivos à sua solução, diretamente ou você pode importá-los. Em ambos os casos, você deve criar as pastas mapeadas apropriadas para cada item que você adicionar. Para obter mais informações sobre como criar uma pasta mapeada, consulte [como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).  
  
 Para obter mais informações sobre a criação de folhas de estilo em cascata, consulte [em cascata uso classe de folhas de estilo no SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkID=182098). Para obter mais informações sobre como criar arquivos JavaScript e JScript para uma solução do SharePoint, consulte [configuração de backup de um ASPX página básica para ECMAScript](http://go.microsoft.com/fwlink/?LinkID=182099). Para obter mais informações sobre temas, consulte [bloco de construção: páginas e a Interface do usuário](http://go.microsoft.com/fwlink/?LinkID=182095).  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Criar páginas de aplicativo do SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)|Descreve como adicionar páginas de aplicativos: *. aspx* conteúdo que será mesclado com uma página mestra do SharePoint.|  
|[Como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md)|Mostra como criar páginas ASP.NET que são executados em um site do SharePoint.|  
|[Passo a passo: Criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|Mostra como criar e depurar uma página da Web do ASP.NET para um site do SharePoint.|  
  
