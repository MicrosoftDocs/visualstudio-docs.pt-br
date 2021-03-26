---
title: Escolhendo o diretório de instalação para um VSPackage | Microsoft Docs
description: Saiba como escolher o diretório de instalação para um VSPackage e seus arquivos de suporte usando fatores como, por exemplo, se eles são gerenciados ou não.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6442a8475c862693b851be783ae85bbb0a2e90af
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082108"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>Escolha o diretório de instalação para um VSPackage
Um VSPackage e seus arquivos de suporte devem estar no sistema de arquivos de um usuário. O local depende de o VSPackage ser gerenciado ou não gerenciado, seu esquema de controle de versão lado a lado e a escolha do usuário.

## <a name="unmanaged-vspackages"></a>VSPackages não gerenciado
 Um VSPackage não gerenciado é um servidor COM que pode ser instalado em qualquer local. Suas informações de registro devem refletir com precisão seu local. A interface do usuário do instalador deve fornecer um local padrão como um subdiretório do `ProgramFilesFolder` valor da propriedade Windows Installer. Por exemplo:

*&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \V1.0\\*

 O usuário deve ter permissão para alterar o diretório padrão para acomodar usuários que mantêm uma pequena partição de inicialização e preferem instalar aplicativos e ferramentas em outro volume.

 Se o esquema lado a lado usar um VSPackage com controle de versão, você poderá usar subdiretórios para armazenar versões diferentes. Por exemplo:

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ v 1.0 \\ 2002\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ v 1.0 \\ 2003\\*

 *&lt;ProgramFilesFolder &gt; \\ &lt; MyCompany &gt; \\ &lt; MyVSPackageProduct &gt; \\ v 1.0 \\ 2005\\*

## <a name="managed-vspackages"></a>VSPackages gerenciados
 O VSPackages gerenciado também pode ser instalado em qualquer local. No entanto, você deve considerar sempre instalá-los no GAC (cache de assembly global) para reduzir os tempos de carregamento do assembly. Como os VSPackages gerenciados são sempre assemblies com nomes fortes, instalá-los no GAC significa que a verificação de assinatura de nome forte leva apenas no momento da instalação. Os assemblies de nome forte instalados em outro lugar no sistema de arquivos devem ter suas assinaturas verificadas toda vez que forem carregados. Ao instalar o VSPackages gerenciado no GAC, use a opção **/assembly** da ferramenta regpkg para gravar entradas do registro apontando para o nome forte do assembly.

 Se você instalar o VSPackages gerenciado em um local diferente do GAC, siga o aviso anterior fornecido para VSPackages não gerenciado para escolher hierarquias de diretório. Use a opção **/codebase** da ferramenta regpkg para gravar entradas do registro apontando para o caminho do assembly VSPackage.

 Para obter mais informações, consulte [registrar e cancelar o registro de VSPackages](../../extensibility/registering-and-unregistering-vspackages.md).

## <a name="satellite-dlls"></a>DLLs satélites
 Por convenção, as DLLs satélite VSPackage, que contêm recursos para uma localidade específica, estão localizadas em subdiretórios do diretório *VSPackage* . Os subdiretórios correspondem aos valores de LCID (ID de localidade).

 O artigo [Manage VSPackages](../../extensibility/managing-vspackages.md) indica que as entradas do registro controlam onde [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] realmente procura pela DLL satélite de um VSPackage. No entanto, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o tenta carregar uma DLL satélite em um subdiretório nomeado para um valor LCID, na seguinte ordem:

1. LCID padrão (LCID do Visual Studio; por exemplo, *\ 1033* para inglês)

2. LCID padrão com o subidioma padrão.

3. LCID padrão do sistema.

4. LCID padrão do sistema com o subidioma padrão.

5. Inglês americano (*. \ 1033* ou *.\0x409*).

Se a DLL VSPackage incluir recursos e os pontos de entrada do registro **SatelliteDll\DllName** , o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tentará carregá-los na ordem acima.

## <a name="see-also"></a>Confira também
- [Escolha entre VSPackages compartilhadas e com controle de versão](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [Gerenciar VSPackages](../../extensibility/managing-vspackages.md)
- [Gerenciar registro de pacote](/previous-versions/bb166783(v=vs.100))