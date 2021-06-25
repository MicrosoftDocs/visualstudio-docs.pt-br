---
title: Verificando subtipos de um projeto em tempo de | Microsoft Docs
description: Saiba como fazer com que o VSPackage verifique a presença de um subtipo de projeto personalizado especificado do qual ele depende.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 621a40e1857d7c78ec4c5be08a3b7c3808a0d48b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905467"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>Verificar subtipos de um projeto em tempo de executar
Um VSPackage que depende de um subtipo de projeto personalizado deve incluir lógica para procurar esse subtipo para que ele possa falhar normalmente se o subtipo não estiver presente. O procedimento a seguir mostra como verificar a presença de um subtipo especificado.

### <a name="to-verify-the-presence-of-a-subtype"></a>Para verificar a presença de um subtipo

1. Obter a hierarquia de projeto dos objetos de projeto e solução como um objeto adicionando o código a <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> seguir ao VSPackage.

    ```csharp
    EnvDTE.DTE dte;
    dte = (EnvDTE.DTE)Package.GetGlobalService(typeof(EnvDTE.DTE));

    EnvDTE.Project project;
    project = dte.Solution.Projects.Item(1);

    IVsSolution solution;
    solution = (IVsSolution)Package.GetGlobalService(typeof(SVsSolution));

    IVsHierarchy hierarchy;
    hierarchy = solution.GetProjectOfUniqueName(project.UniqueName);

    ```

2. Caste a hierarquia para a <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> interface .

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. Obter a lista de GUIDs do tipo de projeto invocando o <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> .

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. Verifique a lista para o GUID do subtipo especificado.

    ```csharp
    // Replace the string "MyGUID" with the GUID of the subtype.
    string guidMySubtype = "MyGUID";
    if (projTypeGuids.IndexOf(guidMySubtype) > 0)
    {
        // The specified subtype is present.
    }
    ```

## <a name="see-also"></a>Confira também
- [Subtipos de projeto](../extensibility/internals/project-subtypes.md)
- [Design de subtipos de projeto](../extensibility/internals/project-subtypes-design.md)
- [Propriedades e métodos estendidos por subtipos de projeto](../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)
