---
title: Registrando e cancelando o registro de VSPackages | Microsoft Docs
description: Saiba mais sobre como registrar e cancelar o registro de seu VSPackages, incluindo os atributos que você usa e o arquivo. pkgdef.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5238ef7d544bcdeb3dd68a4741791262aaa77c0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056539"
---
# <a name="register-and-unregister-vspackages"></a>Registrar e cancelar o registro de VSPackages
Você usa atributos para registrar um VSPackage, mas

## <a name="register-a-vspackage"></a>Registrar um VSPackage
 Você pode usar atributos para controlar o registro de VSPackages gerenciados. Todas as informações de registro estão contidas em um arquivo *. pkgdef* . Para obter mais informações sobre o registro baseado em arquivo, consulte [utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md).

 O código a seguir mostra como usar os atributos de registro padrão para registrar seu VSPackage.

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>Retirar o registro de uma extensão
 Se você estiver experimentando vários VSPackages diferentes e quiser removê-los da instância experimental, bastará executar o comando **Reset** . Procure **redefinir a instância experimental do Visual Studio** na página inicial do computador ou execute este comando na linha de comando:

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 Se você quiser desinstalar uma extensão que você instalou em sua instância de desenvolvimento do Visual Studio, vá para **ferramentas**  >  **extensões e atualizações**, localize a extensão e clique em **desinstalar**.

 Se, por algum motivo, nenhum desses métodos obtiver sucesso ao desinstalar a extensão, você poderá cancelar o registro do assembly VSPackage da linha de comando da seguinte maneira:

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>Usar um atributo de registro personalizado para registrar uma extensão

Em alguns casos, talvez seja necessário criar um novo atributo de registro para sua extensão. Você pode usar atributos de registro para adicionar novas chaves do registro ou para adicionar novos valores às chaves existentes. O novo atributo deve derivar de e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> deve substituir os <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> métodos e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> .

### <a name="create-a-custom-attribute"></a>Como criar um atributo personalizado

O código a seguir mostra como criar um novo atributo de registro.

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 O <xref:System.AttributeUsageAttribute> é usado em classes de atributo para especificar o elemento Program (classe, método, etc.) ao qual o atributo pertence, se ele pode ser usado mais de uma vez e se pode ser herdado.

### <a name="create-a-registry-key"></a>Criar uma chave do registro

No código a seguir, o atributo personalizado cria uma subchave **personalizada** sob a chave para o VSPackage que está sendo registrado.

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

### <a name="create-a-new-value-under-an-existing-registry-key"></a>Criar um novo valor em uma chave de registro existente

Você pode adicionar valores personalizados a uma chave existente. O código a seguir mostra como adicionar um novo valor a uma chave de registro do VSPackage.

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

## <a name="see-also"></a>Confira também
- [VSPackages](../extensibility/internals/vspackages.md)
