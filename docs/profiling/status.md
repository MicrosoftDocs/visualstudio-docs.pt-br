---
title: Status | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: ba656fa4-ef9d-4d8c-a3b6-739c3b5d23ae
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5cd721dc6682057519821ee155ac8a5d803769dc
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668110"
---
# <a name="status"></a>Status
A opção **Status** de *VSPerfCmd.exe* exibe informações sobre o estado do criador de perfil e todos os processos cujos perfis estão sendo criados.  
  
 A opção **Status** deve ser a única opção especificada na linha de comando. O criador de perfil precisa ser inicializado com a opção **Status** de *VSPerfCmd.exe* antes que qualquer status possa ser exibido.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
VSPerfCmd.exe /Status  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A opção **Status** exibe as seguintes informações de estado para o criador de perfil.  
  
 **Nome do arquivo de saída**  
 O caminho e o nome do arquivo de dados atual do criador de perfil.  
  
 **Modo de coleta**  
 SAMPLE ou TRACE  
  
 **Processos Máximos**  
 O número máximo de processos que podem ser perfilados ao mesmo tempo e o número de processos ativos no momento.  
  
 **Threads Máximos**  
 O número máximo de threads que podem ser perfilados ao mesmo tempo.  
  
 **Número de Buffers**  
 O número de buffers de memória dedicada a gravação de dados de criação de perfil.  
  
 **Tamanho dos Buffers**  
 O tamanho em bytes do buffer de memória.  
  
 A opção **Status** exibe as seguintes informações de estado para cada processo que está atualmente sendo perfilado.  
  
 **Processo**  
 O nome do processo perfilado.  
  
 **ID do Processo**  
 O identificador de sistema do processo.  
  
 **Num Threads**  
 Número de threads em execução atualmente.  
  
 **Iniciar/Parar Contagem**  
 A contagem do criador de perfil principal interno para controlar a coleta de dados para esse processo. A contagem deve ser igual a um para coletar dados. Iniciar/Parar Contagem pode ser manipulada por APIs do criador de perfil e as opções de VSPerfCmd **GlobalOn**, **GlobalOff**, **ProcessOn**, **ProcessOff**, **ThreadOn** e **ThreadOff**.  
  
 **Suspender/Retomar Contagem**  
 A contagem do criador de perfil secundário interno para controlar a coleta de dados para esse processo. A contagem deve ser menor ou igual a zero para coletar dados. A opção **Suspender/Retomar** contagem pode ser manipulada somente pela APIs do criador de perfil.  
  
 **Usuários com direitos de acesso para monitorar**  
 Lista os nomes de usuários que têm acesso para o criador de perfil. Usuários adicionais podem ser concedidos acesso por meio da opção VSPerfCmd.exe **Admin**  
  
## <a name="see-also"></a>Consulte também  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Criar perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [Criar o perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [Profile services (Serviços de perfil)](../profiling/command-line-profiling-of-services.md)