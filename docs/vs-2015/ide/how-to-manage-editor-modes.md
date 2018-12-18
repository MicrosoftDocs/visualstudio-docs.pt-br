---
title: Como gerenciar modos do editor | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- word wrap
- views, virtual space
- line numbers, displaying
- virtual space mode
- line numbers
- Code Editor, view and display options
- full screen mode
- Code Editor, modes
- views, splitting
- views, word wrapping
- fonts and size
- views, creating new windows
- views, line numbers
- views, changing mode
- views, outlining
ms.assetid: 1fb48027-d870-439f-8b72-4a0321390748
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8d38812007e042d014cb0090f1334bee2cce0858
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49229210"
---
# <a name="how-to-manage-editor-modes"></a>Como gerenciar modos do editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível exibir o Editor de Código do Visual Studio em vários modos de exibição.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="enabling-full-screen-mode"></a>Habilitando o modo de tela inteira  
 É possível escolher ocultar todas as janelas de ferramentas e exibir apenas janelas do documento, habilitando o modo de **Tela Inteira**.  
  
#### <a name="to-enable-full-screen-mode"></a>Para habilitar o modo de Tela Inteira  
  
-   Pressione ALT+SHIFT+ENTER para entrar ou sair do modo de **Tela Inteira**.  
  
     --ou--  
  
-   Emita o comando `View.Fullscreen` na janela **Comando**.  
  
## <a name="enabling-virtual-space-mode"></a>Habilitando o modo Espaço virtual  
 No modo **Espaço virtual**, os espaços são inseridos no final de cada linha de código. Selecione essa opção para posicionar comentários em um ponto consistente ao lado do seu código.  
  
#### <a name="to-enable-virtual-space-mode"></a>Para habilitar o modo Espaço virtual  
  
1.  Selecione **Opções** no menu **Ferramentas**.  
  
2.  Expanda a pasta **Editor de Texto** e escolha **Todas as Linguagens** para definir essa opção globalmente ou escolha uma pasta de idioma específico. (Por exemplo, para ativar os números de linha apenas no Visual Basic, escolha as opções Basic, Editor de Texto.)  
  
3.  Selecione as opções **Gerais** e, em **Configurações**, selecione **Habilitar Espaço virtual**.  
  
    > [!NOTE]
    >  O **Espaço virtual** está habilitado no modo **Seleção de Coluna**. Quando o modo **Espaço virtual** não está habilitado, o ponto de inserção é movido do final de uma linha diretamente para o primeiro caractere da próxima.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando o editor](../ide/customizing-the-editor.md)   
 [Como organizar e encaixar janelas](../misc/how-to-arrange-and-dock-windows.md)   
 [Caixa de diálogo Fontes e Cores, Ambiente, Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)



