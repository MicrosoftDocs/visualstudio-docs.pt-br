---
title: Fornecendo automação para VSPackages | Microsoft Docs
description: Saiba mais sobre como fornecer automação para seu VSPackages implementando objetos específicos do VSPackage e implementando objetos de automação padrão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9a19b5e0e543052dad492ab319595c8ef76dfe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060946"
---
# <a name="providing-automation-for-vspackages"></a>Fornecendo automação para VSPackages
Há duas maneiras principais de fornecer automação para seu VSPackages: implementando objetos específicos do VSPackage e implementando objetos de automação padrão. Em geral, eles são usados juntos para estender o modelo de automação do ambiente.

## <a name="vspackage-specific-objects"></a>Objetos VSPackage-Specific
 Determinados locais dentro do modelo de automação exigem que você forneça objetos de automação exclusivos para seu VSPackage. Por exemplo, novos projetos exigem objetos distintos que apenas seu VSPackage fornece. Os nomes desses objetos são inseridos no registro e obtidos por meio de chamadas para o `DTE` objeto de ambiente.

 Os objetos específicos do VSPackage também podem ser obtidos quando um consumidor de automação usa o objeto fornecido por meio da propriedade Object de um objeto padrão. Por exemplo, o `Window` objeto padrão tem uma `Object` propriedade, normalmente conhecida como a `Windows.Object` propriedade. Quando os consumidores chamam o `Window.Object` em uma janela implementada em seu VSPackage, você passa um objeto de automação específico de seu próprio design.

#### <a name="projects"></a>Projetos
 O VSPackages pode estender o modelo de automação para novos tipos de projeto por meio de seus próprios objetos específicos do VSPackage. A principal finalidade de fornecer novos objetos de automação para seu VSPackage é diferenciar seus objetos de projeto exclusivos de um <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> ou de um <xref:VSLangProj80.VSProject2> objeto. Essa diferenciação é útil quando você deseja fornecer uma maneira de separar ou iterar seu tipo de projeto além de outros tipos de projeto, caso eles apareçam lado a lado em uma solução. Para obter mais informações, consulte [expondo objetos do projeto](../../extensibility/internals/exposing-project-objects.md).

#### <a name="events"></a>Eventos
 A arquitetura de eventos do ambiente oferece outro lugar para você acrescentar seus próprios objetos específicos do VSPackage. Por exemplo, ao criar seus próprios objetos de evento exclusivos, você pode estender o modelo de evento do ambiente para projetos. Talvez você queira fornecer seus próprios eventos quando um novo item for adicionado ao seu próprio tipo de projeto. Para obter mais informações, consulte [expondo eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md).

#### <a name="window-objects"></a>Objetos de janela
 O Windows pode retornar um objeto de automação específico do VSPackage para o ambiente quando chamado. Implemente um objeto derivado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> , <xref:EnvDTE.IExtensibleObject> ou `IDispatch` que retorne Propriedades, estendendo o objeto Window no qual ele é site. Por exemplo, você pode usar essa abordagem para fornecer automação para um controle local em um quadro de janela. A semântica desse objeto e de quaisquer outros objetos que ele possa estender é sua para design. Para obter mais informações, consulte [como: fornecer automação para o Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md).

#### <a name="options-pages-on-the-tools-menu"></a>Páginas de opções no menu ferramentas
 Você pode criar páginas para estender as ferramentas, o modelo de automação de opções por meio da implementação de páginas e a adição de informações ao registro para criar suas próprias opções. Em seguida, suas páginas podem ser chamadas por meio do modelo de objeto de ambiente como qualquer outra página de opções. Se o design do recurso que você está adicionando ao ambiente por meio do VSPackages exigir páginas de opções, você também deverá adicionar o suporte de automação. Para obter mais informações, consulte [suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md).

## <a name="standard-automation-objects"></a>Objetos de automação padrão
 Para estender a automação para projetos, você também implementa os objetos de automação padrão (derivados de `IDispatch` ) que ficam ao lado dos outros objetos de projeto e implementam métodos e propriedades padrão. Exemplos de objetos padrão incluem os objetos de projeto que são inseridos na hierarquia da solução, como `Projects` ,, `Project` `ProjectItem` e `ProjectItems` . Cada novo tipo de projeto deve implementar esses objetos (e possivelmente outros, dependendo da semântica do seu projeto).

 De certa forma, esses objetos fornecem a vantagem oposta dos objetos de projeto específicos ao VSPackage. Os objetos de automação padrão permitem que seu projeto seja usado de forma generalizada, como qualquer outro projeto que dê suporte aos mesmos objetos. Assim, um suplemento que é escrito em geral `Project` e `ProjectItem` objetos pode funcionar em projetos de qualquer tipo. Para obter mais informações, consulte [modelagem de projeto](../../extensibility/internals/project-modeling.md).
