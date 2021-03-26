---
title: Carregando VSPackages | Microsoft Docs
description: Saiba mais sobre como carregar VSPackages no Visual Studio, incluindo carregamento atrasado, que é usado sempre que possível para melhorar o desempenho.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 39a58bcbad79191f54a7b4eeb2aa12e90d8a6e44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073281"
---
# <a name="load-vspackages"></a>Carregar VSPackages
VSPackages são carregados no Visual Studio somente quando sua funcionalidade é necessária. Por exemplo, um VSPackage é carregado quando o Visual Studio usa uma fábrica de projetos ou um serviço que o VSPackage implementa. Esse recurso é chamado de carregamento atrasado, que é usado sempre que possível para melhorar o desempenho.

> [!NOTE]
> O Visual Studio pode determinar determinadas informações de VSPackage, como os comandos que um VSPackage oferece, sem carregar o VSPackage.

 VSPackages pode ser definido como AutoLoad em um contexto de interface do usuário específico (IU), por exemplo, quando uma solução é aberta. O <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> atributo define esse contexto.

### <a name="autoload-a-vspackage-in-a-specific-context"></a>Autocarregar um VSPackage em um contexto específico

- Adicione o `ProvideAutoLoad` atributo aos atributos VSPackage:

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     Consulte os campos enumerados de <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> para obter uma lista dos contextos da interface do usuário e seus valores GUID.

- Defina um ponto de interrupção no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.

- Compile o VSPackage e inicie a depuração.

- Carregue uma solução ou crie uma.

     O VSPackage é carregado e interrompido no ponto de interrupção.

## <a name="force-a-vspackage-to-load"></a>Forçar o carregamento de um VSPackage
 Em algumas circunstâncias, um VSPackage pode ter que forçar outro VSPackage a ser carregado. Por exemplo, um VSPackage leve pode carregar um VSPackage maior em um contexto que não está disponível como um CMDUIContext.

 Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> método para forçar o carregamento de um VSPackage.

- Insira esse código no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método do VSPackage que força a carga de outro VSPackage:

    ```csharp
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;
    if (shell == null) return;

    IVsPackage package = null;
    Guid PackageToBeLoadedGuid =
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);

    ```

     Quando o VSPackage for inicializado, ele forçará `PackageToBeLoaded` a carga.

     O carregamento forçado não deve ser usado para comunicação VSPackage. Use [usar e fornecer serviços](../extensibility/using-and-providing-services.md) em vez disso.

## <a name="see-also"></a>Confira também
- [VSPackages](../extensibility/internals/vspackages.md)
