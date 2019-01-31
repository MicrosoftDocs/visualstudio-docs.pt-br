---
title: Números de versão para assemblies satélite principais e localizados | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- satellite assemblies, version numbers
- SatelliteContractVersionAttribute
- version numbers, assemblies
- assemblies [Visual Studio], version numbers
- versioning, assemblies
ms.assetid: 5489aea1-57b4-4561-9bb4-24d490269602
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: eb699c7b5ab2aec928bf83ada5dd8824f93f3006
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54790133"
---
# <a name="version-numbers-for-main-and-localized-satellite-assemblies"></a>Números de versão para assemblies principal e satélite localizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A classe <xref:System.Resources.SatelliteContractVersionAttribute> fornece suporte ao controle de versão de um assembly principal que usa recursos localizados por meio do gerenciador de recursos. A aplicação de <xref:System.Resources.SatelliteContractVersionAttribute> ao assembly principal de um aplicativo permite atualizar e reimplantar o assembly sem atualizar seus assemblies satélites. Por exemplo, é possível usar a classe <xref:System.Resources.SatelliteContractVersionAttribute> com um service pack que não introduz novos recursos sem recompilar e reimplantar os assemblies satélites. Para que os recursos localizados fiquem disponíveis, a versão do contrato satélite do assembly principal deve corresponder à classe <xref:System.Reflection.AssemblyVersionAttribute> dos assemblies satélites. Você deve especificar um número de versão exato no <xref:System.Resources.SatelliteContractVersionAttribute>; não são permitidos caracteres curinga, como "*". Para obter mais informações, consulte [Recuperando recursos](http://msdn.microsoft.com/library/eca16922-1c46-4f68-aefe-e7a12283641f).  
  
## <a name="updating-assemblies"></a>Atualizando assemblies  
 A classe <xref:System.Resources.SatelliteContractVersionAttribute> permite atualizar um assembly principal sem a necessidade de atualizar o assembly satélite ou vice-versa. Quando o assembly principal é atualizado, seu número de versão do assembly é alterado. Se você desejar continuar usando os assemblies satélite existentes, altere o número de versão do assembly principal, mas não altere o número de versão do contrato satélite. Por exemplo, na primeira versão, a versão do assembly principal pode ser 1.0.0.0. A versão do contrato satélite e a versão do assembly satélite também serão 1.0.0.0. Se você precisar atualizar um service pack do assembly principal, é possível alterar a versão do assembly para 1.0.0.1, mantendo a versão do contrato satélite e a versão do assembly satélite como 1.0.0.0.  
  
 Se precisar atualizar um assembly satélite mas não o assembly principal, altere <xref:System.Reflection.AssemblyVersionAttribute> do assembly satélite. Juntamente com o assembly satélite, você precisará enviar um assembly de política que afirma que o novo assembly satélite é compatível com o assembly satélite antigo. Para obter mais informações sobre políticas, consulte [Como o tempo de execução localiza assemblies](http://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34).  
  
 O código a seguir mostra como definir a versão do contrato satélite. O código pode ser colocado em um script de build ou no arquivo AssemblyInfo.vb ou AssemblyInfo.cs.  
  
```vb  
<Assembly: SatelliteContractVersionAttribute("4.3.2.1")>  
  
```  
  
```csharp  
[assembly: SatelliteContractVersionAttribute("4.3.2.1")]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como o tempo de execução localiza assemblies](http://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)   
 [Definindo atributos de assembly](http://msdn.microsoft.com/library/36a98a81-b5b5-4c19-912a-11f91eff7f4e)   
 [Security and Localized Satellite Assemblies](../ide/security-and-localized-satellite-assemblies.md)  (Assemblies satélite de segurança e localizados)  
 [Localizando aplicativos](../ide/localizing-applications.md)   
 [Globalizando e localizando aplicativos](../ide/globalizing-and-localizing-applications.md)
