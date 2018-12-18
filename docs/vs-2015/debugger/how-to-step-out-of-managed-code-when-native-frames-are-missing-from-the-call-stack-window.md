---
title: 'Como: sair do código gerenciado quando quadros nativos estiverem ausentes da janela pilha de chamadas | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- Call Stack window, missing native frames
- code, managed code
- native frames
- stepping, out of managed code
- managed code, stepping out of
ms.assetid: 97cdd2a8-02a9-4a06-a5b1-c92b1e431979
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0f67dcff047b29d2fb51044e6c0973c5b6e6b747
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788492"
---
# <a name="how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window"></a>Como sair do código gerenciado quando quadros nativos não forem encontrados na janela Pilha de Chamadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se seu código tiver quadros nativos que são invisíveis na **pilha de chamadas** janela, passo a passo fora do código gerenciado pode produzir resultados inesperados. Como alternativa, você pode usar um ponto de interrupção em vez de **depuração circular**.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-display"></a>Para depurar fora do código gerenciado quando os quadros nativos estiverem ausentes da exibição da pilha de chamadas  
  
1.  No código nativo, defina um ponto de interrupção do local depois da chamada para o código gerenciado.  
  
2.  Sobre o **Debug** menu, escolha **continuar**.  
  
     Quando a chamada gerenciada for concluída, a execução será interrompida no ponto de interrupção no código nativo.  
  
## <a name="see-also"></a>Consulte também  
 [Como usar a janela Pilha de Chamadas](../debugger/how-to-use-the-call-stack-window.md)





