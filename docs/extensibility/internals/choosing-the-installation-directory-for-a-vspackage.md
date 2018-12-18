---
title: Escolhendo o diretório de instalação para um VSPackage | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4e32f2581e4980feebbbecb3cc8e7aa98bfeb670
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370946"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>Escolha o diretório de instalação para um VSPackage
Um VSPackage e seus arquivos de suporte devem estar no sistema de arquivos do usuário. O local depende se o VSPackage é gerenciado ou não, seu esquema de controle de versão lado a lado e escolha do usuário.  
  
## <a name="unmanaged-vspackages"></a>VSPackages gerenciados  
 Um VSPackage não gerenciado é um servidor COM que pode ser instalado em qualquer local. Suas informações de registro devem refletir com precisão o seu local. Sua interface de usuário (IU) installer deve fornecer um local padrão como um subdiretório do `ProgramFilesFolder` valor da propriedade do Windows Installer. Por exemplo:  
  
*&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\V1.0\\*
  
 O usuário deve ter permissão para alterar o diretório padrão para acomodar os usuários que manter uma partição de inicialização de pequeno e preferir instalar aplicativos e ferramentas em outro volume.  
  
 Se o esquema de lado a lado usa um VSPackage de controle de versão, você pode usar subdiretórios para armazenar versões diferentes. Por exemplo:

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2002\\*
  
 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2003\\*
  
 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2005\\*
  
## <a name="managed-vspackages"></a>VSPackages gerenciados  
 VSPackages gerenciados também podem ser instalados em qualquer local. No entanto, você deve considerar sempre instalá-los para o cache de assembly global (GAC) para reduzir os tempos de carregamento de assembly. Como os VSPackages gerenciados sempre são assemblies de nome forte, instalá-los no GAC significa que sua verificação de assinatura de nome forte leva apenas no momento da instalação. Assemblies de nome forte instalados em outro lugar no sistema de arquivos devem ter suas assinaturas e verificadas sempre que eles são carregados. Quando você instala os VSPackages gerenciados no GAC, use a ferramenta de regpkg **/assembly** switch para gravar as entradas do registro que aponta para o nome forte do assembly.  
  
 Se você instalar VSPackages gerenciados em um local diferente no GAC, seguir o conselho anterior fornecido para VSPackages gerenciados para a escolha de hierarquias de diretório. Use a ferramenta de regpkg **/codebase** switch para gravar as entradas do registro que aponta para o caminho do assembly VSPackage.  
  
 Para obter mais informações, consulte [registrar e cancelar o registro de VSPackages](../../extensibility/registering-and-unregistering-vspackages.md).  
  
## <a name="satellite-dlls"></a>DLLs satélite  
 Por convenção, o VSPackage DLLs, que contêm recursos para uma determinada localidade, satélites estão localizados em subpastas do *VSPackage* directory. Os subdiretórios correspondem aos valores de LCID (identificação) de localidade.  
  
 O [gerenciar VSPackages](../../extensibility/managing-vspackages.md) artigo indica que as entradas do registro controlam onde [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , na verdade, o DLL de satélite procura um VSPackage. No entanto, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tenta carregar uma DLL satélite em um subdiretório nomeado para um valor LCID, na seguinte ordem:  
  
1.  LCID de padrão (LCID do Visual Studio; por exemplo, *\1033* para inglês)  
  
2.  LCID padrão com a subidioma padrão.  
  
3.  LCID padrão do sistema.  
  
4.  Padrão do sistema LCID com subidioma o padrão.  
  
5.  DOS EUA Inglês (*. \1033* ou *. \0x409*).  
  

Se a sua DLL VSPackage inclui recursos e o **SatelliteDll\DllName** entrada de registro aponta para ela, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tentará carregá-los na ordem acima.  
  
## <a name="see-also"></a>Consulte também  
 [Escolher entre VSPackages compartilhados e com controle de versão](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)   
 [Gerenciar VSPackages](../../extensibility/managing-vspackages.md)   
 [Gerenciar registro do pacote](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)