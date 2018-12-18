---
title: Suporte de automação para páginas de opções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b18f8df30dc9f3385c2c5f154d66c598b423968e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49929641"
---
# <a name="automation-support-for-options-pages"></a>Suporte de automação para páginas de opções
Os VSPackages pode fornecer personalizado **opções** caixas de diálogo para o **ferramentas** menu (**opções de ferramentas** páginas) no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e podem disponibilizá-los para a automação modelo.  
  
## <a name="tools-options-pages"></a>páginas de Opções de Ferramentas  
 Para criar uma **opções de ferramentas** página, um VSPackage deve fornecer uma implementação de controle de usuário retornada para o ambiente por meio da implementação do VSPackage o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método. (Ou, para código gerenciado, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método.) 
  
 É opcional, mas altamente recomendável, para permitir o acesso a essa nova página por meio do modelo de automação. Você pode fazer isso com as seguintes etapas:  
  
1. Estender o <xref:EnvDTE._DTE.Properties%2A> objeto por meio da implementação de um objeto derivado de IDispatch.  
  
2. Retornam uma implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método (ou para código gerenciado a <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> método) para o objeto derivado de IDispatch.  
  
3. Quando um consumidor de automação chama o <xref:EnvDTE._DTE.Properties%2A> método em um personalizado **opção** página de propriedade, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método para obter um personalizado **opções de ferramentas** automação da página implementação.  
  
4. O objeto de automação do VSPackage, em seguida, é usado para fornecer a cada <xref:EnvDTE.Property> retornado por <xref:EnvDTE._DTE.Properties%2A>.  
  
   Para obter um exemplo de implementação de uma **opções de ferramentas** página, consulte [exemplos de VSSDK](http://aka.ms/vs2015sdksamples).  
  
## <a name="see-also"></a>Consulte também  
 [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)