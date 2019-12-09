---
title: 'Como: Especificar o tempo de execução do .NET Framework | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, .NET Framework versions
- .NET Framework versions,profililng
ms.assetid: d39f3579-719a-4f47-a97d-5b4232fe4c64
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2f631e8639c1004fa2cb005da3b6c8bcb27f1a9b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203406"
---
# <a name="how-to-specify-the-net-framework-runtime"></a>Como: Especificar o tempo de execução do .NET Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Com o lançamento do [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)], os aplicativos podem ser compostos de módulos que foram compilados usando versões diferentes do tempo de execução do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Por padrão, as Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] analisam o primeiro tempo de execução que é carregado pelo aplicativo. Você pode especificar o tempo de execução a ser analisado ao iniciar um aplicativo com o criador de perfil e ao anexar o criador de perfil a um aplicativo que já esteja em execução.  
  
 **Requisitos**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
### <a name="to-specify-the-net-framework-run-time-to-profile-when-starting-an-application-with-the-profiler"></a>Para especificar o tempo de execução do .NET Framework a ser analisado ao iniciar um aplicativo com o criador de perfil  
  
1. No **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão de desempenho, clique em **Propriedades** e, em seguida, clique em **Avançado**.  
  
     A caixa de listagem **Versão do CLR de Destino** exibe **Automático** e as versões de tempo de execução do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que estão instaladas no computador.  
  
2. Execute uma das seguintes etapas:  
  
    - Clique na versão do CLR que você deseja analisar.  
  
    - Clique em **Automático** para analisar a primeira versão que é carregada pelo aplicativo.  
  
### <a name="to-specify-the-net-framework-run-time-to-profile-when-attaching-the-profiler-to-an-application"></a>Para especificar o tempo de execução do .NET Framework a ser analisado ao anexar o criador de perfil a um aplicativo  
  
1. No menu Analisar, aponte para Criador de Perfil e, em seguida, clique em Anexar/Desanexar.  
  
2. Na caixa de diálogo Anexar Criador de Perfil a Processo, clique no processo você deseja analisar.  
  
     A caixa de listagem **Versão do CLR de Destino** exibe **Automático** e as versões de tempo de execução do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que estão instaladas no computador.  
  
3. Execute uma das seguintes etapas:  
  
    - Clique na versão do CLR que você deseja analisar.  
  
    - Clique em **Automático** para analisar a versão que é carregada quando o criador de perfil se anexa ao aplicativo.
