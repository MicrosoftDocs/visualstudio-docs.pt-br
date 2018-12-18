---
title: Usando e fornecer serviços | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 351b5b5c0ab32ab7e8267864eddaae10459a23bd
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31138334"
---
# <a name="using-and-providing-services"></a>Usando e fornecer serviços
Um serviço é um contrato entre dois VSPackages. Um VSPackage oferece um conjunto específico de interfaces para outro VSPackage consumir. Por exemplo, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] oferece o <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> de serviço para qualquer VSPackage ele carrega. Esse serviço fornece o <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface, que pode ser usado para gravar no log de atividade. Para obter mais informações, consulte [como: usar o Log de atividades](../extensibility/how-to-use-the-activity-log.md).  
  
 VSPackages podem oferecer serviços de seus próprios usando o <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> interface.  
  
 O Visual Studio oferece serviços importantes, como o seguinte:  
  
|Serviço IDE|Descrição|  
|-----------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|Fornece acesso ao IDE serviços lidar com a funcionalidade básica, VSPackages e o registro.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|Fornece janelas básicas e funcionalidades relacionadas a interface do usuário no IDE, como a capacidade de criar ferramentas e janelas de documento.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|Fornece funcionalidades básicas relacionadas à solução, como a capacidade de enumerar os projetos, criar novos projetos e monitorar as alterações do projeto.|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)  
 Apresenta os elementos importantes de um serviço do Visual Studio.  
  
 [Como obter um serviço](../extensibility/how-to-get-a-service.md)  
 Discute como solicitar (consumir) um serviço.  
  
 [Como fornecer um serviço](../extensibility/how-to-provide-a-service.md)  
 Descreve como fornecer um serviço.  
  
 [Como fornecer um serviço assíncrono do Visual Studio](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)  
 Descreve como fornecer um serviço assíncrono.  
  
 [Como solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md)  
 Aborda problemas comuns e apresenta soluções para eles.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [SDK do Visual Studio](../extensibility/visual-studio-sdk.md)