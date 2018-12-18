---
title: 'Como: usar GetGlobalService | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- services, GetGlobalService
ms.assetid: 4cdf5ab5-9f09-4caf-9011-2dcb2c62f1b7
caps.latest.revision: 14
manager: douge
ms.openlocfilehash: 5ce0d5657fa65cd727da2b97b3dd24735a81937a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49276115"
---
# <a name="how-to-use-getglobalservice"></a>Como: usar GetGlobalService
Às vezes, você precisará obter um serviço de uma janela de ferramenta ou controle de contêiner que não tenha sido colocado no local, caso contrário, foi colocado no local com um provedor de serviço que não sabe sobre o serviço que você deseja. Por exemplo, você talvez queira gravar no log de atividade de dentro de um controle. Para obter mais informações sobre esses e outros cenários, consulte [como: solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md).  
  
 Você pode obter a maioria dos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] services chamando estático <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método.  
  
 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> se baseia em um provedor de serviços em cache que é inicializado na primeira vez que qualquer VSPackage derivado de <xref:Microsoft.VisualStudio.Shell.Package> é colocado no local. Você deve assegurar que essa condição for atendida, ou então estar preparada para um serviço de nulo.  
  
 Felizmente, <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> funciona corretamente na maioria das vezes.  
  
-   Se um VSPackage fornece um serviço conhecido apenas outro VSPackage, o VSPackage solicitando o serviço é colocado no local antes do VSPackage fornecendo que o serviço é carregado.  
  
-   Se uma janela de ferramenta é criada por um VSPackage, o VSPackage é colocado antes que a janela da ferramenta é criada no local.  
  
-   Se um contêiner de controle for hospedado por uma janela de ferramenta criada por um VSPackage, o VSPackage é colocado antes que o contêiner de controle é criado no local.  
  
### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>Para obter um serviço de dentro de um contêiner de controle ou janela de ferramenta  
  
-   Inserir este código na janela da ferramenta, construtor ou contêiner de controle:  
  
     [!code-csharp[UseGetGlobalService#1](../snippets/csharp/VS_Snippets_VSSDK/usegetglobalservice/cs/getglobalservicepackage.cs#1)]
     [!code-vb[UseGetGlobalService#1](../snippets/visualbasic/VS_Snippets_VSSDK/usegetglobalservice/vb/getglobalservicepackage.vb#1)]  
  
     Esse código obtém um serviço SVsActivityLog e converte-o para um <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> interface, que pode ser usado para gravar no log de atividade. Por exemplo, consulte [como: usar o Log de atividades](../extensibility/how-to-use-the-activity-log.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: solucionar problemas de serviços](../extensibility/how-to-troubleshoot-services.md)   
 [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)   
 [Fundamentos do serviço](../extensibility/internals/service-essentials.md)