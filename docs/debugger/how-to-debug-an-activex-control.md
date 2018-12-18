---
title: 'Como: depurar um controle ActiveX | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d53c2601bc8c4490f9ca43a7e213a90d66b26aac
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389287"
---
# <a name="how-to-debug-an-activex-control"></a>Como depurar um controle ActiveX

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
- [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)