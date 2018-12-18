---
title: GC (VSPerfCmd) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7c81e88b-a748-4cf5-a7a1-3429608e1b54
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 45b93d3184a825c11e0a4742ad752c6a2c1c031e
ms.sourcegitcommit: 269b55b413d2c82e6aa56c6ab8e53da7926fb2e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35237559"
---
# <a name="gc-vsperfcmd"></a>GC (VSPerfCmd)
A opção **GC** habilita a coleta de dados de alocação de memória do.NET Framework e dados de tempo de vida do objeto. A opção **GC** pode ser usada somente com o método de criação de perfil de amostragem e somente com a opção **Inicializar**.  
  
 Quando você estiver usando a opção **GC**, o comando VSPerfClrEnv **/sampleon** não é obrigatório.  
  
 Se nenhum parâmetro for especificado ou se o parâmetro **Alocação** for especificado, apenas os dados de alocação de memória do .NET Framework são coletados. Se o parâmetro **Tempo de Vida** for especificado, os dados de alocação de memória do .NET Framework e de tempo de vida do objeto do .NET Framework são coletados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
VSPerfCmd.exe /Launch:AppName /GC[:{Allocation|Lifetime}] [Options]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 **Alocação**  
 Padrão. Coleta dados de alocação de memória do .NET Framework.  
  
 **Tempo de Vida**  
 Coleta dados de alocação de memória do .NET Framework e dados de tempo de vida do objeto do .NET Framework.  
  
## <a name="required-options"></a>Opções obrigatórias  
 A opção **GC** pode ser usada somente com a opção **Inicializar**.  
  
 **Inicialize:** `AppName`  
 Inicia o aplicativo especificado e começa a criação de perfil com o método de amostragem.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir inicia um aplicativo e coleta dados de alocação de memória do .NET Framework.  
  
```cmd  
VSPerfCmd.exe /Launch:TestApp.exe /gc  
```  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)