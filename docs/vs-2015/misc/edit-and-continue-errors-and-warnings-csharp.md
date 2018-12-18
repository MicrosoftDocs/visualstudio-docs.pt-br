---
title: Editar e continuar erros e avisos (c#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.csharp.enc.error_4001
- vs.csharp.enc.error_4034
- vs.csharp.enc.error_4003
- vs.csharp.enc.error_4026
- vs.csharp.enc.error_4032
- vs.csharp.enc.error_4017
- vs.csharp.enc.error_4053
- vs.csharp.enc.error_4024
- vs.csharp.enc.error_4012
- vs.csharp.enc.error_4066
- vs.csharp.enc.error_4020
- vs.csharp.enc.error_4008
- vs.csharp.enc.error_4033
- vs.csharp.enc.error_4014
- vs.csharp.enc.error_4023
- vs.csharp.enc.error_4011
- vs.csharp.enc.error_4006
- vs.csharp.enc.error_4059
- vs.csharp.enc.error_4015
- vs.csharp.enc.error_4018
- vs.csharp.enc.error_4028
- vs.csharp.enc.error_4013
- vs.csharp.enc.error_4009
- vs.csharp.enc.error_4021
- vs.csharp.enc.error_4065
- vs.csharp.enc.error_4029
- vs.csharp.enc.error_4058
- vs.csharp.enc.error_4019
- vs.csharp.enc.error_4007
- vs.csharp.enc.error_4052
- vs.csharp.enc.error_4025
- vs.csharp.enc.error_4055
- vs.csharp.enc.error_4022
- vs.csharp.enc.error_4002
- vs.csharp.enc.error_4016
- vs.csharp.enc.error_4043
- vs.csharp.enc.error_4027
- vs.csharp.enc.error_4054
- vs.csharp.enc.error_4004
- vs.csharp.enc.error_4010
- vs.csharp.enc.error_4030
- vs.csharp.enc.error_4005
- vs.csharp.enc.error_4035
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], errors and warnings
- errors [C#], debugging
- errors [debugger], Edit and Continue
ms.assetid: c0e12b0a-8009-4a4a-979f-c804a91a5d9b
caps.latest.revision: 11
ms.author: mikejo
manager: douge
ms.openlocfilehash: ca47a7b7ea5a330176b6f75862819a4c0a5c64d9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793315"
---
# <a name="edit-and-continue-errors-and-warnings-c"></a>Erros e avisos de Editar e Continuar (C#)
Você fez uma edição em uma seção do código que não é permitido em Editar e Continuar do Visual C#.  
  
 [!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)] Editar e Continuar permite parar a execução do programa no modo de interrupção, fazer alterações no código de execução e, em seguida, retomar a execução do programa com as alterações recém-inseridas.  
  
 As edições declarativas de código que afetam a estrutura pública de uma classe são proibidas em geral, e algumas edições que você pode fazer em um método, corpo da propriedade ou declarações privadas dentro de uma classe não são permitidas. Sempre que possível, Editar e Continuar marca o código que não pode ser editado como cinza claro e exibe uma mensagem de erro.  
  
 Para obter mais informações sobre as edições com suporte em Editar e continuar para [!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)], consulte [Supported Code Changes (c#)](../debugger/supported-code-changes-csharp.md). Se você precisar obter mais informações sobre um erro específico ou um aviso, você pode pesquisar ou postar no MSDN [Fórum do IDE do Visual C#](http://go.microsoft.com/fwlink/?LinkId=214693).  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Sobre o **Debug** menu, escolha **desfazer** para desfazer a alteração.  
  
     -ou-  
  
2.  Pare a sessão de depuração, faça as edições e inicie uma nova sessão de depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Editar e continuar (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)