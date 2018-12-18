---
title: LineOff | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 76082063-20ef-47ae-ad64-81b43b654865
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ba5d8c3e2644c94a4e15115661341a34c9e6f761
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34845422"
---
# <a name="lineoff"></a>LineOff
Por padrão, o criador de perfil coleta os números de linha do código-fonte e dos dados de deslocamento quando o método de criação de perfil de amostragem estiver sendo usado. A opção **LineOff** do VSPerfCmd desabilita a coleta de dados de número de linha quando o VSPerfCmd é usado para iniciar o aplicativo. Quando o **LineOff** for especificado, os dados de criação de perfil serão coletados para o nível de função.  
  
 É possível usar o **LineOff** somente com a opção de **Inicialização** e quando o criador de perfil tiver sido inicializado para amostragem com a opção **Iniciar**:**Amostra**.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
VSPerfCmd.exe /Launch:AppName /LineOff [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum  
  
## <a name="required-options"></a>Opções obrigatórias  
 A opção **LineOff** pode ser usada apenas em uma linha de comando que contenha a opção **Inicializar**.  
  
 **Inicialize:** `AppName`  
 Inicia o aplicativo especificado e começa a criação de perfil com o método de amostragem.  
  
## <a name="example"></a>Exemplo  
 Esse exemplo inicia o aplicativo e o criador de perfil e desabilita a amostragem de nível de linha.  
  
```cmd  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /LineOff  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)