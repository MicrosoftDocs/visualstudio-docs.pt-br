---
title: Como depurar um controle ActiveX | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 76bc982db167624e567f88a1cf139b41cad9feb7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350206"
---
# <a name="how-to-debug-an-activex-control"></a>Como depurar um controle ActiveX

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

Para depurar seu controle ActiveX, você deverá especificar um contêiner (executável) em que o controle será executado.

## <a name="to-specify-a-container-for-the-debug-session"></a>Para especificar um contêiner para a sessão de depuração

1. No Gerenciador de Soluções, selecione o projeto.

2. No menu **Exibir** , escolha **páginas de propriedades**.

3. Na caixa de diálogo **Páginas de Propriedades de Projeto**, abra a pasta **Propriedades de Configuração** e selecione **Depurando**.

4. Na categoria **Depurando**, localize a propriedade **Comando**.

5. Especifique o nome do caminho para o contêiner. Por exemplo, C:\Arquivos de Programas\Internet Explorer\IEXPLORE.EXE.

6. Se você especificar o Internet Explorer como o contêiner e estiver usando o Active Desktop, digite `/new` na caixa **Argumentos do Comando**.

7. Clique em **OK**.

     Se você não especificar um contêiner na caixa de diálogo **Páginas de Propriedades do Projeto**, poderá especificar o contêiner quando iniciar a depuração. Quando você selecionar um comando de execução para iniciar a depuração, a [caixa de diálogo Executável para Sessão de Depuração](../debugger/executable-for-debugging-session-dialog-box.md) é exibida. Especifique o nome do caminho do contêiner na caixa de diálogo.

## <a name="see-also"></a>Veja também

- [Controles ActiveX](/cpp/mfc/activex-controls)
- [Testando Propriedades e eventos com contêiner de teste](/cpp/mfc/testing-properties-and-events-with-test-container)
- [Depuração de COM e ActiveX](../debugger/com-and-activex-debugging.md)
- [Depurando no Visual Studio](../debugger/index.yml)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)