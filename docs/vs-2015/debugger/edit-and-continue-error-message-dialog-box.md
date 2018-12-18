---
title: Editar e continuar a caixa de diálogo de mensagem de erro | Microsoft Docs
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
- vs.debug.ENC.SupportedButNotAvaiable
- vs.debug.ENC.CannotEditWhileException
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue Error Message dialog box
ms.assetid: f98c91c0-447a-4533-85b6-87170a0dc4c3
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c311f6243ddbf087fd18fd9209e2e17bbe3065a6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51771320"
---
# <a name="edit-and-continue-error-message-dialog-box"></a>Caixa de diálogo Mensagem de Erro de Editar e Continuar
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa caixa de diálogo aparece quando você estiver depurando em uma linguagem que dá suporte a editar e continuar, mas **editar e continuar** não está disponível para o tipo de alterações de código que você fez. A mensagem de erro dentro da caixa fornece uma explicação mais detalhada. As possíveis razões para ver essa caixa de diálogo incluem:  
  
-   Você tentou editar o código gerenciado quando a depuração não gerenciada foi habilitada. Editar e Continuar não funcionam com depuração de modo misto.  
  
-   Você tentou editar o código do SQL Server.  
  
-   Você tentou editar o código durante a depuração de um Dr. Watson.  
  
-   Você tentou editar o código depois que ocorreu uma exceção sem tratamento e a opção "**desenrolar a pilha de chamadas em exceções não tratadas**" não foi selecionada.  
  
-   Você tentou editar o código ao depurar um aplicativo inserido de tempo de execução.  
  
-   Você tentou editar o código em um programa que você anexou em vez de a partir de **depurar** menu.  
  
-   Você tentou editar o código otimizado.  
  
-   Você tentou editar o código gerenciado quando o destino é um aplicativo de 64 bits. Se você desejar usar Editar e Continuar, deve definir o destino como x86. (*Projeto* **Properties**, **compilar** guia **avançado compilador** configuração.).  
  
-   Você tentou editar o código em um assembly que foi modificado durante a depuração e foi recarregado.  
  
-   Você tentou editar o código em um assembly que não foi carregado.  
  
-   Você iniciou a depuração de uma versão antiga do aplicativo (já que a nova versão tem erros de compilação).  
  
-   Você tentou editar o código durante a execução.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **OK**  
 Saia da caixa de diálogo e cancele a tentativa de edição imediatamente anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Alterações de código com suporte (C++)](../debugger/supported-code-changes-cpp.md)



