---
title: Utilitário RegPkg | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e3f9eecfaeffd19ece7e0ca2fe14e3f95556503d
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53904871"
---
# <a name="regpkg-utility"></a>Utilitário RegPkg
> [!NOTE]
>  É a maneira preferencial para registrar os pacotes no Visual Studio por meio de arquivos. pkgdef. Isso permite a implantação de extensão sem a necessidade de acessar o registro do sistema, que é um requisito para a implantação do VSIX. Pkgdef arquivos são criados usando o [utilitário CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md). Para obter mais informações sobre a implantação de pacote do Visual Studio, consulte [envio extensões do Visual Studio](../../extensibility/shipping-visual-studio-extensions.md).  
  
 O utilitário RegPkg.exe registra um VSPackage com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e prepará-lo para implantação. Esse utilitário é usado nos bastidores durante o desenvolvimento de VSPackage. Ele é executado como parte do processo de compilação para que você pode compilar e executar um VSPackage no hive experimental.  
  
 RegPkg pode gerar scripts de registro do sistema em vários formatos. Você pode incorporar esses scripts em projetos de implantação, como arquivos de conjunto de ferramentas do Windows Installer XML ou projetos. msi.  
  
 RegPkg.exe normalmente está localizado em \< *caminho de instalação do SDK do Visual Studio*> \VisualStudioIntegration\Tools\Bin\RegPkg.exe. RegPkg segue esta sintaxe:  
  
```  
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath  
```  
  
 /root:root  
 Executa o registro sob especificado  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] raiz.  
  
 /regfile:filename  
 Cria um arquivo. reg em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /rgsfile ou /wixfile.  
  
 /rgsfile:filename  
 Cria um arquivo. rgs em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /regfile ou /wixfile.  
  
 /vrgfile:filename  
 Cria um arquivo .vrg em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /wixfile.  
  
 /rgm  
 Cria um arquivo .rgm além do arquivo rgs.  Deve ser combinada com /rgsfile.  
  
 /wixfile:filename  
 Cria um arquivo compatível com o Windows Installer XML conjunto de ferramentas em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /vrgfile.  
  
 /codebase  
 Registro de forças com base de código em vez de um Assembly.  
  
 /assembly  
 Registro de forças com o Assembly em vez da Base de código.  
  
 / Cancelar  
 Cancela o registro desse pacote.  Não pode ser usado  
  
 com /regfile ou /vrgfile ou /rgsfile ou /wixfile.  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../../extensibility/internals/vspackages.md)  
 [Solucionar problemas de registro de pacote RegPkg](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)