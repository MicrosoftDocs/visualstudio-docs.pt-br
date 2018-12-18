---
title: Configurar destinos e tarefas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9aabe67a-1720-4bbf-80d3-822b3ccf75c0
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1bb82483b0adef6343423984e3b0d6fa21d0d678
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263504"
---
# <a name="configuring-targets-and-tasks"></a>Configurando destinos e tarefas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode configurar destinos do MSBuild e tarefas para execução fora de processo com o MSBuild para que você possa direcionar contextos diferentes daqueles que você está executando. Por exemplo, você pode direcionar um aplicativo do .NET Framework 2.0 de 32 bits, enquanto o computador de desenvolvimento está em execução em um sistema de operacional de 64 bits do .NET Framework 4.5. Você também pode direcionar os computadores que executam o .NET Framework 4 ou anterior. A combinação de 32 ou 64 bits e a versão específica do .NET Framework é conhecida como o *contexto de destino*.  
  
## <a name="installation"></a>Instalação  
 O .NET Framework 4.5 e 4.5.1 substitui o CLR (Common Language Runtime), os destinos, as tarefas e as ferramentas do .NET Framework 4 sem renomeá-los. O .NET Framework 4.5.1 é instalado como parte do [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)].  
  
 Se desejar instalar o MSBuild separadamente do Visual Studio, baixe o pacote de instalação em [Download do MSBuild](http://go.microsoft.com/fwlink/?LinkId=309745). Você também deve instalar as versões do .NET Framework que deseja usar.  
  
## <a name="targets-and-tasks"></a>Destinos e tarefas  
 O MSBuild executa certas tarefas de build fora do processo para destinar para um conjunto maior de contextos.  Por exemplo, um MSBuild de 32 bits pode executar uma tarefa de build em um processo de 64 bits para destinar um computador de 64 bits. Isso é controlado pelos argumentos `UsingTask` e parâmetros `Task`. Os destinos instalados pelo .NET Framework 4.5 definem esses parâmetros e argumentos e nenhuma alteração é necessária para compilar aplicativos para os vários contextos de destino.  
  
 Se quiser criar seu próprio contexto de destino, você deverá definir esses parâmetros e argumentos adequadamente. Examine o arquivo Microsoft.Common.targets do .NET Framework 4.5 e o arquivo Microsoft.Common.Tasks para obter exemplos.  Para obter informações sobre como criar uma tarefa personalizada que possa trabalhar com vários contextos de destino ou modificar tarefas existentes, consulte [Como configurar destinos e tarefas](../msbuild/how-to-configure-targets-and-tasks.md).  
  
## <a name="see-also"></a>Consulte também  
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)



