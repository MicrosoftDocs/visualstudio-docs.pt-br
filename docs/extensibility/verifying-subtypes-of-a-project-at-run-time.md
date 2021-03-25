---
title: Verificando subtipos de um projeto em tempo de execução | Microsoft Docs
description: Saiba como fazer seu VSPackage verificar a presença de um subtipo de projeto personalizado especificado do qual ele depende.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes
- check subtypes
ms.assetid: b87780ec-36a3-4e9a-9ee2-7abdc26db739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c52d3297ce4903cb8f8e7cb2f9ab5169d21ac94e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062597"
---
# <a name="verify-subtypes-of-a-project-at-run-time"></a>Verificar subtipos de um projeto em tempo de execução
Um VSPackage que depende de um subtipo de projeto personalizado deve incluir a lógica para procurar esse subtipo, de modo que ele possa falhar normalmente se o subtipo não estiver presente. O procedimento a seguir mostra como verificar a presença de um subtipo especificado.

### <a name="to-verify-the-presence-of-a-subtype"></a>Para verificar a presença de um subtipo

1. Obtenha a hierarquia do projeto do projeto e dos objetos de solução como um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto adicionando o código a seguir ao seu VSPackage.

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

2. Converta a hierarquia na <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected> interface.

    ```csharp
    IVsAggregatableProjectCorrected AP;
    AP = hierarchy as IVsAggregatableProjectCorrected;

    ```

3. Obtenha a lista de GUIDs de tipo de projeto invocando o <xref:Microsoft.VisualStudio.Shell.Flavor.IVsAggregatableProjectCorrected.GetAggregateProjectTypeGuids%2A> .

    ```csharp
    string projTypeGuids = AP.GetAggregateProjectTypeGuids().ToUpper();

    ```

4. Verifique a lista do GUID do subtipo especificado.

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
