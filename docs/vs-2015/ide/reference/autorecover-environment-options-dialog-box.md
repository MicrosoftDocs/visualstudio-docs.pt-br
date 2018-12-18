---
title: Caixa de diálogo AutoRecuperação, Ambiente, Opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPag.Environment.AutoRecover
- VS.DialogAutoRestore
- VS.ToolsOptionsPages.Environment.AutoRecover
- VS.ToolsOptionsPages.Environment.Auto_Save_and_Restore
helpviewer_keywords:
- files, recovering
- AutoRecover page
- saving files, automatically
- files, saving automatically
ms.assetid: 397e5e44-4bbe-4289-94d1-642b466c9111
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4be9e975c850101874bd0ecef51478cc4c3067c6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263966"
---
# <a name="autorecover-environment-options-dialog-box"></a>AutoRecover, Caixa de diálogo Opções, Ambiente
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use essa página da caixa de diálogo Opções para especificar se os arquivos passam por backup automático ou não. Essa página também permite especificar se arquivos modificados são restaurados ou não quando o IDE (ambiente de desenvolvimento integrado) é desligado inesperadamente. Você pode acessar essa caixa de diálogo selecionando o menu **Ferramentas** e escolhendo **Opções** e, em seguida, selecionando a pasta **Ambiente** e a página **AutoRecuperação**. Se essa página não aparecer na lista, selecione **Mostrar todas as configurações** na caixa de diálogo **Opções**.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 **Salvar informações de AutoRecuperação a cada \<n> minutos**  
 Use esta opção para personalizar a frequência com que um arquivo é salvo automaticamente no editor. Para arquivos salvos anteriormente, uma cópia do arquivo é salva em \\...\meus Documentos\Visual Studio \<*versão*>\Arquivos de Backup\\<*nome do projeto*>. Se o arquivo for novo e não tiver sido salvo manualmente, ele será salvo automaticamente usando um nome de arquivo gerado aleatoriamente.  
  
 **Manter informações de AutoRecuperação por \<n> dias**  
 Use esta opção para especificar por quanto tempo o Visual Studio manterá arquivos criados para AutoRecuperação.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Opções](../../ide/reference/options-dialog-box-visual-studio.md)



