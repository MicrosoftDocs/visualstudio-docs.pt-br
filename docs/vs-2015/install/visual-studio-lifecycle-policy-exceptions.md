---
title: Exceções de política de ciclo de vida do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c238489d-6181-42c6-aa60-f75d0889dc68
caps.latest.revision: 3
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: c7c60747429bd702cdcea5f19891829411cd4a9c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772619"
---
# <a name="visual-studio-lifecycle-policy-exceptions"></a>Exceções de política de ciclo de vida do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visual Studio inclui um conjunto de compiladores, linguagens, tempos de execução, ambientes e outros recursos que permitem o desenvolvimento de várias plataformas da Microsoft. Como uma conveniência para nossos clientes do Visual Studio, o Visual Studio poderá instalar determinados SDKs da Microsoft e outros componentes da Microsoft que direcionam e dão suporte a essas plataformas da Microsoft. Esses componentes podem ser licenciados e ter suporte sob seus próprios termos e políticas.  
  
## <a name="external-components-that-follow-a-lifecycle-policy-other-than-the-visual-studio-policy"></a>Componentes externos que seguem uma política de ciclo de vida que não seja a política do Visual Studio  
 A tabela a seguir lista os componentes da plataforma Microsoft que podem ser incluídos com o Visual Studio (dependendo da edição específica do software Visual Studio), e que estão sujeitos a suas próprias políticas de suporte e os períodos de tempo.  
  
|FAMÍLIA DE PRODUTOS|NOME EXTERNO|  
|--------------------|-------------------|  
|[.NET 3.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%203.5&Filter=FilterNO)|SDK do .NET 3.5<br /><br /> Windows Identity Foundation|  
|[.NET 4.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%204.5&Filter=FilterNO)|SDK do .NET 4.5|  
|[.NET 4.5.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=.NET%20Framework%204.5.1&Filter=FilterNO)|Pacote multiplataforma do .NET 4.5.1 (Clássico)<br /><br /> Pacote multiplataforma do NET 4.5.1 (Repositório)<br /><br /> .NET 4.5.1 OOB MSU<br /><br /> Pacote Redistribuível do .NET 4.5.1<br /><br /> Pacotes de idiomas do .NET 4.5.1 Redist<br /><br /> SDK do .NET 4.5.1|  
|[ASP.NET Web Stack](http://go.microsoft.com/fwlink/?LinkId=328918)|ASP.NET MVC 4<br /><br /> ASP.NET MVC 5<br /><br /> ASP.NET Web API<br /><br /> ASP.NET Web API 2<br /><br /> Páginas da Web do ASP.NET 2<br /><br /> Páginas da Web do ASP.NET 3|  
|[Entity Framework 6](http://go.microsoft.com/fwlink/?LinkId=328950)|Entity Framework 6|  
|[Exchange 2013](http://go.microsoft.com/fwlink/?LinkId=328950)|Serviços Web do Exchange|  
|[Microsoft OWIN](http://go.microsoft.com/fwlink/?LinkId=328951)|Microsoft OWIN|  
|[Microsoft Web Developer Tools 2013](http://go.microsoft.com/fwlink/?LinkId=328952)|Ferramentas de Desenvolvimento na Web da Microsoft 2013|  
|As atualizações desses componentes são distribuídas pelo NuGet e não seguem as políticas padrão de ciclo de vida da Microsoft.  Veja [http://docs.nuget.org/](http://docs.nuget.org/) para obter mais informações.|Manipulador de Token Web JSON para o Microsoft .NET Framework 4.5<br /><br /> NuGet 2.7<br /><br /> SignalR<br /><br /> Web Optimization Framework<br /><br /> WebGrease|  
|[ODataLib](http://go.microsoft.com/fwlink/?LinkId=328954)|ODataLib|  
|[Office 2013](http://support.microsoft.com/lifecycle/?p1=16674)|Open XML SDK|  
|[Política de serviços online](http://support.microsoft.com/gp/OSSLpolicy)|SDK do Microsoft Ads|  
|[SharePoint 2013](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=sharepoint%20server%202013&Filter=FilterNO)|Componente cliente do SharePoint<br /><br /> SharePoint Foundation 2013<br /><br /> Windows Identity Foundation Extensions|  
|[Silverlight 5](http://support.microsoft.com/lifecycle/?p1=16278)<br /><br /> <br />> Consulte também: [http://support.microsoft.com/gp/lifean45](http://support.microsoft.com/gp/lifean45)|Tempo de execução do Silverlight 5<br /><br /> SDK do Silverlight 5|  
|[SQL Server 2008 R2](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202008%20R2&Filter=FilterNO)|SQL System CLR Types (SQL Server 2008 R2)|  
|[SQL Server 2012](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202012&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> Utilitários de linha de comando SQL<br /><br /> Serviço de linguagem SQL – IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL Native Client (Sqlncli)<br /><br /> SQL Server Express 2012 SP1<br /><br /> SQL System CLR Types (SQL Server 2012)<br /><br /> SQLDOM|  
|[SQL Server 2014](https://support.microsoft.com/en-us/lifecycle/search?sort=PN&alpha=SQL%20Server%202014&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> Utilitários de linha de comando SQL<br /><br /> Serviço de linguagem SQL – IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL Native Client (Sqlncli)<br /><br /> SQL Server Express 2014<br /><br /> SQL System CLR Types (SQL Server 2014)<br /><br /> SQLDOM|  
|[SQL Server Compact Edition 4.0](http://support.microsoft.com/lifecycle/?p1=16106)|SQL Server Compact Edition 4.0|  
|[O WCF RIA Services v 1.0 SP2](http://go.microsoft.com/fwlink/?LinkId=328955)|WCF RIA Services v1.0 SP2|  
|[Windows Server 2008](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows%20Server%202008&Filter=FilterNO)|Serviços Web do Windows (WWS) para Windows Server 2008|  
|[Windows 7](http://support.microsoft.com/lifecycle/?c2=14019)|SDK do Windows 7|  
|[Windows 8](http://support.microsoft.com/lifecycle/?c2=16796)|SDK do Windows 8|  
|[Windows 8.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=windows%208.1&Filter=FilterNO)|SDK do Windows 8.1<br /><br /> Windows Library para JavaScript (WinJS)|  
|[Microsoft Azure](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq)<br /><br /> <br />> Consulte também: [política de ciclo de vida Online](http://support.microsoft.com/gp/OSSLpolicy)|SDK de Serviços Móveis do Microsoft Azure<br /><br /> Ferramentas dos Serviços Móveis do Microsoft Azure|