---
title: Caixa de diálogo de opções de teclado do Word do Microsoft Office, configurações de teclado do Microsoft Office,
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Word.Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Word_Keyboard
- VST.WordOptions.KeyboardMappingScheme
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- keyboard shortcuts, Office development in Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2f0785ec339da51f4f6b52e2093c1bb2ba273285
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669775"
---
# <a name="microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box"></a>Caixa de diálogo de opções de teclado do Word do Microsoft Office, configurações de teclado do Microsoft Office,
  Microsoft Office Word e o Visual Studio ambos manipulam teclas de atalho. Comandos diferentes no Word e no Visual Studio pode representar a mesma combinação de teclas de atalho. Quando o Word for aberto em um projeto de nível de documento no Visual Studio, apenas um aplicativo por vez recebe os comandos de tecla de atalho. Por padrão, o Visual Studio recebe todos os comandos de tecla de atalho, mas você pode fazer com que o Word recebê-las quando o documento tem o foco, selecionando **esquema de teclado dinâmico**.  
  
 Se você usar uma tecla de atalho que não está atribuída a um comando no aplicativo que atualmente está tratando as teclas de atalho, a tecla de atalho é passada para o outro aplicativo.  
  
 A opção que você selecione permanecerá em vigor para projetos do Word, até você alterá-lo. A seleção não afeta seus projetos do Microsoft Office Excel; Você deve fazer qualquer alteração para o Excel usando as opções de teclado do Microsoft Office Excel.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Esquema de teclado do Visual Studio**  
 Visual Studio recebe todos os comandos de tecla de atalho, mesmo se o documento do Word tem o foco. Por exemplo, se você pressionar a tecla de função **F5** enquanto o documento tem o foco, o Visual Studio inicia a depuração de sua solução.  
  
 **Esquema de teclado dinâmico**  
 Visual Studio recebe comandos de tecla de atalho somente quando ele tem o foco. Quando o documento do Word tem o foco, o Word recebe todos os comandos de tecla de atalho. Por exemplo, se você pressionar a tecla de função **F5** enquanto o documento do Word tem o foco, o Word abrirá o **localizar e substituir** caixa de diálogo com o **ir para** guia selecionada. Se você pressionar **F5** enquanto o Visual Studio tem o foco, o Visual Studio inicia a depuração de sua solução.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de opções de teclado do Excel do Microsoft Office, configurações de teclado do Microsoft Office,](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)  
  
  