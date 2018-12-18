---
title: Fornecer automação a VSPackages | Microsoft Docs
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
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fc6eb16d1873c7986d9fac556440f24eb007396f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774166"
---
# <a name="providing-automation-for-vspackages"></a>Fornecendo automação para VSPackages
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Há duas maneiras de fornecer automação a VSPackages: Implementando objetos específicos de VSPackage e implementando objetos de automação padrão. Em geral, eles são usados juntos para estender o modelo de automação do ambiente.  
  
## <a name="vspackage-specific-objects"></a>Objetos específicos do VSPackage  
 Certos locais dentro do modelo de automação exigem que você fornecer objetos de automação que são exclusivos para o VSPackage. Por exemplo, os novos projetos exigem objetos distintos que fornece apenas o VSPackage. Os nomes desses objetos são inseridos no registro e obtidos por meio de chamadas para o ambiente `DTE` objeto.  
  
 Objetos específicos do VSPackage também podem ser obtidos quando um consumidor de automação usa o objeto fornecido por meio da propriedade do objeto de um objeto padrão. Por exemplo, o padrão `Window` objeto tem uma `Object` propriedade, comumente conhecida como o `Windows.Object` propriedade. Quando os consumidores chama o `Window.Object` em uma janela implementada no VSPackage, transmissão de um objeto de automação específico do seu próprio design.  
  
#### <a name="projects"></a>Projetos  
 Os VSPackages pode estender o modelo de automação para novos tipos de projeto por meio de seus próprios objetos específicos do VSPackage. A principal finalidade de fornecer novos objetos de automação para o VSPackage é diferenciar o seu projeto exclusivo objetos de um <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> ou um <xref:VSLangProj80.VSProject2> objeto. Essa diferenciação é útil quando você deseja fornecer uma maneira para destacar ou iterar seu tipo de projeto, além de outros tipos de projeto, eles aparecerão lado a lado em uma solução. Para obter mais informações, consulte [expondo objetos do projeto](../../extensibility/internals/exposing-project-objects.md).  
  
#### <a name="events"></a>Eventos  
 A arquitetura de eventos do ambiente oferece outro lugar para anexar seus próprios objetos específicos do VSPackage. Por exemplo, ao criar seus próprios objetos de evento exclusivo, você pode estender o modelo de evento do ambiente para projetos. Você talvez queira fornecer seus próprios eventos quando um novo item é adicionado ao tipo de projeto. Para obter mais informações, consulte [expor eventos](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md).  
  
#### <a name="window-objects"></a>Objetos de janela  
 Windows podem devolver um objeto de automação de VSPackage específico para o ambiente quando chamado. Você implementa um objeto que é derivado de <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>, <xref:EnvDTE.IExtensibleObject> ou `IDispatch` que entrega novamente as propriedades, estendendo o objeto de janela no qual ele é colocado no local. Por exemplo, você pode usar essa abordagem para fornecer automação para um controle colocado no local em um quadro de janela. A semântica deste objeto e todos os objetos que ela pode estender é sua para design. Para obter mais informações, consulte [como: fornecer automação para Windows](../../extensibility/internals/how-to-provide-automation-for-windows.md).  
  
#### <a name="options-pages-on-the-tools-menu"></a>Páginas de opções no menu Ferramentas  
 Você pode criar páginas para estender as ferramentas, o modelo de automação de opções por meio da implementação de páginas e adicionar informações ao registro para criar suas próprias opções. As páginas, em seguida, podem ser chamadas por meio do modelo de objeto de ambiente como qualquer outras páginas de opções. Se o design do recurso que você está adicionando ao ambiente por meio de VSPackages requer que as páginas de opções, você deve adicionar também o suporte de automação. Para obter mais informações, consulte [suporte de automação para páginas de opções](../../extensibility/internals/automation-support-for-options-pages.md).  
  
## <a name="standard-automation-objects"></a>Objetos de automação Standard  
 Para estender a automação para projetos, você também implementa objetos de automação padrão (derivado de `IDispatch`) que espera ao lado de outros objetos do projeto e implementar propriedades e métodos padrão. Exemplos de objetos padrão os objetos do projeto que são inseridos na hierarquia de solução, como `Projects`, `Project`, `ProjectItem`, e `ProjectItems`. Cada novo tipo de projeto deve implementar esses objetos (e possivelmente outros dependendo da semântica do seu projeto).  
  
 De certa forma, esses objetos fornecem oposta aproveitar os objetos do projeto de VSPackage específicos. Os objetos de automação padrão permitem que seu projeto a ser usado de forma generalizada como qualquer outro projeto que dão suporte aos mesmos objetos. Assim, um suplemento que é escrito em relação ao gerais `Project` e `ProjectItem` objetos podem funcionar em relação aos projetos de qualquer tipo. Para obter mais informações, consulte [projeto de modelagem](../../extensibility/internals/project-modeling.md).

