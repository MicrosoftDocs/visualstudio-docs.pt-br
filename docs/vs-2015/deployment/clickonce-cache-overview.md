---
title: Visão geral do Cache do ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 5e976877a045b6efc7ca3d9fb103b9d1a8e88df7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49217289"
---
# <a name="clickonce-cache-overview"></a>Visão geral do cache do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos, se eles são instalados localmente ou hospedados online, são armazenados no computador cliente em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]aplicativo *cache*. Um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] cache é uma família de diretórios sob o diretório de configurações Local da pasta de documentos e configurações do usuário atual. Esse cache contém todos os arquivos do aplicativo, incluindo assemblies, arquivos de configuração, aplicativo e as configurações de usuário e diretório de dados. O cache também é responsável para migrar o diretório de dados do aplicativo para a versão mais recente. Para obter mais informações sobre migração de dados, consulte [acessando dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md).  
  
 Fornecendo um único local para o armazenamento de aplicativos, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] assume a tarefa de gerenciar a instalação física de um aplicativo do usuário. O cache também ajuda a isolar os aplicativos ao manter os assemblies e arquivos de dados para todos os aplicativos e suas versões distintas separam uns dos outros. Por exemplo, quando você atualiza um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, versão e seus recursos de dados são fornecidos com seus próprios diretórios no cache.  
  
## <a name="cache-storage-quota"></a>Cota de armazenamento de cache  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos que são hospedados online são restritos na quantidade de espaço que pode ser ocupado por uma cota que limita o tamanho do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] cache. O tamanho do cache se aplica a todos os aplicativos do usuário online; um único aplicativo parcialmente confiável, online é limitado a que ocupa metade do espaço de cota. Aplicativos instalados não são limitados pelo tamanho do cache e não contam para o limite de cache. Para todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos, o cache retém apenas a versão atual e a versão instalada anteriormente.  
  
 Por padrão, os computadores cliente têm 250 MB de armazenamento online [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos. Arquivos de dados não contam para esse limite. Um administrador do sistema pode ampliar ou reduzir essa cota em um computador cliente específico, alterando a chave do registro, HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB, que é um valor DWORD que expresse o tamanho do cache em quilobytes. Por exemplo, para reduzir o tamanho do cache de 50 MB, altere esse valor para 51200.  
  
## <a name="see-also"></a>Consulte também  
 [Acessando dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)



