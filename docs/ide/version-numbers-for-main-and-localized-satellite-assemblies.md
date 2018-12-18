---
title: Números de versão para assemblies satélite principais e localizados
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- satellite assemblies, version numbers
- SatelliteContractVersionAttribute
- version numbers, assemblies
- assemblies [Visual Studio], version numbers
- versioning, assemblies
ms.assetid: 5489aea1-57b4-4561-9bb4-24d490269602
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cbc74d746453c5d8e60161004a5b56a2c21915dd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882583"
---
# <a name="version-numbers-for-main-and-localized-satellite-assemblies"></a>Números de versão para assemblies satélite principais e localizados
A classe <xref:System.Resources.SatelliteContractVersionAttribute> fornece suporte ao controle de versão de um assembly principal que usa recursos localizados por meio do Gerenciador de Recursos. A aplicação de <xref:System.Resources.SatelliteContractVersionAttribute> ao assembly principal de um aplicativo permite atualizar e reimplantar o assembly sem atualizar seus assemblies satélites. Por exemplo, é possível usar a classe <xref:System.Resources.SatelliteContractVersionAttribute> com um service pack que não introduz novos recursos sem recompilar e reimplantar os assemblies satélites. Para que os recursos localizados fiquem disponíveis, a versão do contrato satélite do assembly principal deve corresponder à classe <xref:System.Reflection.AssemblyVersionAttribute> dos assemblies satélites. Especifique um número de versão exato no <xref:System.Resources.SatelliteContractVersionAttribute>. Não são permitidos caracteres curinga, como "*". Para obter mais informações, consulte [Recuperar recursos](/dotnet/framework/resources/retrieving-resources-in-desktop-apps).

## <a name="update-assemblies"></a>Atualizar assemblies
 A classe <xref:System.Resources.SatelliteContractVersionAttribute> permite atualizar um assembly principal sem a necessidade de atualizar o assembly satélite ou vice-versa. Quando o assembly principal é atualizado, seu número de versão do assembly é alterado. Se você desejar continuar usando os assemblies satélite existentes, altere o número de versão do assembly principal, mas não altere o número de versão do contrato satélite. Por exemplo, na primeira versão, a versão do assembly principal pode ser 1.0.0.0. A versão do contrato satélite e a versão do assembly satélite também serão 1.0.0.0. Se você precisar atualizar um service pack do assembly principal, é possível alterar a versão do assembly para 1.0.0.1, mantendo a versão do contrato satélite e a versão do assembly satélite como 1.0.0.0.

 Se precisar atualizar um assembly satélite mas não o assembly principal, altere <xref:System.Reflection.AssemblyVersionAttribute> do assembly satélite. Juntamente com o assembly satélite, você precisará enviar um assembly de política que afirma que o novo assembly satélite é compatível com o assembly satélite antigo. Para obter mais informações sobre políticas, consulte [Como o tempo de execução localiza assemblies](/dotnet/framework/deployment/how-the-runtime-locates-assemblies).

 O código a seguir mostra como definir a versão do contrato satélite. O código pode ser colocado em um script de build ou no arquivo *AssemblyInfo.vb* ou *AssemblyInfo.cs*.

```vb
<Assembly: SatelliteContractVersionAttribute("4.3.2.1")>
```

```csharp
[assembly: SatelliteContractVersionAttribute("4.3.2.1")]
```

## <a name="see-also"></a>Consulte também

- [Como o tempo de execução localiza assemblies](/dotnet/framework/deployment/how-the-runtime-locates-assemblies)
- [Definir atributos de assembly](/dotnet/framework/app-domains/set-assembly-attributes)
- [Assemblies satélite de segurança e localizados](../ide/security-and-localized-satellite-assemblies.md)
- [Localizar aplicativos](../ide/localizing-applications.md)
- [Globalizar e localizar aplicativos](../ide/globalizing-and-localizing-applications.md)