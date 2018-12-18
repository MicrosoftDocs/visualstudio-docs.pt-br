---
title: Caixa de diálogo de configuração tema (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Workflow.ComponentModel.Design.ThemeConfigurationDialog.UI
helpviewer_keywords:
- themes, configuring
- Theme Configuration dialog box
ms.assetid: 9e6d182a-c4d9-4e71-b2b9-02f675fc2b29
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: d8cd8427bf239b1f99d339f822800c8e9c3f5003
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223945"
---
# <a name="theme-configuration-dialog-box-legacy"></a>Caixa de diálogo de configuração tema (legados)
Este tópico descreve como usar o **configuração de tema** caixa de diálogo em novas [!INCLUDE[wfd1](../includes/wfd1-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Um tema define o plano de fundo e de primeiro plano as cores, estilos, ícones, e outros elementos visuais de um fluxo de trabalho. Você pode salvar temas para reutilização por outros fluxos de trabalho.  
  
 Você cria e edita temas usando o **configuração de tema** caixa de diálogo. Para abrir a caixa de diálogo, selecione **criar novo tema** sobre o **fluxo de trabalho** menu ou botão direito do mouse o fluxo de trabalho superfície de design e selecione **criar novo tema**.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **configuração de tema** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Nome do tema:**|O nome que identifica o tema na [caixa de diálogo de opções de temas, Designer de fluxo de trabalho (herdado)](../workflow-designer/themes-workflow-designer-options-dialog-box-legacy.md). Um nome de variável é gerado para novos temas.|  
|**Local do tema:**|Nome de arquivo e caminho do arquivo de tema. Um nome de arquivo variável é gerado para novos temas gerado com base no nome do tema. Se você alterar o nome gerado de tema, convém alterar o nome de arquivo para corresponder ao nome do tema.|  
|**...**|Clique para selecionar o local para salvar o arquivo de tema de fluxo de trabalho, que usa uma extensão de nome de arquivo .wtm. O caminho selecionado será visto na **local do tema** caixa de texto.|  
|**Selecione o Designer e Configure as propriedades:**|O painel esquerdo lista um modo de exibição de árvore de atividades para que o tema pode ser personalizado. Selecione uma atividade no modo de exibição de árvore e propriedades de tema para atividades serão exibidas no painel de propriedades, que é à direita do painel modo de exibição de árvore. Clique em uma propriedade para alterar seu valor.|  
|**Visualizar**|Clique para exibir uma janela para visualizar os efeitos de alterações de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de opções de temas, Designer de fluxo de trabalho (herdado)](../workflow-designer/themes-workflow-designer-options-dialog-box-legacy.md)   
 [Designer herdado para a ajuda da interface do usuário do Windows Workflow Foundation](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)