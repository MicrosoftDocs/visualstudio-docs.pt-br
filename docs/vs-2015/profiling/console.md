---
title: Console | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e825ba66-1383-46ad-8712-396bc9c14036
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 512e04bc3da16c57a97536e02a12475182746e56
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786672"
---
# <a name="console"></a>Console
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A opção **Console** VSPerfCmd.exe inicia o aplicativo especificado em uma nova janela de prompt de comando. O **Console** só pode ser usado com a opção **Iniciar** VSPerfCmd. Se o aplicativo não é um aplicativo de linha de comando, o **Console** não tem nenhum efeito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
VSPerfCmd.exe /Launch:AppName /Console  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum  
  
## <a name="required-options"></a>Opções obrigatórias  
 O **Console** só pode ser especificado em uma linha de comando que também tem a opção **Iniciar**.  
  
 **Inicialize:** `AppName`  
 Inicia o criador de perfil e o aplicativo especificado por `AppName`.  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)



