---
title: Usando um atributo de registro personalizado para registrar uma extensão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98068fa7-bda1-4922-b3f6-28680de58c3d
caps.latest.revision: 3
manager: douge
ms.openlocfilehash: 251c31efcbb8a72efac51f246e644a30a79ed999
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49279832"
---
# <a name="using-a-custom-registration-attribute-to-register-an-extension"></a>Usando um atributo de registro personalizado para registrar uma extensão
Em alguns casos, você talvez precise criar um novo atributo de registro para a sua extensão. Você pode usar atributos de registro para adicionar novas chaves de registro ou para adicionar novos valores para as chaves existentes. O novo atributo deve derivar de <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>, e ele deve substituir o <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> e <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> métodos.  
  
## <a name="creating-a-custom-attribute"></a>Criando um atributo personalizado  
 O código a seguir mostra como criar um novo atributo de registro.  
  
```  
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]  
    public class CustomRegistrationAttribute : RegistrationAttribute  
    {  
    }  
  
```  
  
 O <xref:System.AttributeUsageAttribute> é usado em classes de atributos para especificar o elemento de programa (classe, método, etc.) para que o atributo pertence, se ele pode ser usado mais de uma vez e se ele pode ser herdado.  
  
### <a name="creating-a-registry-key"></a>Criando uma chave do registro  
 No código a seguir, o atributo personalizado cria uma **personalizado** subchave sob a chave para o VSPackage que está sendo registrado.  
  
```  
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
  
### <a name="creating-a-new-value-under-an-existing-registry-key"></a>Criando um novo valor em uma chave do registro existente  
 Você pode adicionar valores personalizados para uma chave existente. O código a seguir mostra como adicionar um novo valor a uma chave de registro de VSPackage.  
  
```  
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