---
title: Códigos de mensagem | Microsoft Docs
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
- message codes
ms.assetid: 9f91f4e2-c1f1-4349-9f11-2fbbf59654be
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0464042c17a3ed0836b99183dacbe4918823c752
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51724638"
---
# <a name="message-codes"></a>Códigos de mensagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Cada linha da mensagem mostrada na [exibição de mensagens](../debugger/messages-view.md) contém um 'P', do,' do,' ou 'R' código. Esses códigos têm os seguintes significados:  
  
|Código|Significado|  
|----------|-------------|  
|P|A mensagem foi postada na fila com o **PostMessage** função. Nenhuma informação está disponível sobre a ultimate disposição da mensagem.|  
|S|A mensagem foi enviada com o **SendMessage** função. Isso significa que o remetente não recuperar o controle até que o receptor processa e retorna a mensagem. O receptor pode, portanto, passar um valor de retorno volta ao remetente.|  
|s|A mensagem foi enviada, mas segurança impede o acesso ao valor de retorno.|  
|R|De cada um ' linha tem uma linha correspondente 'R' (retorno) que lista o valor de retorno de mensagem. Às vezes chamadas de mensagem são aninhadas, que significa que esse manipulador de uma mensagem envia outra mensagem.|



