---
title: AutoMark | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c4de965e-0364-4f78-9936-1f509e85df74
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 31c40c0ad4f63f2190dd09f0a8d106816cda78ba
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747970"
---
# <a name="automark"></a>AutoMark
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção **AutoMark** especifica o número de milésimos de segundos entre a coleção de eventos de contador de desempenho de software do Windows. Contadores de desempenho do Windows são especificados na opção **WinCounter**.  
  
 Apenas uma opção **AutoMark** pode ser especificada na linha de comando. Observe que o intervalo de amostragem de **WinCounter** especificado por **AutoMark** é independente do intervalo de amostragem principal.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Start:Method /WinCounter:Path /AutoMark:Milliseconds  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Milliseconds`  
 Especifica o número de milésimos de segundos entre coleções de eventos do contador de desempenho do Windows.  
  
## <a name="required-options"></a>Opções obrigatórias  
 **WinCounter:** `Path`  
 Especifica o contador de desempenho do Windows para coletar. Quando você estiver usando o método de instrumentação, vários contadores do Windows podem ser especificados. Quando você estiver usando o método de amostragem, apenas um contador de software pode ser especificado. A opção **WinCounter** deve ser especificada em uma linha de comando que contém a opção **Iniciar**.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, um intervalo de amostragem de 1000 milésimos de segundos é definido para dois contadores de desempenho do Windows.  
  
```  
VSPerfCmd.exe /Start:Trace /Output:TestApp.exe.vsp /WinCounter:"\Process(*)\% Processor Time" /WinCounter:"\ASP.NET\Pages/sec" /AutoMark:1000  
VSPerfCmd.exe /Launch:TestApp.exe  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



