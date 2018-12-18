---
title: Executável para a caixa de diálogo de sessão de depuração | Microsoft Docs
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
- vs.debug.exefordebug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- executable files, specifying when debugging
- DLLs, debugging
- debugger, Executable for Debugging Session dialog box
- Executable for Debugging Session dialog box
ms.assetid: c0ddbe32-b99f-4425-acf1-f48842804f56
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 26a7eabe624b75c2b9ded6d14e6bf7c92505ba2d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51753618"
---
# <a name="executable-for-debugging-session-dialog-box"></a>Caixa de diálogo Executável para Sessão de Depuração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa caixa de diálogo aparece quando você tenta depurar uma DLL para a qual nenhum executável está especificado. O Visual Studio não pode iniciar uma DLL diretamente. Em vez disso, ele iniciará o executável especificado. Você pode depurar a DLL quando ela for chamada pelo executável.  
  
 **Nome do arquivo executável**  
 Digite o nome do caminho para um executável que chama a DLL que você está depurando.  
  
 **URL em que o projeto pode ser acessado (somente servidor ATL)**  
 Se você estiver depurando um DLL do servidor ATL, digite a URL onde o projeto pode ser localizado.  
  
 Uma vez inseridas, essas configurações são armazenadas nas Páginas de Propriedades do projeto, de modo que você não precise inseri-las novamente para sessões de depuração subsequentes. Se você precisar alterar as configurações, poderá abrir as Páginas de Propriedades e alterar os valores. Para obter mais informações sobre como especificar um executável para sessão de depuração, consulte [depurando DLLs](../debugger/how-to-debug-native-dlls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)



