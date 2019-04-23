---
title: Web (código gerenciado) de biblioteca de controle | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- debugging [Visual Studio], Web control libraries
ms.assetid: 2413883f-9e88-406d-b874-0ed743b75d40
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 18f6e72d18154f11866671a3e448d88c91768c7f
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60047092"
---
# <a name="web-control-library-managed-code"></a>Biblioteca de Controles da Web (código gerenciado)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modelo de projeto da Biblioteca de Controles da Web cria uma DLL. Como a biblioteca de classe é uma DLL, você não pode executá-la diretamente. Você deve criar uma página do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que insira o controle. Para obter mais informações, consulte [modelo de biblioteca de controle da Web](http://msdn.microsoft.com/00666b07-71d2-4ace-a13c-cc130a3ce372).  
  
### <a name="to-debug-a-web-control-library-method-1"></a>Para depurar uma Biblioteca de Controles da Web (método 1)  
  
1. Abra um projeto existente da Biblioteca de Controles da Web ou crie um novo.  
  
2. Crie uma página do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que insira o controle.  
  
3. No site que está hospedando o agente de teste do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], crie um subdiretório chamado `/Code`.  
  
4. Copie o código-fonte do controle no subdiretório `/Code`.  
  
5. Abra o código-fonte no subdiretório `/Code` e defina pontos de interrupção.  
  
6. Abra uma janela do navegador com uma URL que aponte para o agente de teste. Um ponto de interrupção no controle será atingido e você poderá iniciar a depuração.  
  
### <a name="to-debug-a-web-control-library-method-2"></a>Para depurar uma biblioteca de controle da Web (método 2)  
  
1. Crie o projeto de aplicativo host e o projeto de controle da Web na mesma solução.  
  
2. Na **Gerenciador de soluções**, o aplicativo host com o botão direito e escolha **adicionar referência**.  
  
3. Adicione uma referência ao projeto de controle da Web.  
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos Web ASP.NET](../debugger/debugging-preparation-aspnet-web-applications.md)
