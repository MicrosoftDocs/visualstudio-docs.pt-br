---
title: 'Como: Depurar um controle ActiveX | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vc.controls.debug
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 385f5c9e03aaeb84cf33c6d76a499b0d1e35d5c3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54931980"
---
# <a name="how-to-debug-an-activex-control"></a>Como: Depurar um controle ActiveX

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Para depurar seu controle ActiveX, você deverá especificar um contêiner (executável) em que o controle será executado.

## <a name="to-specify-a-container-for-the-debug-session"></a>Para especificar um contêiner para a sessão de depuração

1.  No Gerenciador de Soluções, selecione o projeto.

2.  Dos **modo de exibição** menu, escolha **páginas de propriedade**.

3.  Na caixa de diálogo **Páginas de Propriedades de Projeto**, abra a pasta **Propriedades de Configuração** e selecione **Depurando**.

4.  Na categoria **Depurando**, localize a propriedade **Comando**.

5.  Especifique o nome do caminho para o contêiner. Por exemplo, C:\Arquivos de Programas\Internet Explorer\IEXPLORE.EXE.

6.  Se você especificar o Internet Explorer como o contêiner e estiver usando o Active Desktop, digite `/new` na caixa **Argumentos do Comando**.

7.  Clique em **OK**.

     Se você não especificar um contêiner na caixa de diálogo **Páginas de Propriedades do Projeto**, poderá especificar o contêiner quando iniciar a depuração. Quando você selecionar um comando de execução para iniciar a depuração, a [caixa de diálogo Executável para Sessão de Depuração](../debugger/executable-for-debugging-session-dialog-box.md) é exibida. Especifique o nome do caminho do contêiner na caixa de diálogo.

## <a name="see-also"></a>Consulte também

- [Controles ActiveX](/cpp/mfc/activex-controls)
- [Testando propriedades e eventos com contêiner de teste](/cpp/mfc/testing-properties-and-events-with-test-container)
- [Depuração de COM e ActiveX](../debugger/com-and-activex-debugging.md)
- [Depurando no Visual Studio](../debugger/index.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)