---
title: 'Como: depurar um controle ActiveX | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vc.controls.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- testing [Visual Studio], test containers
- ActiveX control container debugging [Visual Studio]
- debugging ActiveX controls
- data-bound controls, ActiveX
- test container
- containers, specifying for debug sessions
- ActiveX controls, debugging
- testing [Visual Studio], ActiveX controls
ms.assetid: bbc02cf7-a7e6-44fe-99af-87a43e1d7251
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f1e43d94807fa28f86193fc7818b77887d797772
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745152"
---
# <a name="how-to-debug-an-activex-control"></a>Como depurar um controle ActiveX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

OBSERVAÇÃO]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Para depurar seu controle ActiveX, você deverá especificar um contêiner (executável) em que o controle será executado.  
  
### <a name="to-specify-a-container-for-the-debug-session"></a>Para especificar um contêiner para a sessão de depuração  
  
1.  No Gerenciador de Soluções, selecione o projeto.  
  
2.  Dos **modo de exibição** menu, escolha **páginas de propriedade**.  
  
3.  No **páginas de propriedades do projeto** caixa de diálogo, abra o **propriedades de configuração** pasta e selecione **depuração**.  
  
4.  Sob o **Debugging** categoria, localize a **comando** propriedade.  
  
5.  Especifique o nome do caminho para o contêiner. Por exemplo, C:\Arquivos de Programas\Internet Explorer\IEXPLORE.EXE.  
  
6.  Se você especifica o Internet Explorer como o contêiner e você estiver usando a área de trabalho ativa, digite `/new` no **argumentos do comando** caixa.  
  
7.  Clique em **OK**.  
  
     Se você não especificar um contêiner na **páginas de propriedades do projeto** caixa de diálogo, você pode especificar o contêiner ao iniciar a depuração. Quando você seleciona um comando de execução para iniciar a depuração, o [executável para a caixa de diálogo de sessão de depuração](../debugger/executable-for-debugging-session-dialog-box.md) é exibida. Especifique o nome do caminho do contêiner na caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Controles ActiveX](http://msdn.microsoft.com/library/52aaec4d-3889-402e-b57d-758078f8ac57)   
 [Testando propriedades e eventos com contêiner de teste](http://msdn.microsoft.com/library/626867cf-fe53-4c30-8973-55bb93ef3917)   
 [Depuração de COM e ActiveX](../debugger/com-and-activex-debugging.md)   
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)



