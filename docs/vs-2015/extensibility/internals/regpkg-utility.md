---
title: Utilitário RegPkg | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- regpkg, registration utility
- registration, regpkg utility
ms.assetid: 1683ee18-59d1-4bab-a674-dd00dd960de3
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1895d3b57e5109f824728021cb1d64f0c527384b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436593"
---
# <a name="regpkg-utility"></a>Utilitário RegPkg
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!NOTE]
> É a maneira preferencial para registrar os pacotes no Visual Studio por meio de arquivos. pkgdef. Isso permite a implantação de extensão sem a necessidade de acessar o registro do sistema, que é um requisito para a implantação do VSIX. Pkgdef arquivos são criados usando o [utilitário CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md). Para obter mais informações sobre a implantação de pacote do Visual Studio, consulte [envio extensões do Visual Studio](../../extensibility/shipping-visual-studio-extensions.md).  
  
 O utilitário RegPkg.exe registra um VSPackage com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e prepará-lo para implantação. Esse utilitário é usado nos bastidores durante o desenvolvimento de VSPackage. Ele é executado como parte do processo de compilação para que você pode compilar e executar um VSPackage no hive experimental.  
  
 RegPkg pode gerar scripts de registro do sistema em vários formatos. Você pode incorporar esses scripts em projetos de implantação, como arquivos de conjunto de ferramentas do Windows Installer XML ou projetos. msi.  
  
 RegPkg.exe normalmente está localizado em \< *caminho de instalação do SDK do Visual Studio*> \VisualStudioIntegration\Tools\Bin\RegPkg.exe. RegPkg segue esta sintaxe:  
  
```  
RegPkg [/root:<root>] [/regfile:<regfile>] [/rgsfile:<rgsfile> [/rgm]] [/vrgfile:<vrgfile>] [/codebase | /assembly] [/unregister] AssemblyPath  
```  
  
 /root:root  
 Executa o registro sob especificado  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] raiz.  
  
 /regfile:FileName  
 Cria um arquivo. reg em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /rgsfile ou /wixfile.  
  
 /rgsfile:FileName  
 Cria um arquivo. rgs em vez de atualizar o registro.  Não pode ser usado com /vrgfile ou /regfile ou /wixfile.  
  
 /vrgfile:FileName  
 Cria um arquivo .vrg em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /wixfile.  
  
 /rgm  
 Cria um arquivo .rgm além do arquivo rgs.  Deve ser combinada com /rgsfile.  
  
 /wixfile:FileName  
 Cria um arquivo compatível com o Windows Installer XML conjunto de ferramentas em vez de atualizar o registro.  Não pode ser usado com /regfile ou /rgsfile ou /vrgfile.  
  
 /codebase  
 Registro de forças com base de código em vez de um Assembly.  
  
 /assembly  
 Registro de forças com o Assembly em vez da Base de código.  
  
 /unregister  
 Cancela o registro desse pacote.  Não pode ser usado  
  
 com /regfile ou /vrgfile ou /rgsfile ou /wixfile.  
  
## <a name="see-also"></a>Consulte também  
 [Liberando um produto](../../misc/releasing-a-visual-studio-integration-product.md)   
 [Solucionar problemas de registro de pacote RegPkg](../../extensibility/internals/troubleshooting-regpkg-package-registration.md)
