---
title: Caixa de diálogo de opções de teclado do Microsoft Office Excel, configurações de teclado do Microsoft Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.ExcelOptions.KeyboardMappingScheme
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Excel_Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Excel.Keyboard
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
ms.openlocfilehash: fc71c699dfea11b8654791efdd52e4c0751a9762
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34692441"
---
# <a name="microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box"></a>Caixa de diálogo de opções de teclado do Microsoft Office Excel, configurações de teclado do Microsoft Office
  O Microsoft Office Excel e o Visual Studio ambos manipulam teclas de atalho. Comandos diferentes no Excel e no Visual Studio pode representar a mesma combinação de teclas de atalho. Quando o Excel está aberto em um projeto no nível do documento no Visual Studio, apenas um aplicativo em um momento recebe os comandos de teclas de atalho. Por padrão, o Visual Studio receberá todos os comandos de tecla de atalho, mas você pode fazer com que o Excel recebê-las quando o documento tem foco selecionando **esquema de teclado dinâmico**.  
  
 Se você usar uma tecla de atalho que não está atribuída a um comando no aplicativo que está tratando as teclas de atalho no momento, a tecla de atalho é passada para o outro aplicativo.  
  
 A opção que você selecionar permanecerá em vigor para projetos do Excel até você alterá-lo. A seleção não afeta seus projetos do Microsoft Office Word; Você deve fazer qualquer alteração para o Word usando as opções de teclado do Microsoft Office Word.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Esquema de teclado do Visual Studio**  
 O Visual Studio recebe todos os comandos de tecla de atalho, mesmo que o Excel tem foco. Por exemplo, se você pressionar a tecla de função **F5** enquanto o Excel tem foco, o Visual Studio inicia a depuração de sua solução.  
  
 **Esquema de teclado dinâmico**  
 O Visual Studio recebe comandos de tecla de atalho apenas quando ele tem o foco. Quando o Excel tem foco, o Excel recebe todos os comandos de tecla de atalho. Por exemplo, se você pressionar a tecla de função **F5** enquanto o Excel tem foco, o Excel abre o **ir para** caixa de diálogo. Se você pressionar **F5** enquanto o Visual Studio tem foco, o Visual Studio inicia a depuração de sua solução.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de opções de teclado do Word do Microsoft Office, configurações de teclado do Microsoft Office](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)  
  
  