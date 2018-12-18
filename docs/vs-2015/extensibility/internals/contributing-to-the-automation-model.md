---
title: Contribuindo para o modelo de automação | Microsoft Docs
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
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 53a669ed6f1ddaa9c2274371439828da24b92789
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51726972"
---
# <a name="contributing-to-the-automation-model"></a>Contribuindo com o modelo de automação
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio fornece um conjunto de interfaces de automação para personalizar o ambiente. O modelo de automação é o modelo de objeto que permite aos usuários finais criar suplementos do Visual Studio e extensões.  
  
 Além disso, é apropriado para você, como um desenvolvedor de VSPackage, contribuir com o modelo de automação. ao fazer isso, você habilitar os usuários finais de seu VSPackage criar suplementos e geralmente fornecem uma experiência do usuário consistente modelo ao usarem o VSPackage em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 Para tornar o usuário final experiência consistente, você pode seguir um conjunto de diretrizes ao projetar o VSPackage para que o modelo de automação para o VSPackage segue as ideias em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral do modelo de automação](../../extensibility/internals/automation-model-overview.md)  
 Define o modelo de automação como um grupos de objetos que controlam as principais facetas do ambiente comum. Esse conjunto de objetos é representado em um diagrama do modelo de automação.  
  
 [Fornecer automação a VSPackages](../../extensibility/internals/providing-automation-for-vspackages.md)  
 Discute as duas maneiras principais para fornecer automação para o VSPackage.  
  
 [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)  
 Fornece instruções passo a passo para a criação de objetos específicos do VSPackage.  
  
 [Modelagem do projeto](../../extensibility/internals/project-modeling.md)  
 Explica os objetos de projeto padrão que são necessárias para criar a automação para o novo tipo de projeto e ilustra o caminho a seguir de automação de projeto. Este tópico também fornece listagens de declarações e a implementação de classes.  
  
 [Expondo eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)  
 Fornece instruções passo a passo para a criação de eventos para o seu modelo de automação.  
  
 [Suporte à automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)  
 Descreve como retornar um objeto de automação para dar suporte a propriedades de um VSPackage personalizada **opções** caixa de diálogo na **ferramenta** menu estendendo o `DTE.Properties` objeto.  
  
 [Fornecer automação para código](../../extensibility/internals/providing-automation-for-code.md)  
 Explica que a criação de um modelo de automação para o seu código não é necessária. No entanto, um link é fornecido neste tópico que fornece informações criteriosas em modelos de código.  
  
 [Como fornecer automação para o Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md)  
 Explica que fornecer automação é uma boa ideia sempre que você deseja disponibilizar os objetos de automação em uma janela, e o ambiente já não fornecem um objeto de automação prontas para uso. Discute a automação para janelas de ferramentas e janelas de documento.  
  
 [Usar o modelo de automação](../../extensibility/internals/using-the-automation-model.md)  
 Fornece dois exemplos de código que mostram como um consumidor de automação obtém o projeto inicial objetos de automação.  
  
 [Automação de configuração e objetos SelectedItem](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)  
 Fornece informações sobre a automação para opções de configuração e automação para itens selecionados.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>  
 Fornece um exemplo de código que mostra como um VSPackage participa no modelo de objeto de automação de DTE. Lista de parâmetros, valores de retorno e comentários selecionados.  
  
## <a name="related-sections"></a>Seções relacionadas

