---
title: Contribuindo para o modelo de automação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5d56b446914ae7345ccb0d393db8f17fc7f82c47
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39513149"
---
# <a name="contribute-to-the-automation-model"></a>Contribuir para o modelo de automação
Visual Studio fornece um conjunto de interfaces de automação para personalizar o ambiente. O modelo de automação é o modelo de objeto que permite aos usuários finais criar suplementos do Visual Studio e extensões.  
  
 Além disso, é apropriado para você, como um desenvolvedor de VSPackage, contribuir com o modelo de automação. ao fazer isso, você habilitar os usuários finais de seu VSPackage criar suplementos e geralmente fornecem uma experiência do usuário consistente modelo ao usarem o VSPackage em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
 Para tornar o usuário final experiência consistente, você pode seguir um conjunto de diretrizes ao projetar o VSPackage para que o modelo de automação para o VSPackage segue as ideias em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Visão geral do modelo de automação](../../extensibility/internals/automation-model-overview.md)  
 Define o modelo de automação como um grupos de objetos que controlam as principais facetas do ambiente comum. Esse conjunto de objetos é representado em um diagrama do modelo de automação.  
  
 [Fornecer automação a VSPackages](../../extensibility/internals/providing-automation-for-vspackages.md)  
 Discute as duas maneiras principais para fornecer automação para o VSPackage.  
  
 [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)  
 Fornece instruções passo a passo para a criação de objetos específicos do VSPackage.  
  
 [Projeto de modelagem](../../extensibility/internals/project-modeling.md)  
 Explica os objetos de projeto padrão que são necessárias para criar a automação para o novo tipo de projeto e ilustra o caminho a seguir de automação de projeto. Este tópico também fornece listagens de declarações e a implementação de classes.  
  
 [Expõe eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)  
 Fornece instruções passo a passo para a criação de eventos para o seu modelo de automação.  
  
 [Suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)  
 Descreve como retornar um objeto de automação para dar suporte a propriedades de um VSPackage personalizada **opções** caixa de diálogo na **ferramenta** menu estendendo o `DTE.Properties` objeto.  
  
 [Fornecer automação para o código](../../extensibility/internals/providing-automation-for-code.md)  
 Explica que a criação de um modelo de automação para o seu código não é necessária. No entanto, um link é fornecido neste tópico que fornece informações criteriosas em modelos de código.  
  
 [Como: fornecer automação para Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md)  
 Explica que fornecer automação é uma boa ideia sempre que você deseja disponibilizar os objetos de automação em uma janela, e o ambiente já não fornecem um objeto de automação prontas para uso. Discute a automação para janelas de ferramentas e janelas de documento.  
  
 [Use o modelo de automação](../../extensibility/internals/using-the-automation-model.md)  
 Fornece dois exemplos de código que mostram como um consumidor de automação obtém o projeto inicial objetos de automação.  
  
 [Automação para objetos de configuração e SelectedItem](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)  
 Fornece informações sobre a automação para objetos de configuração e SelectedItems.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>  
 Fornece um exemplo de código que mostra como um VSPackage participa no modelo de objeto de automação de DTE. Lista de parâmetros, valores de retorno e comentários selecionados.  
  
