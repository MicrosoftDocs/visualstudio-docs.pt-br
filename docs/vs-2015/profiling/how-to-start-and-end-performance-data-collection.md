---
title: Como iniciar e terminar a coleta de dados de desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.wizard.summarypage
helpviewer_keywords:
- profiling tools, launching sessions
- performance sessions, launching
- performance sessions, ending
- profiling tools, ending sessions
ms.assetid: 9f6eb0d5-d9e9-4bec-b627-445065610bce
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 393cb5776043f3e9543cc9fe2c45773e36c09dd7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51790026"
---
# <a name="how-to-start-and-end-performance-data-collection"></a>Como iniciar e terminar a coleta de dados de desempenho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você deve adicionar o binário de destino do qual você deseja criar o perfil para a sessão de desempenho antes de iniciar a criação de perfil. Para adicionar um destino, clique com botão direito do mouse em **Destinos** no **Gerenciador de Desempenho** e clique em **Adicionar Binário de Destino**. Na caixa de diálogo **Adicionar Binário de Destino**, selecione o nome do arquivo e clique em **Abrir**. Um novo binário é adicionado.  
  
### <a name="to-start-profiling"></a>Para iniciar a criação de perfil  
  
1.  Clique com o botão direito do mouse no nome da sessão de desempenho na janela **Gerenciador de Desempenho** e escolha uma das opções a seguir:  
  
    -   **Iniciar com Criação de Perfil** – inicia o aplicativo e imediatamente começa a criação de perfil.  
  
    -   **Iniciar com Criação de Perfil em Pausa** – inicia o aplicativo, mas não começa a criação de perfil. Você pode iniciar a criação de perfil selecionando **Retome a Coleta** na janela **Controle de Coleta de Dados**. Para obter mais informações, consulte [How to: Pause and Resume Performance Data Collection](../profiling/how-to-pause-and-resume-performance-data-collection.md) (Como pausar e retomar a coleta de dados de desempenho).  
  
### <a name="to-end-profiling"></a>Para encerrar a criação de perfil  
  
-   O método preferido de encerrar uma sessão de criação de perfil é sair do aplicativo. Para parar imediatamente a criação de perfil, na barra de ferramentas de **Gerenciador de Desempenho**, clique em **Parar**.  
  
## <a name="see-also"></a>Consulte também  
 [Controlling Data Collection](../profiling/controlling-data-collection.md)  (Controlando a coleta de dados)  
 [Como pausar e retomar a coleta de dados de desempenho](../profiling/how-to-pause-and-resume-performance-data-collection.md)



