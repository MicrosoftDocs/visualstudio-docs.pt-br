---
title: Solucionando problemas de registro do pacote RegPkg | Microsoft Docs
description: Use essas informações para solucionar problemas de registro de pacote RegPkg no Visual Studio. Use a versão do RegPkg que é apropriada para seu pacote.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- RegPkg
ms.assetid: f33f822f-697a-4bad-9c10-554b4c8f6246
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48e3699b095ed7b9d0e72cf7b09ad02e26ac5a51
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090753"
---
# <a name="troubleshooting-regpkg-package-registration"></a>Solucionando problemas de registro de pacote RegPkg
> [!NOTE]
> A maneira preferida de registrar pacotes no Visual Studio é usando arquivos. pkgdef. Isso permite a implantação da extensão sem a necessidade de acessar o registro do sistema. Os arquivos pkgdef são criados usando o [utilitário CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md).

 Para registrar um pacote usando o RegPkg no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , você deve usar a versão do RegPkg apropriada para seu pacote.

## <a name="regpkg-versions-related-to-package-versions"></a>Versões do RegPkg relacionadas a versões do pacote
 Há duas versões do RegPkg. Uma versão está incluída no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Use esta versão para registrar pacotes que foram criados usando um dos seguintes assemblies:

1. Microsoft.VisualStudioShell.9.0.dll

2. Microsoft.VisualStudioShell.10.0.dll

3. Microsoft.VisualStudioShell.11.0.dll

   Ele não pode registrar pacotes que foram criados usando o assembly de Microsoft.VisualStudio.Shell.dll anterior.

   A versão anterior do RegPkg pode registrar pacotes que foram criados usando o assembly Microsoft.VisualStudio.Shell.dll. No entanto, ele não pode registrar pacotes criados usando versões posteriores desse assembly.

## <a name="see-also"></a>Confira também
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Solução de problemas do Visual Studio](/troubleshoot/visualstudio/welcome-visual-studio/)
