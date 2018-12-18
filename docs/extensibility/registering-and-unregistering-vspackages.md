---
title: Registrar e cancelar o registro de VSPackages | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2075bec37e29359fb9c403f9cb149b70c01845b6
ms.sourcegitcommit: 9571742f4a808c75b1034aa72fc24b54bc50692e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49410982"
---
# <a name="register-and-unregister-vspackages"></a>Registrar e cancelar o registro de VSPackages
Usar atributos para registrar um VSPackage, mas  
  
## <a name="register-a-vspackage"></a>Registrar um VSPackage  
 Você pode usar atributos para controlar o registro de VSPackages gerenciados. Todas as informações de registro estão contidas em uma *pkgdef* arquivo. Para obter mais informações sobre o registro baseado em arquivo, consulte [utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md).  
  
 O código a seguir mostra como usar os atributos padrão de registro para registrar o VSPackage.  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]  
public sealed class BasicPackage : Package  
{
    // ...
}  
```  
  
## <a name="unregister-an-extension"></a>Cancelar o registro de uma extensão  
 Se você estiver fazendo experiências com muita VSPackages diferentes e deseja removê-los da instância experimental, é possível executar o **redefinir** comando. Procure **redefinir a instância Experimental do Visual Studio** na página inicial do seu computador, ou execute este comando da linha de comando:  
  
```cmd  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp  
```  
  
 Se você quiser desinstalar uma extensão que você instalou na sua instância de desenvolvimento do Visual Studio, acesse **ferramentas** > **extensões e atualizações**, localize a extensão e clique em  **Desinstalar**.  
  
 Se por alguma razão, nenhum desses métodos bem-sucedida em desinstalar a extensão, você pode cancelar o registro do assembly de VSPackage da linha de comando da seguinte maneira:  
  
```cmd  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>  
```  
  
<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>  
  
## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>Use um atributo personalizado de registro para registrar uma extensão  
  
Em alguns casos, você talvez precise criar um novo atributo de registro para a sua extensão. Você pode usar atributos de registro para adicionar novas chaves de registro ou para adicionar novos valores para as chaves existentes. O novo atributo deve derivar de <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>, e ele deve substituir o <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> métodos.  
  
### <a name="create-a-custom-attribute"></a>Criar um atributo personalizado  
  
O código a seguir mostra como criar um novo atributo de registro.  
  
```csharp  
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]  
public class CustomRegistrationAttribute : RegistrationAttribute  
{  
}  
```  
  
 O <xref:System.AttributeUsageAttribute> é usado em classes de atributos para especificar o elemento de programa (classe, método, etc.) para que o atributo pertence, se ele pode ser usado mais de uma vez e se ele pode ser herdado.  
  
### <a name="create-a-registry-key"></a>Criar uma chave do registro  
  
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
  
### <a name="create-a-new-value-under-an-existing-registry-key"></a>Criar um novo valor em uma chave do registro existente  
  
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
