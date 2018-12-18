---
title: WaitStart | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6c737177-2dfb-4150-963e-a49ac9aaa591
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 13f52c2c9449b8f1abdc51fca9c9f989163a2a39
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760286"
---
# <a name="waitstart"></a>WaitStart
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção WaitStart faz com que o subcomando VSPerfCmd.exe Start retorne somente quando o criador de perfil tiver sido inicializado ou o número de segundos especificado tiver passado. Por padrão, o comando Start retorna imediatamente. Se o subcomando Start for retornado sem inicializar o criador de perfil, um erro será retornado. Se o número de segundos não for especificado, o comando Start aguardará indefinidamente.  
  
 A opção WaitStart é útil para arquivos de lote a fim de garantir se o criador de perfil foi inicializado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Start:Method /Output:FileName[Options] /StartWait[:Seconds]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Seconds`  
 O número de segundos a aguardar antes de retornar do subcomando Start.  
  
## <a name="required-options"></a>Opções obrigatórias  
 A opção WaitStart só pode ser usada com o subcomando Start.  
  
 **Output:** `filename`  
 Especifica o nome do arquivo de saída.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="example"></a>Exemplo  
 Neste exemplo de arquivo em lotes, o comando Start aguardará 5 segundos para inicializar o criador de perfil.  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /WaitStart:5  
if not %errorlevel% 0 goto :error_tag  
VSPerfCmd.exe /Launch:TestApp.exe  
goto :end  
:error_tag  
@echo Could not start Profiler!  
@echo Error %errorlevel%  
:end  
```



