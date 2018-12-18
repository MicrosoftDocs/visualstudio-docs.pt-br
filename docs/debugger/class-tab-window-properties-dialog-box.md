---
title: Guia classe, caixa de diálogo de propriedades de janela | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- Window Properties dialog box, Class Tab
ms.assetid: eaec9f07-d580-436d-934d-76c4e59439aa
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4afce149a2124ba8caa827b73b258fb421792c13
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31458899"
---
# <a name="class-tab-window-properties-dialog-box"></a>Guia Classe, Caixa de diálogo Propriedades da Janela
Use o **classe** guia para exibir informações sobre a classe da janela selecionada. Para exibir o [caixa de diálogo de propriedades de janela](../debugger/window-properties-dialog-box.md), move o foco para o [exibição Windows](../debugger/windows-view.md) janela. Selecione qualquer nó de janela na árvore e escolha **propriedades** do **exibição** menu.  
  
 As configurações a seguir estão disponíveis no **classe** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Nome de Classe**|O nome ou número ordinal dessa classe de janela.|  
|**Estilos de classe**|Uma combinação de códigos de estilo de classe.|  
|**Bytes de classe**|Dados específicos do aplicativo associados a essa classe de janela.|  
|**Classe Atom**|O atom para a classe retornado pelo **RegisterClass** chamar.|  
|**Identificador de instância**|O identificador de instância do módulo que registrou a classe. Identificadores de instância não são exclusivos.|  
|**Bytes de janela**|O número de bytes adicionais associadas a cada janela dessa classe. O significado desses bytes é determinado pelo aplicativo. Expanda a caixa de lista para ver os valores de byte em formato DWORD.|  
|**Procedimento de janela**|O endereço atual do **WndProc** função para windows dessa classe. Isso é diferente do **procedimento de janela** no **geral** guia se a janela é uma subclasse.|  
|**Nome do menu**|O nome do menu principal que está associado com o windows dessa classe ("none" se não houver nenhum menu).|  
|**Identificador de ícone**|O identificador para o ícone que está associado com o windows dessa classe ("none" se não houver nenhum ícone).|  
|**Identificador de cursor**|O identificador para o cursor que está associado com o windows dessa classe ("none" se não houver nenhum cursor).|  
|**Pincel de plano de fundo**|O identificador para o pincel do plano de fundo que está associado com o windows dessa classe ou uma das COLOR_ * cores predefinidas para pintar o plano de fundo de janela ("none" se não houver nenhum pincel).|