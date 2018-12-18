---
title: Processo de hospedagem (vshost.exe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- vshost.exe
- hosting process
ms.assetid: c6b9e2be-f18d-4d75-ac52-56d55784734b
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4d45da37dae805399f9af8591bcd017ed61a975c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49216678"
---
# <a name="hosting-process-vshostexe"></a>Processo de hospedagem (vshost.exe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O processo de hospedagem é um recurso do Visual Studio que melhora o desempenho de depuração, habilita a depuração de confiança parcial e habilita a avaliação de expressão em tempo de design. Os arquivos do processo de hospedagem contêm vshost no nome do arquivo e são colocados na pasta de saída do projeto. Para obter mais informações, consulte [Depuração e o processo de hospedagem](../debugger/debugging-and-the-hosting-process.md).  
  
> [!NOTE]
>  Arquivos do processo de hospedagem (.vshost.exe) são para uso do Visual Studio e não devem ser executados diretamente ou implantados com o aplicativo.  
  
## <a name="improved-debugging-performance"></a>Melhor desempenho de depuração  
 O processo de hospedagem cria um domínio do aplicativo e associa o depurador ao aplicativo. A execução dessas tarefas pode introduzir um atraso notável entre o tempo de início da depuração e o tempo do início da execução do aplicativo. O processo de hospedagem ajuda a melhorar o desempenho criando o domínio do aplicativo, associando o depurador na tela de fundo e salvando o domínio do aplicativo e o estado do depurador entre execuções do aplicativo. Para obter mais informações sobre domínios do aplicativo, consulte [Domínios do aplicativo](http://msdn.microsoft.com/library/113a8bbf-6875-4a72-a49d-ca2d92e19cc8).  
  
## <a name="partial-trust-debugging"></a>Depuração de relação de confiança parcial  
 Um aplicativo pode ser especificado como um aplicativo de relação de confiança parcial na [página Segurança](../ide/reference/security-page-project-designer.md) do **Designer de Projeto**. A depuração de um aplicativo de relação de confiança parcial exige uma inicialização especial do domínio do aplicativo. Essa inicialização é manipulada pelo processo de hospedagem.  
  
## <a name="design-time-expression-evaluation"></a>Avaliação de expressão de tempo de design  
 A avaliação de expressão em tempo de design permite testar o código na janela **Imediata** sem a necessidade de executar o aplicativo. O processo de hospedagem executa esse código durante a avaliação da expressão em tempo de design. Para obter mais informações, consulte [Janela Imediata](../ide/reference/immediate-window.md).  
  
## <a name="see-also"></a>Consulte também  
 [Depuração e o processo de hospedagem](../debugger/debugging-and-the-hosting-process.md)   
 [Como desabilitar o processo de hospedagem](../ide/how-to-disable-the-hosting-process.md)   
 [Janela Imediata](../ide/reference/immediate-window.md)   
 [Domínios do aplicativo](http://msdn.microsoft.com/library/113a8bbf-6875-4a72-a49d-ca2d92e19cc8)



