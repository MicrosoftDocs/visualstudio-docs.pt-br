---
title: Registrando e registrando vspackages | Microsoft Docs
description: Saiba mais sobre como registrar e não registrar seus VSPackages, incluindo os atributos que você usa e o arquivo .pkgdef.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48067ed883a44870b3b753cb5e3d6943eca91ca5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900298"
---
# <a name="register-and-unregister-vspackages"></a>Registrar e não registrar VSPackages
Você usa atributos para registrar um VSPackage, mas

## <a name="register-a-vspackage"></a>Registrar um VSPackage
 Você pode usar atributos para controlar o registro de VSPackages gerenciados. Todas as informações de registro estão contidas em *um arquivo .pkgdef.* Para obter mais informações sobre o registro baseado em arquivo, consulte [Utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md).

 O código a seguir mostra como usar os atributos de registro padrão para registrar o VSPackage.

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>Retirar o registro de uma extensão
 Se você já experimentou muitos VSPackages diferentes e deseja removê-los da instância experimental, basta executar o comando **Redefinir.** Procure **Redefinir o Visual Studio Instância Experimental** na página inicial do computador ou execute este comando na linha de comando:

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 Se você quiser desinstalar uma extensão instalada na instância de desenvolvimento do Visual Studio, acesse Extensões e Atualizações de Ferramentas, localize a extensão e clique em  >   **Desinstalar**.

 Se, por algum motivo, nenhum desses métodos for bem-sucedido na desinstalação da extensão, você poderá ressinstalar o assembly VSPackage da linha de comando da seguinte forma:

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>Usar um atributo de registro personalizado para registrar uma extensão

Em determinados casos, talvez seja necessário criar um novo atributo de registro para sua extensão. Você pode usar atributos de registro para adicionar novas chaves do Registro ou para adicionar novos valores às chaves existentes. O novo atributo deve derivar <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> de e deve substituir os métodos e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> .

### <a name="create-a-custom-attribute"></a>Como criar um atributo personalizado

O código a seguir mostra como criar um novo atributo de registro.

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 O é usado em classes de atributo para especificar o elemento de programa (classe, método etc.) ao qual o atributo pertence, se ele pode ser usado mais de uma vez e se ele pode <xref:System.AttributeUsageAttribute> ser herdado.

### <a name="create-a-registry-key"></a>Criar uma chave do Registro

No código a seguir, o atributo personalizado cria **uma** sub-chave Personalizada sob a chave para o VSPackage que está sendo registrado.

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

### <a name="create-a-new-value-under-an-existing-registry-key"></a>Criar um novo valor em uma chave do Registro existente

Você pode adicionar valores personalizados a uma chave existente. O código a seguir mostra como adicionar um novo valor a uma chave de registro vsPackage.

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
