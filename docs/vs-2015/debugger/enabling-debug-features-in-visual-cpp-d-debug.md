---
title: Habilitando recursos de depuração no Visual C++ (-D_DEBUG) | Microsoft Docs
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
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- /D_DEBUG compiler option [C++]
- debugging [C++], enabling debug features
- debugging [MFC], enabling debug features
- assertions, enabling debug features
- D_DEBUG compiler option
- MFC libraries, debug version
- debug builds, MFC
- _DEBUG macro
ms.assetid: 276e2254-7274-435e-ba4d-67fcef4f33bc
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e512620e1af8da85039ed403d4280568101fbe57
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49829255"
---
# <a name="enabling-debug-features-in-visual-c-ddebug"></a>Habilitando funcionalidades de depuração no Visual C++ (/D_DEBUG)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na [!INCLUDE[vcprvc](../includes/vcprvc-md.md)], recursos de depuração como asserções são habilitados quando você compila seu programa com o símbolo **Debug** definido. Você pode definir **Debug** em uma das duas maneiras:  
  
- Especificar **#define Debug** no seu código-fonte, ou  
  
- Especifique o **/D_DEBUG** opção de compilador. (Se você criar seu projeto no Visual Studio usando assistentes **/D_DEBUG** é definido automaticamente na configuração de depuração.)  
  
  Quando **Debug** é definido, o compilador compila as seções de código cercadas por **#ifdef DEBUG** e `#endif`.  
  
  A configuração Depuração de um programa MFC deve ser vinculada a uma versão de depuração da biblioteca MFC. Os arquivos de cabeçalho MFC determinam a versão correta da biblioteca MFC para vincular com base nos símbolos que você definiu, tais como **Debug** e **Unicode**. Para obter detalhes, consulte [versões de biblioteca MFC](http://msdn.microsoft.com/library/3d7a8ae1-e276-4cf8-ba63-360c2f85ad0e).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código nativo](../debugger/debugging-native-code.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)



