---
title: 'Depuração do ASP.NET: Requisitos do sistema | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications, system requirements
- debugging ASP.NET Web applications, security requirements
ms.assetid: 7810b9b2-debf-4271-8fc7-1df031123255
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 71b6cbc3f523b8f21b21b0e69b1d6e45e23acb0c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915341"
---
# <a name="aspnet-debugging-system-requirements"></a>Depuração do ASP.NET: requisitos do sistema
Este tópico descreve os requisitos de software e segurança para [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] cenários de depuração:  
  
- Depuração local, na qual o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e o aplicativo Web são executados no mesmo computador. Há duas versões do controle desse cenário:  
  
  - O código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] reside no sistema de arquivos.  
  
  - O código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] reside em um site do IIS.  
  
- Depuração remota, na qual o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é executado em um computador cliente e depura um aplicativo Web que esteja em execução em um computador de servidor remoto.  
  
## <a name="security-requirements"></a>Requisitos de segurança  
 Para a depuração remota, os computadores locais e remotos devem estar em uma configuração de domínio ou em uma configuração de grupo de trabalho.  
  
 Para depurar o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] o processo de trabalho (hospedado por um Pool de aplicativos), você deve ter permissão para depurar esse processo. Por padrão, [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos antes do IIS 6.0 são executados como a **ASPNET** usuário. No IIS 6.0 e IIS 7.0, o **serviço de rede** conta é o padrão. Se o processo de trabalho é executado como **ASPNET**, ou como **serviço de rede**, você deve ter privilégios de administrador para depurá-lo.

 > [!IMPORTANT]
 > Começando com o Windows Server 2008 R2, recomendamos o uso do [ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities) como a identidade para cada pool de aplicativos.
  
 O nome do processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] varia de acordo com o cenário de depuração e a versão do IIS. Para obter mais informações, consulte [como: localizar o nome do processo do ASP.NET](../debugger/how-to-find-the-name-of-the-aspnet-process.md).  
  
 Você pode alterar o usuário da conta que o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] o processo de trabalho é executado, editando o arquivo Machine. config no servidor que está executando o IIS. A melhor maneira de fazer isso é usar o **serviços de informações da Internet (IIS) Manager**. Para obter mais informações, consulte [como: executar o trabalho processo sob uma conta de usuário](../debugger/how-to-run-the-worker-process-under-a-user-account.md).  
  
 Se você alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado em sua própria conta de usuário, não precisará ser um administrador no servidor que está executando o IIS.  
  
> [!CAUTION]
>  Antes de alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado em uma conta diferente, considere as possíveis consequências se o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] for invadido ao executar sob essa conta. As contas de usuário ASPNET and NETWORK SERVICE são executadas com as permissões mínimas, reduzindo o dano possível se o processo for invadido. Se você precisar alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado sob uma conta que tenha permissões maiores, o dano potencialmente será maior.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)   
 [Como executar o processo de trabalho em uma conta de usuário](../debugger/how-to-run-the-worker-process-under-a-user-account.md)