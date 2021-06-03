---
title: Utilitário RegPkg | Microsoft Docs
description: Saiba como o utilitário RegPkg.exe registra um VSPackage com Visual Studio e o prepara para implantação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffef522cb85816c36bee1cb623810fb254d1ddec
ms.sourcegitcommit: f50bbdb15c4f9fca0fa245ca765183c378960cc5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2021
ms.locfileid: "111351936"
---
# <a name="regpkg-utility"></a>Utilitário RegPkg
> [!NOTE]
> A maneira preferencial de registrar pacotes no Visual Studio é usando arquivos .pkgdef. Isso permite a implantação de extensão sem precisar acessar o registro do sistema, que é um requisito para a implantação do VSIX. Os arquivos Pkgdef são criados usando o [Utilitário CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md). Para obter mais informações sobre Visual Studio implantação de pacote, consulte [Envio Visual Studio extensões](../../extensibility/shipping-visual-studio-extensions.md).

 O RegPkg.exe utilitário registra um VSPackage com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e o prepara para implantação. Esse utilitário é usado nos bastidores durante o desenvolvimento do VSPackage. Ele é executado como parte do processo de build para que você possa criar e executar um VSPackage no hive experimental.

 RegPkg pode gerar scripts de registro do sistema em vários formatos. Você pode incorporar esses scripts em projetos de implantação, como projetos .msi ou Windows Installer de ferramentas XML.

 RegPkg.exe normalmente está localizado em \<*Visual Studio SDK installation path*>\VisualStudioIntegration\Tools\Bin\RegPkg.exe. RegPkg segue esta sintaxe:

```
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath
```

 /root:root Executa o registro na raiz [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] especificada.

 /regfile:FileName Cria um arquivo .reg em vez de atualizar o Registro.  Não pode ser usado com /vrgfile ou /rgsfile ou /wixfile.

 /rgsfile:FileName Cria um arquivo .rgs em vez de atualizar o Registro.  Não pode ser usado com /vrgfile, /regfile ou /wixfile.

 /vrgfile:FileName Cria um arquivo .vrg em vez de atualizar o Registro.  Não pode ser usado com /regfile ou /rgsfile ou /wixfile.

 /rgm Cria um arquivo .rgm além do arquivo rgs.  Deve ser combinado com /rgsfile.

 /wixfile:FileName Cria um arquivo compatível com o Windows Installer xml toolset em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /vrgfile.

 /codebase Força o registro com CodeBase em vez de Assembly.

 /assembly Força o registro com Assembly em vez de CodeBase.

 /unregister Unregisters this package.  Não pode ser usado

 com /regfile ou /vrgfile ou /rgsfile ou /wixfile.

## <a name="see-also"></a>Confira também
- [VSPackages](../../extensibility/internals/vspackages.md)
- [Solucionando problemas de registro de pacote RegPkg](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
