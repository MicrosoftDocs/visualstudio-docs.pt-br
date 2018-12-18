---
title: VSPerfCLREnv | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- command-line tools, VSPerfCLREnv
- command line, tools
- performance tools, VSPerfCLREnv
- profiling tools,VSPerfCLREnv
- VSPerfCLREnv tool
ms.assetid: 4bc9dd6e-379c-4930-9bba-59a4faa93303
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0ff359904b2b4d8b10dbc180f076606651028e80
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741498"
---
# <a name="vsperfclrenv"></a>VSPerfCLREnv
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta VSPerfCLREnv é usada para definir variáveis de ambiente que são necessárias para criar o perfil de um aplicativo .NET Framework. Ela usa a seguinte sintaxe:  
  
```  
VsPerfCLREnv [/option]  
```  
  
 A opção que você escolhe depende de qual dos três tipos de criação de perfil você usa: amostragem, instrumentação ou global. Uma opção separada é necessária para incluir dados de interação de camadas nos dados de criação de perfil. A sintaxe de cada opção é descrita nas tabelas a seguir.  
  
> [!NOTE]
>  Ao terminar a criação de perfil, execute **VSPerfCLREnv** com a opção **/off** ou **/globaloff** para excluir as variáveis de ambiente necessárias na criação de perfil. Para obter mais informações, consulte as Opções VSPerfCLREnv para excluir configurações de ambiente mostradas aqui.  
  
 **Opções VSPerfCLREnv para incluir dados de interação de camadas**  
  
> [!WARNING]
>  A criação de perfil de interação de camadas pode ser coletada usando [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] ou [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)]. No entanto, os dados de criação de perfil de interação de camadas somente podem ser exibidos no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] e no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
  
 A criação de perfil de interação de camadas fornece informações adicionais sobre consultas ADO.NET em aplicativos de várias camadas. Os dados são coletados apenas para chamadas de função síncronas. Dados de interação podem ser adicionados a qualquer execução de criação de perfil usando qualquer método de criação de perfil.  
  
 As opções **InteractionOn** e **GlobalInteractionOn** permitem a coleta de dados de interação de camada. A opção de interação deve ser definida depois de definir a variável de ambiente VSPerfCLREnv, necessária para criar o perfil de um aplicativo.  
  
 O exemplo a seguir inclui dados de interação de camadas em uma execução de criação de perfil que usa o método de amostragem:  
  
```  
VSPerfCLREnv /SampleOn  
VSPerfCLREnv /InteractionOn  
VSPerfCmd /Start:Sample /Output:MyApp.exe.vsp /Launch:MyApp.exe  
```  
  
 O exemplo a seguir inclui dados de interação de camadas em uma execução de criação de perfil para um serviço Windows:  
  
```  
VSPerfCLREnv /GlobalSampleOn  
VSPerfCLREnv /GlobalInteractionOn  
REM Restart the computer and start the service  
VSPerfCmd /Start:Sample /Output:MyService.exe.vsp   
VSPerfCmd /Attach:MyService.exe  
```  
  
 **Opções de VSPerfCLREnv para criação de perfil de instrumentação de processo**  
  
 A tabela a seguir descreve as opções de VSPerfCLREnv para criação de perfil de instrumentação:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**TraceOn**|Habilita a criação de perfil usando o método de instrumentação. Não habilita a criação de perfil de alocação de memória nem coleta dados de tempo de vida do objeto.|  
|**TraceGC**|Habilita a criação de perfil de alocação de memória usando o método de instrumentação. Não permite coletar dados de tempo de vida do objeto.|  
|**TraceGCLife**|Habilita a criação de perfil de alocação de memória e coleta dados de tempo de vida do objeto usando o método de instrumentação.|  
  
 **Opções de VSPerfCLREnv para criação de perfil de amostragem do processo**  
  
 A tabela a seguir descreve as opções de VSPerfCLREnv para criação de perfil de amostragem:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**SampleOn**|Habilita a criação de perfil usando o método de amostragem. Não habilita a criação de perfil de alocação de memória nem coleta dados de tempo de vida do objeto.|  
|**SampleGC**|Habilita a criação de perfil de alocação de memória usando o método de amostragem. Não permite coletar dados de tempo de vida do objeto.|  
|**SampleGCLife**|Habilita a criação de perfil de alocação de memória usando o método de amostragem. Também permite coletar dados de tempo de vida do objeto.|  
|**SampleLineOff**|Desabilita a coleta de dados de criação de perfil de nível de linha do .NET.|  
  
 **Opções de VSPerfCLREnv para criação de perfil global**  
  
 Para criar o perfil de um serviço gerenciado, como um aplicativo Web ASP .NET que é iniciado pelo sistema operacional, em vez de ser iniciado pelo usuário, use as opções de criação de perfil global das opções de VSPerfCLREnv. A tabela a seguir descreve as versões globais das opções de VSPerfCLREnv. Essas opções definem as variáveis de ambiente adequadas no Registro.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**GlobalTraceOn**|Habilita a criação de perfil global usando o método de instrumentação. Não coleta eventos de alocação de memória nem dados de tempo de vida do objeto.|  
|**GlobalTraceGC**|Habilita a criação de perfil de alocação de memória global usando o método de instrumentação. Não permite coletar dados de tempo de vida do objeto.|  
|**GlobalTraceGCLife**|Habilita a criação de perfil de alocação de memória global usando o método de instrumentação. Também permite coletar dados de tempo de vida do objeto.|  
|**GlobalSampleOn**|Habilita a criação de perfil global usando o método de amostragem. Não permite coleta de eventos de alocação de memória nem dados de tempo de vida do objeto.|  
|**GlobalSampleGC**|Habilita a criação de perfil de alocação de memória global usando o método de amostragem. Não permite coletar dados de tempo de vida do objeto.|  
|**GlobalSampleGCLife**|Habilita a criação de perfil de alocação de memória global usando o método de amostragem. Também permite coletar dados de tempo de vida do objeto.|  
  
 **Opções de VSPerfCLREnv para excluir as configurações de ambiente**  
  
 Ao concluir a criação de perfil do aplicativo gerenciado, use uma das opções a seguir para excluir as variáveis de ambiente adicionadas por VSPerfCLREnv. A tabela a seguir descreve como excluir variáveis de ambiente padrão e globais:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Off**|Exclui as variáveis de ambiente para criação de perfil de .NET padrão. Use essa opção quando as opções de VSPerfClrEnv não globais foram usadas para definir as variáveis de ambiente do criador de perfil.|  
|**GlobalOff**|Exclui as variáveis de ambiente para criação de perfil do .NET global. Use essa opção quando o aplicativo foi iniciado pelo sistema operacional e não pelo criador de perfil.|  
  
## <a name="remarks"></a>Comentários  
 Essas opções não serão necessárias para criar o perfil de um aplicativo gerenciado, se o aplicativo tiver sido iniciado usando o Gerenciador de Desempenho no IDE. O Gerenciador de Desempenho define todas as configurações de ambiente necessárias.  
  
 Se o ambiente certo não foi definido durante a criação de perfil, um aviso será dado durante a análise e os nomes da função gerenciada não serão resolvidos corretamente.  
  
## <a name="see-also"></a>Consulte também  
 [Criando perfil na linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)



