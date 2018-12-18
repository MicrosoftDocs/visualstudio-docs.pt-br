---
title: Usando fontes e cores | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, controlling in IDE
- IDE, controlling text color and fonts
- Fonts and Colors property page
- font and color control [Visual Studio SDK]
- text, IDE
ms.assetid: d1a9b99f-fbdc-45ed-920a-e08c3d931ac9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4415d00e5a1233bfdf14dbc86a3a7ed2f7b8e770
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31141204"
---
# <a name="using-fonts-and-colors"></a>Usando fontes e cores
O [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] fornece suporte ao uso de fontes e cores para exibir o texto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral de cor e de fonte](../extensibility/font-and-color-overview.md)  
 Descreve as configurações de fonte e cor do texto no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE). Também apresenta os conceitos de categorias e itens de exibição e descreve como VSPackages e o editor de núcleo usam atributos de texto.  
  
 [Obtendo informações de cores para coloração de texto e fonte](../extensibility/getting-font-and-color-information-for-text-colorization.md)  
 Fornece diretrizes para implementar a coloração de texto em VSPackages gerenciar **categorias** diferente de **Editor de texto**.  
  
 [Acessando configurações de cor e fonte armazenado](../extensibility/accessing-stored-font-and-color-settings.md)  
 Explica como atual fonte e cor configurações podem ser armazenadas, recuperadas e aplicadas.  
  
 [Implementação de categorias personalizadas e itens de exibição](../extensibility/implementing-custom-categories-and-display-items.md)  
 Descreve as etapas básicas que uma janela pode criar e usar seu próprio de **exibir itens** e **categorias** para oferecer suporte à exibição de texto.  
  
 Essa abordagem requer um VSPackage implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> interface e interfaces relacionadas.  
  
 [Como: acessar o esquema de cores e fontes internas](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)  
 Descreve como definir e registrar uma categoria por meio de cores e fontes internas e iniciar o uso de cores e fontes fornecidas pelo sistema.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>  
 Fornece uma instância do `IVsFontAndColorDefaults` ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> interface que corresponde a um item específico listado no **Mostrar configurações para** lista o **fontes e cores** página do **Opções** caixa de diálogo.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>  
 Permite que um VSPackage dar suporte ao IDE **fontes e cores** página definindo fontes padrão e cores para uma janela ou um componente de interface do usuário.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>  
 Fornece um mecanismo pelo qual um VSPackage que fornece suporte de fonte e cor pode especificar um grupo de Item de exibição - uma categoria super que representa a união de duas ou mais categorias.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>  
 Permite que um VSPackage recuperar dados de fontes e cores, ou salvá-lo no registro.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>  
 Notifica VSPackages que estão usando fontes e cores informações sobre as alterações nas configurações de fonte e cor.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities>  
 Fornece ferramentas para trabalhar com os dados de entrada e saídos que são usados pelos métodos do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] **fontes e cores** mecanismo.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>  
 Controla o cache de configurações de fonte e cor.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)  
 Discute como VSPackages pode usar os serviços de idioma para personalizar o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor.  
  
 [Coloração de sintaxe em editores personalizados](../extensibility/syntax-coloring-in-custom-editors.md)  
 Descries como o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor usa serviços de linguagem para implementar a coloração de sintaxe.  
  
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)  
 Explica como usar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] services para criar elementos de interface do usuário que correspondem ao restante da [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].