---
title: Fornecimento de automação para VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fb5f3393443e41c9bd99a8890b53bedae006d7a5
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131562"
---
# <a name="providing-automation-for-vspackages"></a>Fornecimento de automação para VSPackages
Há duas maneiras de fornecer automação para seu VSPackages: Implementando objetos VSPackage específicos e implementar objetos de automação standard. Em geral, eles são usados juntos para estender o modelo de automação do ambiente.  
  
## <a name="vspackage-specific-objects"></a>Objetos específicos de VSPackage  
 Certos locais dentro do modelo de automação exigem que você fornecer objetos de automação que são exclusivos para seu VSPackage. Por exemplo, novos projetos exigem objetos distintos que fornece apenas o VSPackage. Os nomes desses objetos são inseridos no registro e obtidos por meio de chamadas para o ambiente `DTE` objeto.  
  
 Objetos específicos do VSPackage também podem ser obtidos quando um consumidor de automação usa o objeto fornecido por meio da propriedade do objeto de um objeto padrão. Por exemplo, o padrão `Window` objeto tem um `Object` propriedade, geralmente conhecida como o `Windows.Object` propriedade. Quando os consumidores chamam o `Window.Object` em uma janela implementada no seu VSPackage, você volta passar um objeto de automação específico do seu próprio design.  
  
#### <a name="projects"></a>Projetos  
 VSPackages pode estender o modelo de automação para novos tipos de projeto por meio de seus próprios objetos VSPackage específicos. A principal finalidade de fornecer novos objetos de automação para o VSPackage é exclusivo do seu projeto de diferenciar objetos de um <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> ou um <xref:VSLangProj80.VSProject2> objeto. Essa diferenciação é útil quando você deseja fornecer uma maneira para destacar ou iterar o tipo de projeto, além de outros tipos de projeto, eles devem aparecer lado a lado em uma solução. Para obter mais informações, consulte [expondo objetos do projeto](../../extensibility/internals/exposing-project-objects.md).  
  
#### <a name="events"></a>Eventos  
 A arquitetura de eventos do ambiente oferece outro lugar para anexar seus próprios objetos VSPackage específicos. Por exemplo, ao criar seus próprios objetos de eventos exclusivas, você pode estender o modelo de evento do ambiente para projetos. Você talvez queira fornecer seus próprios eventos quando um novo item é adicionado ao tipo de projeto. Para obter mais informações, consulte [expondo eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md).  
  
#### <a name="window-objects"></a>Objetos de janela  
 Windows pode devolver um objeto de automação de VSPackage específico para o ambiente quando chamado. Implementar um objeto que é derivado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>, <xref:EnvDTE.IExtensibleObject> ou `IDispatch` que volta passa propriedades, estendendo o objeto de janela na qual ele está localizado. Por exemplo, você pode usar essa abordagem para fornecer a automação para um controle colocado em um quadro de janela. A semântica deste objeto e todos os outros objetos que podem estender é sua para design. Para obter mais informações, consulte [como: fornecem automação para Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md).  
  
#### <a name="options-pages-on-the-tools-menu"></a>Páginas de opções no menu Ferramentas  
 Você pode criar páginas para estender as ferramentas, o modelo de automação de opções por meio da implementação de páginas e adicionar informações ao registro a fim de criar suas próprias opções. As páginas, em seguida, podem ser chamadas por meio do modelo de objeto do ambiente como quaisquer outras páginas de opções. Se o design do recurso que você está adicionando ao ambiente por meio de VSPackages requer páginas de opções, você deve adicionar o suporte da automação. Para obter mais informações, consulte [suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md).  
  
## <a name="standard-automation-objects"></a>Objetos de automação Standard  
 Para estender a automação para projetos, você também implementar objetos de automação padrão (derivado de `IDispatch`) que espera ao lado de outros objetos do projeto e implementar métodos padrão e propriedades. Exemplos de objetos padrão os objetos do projeto que são inseridos na hierarquia da solução como `Projects`, `Project`, `ProjectItem`, e `ProjectItems`. Cada novo tipo de projeto deve implementar esses objetos (e possivelmente outros dependendo da semântica do projeto).  
  
 De certa forma, esses objetos fornecem a vantagem oposta dos objetos de projeto VSPackage específicos. Os objetos de automação padrão permitem que seu projeto para ser usado de forma generalizada como qualquer outro projeto os mesmos objetos de suporte. Portanto, um suplemento que é gravado em geral `Project` e `ProjectItem` objetos podem funcionar em relação a projetos de qualquer tipo. Para obter mais informações, consulte [projeto de modelagem](../../extensibility/internals/project-modeling.md).