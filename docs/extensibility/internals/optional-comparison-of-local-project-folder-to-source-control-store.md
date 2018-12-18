---
title: Comparar a pasta do projeto para o repositório de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2e0f6f2185385ee7ec3942556a43f58d43e7a4da
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130564"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>Comparação opcional da pasta do projeto Local para o repositório de controle de origem
1.2 de API de plug-in a comparação entre a pasta do projeto local e o controle de origem é feita usando as funções de controle na fonte [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md) e [SccDirDiff](../../extensibility/sccdirdiff-function.md).  
  
 Dentro de **Solution Explorer**, se uma pasta está selecionada, em vez de um arquivo individual, o **comparar versões** menu de atalho invoca o novo [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md) e [ SccDirDiff](../../extensibility/sccdirdiff-function.md) no plug-in de controle de origem.  
  
## <a name="new-capability-flags"></a>Novo sinalizadores de recursos  
 `SCC_CAP_DIRECTORYDIFF`  
  
 `SCC_CAP_DIRECTORYCHECKOUT`  
  
## <a name="new-functions"></a>Novas funções  
 [SccDirDiff](../../extensibility/sccdirdiff-function.md)  
  
 [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)  
  
 O `SccDirQueryInfo` função é chamada antes de `SccDirDiff` para determinar se o diretório de trabalho é o controle do código-fonte. O `SccDirDiff` função exibe as diferenças entre o diretório local atual e a pasta de controle de origem correspondente. Este comando solicita que o plug-in para exibir a lista de alterações para o diretório de controle de origem. Um plug-in de controle do código-fonte fornece sua própria interface do usuário para exibir as diferenças.  
  
> [!NOTE]
>  Essa função usa os mesmos sinalizadores de comando como [SccDiff](../../extensibility/sccdiff-function.md). Como um provedor de plug-in de controle de origem, você pode optar por não oferece suporte à operação de "comparação rápida" para diretórios.  
  
## <a name="see-also"></a>Consulte também  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)