---
title: 'Depuração ASP.NET: requisitos do sistema | Microsoft Docs'
description: Examine os requisitos de software e segurança para a depuração local do ASP.NET, na qual o Visual Studio e o aplicativo Web são executados no mesmo computador e na depuração remota.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 8ab32e855ee93ceb328bc33340597ce65e3ee871
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866093"
---
# <a name="aspnet-debugging-system-requirements"></a>Depuração do ASP.NET: requisitos do sistema
Este tópico descreve os requisitos de software e de segurança para cenários de depuração do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]:

- Depuração local, na qual o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e o aplicativo Web são executados no mesmo computador. Há duas versões do controle desse cenário:

  - O código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] reside no sistema de arquivos.

  - O código do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] reside em um site do IIS.

- Depuração remota, na qual o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é executado em um computador cliente e depura um aplicativo Web que esteja em execução em um computador de servidor remoto.

## <a name="security-requirements"></a>Requisitos de segurança
 Para a depuração remota, os computadores locais e remotos devem estar em uma configuração de domínio ou em uma configuração de grupo de trabalho.

 Para depurar o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo de trabalho (hospedado por um pool de aplicativos), você deve ter permissão para depurar esse processo. Por padrão, [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] os aplicativos anteriores ao IIS 6,0 são executados como o usuário **ASPNET** . No IIS 6,0 e no IIS 7,0, a conta de **serviço de rede** é o padrão. Se o processo de trabalho estiver sendo executado como **ASPNET** ou como **SERVIÇO DE REDE**, você deverá ter privilégios de administrador para depurá-lo.

 > [!IMPORTANT]
 > A partir do Windows Server 2008 R2, recomendamos o uso do [ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities) como a identidade de cada pool de aplicativos.

 O nome do processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] varia de acordo com o cenário de depuração e a versão do IIS. Para obter mais informações, consulte [como: localizar o nome do processo ASP.net](../debugger/how-to-find-the-name-of-the-aspnet-process.md).

 Você pode alterar a conta de usuário sob a qual o [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] processo de trabalho é executado editando o machine.config arquivo no servidor que está executando o IIS. A melhor maneira de fazer isso é usar o **Gerenciador do serviços de informações da Internet (IIS)**. Para obter mais informações, consulte [como: executar o processo de trabalho em uma conta de usuário](../debugger/how-to-run-the-worker-process-under-a-user-account.md).

 Se você alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado em sua própria conta de usuário, não precisará ser um administrador no servidor que está executando o IIS.

> [!CAUTION]
> Antes de alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado em uma conta diferente, considere as possíveis consequências se o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] for invadido ao executar sob essa conta. As contas de usuário ASPNET and NETWORK SERVICE são executadas com as permissões mínimas, reduzindo o dano possível se o processo for invadido. Se você precisar alterar o processo de trabalho do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] para ser executado sob uma conta que tenha permissões maiores, o dano potencialmente será maior.

## <a name="see-also"></a>Confira também

- [Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [Como executar o processo de trabalho em uma conta de usuário](../debugger/how-to-run-the-worker-process-under-a-user-account.md)