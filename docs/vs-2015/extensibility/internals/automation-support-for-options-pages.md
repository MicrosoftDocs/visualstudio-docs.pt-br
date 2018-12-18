---
title: Suporte de automação para páginas de opções | Microsoft Docs
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
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
caps.latest.revision: 30
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6205d01547f7243234facfb43db80303c9b71c51
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51720262"
---
# <a name="automation-support-for-options-pages"></a>Suporte à automação para páginas de opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os VSPackages pode fornecer personalizado **opções** caixas de diálogo para o **ferramentas** menu (páginas de opções de ferramentas) no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e podem disponibilizá-las para o modelo de automação.  
  
## <a name="tools-options-pages"></a>Páginas de opções de ferramentas  
 Para criar uma **opções de ferramentas** página, um VSPackage deve fornecer uma implementação de controle de usuário retornada para o ambiente por meio da implementação do VSPackage a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método, (ou para código gerenciado a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método).  
  
 É opcional, mas altamente recomendável, para permitir o acesso a essa nova página por meio do modelo de automação. Você pode fazer isso nas seguintes etapas:  
  
1. Estender o <xref:EnvDTE._DTE.Properties%2A> objeto por meio da implementação de um objeto derivado de IDispatch.  
  
2. Retornam uma implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método (ou para código gerenciado a <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> método) para o objeto derivado de IDispatch.  
  
3. Quando um consumidor de automação chama o <xref:EnvDTE._DTE.Properties%2A> método em um personalizado **opção** página de propriedade, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método para obter um personalizado **opções de ferramentas** automação da página implementação.  
  
4. O objeto de automação do VSPackage, em seguida, é usado para fornecer a cada <xref:EnvDTE.Property> retornado por <xref:EnvDTE._DTE.Properties%2A>.  
  
   Para obter um exemplo implementando uma página de opções de ferramentas personalizada, consulte [exemplos de VSSDK](../../misc/vssdk-samples.md).  
  
## <a name="see-also"></a>Consulte também  
 [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)

