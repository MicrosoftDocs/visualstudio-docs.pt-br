---
title: Utilitário de RegPkg | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
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
ms.openlocfilehash: 5d677aaf155e533c27a775f3995b53dd59b65385
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130939"
---
# <a name="regpkg-utility"></a>Utilitário de RegPkg
> [!NOTE]
>  É a melhor maneira de registrar os pacotes no Visual Studio usando .pkgdef arquivos. Isso permite a implantação de extensão sem a necessidade de acessar o registro do sistema, que é um requisito para a implantação do VSIX. Arquivos de Pkgdef são criados usando o [CreatePkgDef utilitário](../../extensibility/internals/createpkgdef-utility.md). Para obter mais informações sobre implantação de pacote do Visual Studio, consulte [envio extensões do Visual Studio](../../extensibility/shipping-visual-studio-extensions.md).  
  
 O utilitário RegPkg.exe registra um VSPackage com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e prepará-lo para implantação. Esse utilitário é usado em segundo plano durante o desenvolvimento de VSPackage. Ele é executado como parte do processo de compilação para que você pode criar e executar um VSPackage na seção experimental.  
  
 RegPkg pode gerar scripts de registro do sistema em vários formatos. Você pode incorporar esses scripts em projetos de implantação, como arquivos de conjunto de ferramentas XML do Windows Installer ou. msi projetos.  
  
 RegPkg.exe normalmente está localizado em \< *caminho de instalação do SDK do Visual Studio*> \VisualStudioIntegration\Tools\Bin\RegPkg.exe. RegPkg segue esta sintaxe:  
  
```  
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath  
```  
  
 /root:root  
 Executa o registro em especificado  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] raiz.  
  
 /regfile:filename  
 Cria um arquivo. reg em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /rgsfile ou /wixfile.  
  
 /rgsfile:filename  
 Cria um arquivo. rgs em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /regfile ou /wixfile.  
  
 /vrgfile:filename  
 Cria um arquivo. vrg em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /wixfile.  
  
 /rgm  
 Cria um arquivo .rgm além do arquivo rgs.  Deve ser combinada com /rgsfile.  
  
 /wixfile:filename  
 Cria um arquivo compatível com o conjunto de ferramentas XML do Windows Installer em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /vrgfile.  
  
 /codebase  
 Registro de forças com base de código em vez de Assembly.  
  
 /assembly  
 Registro de forças com o Assembly em vez de base de código.  
  
 /unregister  
 Cancela o registro deste pacote.  Não pode ser usado  
  
 com /regfile ou /vrgfile ou /rgsfile ou /wixfile.  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages](../../extensibility/internals/vspackages.md)  
 [Solucionar problemas de registro de pacote RegPkg](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)