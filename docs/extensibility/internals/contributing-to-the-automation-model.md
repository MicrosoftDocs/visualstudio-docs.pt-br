---
title: Contribuindo para o modelo de automação | Microsoft Docs
description: Saiba como contribuir com o modelo de automação do Visual Studio seguindo um conjunto de diretrizes ao criar um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44da0c91eb425cbd558aea4335447f9293684b90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057033"
---
# <a name="contribute-to-the-automation-model"></a>Contribuir para o modelo de automação
O Visual Studio fornece um conjunto de interfaces de automação para personalizar o ambiente. O modelo de automação é o modelo de objeto que permite que os usuários finais criem suplementos e extensões do Visual Studio.

 Além disso, é apropriado para você, como desenvolvedor VSPackage, para contribuir com o modelo de automação; ao fazer isso, você permite que os usuários finais do seu VSPackage criem suplementos e geralmente fornecem uma experiência de modelo de usuário consistente quando usam o VSPackage no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

 Para tornar a experiência do usuário final consistente, você pode seguir um conjunto de diretrizes ao projetar seu VSPackage para que o modelo de automação para seu VSPackage siga as ideias em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="in-this-section"></a>Nesta seção
- [Visão geral do modelo de automação](../../extensibility/internals/automation-model-overview.md)

 Define o modelo de automação como um grupo de objetos relacionados que controlam as principais facetas do ambiente comum. Esse conjunto de objetos é mostrado em um diagrama do modelo de automação.

- [Fornecer automação para VSPackages](../../extensibility/internals/providing-automation-for-vspackages.md)

 Discute as duas maneiras principais de fornecer automação para seu VSPackage.

- [Expor objetos do projeto](../../extensibility/internals/exposing-project-objects.md)

 Fornece instruções passo a passo para a criação de objetos específicos do VSPackage.

- [Modelagem de projeto](../../extensibility/internals/project-modeling.md)

 Explica os objetos de projeto padrão que são necessários para criar a automação para o novo tipo de projeto e ilustra o caminho que a automação de projeto segue. Este tópico também fornece listagens de declarações e implementação para classes.

- [Expor eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 Fornece instruções passo a passo para a criação de eventos para seu modelo de automação.

- [Suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md)

 Descreve como retornar um objeto Automation para dar suporte a propriedades de uma caixa de diálogo de **Opções** personalizadas do VSPackage no menu de **ferramentas** , estendendo o `DTE.Properties` objeto.

- [Fornecer automação para código](../../extensibility/internals/providing-automation-for-code.md)

 Explica que a criação de um modelo de automação para seu código não é necessária. No entanto, um link é fornecido neste tópico que fornece informações criteriosas sobre modelos de código.

- [Como: fornecer automação para o Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 Explica que fornecer automação é uma boa ideia sempre que você deseja disponibilizar objetos de automação em uma janela, e o ambiente ainda não fornece um objeto de automação pronto. Discute a automação para janelas de ferramentas e janelas de documentos.

- [Usar o modelo de automação](../../extensibility/internals/using-the-automation-model.md)

 Fornece dois exemplos de código que mostram como um consumidor de automação Obtém os objetos de automação de projeto iniciais.

- [Automação para objetos de configuração e SelectedItem](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 Fornece informações sobre a automação para objetos de configuração e SelectedItems.

## <a name="reference"></a>Referência
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> Fornece um exemplo de código que mostra como um VSPackage participa do modelo de objeto de automação do DTE. Lista os parâmetros, valores de retorno e comentários selecionados.
