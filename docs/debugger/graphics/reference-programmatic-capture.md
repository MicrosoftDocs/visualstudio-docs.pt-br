---
title: Referência (Captura programática) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ef60eb8d-1ac2-4e3a-9b4b-f6da0bdd9da8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0046268ff073949db3e3fc0c0753c9008b262c6e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847182"
---
# <a name="reference-programmatic-capture"></a>Referência (captura programática)
Diagnóstico de gráficos oferece suporte a controle programático sobre seus recursos de captura, por meio da API de captura programática. Você pode usar essa API para ativar/desativar e adicionar mensagens para o diagnóstico de gráficos HUD (Head-Up Display), inicializar e criar arquivos de log de gráficos e capturar informações gráficas.  

## <a name="programmatic-capture-apis"></a>APIs de captura programática  

### <a name="classes"></a>Classes  

|Nome|Descrição|  
|----------|-----------------|  
|[Classe VsgDbg](vsgdbg-class.md)|Representa a interface por meio do qual o componente no aplicativo de diagnóstico de gráficos é controlado por meio de programação.|  

### <a name="preprocessor-symbols"></a>Símbolos de pré-processador  

|Nome|Descrição|  
|----------|-----------------|  
|[DONT_SAVE_VSGLOG_TO_TEMP](dont-save-vsglog-to-temp.md)|Define sua presença se o arquivo de log de gráficos é salvo para o diretório de arquivos temporários do usuário.|  
|[VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)|Define o nome de arquivo padrão do arquivo de log de gráficos.|  
|[VSG_NODEFAULT_INSTANCE](vsg-nodefault-instance.md)|Define por sua presença se uma instância padrão do `VsgDbg` classe é fornecida.|  

## <a name="related-articles"></a>Artigos relacionados  

| Título | Descrição |
| - | - |
| [Capturando informações de gráficos](capturing-graphics-information.md) | Mostra como capturar informações gráficas de seu aplicativo baseado no DirectX para que você possa usar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ferramentas de diagnóstico de gráficos para diagnosticar problemas de renderização. |
| [Visão geral](overview-of-visual-studio-graphics-diagnostics.md) | Mostra como o diagnóstico de gráficos podem ajudar você a depurar erros de renderização em aplicativos e jogos do DirectX. |

