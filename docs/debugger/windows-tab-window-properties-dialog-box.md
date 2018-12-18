---
title: Guia janelas, caixa de diálogo de propriedades de janela | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, Windows Tab
ms.assetid: 9001342a-09a8-4f5e-b6ed-881a3b9d7246
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e3589f3242c72002bf28e8aee135b2713c39fdb7
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31475734"
---
# <a name="windows-tab-window-properties-dialog-box"></a>Guia Janelas, Caixa de diálogo Propriedades da Janela
Use o **Windows** guia para exibir informações sobre o windows relacionados a janela selecionada. Para exibir o [caixa de diálogo de propriedades de janela](../debugger/window-properties-dialog-box.md), move o foco para o [exibição Windows](../debugger/windows-view.md) janela. Selecione qualquer nó de janela na árvore e escolha **propriedades** do **exibição** menu.  
  
 As configurações a seguir estão disponíveis no **Windows** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Próxima janela**|O identificador de janela próximo irmão na mesma sequência (ordem Z) mostrada na exibição de árvore da janela ("none" se não houver nenhum próxima janela). Escolha essa entrada para exibir as propriedades da próxima janela.|  
|**Janela anterior**|O identificador da janela do irmão anterior na mesma sequência (ordem Z) mostrada na exibição de árvore da janela ("none" se não houver nenhuma janela anterior). Escolha essa entrada para exibir as propriedades da janela anterior.|  
|**Janela pai**|O identificador da janela do pai dessa janela ("none" se não houver nenhum pai). Escolha essa entrada para exibir as propriedades da janela pai.|  
|**Primeiro filho**|O identificador da primeiro filho janela dessa janela, na sequência (ordem Z) mostrado na exibição de árvore da janela ("none" se não houver nenhum janelas filho). Escolha esse valor para exibir as propriedades da primeira janela filho.|  
|**Janela do proprietário**|O identificador da janela do proprietário desta janela. Janela principal do aplicativo normalmente possui janelas de caixa de diálogo modal do sistema, por exemplo ("none" se não houver nenhum proprietário). Escolha essa entrada para exibir as propriedades da janela do proprietário.|