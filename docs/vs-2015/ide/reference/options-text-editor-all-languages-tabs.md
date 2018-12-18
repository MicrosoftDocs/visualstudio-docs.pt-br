---
title: Opções, Editor de Texto, Todos os idiomas, Guias | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.ResJSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
helpviewer_keywords:
- indents, Code Editor
- Code Editor, default behavior
- tabs, setting in Code Editor
- All Languages Text Editor Options dialog box
- editors, Code Editor
- Code Editor, indenting
- Code Editor, tabs
ms.assetid: 7e208e1d-5e3a-4bf7-a27b-4417e3e049c7
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 940cca6b25ffc04fc017ef8def6dbace7ec35ef9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49213317"
---
# <a name="options-text-editor-all-languages-tabs"></a>Opções, Editor de Texto, Todos os Idiomas, Guias
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Esta caixa de diálogo permite alterar o comportamento padrão do Editor de Código. Essas configurações também se aplicam a outros editores baseados no Editor de código, como o modo de exibição de Fonte do Designer de HTML. Para exibir essas opções, selecione **Opções** do menu **Ferramentas**. Na pasta **Editor de Texto**, expanda a subpasta **Todos os Idiomas** e, em seguida, escolha **Guias**.  
  
> [!CAUTION]
>  Esta página define opções padrão para todas as linguagens de desenvolvimento. Lembre-se de que redefinir uma opção nessa caixa de diálogo redefinirá as opções Guias em todas as linguagens para quaisquer opções selecionadas aqui. Para alterar as opções do Editor de Texto para apenas uma linguagem, expanda a subpasta para aquela linguagem e selecione suas páginas de opções.  
  
 Se forem selecionadas configurações diferentes nas páginas de opções Guias para linguagens de programação específicas, a mensagem “As configurações de recuo para formatos de texto individuais estão em conflito entre si” será exibida para diferentes opções de **Recuo**, e a mensagem “As configurações de guia para formatos de texto individuais estão em conflito entre si” será exibida para diferentes opções de **Guia**. Por exemplo, esse lembrete será exibido se a opção **Recuo inteligente** for selecionada para Visual Basic, mas **Bloquear recuo** estiver selecionado para Visual C++.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="indenting"></a>Recuar  
 Nenhum  
 Quando selecionada, novas linhas não serão recuadas. O ponto de inserção é colocado na primeira coluna de uma linha nova.  
  
 Bloco  
 Quando selecionada, novas linhas serão recuadas automaticamente. O ponto de inserção é colocado no mesmo ponto de partida que a linha anterior.  
  
 Inteligente  
 Quando selecionada, novas linhas serão posicionadas para caber no o contexto do código, conforme as configurações de formatação do outro código e as convenções do IntelliSense para sua linguagem de desenvolvimento. Essa opção não está disponível para todas as linguagens de desenvolvimento.  
  
 Por exemplo, as linhas incluídas entre uma chave de abertura ({) e uma chave de fechamento (}) podem ser recuadas automaticamente em uma parada de tabulação extra da posição das chaves alinhadas.  
  
## <a name="tabs"></a>Tabulações  
 A guia tamanho  
 Define a distância em espaços entre as paradas de tabulação. O padrão é quatro espaços.  
  
 Tamanho do recuo  
 Define o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Os caracteres de tabulação, os caracteres de espaço, ou ambos serão inseridos para preencher o tamanho especificado.  
  
 Insira espaços  
 Quando selecionadas, as operações de recuo inserirão apenas caracteres de espaço, não caracteres de TABULAÇÃO. Se o **Tamanho do recuo** estiver definido como 5, por exemplo, cinco caracteres de espaço serão inseridos sempre que você pressionar a tecla TAB ou o botão **Aumentar Recuo** na barra de ferramentas de **Formatação**.  
  
 Manter tabulações  
 Quando estiverem selecionadas, as operações de recuo inserirão tantos caracteres de TABULAÇÃO quantos forem possíveis. Cada caractere de TABULAÇÃO preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da tabulação**, os caracteres de espaço serão adicionados para preencher a diferença.  
  
## <a name="see-also"></a>Consulte também  
 [Opções, Editor de Texto, Todas as Linguagens](../../ide/reference/options-text-editor-all-languages.md)   
 [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)



