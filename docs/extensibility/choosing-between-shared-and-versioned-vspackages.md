---
title: Escolhendo entre VSPackages compartilhado e com controle de versão | Microsoft Docs
description: Saiba mais sobre as instalações lado a lado do VSPackages por meio de estratégias compartilhadas ou com controle de versão, com várias versões do Visual Studio e do .NET Framework.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 257158ec3c8d4364e1aa52133c457e24fd98cff3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078234"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>Escolha entre VSPackages compartilhadas e com controle de versão
Versões diferentes do Visual Studio podem coexistir no mesmo computador. O VSPackages pode dar suporte a qualquer combinação de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] versões.

 Você pode habilitar instalações lado a lado do VSPackages por meio de uma das duas estratégias, a estratégia compartilhada ou a estratégia com controle de versão. Ambos acomodam a presença de várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e de versões associadas do .NET Framework.

 Na estratégia compartilhada, um VSPackage é registrado para uso em várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Na estratégia com versão, várias DLLs VSPackage são instaladas, uma para cada versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] à qual você dá suporte.

## <a name="shared-vspackages"></a>VSPackages compartilhado
 Usar um VSPackage compartilhado é apropriado quando você usa o mesmo VSPackage em várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Para implementar um VSPackage compartilhado, você deve executar as seguintes etapas:

- Torne seu VSPackage compatível com várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Duas maneiras de fazer isso estão disponíveis:

  - Limite seu VSPackage a usar apenas os recursos da versão mais antiga do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que você dá suporte.

  - Programe seu VSPackage para adaptar-se à versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em que está em execução. Em seguida, se as consultas para serviços mais recentes falharem, seu VSPackage poderá oferecer outros serviços com suporte em versões mais antigas do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

- Registre seu VSPackage adequadamente. Para obter mais informações, consulte [registro de VSPackage](../extensibility/internals/vspackage-registration.md) e [registro VSPackage gerenciado](/previous-versions/bb166783(v=vs.100)).

- Registre as extensões de arquivo adequadamente. Para obter mais informações, consulte [registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md).

- Crie um instalador que implanta seu VSPackage para as versões apropriadas do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Para obter mais informações, consulte [instalando o VSPackages com Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) e [Gerenciamento de componentes](../extensibility/internals/component-management.md).

- Resolva o problema de colisões de registro. Para obter mais informações, consulte [VSPackage Registration](../extensibility/internals/vspackage-registration.md).

- Verifique se os arquivos compartilhados e com controle de versão respeitam a contagem de referência para permitir a instalação e remoção segura de várias versões. Para obter mais informações, consulte [Gerenciamento de componentes](../extensibility/internals/component-management.md).

## <a name="versioned-vspackages"></a>VSPackages com controle de versão
 Sob a estratégia de VSPackage com controle de versão, você cria um VSPackage para cada versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] com suporte. Fazer isso é apropriado quando você espera aproveitar os serviços fornecidos pelas versões posteriores do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , pois cada VSPackage pode evoluir sem afetar os outros. No entanto, a estratégia com controle de versão da criação de vários binários, seja de uma única base de código ou de várias bases de código independentes, pode envolver mais desenvolvimento inicial do que a estratégia compartilhada. Além disso, o trabalho de configuração adicional pode ser necessário porque você deve criar uma configuração separada para cada versão ou uma única configuração que detecta as versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] instaladas e que o VSPackage dá suporte.

## <a name="binary-compatibility"></a>Compatibilidade binária
 Geralmente, a compatibilidade binária permite que VSPackages de código nativo desenvolvidos com versões anteriores do Visual Studio sejam executadas em versões posteriores do Visual Studio. No entanto, há três exceções importantes:

- Se o seu VSPackage se basear em uma versão específica do Common Language Runtime, ele deverá determinar em qual versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] está sendo executada.

- Um VSPackage pode ter uma dependência em um recurso específico de outro VSPackage ou outro produto. Consequentemente, o VSPackage pode executar apenas onde a dependência é satisfeita.

- Um VSPackage pode ser afetado por uma correção de segurança em uma [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Service Pack ou em uma versão posterior do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Nesses casos, um VSPackage desenvolvido com uma versão anterior do [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] pode não ser executado em versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] após a aplicação da correção de segurança. No entanto, você pode recompilar seu pacote com a versão mais recente e fazer com que ele também seja executado em versões anteriores.

  O VSPackages gerenciado deve ser criado usando uma versão do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e o [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] que corresponde à versão de destino do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

  Além de planejar a compatibilidade binária para seus binários do VSPackage, você também deve considerar os formatos de arquivo da solução e do projeto. Se o seu VSPackage cria um novo tipo de projeto, você deve decidir se ele pode ser executado em apenas uma versão ou em várias versões do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Para obter mais informações, consulte [upgrading Custom Projects](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects).

## <a name="see-also"></a>Confira também
- [Instalando o VSPackages com o Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [Gerenciamento de componentes](../extensibility/internals/component-management.md)