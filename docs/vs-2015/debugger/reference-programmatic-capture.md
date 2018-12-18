---
title: Referência (Captura programática) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef60eb8d-1ac2-4e3a-9b4b-f6da0bdd9da8
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 66e80d02ac41d78f2c79e7b2accb11388d456ad8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744266"
---
# <a name="reference-programmatic-capture"></a>Referência (captura programática)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diagnóstico de gráficos oferece suporte a controle programático sobre seus recursos de captura, por meio da API de captura programática. Você pode usar essa API para ativar/desativar e adicionar mensagens para o diagnóstico de gráficos HUD (Head-Up Display), inicializar e criar arquivos de log de gráficos e capturar informações gráficas.  
  
## <a name="programmatic-capture-apis"></a>APIs de captura programática  
  
### <a name="classes"></a>Classes  
  
|Nome|Descrição|  
|----------|-----------------|  
|[Classe VsgDbg](../debugger/vsgdbg-class.md)|Representa a interface por meio do qual o componente no aplicativo de diagnóstico de gráficos é controlado por meio de programação.|  
  
### <a name="preprocessor-symbols"></a>Símbolos de pré-processador  
  
|Nome|Descrição|  
|----------|-----------------|  
|[DONT_SAVE_VSGLOG_TO_TEMP](../debugger/dont-save-vsglog-to-temp.md)|Define sua presença se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário.|  
|[VSG_DEFAULT_RUN_FILENAME](../debugger/vsg-default-run-filename.md)|Define o nome de arquivo padrão do arquivo de log de gráficos.|  
|[VSG_NODEFAULT_INSTANCE](../debugger/vsg-nodefault-instance.md)|Define por sua presença se uma instância padrão do `VsgDbg` classe é fornecida.|  
  
## <a name="related-articles"></a>Artigos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Capturando informações de gráficos](../debugger/capturing-graphics-information.md)|Mostra como capturar informações gráficas de seu aplicativo baseado no DirectX para que você possa usar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ferramentas de diagnóstico de gráficos para diagnosticar problemas de renderização.|  
|[Visão geral](../debugger/overview-of-visual-studio-graphics-diagnostics.md)|Mostra como o diagnóstico de gráficos podem ajudar você a depurar erros de renderização em aplicativos e jogos do DirectX.|



