---
title: Suporte de automação para páginas de opções | Microsoft Docs
description: Saiba como tornar as páginas de opções de ferramentas personalizadas no VSPackages disponíveis para o modelo de automação do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a4f6b33b7a5e17c610831db5d4387065915ea00
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901650"
---
# <a name="automation-support-for-options-pages"></a>Suporte de automação para páginas de opções
O VSPackages pode fornecer caixas de diálogo de **Opções** personalizadas ao menu **ferramentas** (**ferramentas opções** páginas) no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e pode torná-las disponíveis para o modelo de automação.

## <a name="tools-options-pages"></a>páginas de Opções de Ferramentas
 Para criar uma página de **Opções de ferramentas** , um VSPackage deve fornecer uma implementação de controle de usuário retornada ao ambiente por meio da implementação do VSPackage do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método. (Ou, para o código gerenciado, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> método.)

 É opcional, mas altamente recomendável permitir o acesso a essa nova página por meio do modelo de automação. Você pode fazer isso com as seguintes etapas:

1. Estenda o <xref:EnvDTE._DTE.Properties%2A> objeto por meio da implementação de um objeto derivado de IDispatch.

2. Retornar uma implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método (ou para código gerenciado o <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> método) para o objeto derivado de IDispatch.

3. Quando um consumidor de automação chama o <xref:EnvDTE._DTE.Properties%2A> método em uma página de propriedades de **opção** personalizada, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método para obter a implementação de automação de uma página de **Opções de ferramentas** personalizadas.

4. O objeto Automation do VSPackage é usado para fornecer cada um deles <xref:EnvDTE.Property> retornado por <xref:EnvDTE._DTE.Properties%2A> .

   Para obter um exemplo de implementação de uma página de **Opções de ferramentas** personalizadas, consulte [exemplos de VSSDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples).

## <a name="see-also"></a>Confira também
- [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)
