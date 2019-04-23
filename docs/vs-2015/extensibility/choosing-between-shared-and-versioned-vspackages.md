---
title: Escolher entre VSPackages compartilhados e com controle de versão | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f6df66c3a6f34e6137850c68785d0eaadbb13a26
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60088139"
---
# <a name="choosing-between-shared-and-versioned-vspackages"></a>Escolhendo entre VSPackages compartilhados e com controle de versão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diferentes versões do Visual Studio podem coexistir no mesmo computador. Os VSPackages pode dar suporte a qualquer combinação de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] versões.  
  
 Você pode habilitar as instalações lado a lado de VSPackages por meio de qualquer uma das duas estratégias, a estratégia compartilhada ou a estratégia de controle de versão. Ambos acomodar a presença de várias versões dos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e associados a versões do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
 A estratégia compartilhado, um VSPackage é registrado para uso em várias versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. A estratégia de controle de versão, várias DLLs de VSPackage são instalados, uma para cada versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que dão suporte a você.  
  
## <a name="shared-vspackages"></a>VSPackages compartilhados  
 O uso de um VSPackage compartilhado é apropriado quando você usa o mesmo VSPackage em várias versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para implementar um VSPackage compartilhado, você deve executar as seguintes etapas:  
  
- Tornar o VSPackage compatível com várias versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Duas maneiras de fazer, portanto, estão disponíveis:  
  
    - Limitar o VSPackage usando somente os recursos da versão mais antiga do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que dão suporte a você.  
  
    - Programar o VSPackage para adaptar-se para a versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no qual ele está sendo executado. Em seguida, se as consultas para os serviços mais recentes falhar, o VSPackage pode oferecer outros serviços que têm suporte em versões mais antigas do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
- Registre o VSPackage adequadamente. Para obter mais informações, consulte [o VSPackage](../extensibility/internals/vspackage-registration.md) e [gerenciado o VSPackage](http://msdn.microsoft.com/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1).  
  
- Registre extensões de arquivo adequadamente. Para obter mais informações, consulte [registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md).  
  
- Criar um instalador que implanta o VSPackage para as versões apropriadas dos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações, consulte [instalando VSPackages com o Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) e [gerenciamento de componente](../extensibility/internals/component-management.md).  
  
- Resolver o problema de colisões de registro. Para obter mais informações, consulte [o VSPackage](../extensibility/internals/vspackage-registration.md).  
  
- Certifique-se de que arquivos com controle de versão e compartilhados respeitarem permitir a instalação de segurança e remoção de várias versões de contagem de referência. Para obter mais informações, consulte [componente de gerenciamento](../extensibility/internals/component-management.md).  
  
## <a name="versioned-vspackages"></a>VSPackages com controle de versão  
 Sob a estratégia de VSPackage de controle de versão, você criar um VSPackage para cada versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que dão suporte a você. Isso é apropriado quando você espera tirar proveito dos serviços fornecidos por versões mais recentes do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], porque cada VSPackage pode evoluir sem afetar as outras. No entanto, a estratégia de controle de versão de criação de vários binários, de uma única base de código ou de várias bases de código independente, pode envolver mais desenvolvimento inicial que a estratégia compartilhado. Além disso, o trabalho de configuração adicional pode ser necessário porque você deve criar o uma instalação separada para cada versão ou uma única instalação que detecta as versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que são instalados e que suporta o VSPackage.  
  
## <a name="binary-compatibility"></a>Compatibilidade binária  
 Em geral, a compatibilidade binária permite que os VSPackages de código nativo desenvolvidos com versões anteriores do Visual Studio para executar em versões posteriores do Visual Studio. No entanto, há três exceções importantes:  
  
- Se o VSPackage depende de uma versão específica do common language runtime, ele deve determinar em qual versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] está em execução.  
  
- Um VSPackage pode ter uma dependência em um recurso específico do VSPackage outro ou de outro produto. Consequentemente, o VSPackage pode ser executado apenas em que a dependência seja satisfeita.  
  
- Um VSPackage que pode ser afetado por uma correção de segurança em um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] service pack ou uma versão posterior do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Nesses casos, um VSPackage desenvolvido com uma versão anterior da [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] não pode ser executado em versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] após a correção de segurança foi aplicada. No entanto, você pode recompilar seu pacote com a versão mais recente e executá-lo também em versões anteriores.  
  
  VSPackages gerenciados deve ser criados usando uma versão do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e o [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] que corresponde à versão de destino do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
  Além do planejamento para a compatibilidade binária para seus binários de VSPackage, você também deve considerar a solução e formatos de arquivo de projeto. Se o VSPackage cria um novo tipo de projeto, você deve decidir se ele pode ser executado em apenas uma versão ou em várias versões do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Para obter mais informações, consulte [atualização de projetos personalizados](../misc/upgrading-custom-projects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar VSPackages com o Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md)   
 [Gerenciamento de componente](../extensibility/internals/component-management.md)
