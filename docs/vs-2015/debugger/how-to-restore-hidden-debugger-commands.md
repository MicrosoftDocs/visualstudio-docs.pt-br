---
title: 'Como: Restaurar comandos ocultos do depurador | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, restoring commands
- debugging [Visual Studio], restoring commands
- commands, debugger
ms.assetid: 76ac9b77-f536-43b5-a9fc-984854b1c566
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5edc195397b9652d790620b8281100cc7651a02d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802298"
---
# <a name="how-to-restore-hidden-debugger-commands"></a>Como restaurar comandos de depurador ocultos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao configurar o Visual Studio, será solicitado que você escolha um conjunto de configurações padrão da IDE para a sua linguagem de programação principal. As configurações padrão da IDE para algumas linguagens podem ocultar alguns comandos do depurador.  
  
 Se você quiser usar um recurso do depurador que esteja oculto pelas configurações padrão da IDE, poderá adicionar o comando novamente ao menu usando o procedimento a seguir.  
  
### <a name="to-restore-hidden-debugger-commands"></a>Para restaurar comandos ocultos do depurador  
  
1.  Com um projeto aberto, nos **ferramentas** menu, clique em **personalizar**.  
  
2.  No **personalizar** caixa de diálogo, clique o **comandos** guia.  
  
3.  No **barra de menus:** lista suspensa, selecione o **depurar** menu que você deseja que contenha o comando restaurado.  
  
4.  Clique o **adicionar comando...** .  
  
5.  No **comando Add** , selecione o comando que você deseja adicionar e clique em **Okey**.  
  
6.  Repita a etapa anterior para adicionar outro comando.  
  
7.  Clique em **fechar** quando tiver terminado de adicionar comandos ao menu.  
  
    > [!WARNING]
    >  Alguns itens de menu aparecem somente quando o depurador estiver em modos específicos, por exemplo, o modo de execução ou o modo de interrupção. Consequentemente, um item que você adicionou não pode ser visível imediatamente quando você concluir essas etapas.  
  
## <a name="restoring-commands-not-available-from-the-customize-dialog-box"></a>Restaurando os comandos não disponíveis na caixa de diálogo personalizar  
 Alguns comandos, especialmente os encontrados em menus hierárquicos, não podem ser restaurados a **personalizar** caixa de diálogo. Para restaurar esses comandos, você deverá importar uma nova coleção de configurações da IDE.  
  
#### <a name="to-import-new-ide-settings"></a>Para importar novas configurações da IDE  
  
1.  Sobre o **ferramentas** menu, clique em **Import and Export Settings**.  
  
2.  Sobre o **bem-vindo ao Assistente de importação e exportar configurações** , clique em **importar configurações de ambiente selecionadas**e, em seguida, clique em **próxima**.  
  
3.  Sobre o **salvar configurações atuais** página, decida se deseja ou não salvar as configurações existentes e, em seguida, clique em **próxima**.  
  
4.  No **escolha uma coleção de configurações a importar** página na **configurações padrão** pasta, escolha um conjunto de configurações de desenvolvimento que contém os comandos que você deseja usar. Se você não souber qual coleção escolher, tente **configurações gerais de desenvolvimento** ou **configurações de desenvolvimento do Visual C++**, que fornecem a maioria dos comandos do depurador.  
  
5.  Clique em **Avançar**.  
  
6.  No **escolha as configurações a importar** página, em **opções**, certifique-se de **depuração** está selecionado. Desmarque as outras caixas de seleção, a menos que você também queira importar essas configurações.  
  
7.  Clique em **Finalizar**.  
  
8.  Sobre o **importação completa** página, examine os erros associados a redefinição das configurações em **detalhes**.  
  
9. Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)



