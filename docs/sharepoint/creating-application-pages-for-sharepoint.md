---
title: Criando páginas de aplicativo do SharePoint | Microsoft Docs
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
- SharePoint development in Visual Studio, Web pages
- SharePoint development in Visual Studio, content pages
- SharePoint development in Visual Studio, application pages
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5f1c3b03507ca97724106c6ca1d121b3c54eb659
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853136"
---
# <a name="create-application-pages-for-sharepoint"></a>Criar páginas de aplicativo do SharePoint
  Uma *página de aplicativo* é uma página da Web do ASP.NET que foi projetada para uso em um site do SharePoint. Páginas de aplicativo são um tipo especializado de página ASP.NET. A principal diferença entre uma página de aplicativo e uma página ASP.NET padrão é que uma página de aplicativo contém o conteúdo que será mesclado com uma página mestra do SharePoint. Uma página mestra permite que as páginas de aplicativos que compartilham a mesma aparência e comportamento como outras páginas em um site.  
  
 Visual Studio permite criar páginas de aplicativo usando um designer. O designer exibe uma área de conteúdo para cada espaço reservado para conteúdo que é definido em uma página mestra. Você pode criar a página de aplicativo, arrastando controles para essas áreas de conteúdo.  
  
## <a name="application-pages"></a>Páginas de aplicativo
 Páginas de aplicativo são compartilhadas entre todos os sites no servidor, enquanto uma página do site é um site específica. Para obter mais informações, [tipos de página do SharePoint](http://go.microsoft.com/fwlink/?LinkID=211584).  
  
 Por padrão, a maioria das páginas que aparecem quando você cria um site do SharePoint é páginas do site. Uma página de site pode ser adicionada a uma biblioteca de página do SharePoint. Os usuários podem personalizar uma página do site usando ferramentas como o SharePoint Designer. Uma página do site também pode hospedar recursos, como Web Parts dinâmico e zonas de Web Parts.  
  
 Páginas de aplicativo não podem fazer essas coisas. No entanto, uma página de aplicativo é o melhor tipo de página para criar, se você deseja que a página contêm código personalizado. Embora você possa adicionar código personalizado para uma página do site, o código de execução é interrompida quando o usuário personalizar a página usando ferramentas como o SharePoint Designer.  
  
> [!NOTE]  
>  Visual Studio não fornece modelos que ajudam você a criam páginas de site para um site do SharePoint. Para obter mais informações, consulte [tipos de página do SharePoint](http://go.microsoft.com/fwlink/?LinkID=211584).  
  
## <a name="create-an-application-page"></a>Criar uma página de aplicativo
 Para criar uma página de aplicativo, adicione uma **página de aplicativo** item a um projeto do SharePoint. Quando você cria uma página de aplicativo, o Visual Studio adiciona as seguintes pastas para seu projeto:  
  
|Pasta|Descrição|  
|------------|-----------------|  
|Layouts|Mapeia para o diretório virtual _ layouts do sistema de arquivos do SharePoint.|  
|Subpasta de layouts|Contém os arquivos que compõem a página de aplicativo. Por padrão, esta pasta tem o mesmo nome que seu projeto. Você pode renomear essa pasta em qualquer momento. Quando você executa o projeto, o Visual Studio implanta essa pasta ao diretório virtual layouts do sistema de arquivos do SharePoint.|  
  
 Visual Studio adiciona os seguintes arquivos ao seu projeto:  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|Arquivo de página do ASP.NET (*. aspx*)|Contém a marcação XML que define a página.|  
|Arquivo de código da página de aplicativo|Contém o code-behind da página do aplicativo. Adicione o código que manipula os eventos nesse arquivo.|  
|Arquivo de código do designer de página do aplicativo|Contém o código que é gerado pelo designer. Não edite esse arquivo diretamente.|  
  
## <a name="design-and-debug-an-application-page"></a>Criar e depurar uma página de aplicativo
 Projete o conteúdo de uma página de aplicativo usando a exibição do designer no Visual Studio. Esse designer é exibido quando você abre a página do aplicativo em seu projeto (clicando duas vezes nele ou abrindo o menu de atalho e, em seguida, escolhendo **abra**) e, em seguida, escolha o **Design** botão na parte inferior o editor.  
  
> [!NOTE]  
>  Você pode criar a página somente na **origem** modo de exibição do designer. O **Design** modo de exibição do designer está desabilitado para as páginas do aplicativo.  
  
 Você pode depurar uma página de aplicativo, assim como você faria para depurar outros itens de projeto do SharePoint no Visual Studio. Quando você inicia o depurador do Visual Studio, o Visual Studio abre o site do SharePoint.  
  
 Para exibir a página do aplicativo, você deve navegar manualmente até o local da página do aplicativo (por exemplo: http://<em>nome_do_servidor</em>/_layouts/*Project_Name*/ApplicationPage1.aspx).  
  
 Para obter mais informações sobre como depurar projetos do SharePoint, consulte [soluções do SharePoint solucionar](../sharepoint/troubleshooting-sharepoint-solutions.md).  
  
## <a name="choose-a-master-page"></a>Escolha uma página mestra
 Por padrão, uma **página de aplicativo** item faz referência à página mestra do site que você está usando para depurar seu projeto. Que a página é chamada v4.master e você o encontrará listado na **Galeria de páginas mestras** do site do SharePoint.  
  
 Você pode alterar explicitamente qual página mestre é usada pela página de aplicativo, definindo o `MasterPageFile` atributo do aplicativo `Page` elemento. (Por exemplo: `MasterPageFile="~/_layouts/applicationv4.master"`). Na verdade, você deve definir esse atributo se páginas mestras dinâmicas não estiverem habilitadas no servidor do SharePoint. Para obter mais informações sobre páginas mestras no SharePoint, consulte [páginas mestras](http://go.microsoft.com/fwlink/?LinkID=169281).  
  
## <a name="see-also"></a>Consulte também
 [Desenvolvimento do SharePoint Foundation em camadas](http://go.microsoft.com/fwlink/?LinkID=182103)   
 [Visão geral do ASP.NET](/aspnet/overview)   
 [Páginas da Web do ASP.NET](/aspnet/web-pages/index)   
  
