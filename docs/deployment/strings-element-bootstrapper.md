---
title: '&lt;Cadeias de caracteres&gt; elemento (Bootstrapper) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- MSBuild.GenerateBootstrapper.NoStringsForCulture
- MSBuild.GenerateBootstrapper.ProductCultureNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Strings> element [bootstrapper]
ms.assetid: d5ea3613-5fc9-4a11-bef3-46a01178bf60
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fc1cab2fdb0a175fc9365b2a8b4b17dca46a30a2
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39077666"
---
# <a name="ltstringsgt-element-bootstrapper"></a>&lt;Cadeias de caracteres&gt; elemento (bootstrapper)
Define as cadeias de caracteres localizadas para nomes de produtos, nomes de pacote e mensagens de erro de instalação.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<Strings>  
    <String  
        Name  
    >  
    </String>  
</Strings>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `Strings` um filho do elemento é o `Package` elemento. Ele não tem atributos.  
  
## <a name="string"></a>Cadeia de Caracteres  
 O `String` um filho do elemento é o `Strings` elemento. Um `Strings` elemento pode ter um ou mais `String` elementos.  
  
 `String` tem o seguinte atributo.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. O nome da cadeia de caracteres.|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica que todas as cadeias de caracteres em inglês para o [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] installer.  
  
```xml  
<Strings>  
    <String Name="DisplayName">.NET Framework 2.0</String>  
    <String Name="Culture">en</String>  
    <String Name="AdminRequired">Administrator permissions are required to install the .NET Framework 2.0. Contact your administrator.</String>  
    <String Name="InvalidPlatformWin9x">Installation of the .NET Framework 2.0 is not supported on Windows 95. Contact your application vendor.</String>  
    <String Name="InvalidPlatformWinNT">Installation of the .NET Framework 2.0 is not supported on Windows NT 4.0. Contact your application vendor.</String>  
    <String Name="InvalidPlatformIE">Installation of the .NET Framework 2.0 requires Internet Explorer 5.01 or greater. Contact your application vendor.</String>  
    <String Name="InvalidPlatformArchitecture">This version of the .NET Framework 2.0 is not supported on a 64-bit operating system. Contact your application vendor.</String>  
    <String Name="WindowsInstallerImproperInstall">Due to an error with Windows Installer, the installation of the .NET Framework 2.0 cannot proceed.</String>  
    <String Name="AnotherInstanceRunning">Another instance of setup is already running. The running instance must complete before this setup can proceed.</String>  
    <String Name="BetaNDPFailure">A beta version of the .NET Framework was detected on the computer. Uninstall any previous beta versions of .NET Framework before continuing.</String>  
    <String Name="GeneralFailure">A failure occurred attempting to install the .NET Framework 2.0.</String>  
    <String Name="DotNetFXExe">http://go.microsoft.com/fwlink/?LinkId=37283</String>  
    <String Name="InstMsiAExe">http://go.microsoft.com/fwlink/?LinkId=37285</String>  
    <String Name="Msi30Exe">http://go.microsoft.com/fwlink/?LinkId=37287</String>  
</Strings>  
```  
  
## <a name="see-also"></a>Consulte também  
 [\<Pacote > elemento](../deployment/package-element-bootstrapper.md)