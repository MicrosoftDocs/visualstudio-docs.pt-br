---
title: Instalando o VSPackages com o Windows Installer | Microsoft Docs
description: Saiba como usar o Microsoft Windows Installer para instalar um VSPackage e seus arquivos dependentes, bem como registrá-los e integrá-los ao Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1638f6d041dda28ca79492ba2c8e6ef772ce8bc7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074659"
---
# <a name="installing-vspackages-with-windows-installer"></a>Instalando VSPackages com o Windows Installer
A integração do seu VSPackage ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] requer mais do que apenas copiar arquivos para o computador de um usuário. O instalador de seu VSPackage deve instalar o VSPackage e seus arquivos dependentes, bem como registrá-los e integrá-los ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Seu VSPackage pode aproveitar os recursos de integração, como exibir um ícone na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tela inicial e na caixa de diálogo sobre.

 Microsoft Windows Installer arquivos são a maneira recomendada para distribuir seu VSPackages. Os pacotes de Windows Installer fáceis de usar podem ser executados em qualquer sistema operacional Windows com suporte no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Para obter mais informações, consulte [Windows Installer](/previous-versions/2kt85ked(v=vs.120)).

## <a name="in-this-section"></a>Nesta seção
- [Noções básicas do Windows Installer](../../extensibility/internals/windows-installer-basics.md)

 Fornece uma visão geral do Windows Installer.

- [Cenários de instalação do VSPackage](../../extensibility/internals/vspackage-setup-scenarios.md)

 Discute diferentes maneiras pelas quais você pode dar suporte a instalações lado a lado de seu VSPackages e do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Criação de um pacote do Windows Installer](../../extensibility/internals/authoring-a-windows-installer-package.md)

 Fornece uma visão geral das etapas típicas que os instaladores seguem para instalar e integrar o VSPackages corretamente ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Detecção de requisitos do sistema](../../extensibility/internals/detecting-system-requirements.md)

 Descreve como um instalador pode detectar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e seus componentes e cancelar a instalação se os requisitos de VSPackage não forem atendidos.

- [Gerenciamento de componentes](../../extensibility/internals/component-management.md)

 Discute como desenvolver um instalador que manterá a integridade das versões anteriores do produto.

- [Escolhendo o diretório de instalação de um VSPackage](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 Resume as opções para localizar VSPackages.

- [Registro do VSPackage](../../extensibility/internals/vspackage-registration.md)

 Discute como os VSPackages são registrados no momento da instalação e por que o auto-registro é uma má ideia.

- [Tipos de projeto de implantação](../../extensibility/internals/deploying-project-types.md)

 Discute como usar o novo agregador de tipo de projeto para tipos de projeto de código gerenciado.

- [Como gerar informações de registro para um instalador](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 Explica como usar RegPkg.exe para gerar um manifesto de registro para um VSPackage gerenciado.

- [Comandos que precisam ser executados após a instalação](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 Explica como executar comandos pós-instalação para integrar o VSPackages ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- [Desinstalando um VSPackage com o Windows Installer](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 Descreve as etapas que o instalador deve executar quando os usuários desinstalam o VSPackage.