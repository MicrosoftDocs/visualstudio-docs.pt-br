---
title: Executar soluções em diferentes versões do Microsoft Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], multiple Office versions
- Office applications [Office development in Visual Studio], multiple Office versions
- Office development in Visual Studio, multiple Office versions
- Office solutions [Office development in Visual Studio]
- multiple Office versions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ed8a9b7cc78b0605b7fcc3931a7ee8992360125b
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669826"
---
# <a name="run-solutions-in-different-versions-of-microsoft-office"></a>Executar soluções em diferentes versões do Microsoft Office
    
## <a name="run-office-solutions-created-by-using-visual-studio-2010-and-above"></a>Executar soluções do Office criadas usando o Visual Studio 2010 e posterior  
  
|Versão do Office direcionado pelo modelo de projeto|.NET Framework do projeto de destino<sup>1</sup>|Versões do Office que pode executar a solução|Tempo de execução necessário no computador do usuário final|  
|--------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|-------------------------------------------|  
|Office 2016 e [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|  
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|  
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|.NET Framework 3,5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Visual Studio 2010 Tools for Office Runtime|  
|Sistema Microsoft Office 2007|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior,<br /><br /> ou<br /><br /> .NET Framework 3,5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> Sistema Microsoft Office 2007|Visual Studio 2010 Tools for Office Runtime|  
  
 1. A versão do .NET Framework que o destino do seu projeto é necessário nos computadores de usuário final para sua solução executar. Por exemplo, se seu projeto tiver como alvo o .NET Framework 3.5, o .NET Framework 3.5 é necessário nos computadores dos usuários finais. Neste exemplo, sua solução não será executado se apenas o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] está instalado nos computadores dos usuários finais.  
  
 2. Nesse cenário, a solução será executada sem erros no sistema Microsoft Office 2007 somente se ele não usa recursos que são novos no [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)].  
  
## <a name="run-office-solutions-created-by-using-versions-of-visual-studio-prior-to-visual-studio-2010"></a>Executar soluções do Office criadas usando versões do Visual Studio antes do Visual Studio 2010  
 Aplicativos do Microsoft Office podem executar soluções criadas usando versões do Visual Studio anteriores ao Visual Studio 2010. Em alguns casos, essas soluções exigem versões diferentes do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. Versões diferentes do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] pode ser instalado lado a lado no mesmo computador.  
  
 A tabela a seguir mostra quais versões do Microsoft Office podem executar soluções criadas usando versões anteriores do Visual Studio e quais versões do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] e o .NET Framework são necessárias para cada solução.  
  
|Edição do Visual Studio usado para criar a solução|Versão do Office direcionado pelo modelo de projeto|Versões do Office que pode executar a solução|Tempo de execução necessário no computador do usuário final|Versão necessária do .NET Framework no computador do usuário final|  
|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|-------------------------------------------|----------------------------------------------------------|  
|Visual Studio 2008 Professional<br /><br /> ou<br /><br /> Visual Studio Team System 2008|Sistema Microsoft Office 2007|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] <sup>1</sup><br /><br /> Sistema Microsoft Office 2007|Visual Studio 2010 Tools for Office Runtime<sup>1</sup><br /><br /> ou<br /><br /> Ferramentas do Visual Studio para o Microsoft Office system (versão 3.0 Runtime)|.NET Framework 3,5|  
|Uma das seguintes edições do Visual Studio 2005 com o VSTO 2005 SE<sup>2</sup> instalado:<br /><br /> -Visual Studio 2005 Tools for Office<br />-Visual Studio Team System 2005<br />-Visual Studio 2005 Professional|Sistema Microsoft Office 2007|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (somente 32 bits<sup>3</sup>)<br /><br /> Sistema Microsoft Office 2007|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0, .NET Framework 3.0 ou 3.5 do .NET Framework|  
|Qualquer uma das seguintes edições do Visual Studio:<br /><br /> -Visual Studio 2008 Professional<br />-Visual Studio Team System 2008<br />-Visual Studio 2005 Tools for Office (com ou sem o VSTO 2005 SE<sup>2</sup> instalado)<br />-Visual Studio Team System 2005 (com ou sem o VSTO 2005 SE<sup>2</sup> instalado)<br />-Visual Studio 2005 Professional com o VSTO 2005 SE<sup>2</sup> instalado|Microsoft Office 2003|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (somente 32 bits<sup>3</sup>)<br /><br /> Sistema Microsoft Office 2007<br /><br /> Microsoft Office 2003|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0, .NET Framework 3.0 ou 3.5 do .NET Framework|  
  
 1. [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] aplicativos incluem o Visual Studio 2010 Tools for Office runtime. Portanto, esses aplicativos sempre usam o Visual Studio 2010 Tools for Office runtime em vez do Visual Studio Tools para o Microsoft Office system (versão 3.0 Runtime) nesse cenário. Aplicativos no 2007 Microsoft Office system podem usar o Visual Studio 2010 Tools for Office Runtime ou o Visual Studio Tools for Microsoft Office system (versão 3.0 Runtime).  
  
 2. O VSTO 2005 SE é um complemento gratuito do Visual Studio que fornece modelos de projeto do suplemento do VSTO para o Microsoft Office 2003 e o 2007 Microsoft Office system. Ele pode ser instalado com o Visual Studio 2005 Professional, Visual Studio 2005 Tools for Office ou uma edição no Visual Studio Team System 2005. Para obter mais informações, consulte [Visual Studio 2005 Tools for Office Second Edition](http://go.microsoft.com/fwlink/?LinkId=148446).  
  
 3. Soluções do Office que requerem o Visual Studio 2005 Tools para Office Second Edition Runtime não são compatíveis com versões de 64 bits do [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]. Para executar essas soluções na edição de 64 bits [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ou [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)], você deve atualizar o projeto para [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] ou a um projeto do Visual Studio 2008 que tem como alvo o 2007 Microsoft Office system.  
  
## <a name="see-also"></a>Consulte também  
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Ferramentas do Visual Studio para cenários de instalação de tempo de execução do Office](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)   
 [Configurar um computador para desenvolver soluções do Office](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)  
  
  