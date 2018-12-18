---
title: Classe VsgDbg | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6722263c-ccef-40c7-a0ae-87a863fbab00
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0fb4a830c6cc3af49dcb3e26c6711af1a014c9c1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724915"
---
# <a name="vsgdbg-class"></a>Classe VsgDbg
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Representa uma interface para o controle programático do componente no aplicativo do diagnóstico de gráficos.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
class VsgDbg;  
```  
  
## <a name="members"></a>Membros  
 O `VsgDbg` classe oferece suporte aos seguintes membros.  
  
### <a name="public-constructors"></a>Construtores públicos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[VsgDbg::VsgDbg (Construtor)](../debugger/vsgdbg-vsgdbg-constructor.md)|Constrói uma instância do `VsgDbg` de classe e, opcionalmente, prepara o componente no aplicativo de diagnóstico de gráficos para capturar ativamente e registrar informações de gráficos.|  
|[VsgDbg::~VsgDbg (Destruidor)](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)|Destrói uma instância da `VsgDbg` classe.|  
  
### <a name="public-methods"></a>Métodos públicos  
  
|Nome|Descrição|  
|----------|-----------------|  
|[AddMessage](../debugger/addmessage.md)|Adiciona uma mensagem personalizada para o diagnóstico de gráficos HUD (Head-Up Display).|  
|[BeginCapture](../debugger/begincapture.md)|Inicia um intervalo de captura que terminará com `EndCapture`.|  
|[CaptureCurrentFrame](../debugger/capturecurrentframe.md)|Captura o restante do quadro atual para o arquivo de log de gráficos.|  
|[Copiar (captura programática)](../debugger/copy-programmatic-capture.md)|Copia o conteúdo do arquivo de log (. vsglog) de elementos gráficos ativos em um novo arquivo.|  
|[EndCapture](../debugger/endcapture.md)|Termina um intervalo de captura foi iniciado com `BeginCapture`.|  
|[Init](../debugger/init.md)|Prepara o componente no aplicativo de diagnóstico de gráficos para capturar ativamente e registrar informações de gráficos.|  
|[ToggleHUD](../debugger/togglehud.md)|Alterna a sobreposição HUD do diagnóstico de gráficos ativada ou desativada.|  
|[UnInit](../debugger/uninit.md)|Finaliza o arquivo de log de gráficos, fecha e libera os recursos que foram usados enquanto o aplicativo ativamente estava gravando informações de gráficos.|  
  
## <a name="remarks"></a>Comentários  
 O `VsgDbg` classe representa uma interface que você pode usar para controlar recursos de diagnóstico de gráficos programaticamente. Você pode usar alguns recursos mesmo quando você estiver ativamente capturar e registrar informações de gráficos; Isso inclui o `AddMessage` função de membro e `ToggleHUD` função de membro. As outras funções de membro ou preparar o componente no aplicativo de diagnóstico de gráficos para iniciar ou parar a captura de ativa de informações de gráficos ou devem ser chamadas enquanto o aplicativo está ativamente capturando e gravar informações de gráficos em um arquivo de log de gráficos.



