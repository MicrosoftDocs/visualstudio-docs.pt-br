---
title: Carregar VSPackages | Microsoft Docs
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
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e351f49ea3e9579202e21868361e5d6f3d53b8fd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753877"
---
# <a name="loading-vspackages"></a>Carregando VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os VSPackages são carregados no Visual Studio apenas quando sua funcionalidade é necessária. Por exemplo, um VSPackage é carregado quando o Visual Studio usa uma fábrica de projeto ou um serviço que implementa o VSPackage. Esse recurso é chamado de carregamento atrasado, que é usado sempre que possível para melhorar o desempenho.  
  
> [!NOTE]
>  Visual Studio pode determinar determinadas informações de VSPackage, como os comandos que oferece um VSPackage, sem carregar o VSPackage.  
  
 Os VSPackages pode ser definidos como autoload em um contexto de (UI) de interface de usuário específico, por exemplo, quando uma solução é aberta. O <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> atributo define neste contexto.  
  
### <a name="autoloading-a-vspackage-in-a-specific-context"></a>Realiza o carregamento automático um VSPackage em um contexto específico  
  
-   Adicionar o `ProvideAutoLoad` de atributo para os atributos de VSPackage:  
  
    ```csharp  
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID  
    public class MyAutoloadedPackage : Package  
    {. . .}  
    ```  
  
     Ver os campos enumerados de <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> para obter uma lista de contextos de interface do usuário e seus valores GUID.  
  
-   Defina um ponto de interrupção no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.  
  
-   Compile o VSPackage e iniciar a depuração.  
  
-   Carregue uma solução ou crie um.  
  
     O VSPackage carrega e para no ponto de interrupção.  
  
## <a name="forcing-a-vspackage-to-load"></a>Forçar para carregar um VSPackage  
 Em algumas circunstâncias, um VSPackage talvez precise forçar outro VSPackage a ser carregado. Por exemplo, um VSPackage leve pode carregar um VSPackage maior em um contexto que não está disponível como um CMDUIContext.  
  
 Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> método para forçar um VSPackage ao carregar.  
  
-   Inserir este código para o <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método do VSPackage que força o VSPackage outro ao carregar:  
  
    ```csharp  
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;  
    if (shell == null) return;  
  
    IVsPackage package = null;  
    Guid PackageToBeLoadedGuid =   
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);  
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);  
  
    ```  
  
     Quando o VSPackage é inicializado, ele forçará `PackageToBeLoaded` para carregar.  
  
     Carregamento de força não deve ser usado para comunicação de VSPackage. Use [Using e fornecendo serviços](../extensibility/using-and-providing-services.md) em vez disso.  
  
## <a name="using-a-custom-attribute-to-register-a-vspackage"></a>Usando um atributo personalizado para registrar um VSPackage  
 Em alguns casos, você talvez precise criar um novo atributo de registro para a sua extensão. Você pode usar atributos de registro para adicionar novas chaves de registro ou para adicionar novos valores para as chaves existentes. O novo atributo deve derivar de <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>, e ele deve substituir o <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> métodos.  
  
## <a name="creating-a-registry-key"></a>Criando uma chave do registro  
 No código a seguir, o atributo personalizado cria uma **personalizado** subchave sob a chave para o VSPackage que está sendo registrado.  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
    }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");  
}  
  
```  
  
## <a name="creating-a-new-value-under-an-existing-registry-key"></a>Criando um novo valor em uma chave do registro existente  
 Você pode adicionar valores personalizados para uma chave existente. O código a seguir mostra como adicionar um novo valor a uma chave de registro de VSPackage.  
  
```csharp  
public override void Register(RegistrationAttribute.RegistrationContext context)  
{  
    Key packageKey = null;  
    try  
    {   
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");  
        packageKey.SetValue("NewCustom", 1);  
    }  
    finally  
    {  
        if (packageKey != null)  
            packageKey.Close();  
                }  
}  
  
public override void Unregister(RegistrationContext context)  
{  
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)

