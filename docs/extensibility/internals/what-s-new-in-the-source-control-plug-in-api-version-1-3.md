---
title: O que&#39;s novos na fonte de controlar o plug-in API versão 1.3 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: abeb2a0a936a5d706e2e3744e9dd0f4e3123bdbf
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31145003"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>O que&#39;s novos na fonte de controlar o plug-in API versão 1.3
A API de plug-in de controle de origem versão 1.3 apresenta as seguintes funções de novo para fornecer um controle mais avançado.  
  
## <a name="changes"></a>Alterações  
 As funções a seguir são novas para a API de plug-in de controle de origem versão 1.3:  
  
|Função|Visão geral|  
|--------------|--------------|  
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|Permite que os bits de funcionalidade adicional a ser relatado|  
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|Permite que a verificação de arquivos que têm versões mais recentes no versão controle banco de dados no disco local|  
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|Permite o exame do estado de alterações de nome (renomeações, adições e exclusões) para os arquivos especificados|  
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|Permite o exame de diretórios e arquivos do banco de dados de controle de versão|  
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|Adiciona uma lista especificada de arquivos do banco de dados de controle de versão para o projeto atual|  
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|Executa um silenciosa "Get" dos arquivos especificados (sem interface do usuário é mostrada)|  
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|Permite o acesso a opções específicas do usuário|  
  
## <a name="see-also"></a>Consulte também  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)   
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)