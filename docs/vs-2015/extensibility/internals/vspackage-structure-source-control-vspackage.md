---
title: Estrutura de VSPackage (VSPackage de controle do código-fonte) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
caps.latest.revision: 27
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6eaad545d1c1b3fe96ecbad3a88cc7636b777a54
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737978"
---
# <a name="vspackage-structure-source-control-vspackage"></a>Estrutura do VSPackage (VSPackage de controle do código-fonte)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O SDK do pacote de controle do código-fonte fornece diretrizes para criação de um VSPackage que permitem que um implementador de controle do código-fonte integrar sua funcionalidade de controle do código-fonte com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente. Um VSPackage é um componente COM que normalmente é carregado sob demanda pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) com base nos serviços que são anunciados pelo pacote em suas entradas do registro. Cada VSPackage deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>. Um VSPackage geralmente consome serviços oferecidos pelo [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE e oferece alguns serviços da sua própria.  
  
 Um VSPackage declara seus itens de menu e estabelece um estado de item padrão por meio do arquivo. VSCT. O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE exibe os itens de menu nesse estado até que o VSPackage seja carregado. Subsequentemente, a implementação do VSPackage do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método é chamado para habilitar ou desabilitar itens de menu.  
  
## <a name="source-control-package-characteristics"></a>Características do pacote de controle de origem  
 Um controle de fonte VSPackage está profundamente integrado ao [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 A semântica de VSPackage incluem:  
  
- Interface a ser implementada em virtude de ser um VSPackage (o `IVsPackage` interface)  
  
- Implementação de comandos de interface do usuário (arquivo. VSCT e a implementação do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface)  
  
- Registro do VSPackage com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
  O VSPackage de controle de origem deve se comunicar com esses outros [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] entidades:  
  
- Projetos  
  
- Editores  
  
- Soluções  
  
- Windows  
  
- Tabela de documento em execução  
  
### <a name="visual-studio-environment-services-that-may-be-consumed"></a>Ambiente de serviços do Visual Studio que podem ser consumidos  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 Serviço SVsRegisterScciProvider  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>  
  
### <a name="vsip-interfaces-implemented-and-called"></a>VSIP Interfaces implementadas e chamado  
 Um pacote de controle do código-fonte é um VSPackage e, portanto, ele pode interagir diretamente com outros que estão registrados com VSPackages [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para fornecer toda a funcionalidade de controle do código-fonte, um controle de fonte VSPackage pode lidar com interfaces fornecidas pelo projetos ou o shell.  
  
 Todos os projetos [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] deve implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> é reconhecido como um projeto dentro de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE. No entanto, essa interface não é especializada suficiente para o controle de origem. Projetos que devem estar na origem de controle de implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>. Essa interface é usada pelo VSPackage de controle de origem para consultar um projeto para seu conteúdo e fornecê-la glifos e informações de associação (as informações necessárias para estabelecer uma conexão entre o local do servidor e o local de disco de um projeto que está sob controle de origem).  
  
 O controle do código-fonte VSPackage implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>, que por sua vez permite que os projetos se registrem para controle do código-fonte e recuperar os glifos de status.  
  
 Para obter uma lista completa de interfaces que deve ser considerados um VSPackage de controle do código-fonte, consulte [serviços e Interfaces relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de design](../../extensibility/internals/source-control-vspackage-design-elements.md)   
 [Interfaces e serviços relacionados](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

