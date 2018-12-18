---
title: Registrar e cancelar o registro de VSPackages | Microsoft Docs
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
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
caps.latest.revision: 36
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e14422b7430dc0429954bf11c77b30619fb7f7da
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763416"
---
# <a name="registering-and-unregistering-vspackages"></a>Registrando e cancelando o registro de VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usar atributos para registrar um VSPackage, mas  
  
## <a name="registering-a-vspackage"></a>Registrando um VSPackage  
 Você pode usar atributos para controlar o registro de VSPackages gerenciados. Todas as informações de registro estão contidas em um arquivo. pkgdef. Para obter mais informações sobre o registro baseado em arquivo, consulte [utilitário CreatePkgDef](../extensibility/internals/createpkgdef-utility.md).  
  
 O código a seguir mostra como usar os atributos padrão de registro para registrar o VSPackage.  
  
```csharp  
[PackageRegistration(UseManagedResourcesOnly = true)]  
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]  
public sealed class BasicPackage : Package  
{. . .}  
```  
  
## <a name="unregistering-an-extension"></a>Cancelar o registro de uma extensão  
 Se você estiver fazendo experiências com muita VSPackages diferentes e deseja removê-los da instância experimental, é possível executar o **redefinir** comando. Procure **redefinir a instância Experimental do Visual Studio** na página inicial do seu computador, ou execute este comando da linha de comando:  
  
```vb  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp  
```  
  
 Se você quiser desinstalar uma extensão que você instalou na sua instância de desenvolvimento do Visual Studio, acesse **ferramentas / extensões e atualizações**, localize a extensão e clique em **desinstalar**.  
  
 Se por alguma razão, nenhum desses métodos bem-sucedida em desinstalar a extensão, você pode cancelar o registro do assembly de VSPackage da linha de comando da seguinte maneira:  
  
```  
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg” /unregister <pathToVSPackage assembly>  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../extensibility/internals/vspackages.md)

