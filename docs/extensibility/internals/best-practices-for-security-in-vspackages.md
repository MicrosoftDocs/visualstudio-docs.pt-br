---
title: Práticas recomendadas de segurança no VSPackages | Microsoft Docs
description: Saiba mais sobre as práticas recomendadas de segurança em um VSPackage, a unidade básica de segurança e a implantação para um aplicativo do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cca66d6c1fce0deb8103a7d626c16a4e81bc7b5f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086203"
---
# <a name="best-practices-for-security-in-vspackages"></a>Práticas recomendadas de segurança no VSPackages
Para instalar o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] em seu computador, você deve estar executando o em um contexto com credenciais administrativas. A unidade básica de segurança e implantação de um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] aplicativo é a [VSPackage](../../extensibility/internals/vspackages.md). Um VSPackage deve ser registrado usando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , que também requer credenciais administrativas.

 Os administradores têm permissões completas para gravar no registro e no sistema de arquivos e executar qualquer código. Você deve ter essas permissões para desenvolver, implantar ou instalar um VSPackage.

 Assim que ele é instalado, um VSPackage é totalmente confiável. Devido a esse alto nível de permissão associado a um VSPackage, é possível instalar inadvertidamente um VSPackage que tenha uma intenção mal-intencionada.

 Os usuários devem garantir que eles instalem o VSPackages somente de fontes confiáveis. As empresas que estão desenvolvendo o VSPackages devem nomear e assinar com segurança, para garantir ao usuário que a violação seja impedida. As empresas que estão desenvolvendo o VSPackages devem examinar suas dependências externas, como serviços Web e instalação remota, para avaliar e corrigir problemas de segurança.

 Para obter mais informações, consulte [diretrizes de codificação segura para o .NET Framework](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90)).

## <a name="see-also"></a>Confira também
- [Segurança do suplemento](/previous-versions/1326zbk3(v=vs.140))
- [Segurança do DDEX](/previous-versions/bb163703(v=vs.140))