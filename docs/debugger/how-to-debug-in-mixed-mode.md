---
title: Como depurar em modo misto | Microsoft Docs
ms.date: 11/05/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- debugging [Visual Studio], mixed-mode
- mixed-mode debugging
ms.assetid: 2859067d-7fcc-46b0-a4df-8c2101500977
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 53a40c4dc615b5e1b6a3caef3a99be5ab0b56327
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350102"
---
# <a name="how-to-debug-in-mixed-mode-c-c-visual-basic"></a>Como: Depurar no modo misto (C#, C++, Visual Basic)

Os procedimentos a seguir descrevem como habilitar a depuração de código gerenciado e nativo juntos, também conhecida como depuração de modo misto. Há dois cenários de depuração de modo misto:

- O aplicativo que chama uma DLL é escrito em código nativo e a DLL é gerenciada.

- O aplicativo que chama uma DLL é escrito em código gerenciado e a DLL está em código nativo. Para obter um tutorial que orienta esse cenário em mais detalhes, consulte [depurar código gerenciado e nativo](../debugger/how-to-debug-managed-and-native-code.md).

Você pode habilitar os depuradores gerenciados e nativos nas páginas de **Propriedades** do projeto de aplicativo de chamada. As configurações diferem entre aplicativos nativos e gerenciados.

Se você não tiver acesso a um projeto de aplicativo de chamada, poderá depurar a DLL do projeto de DLL. Você não precisa de modo misto para depurar apenas o projeto de DLL. Para obter mais informações, consulte [como: Depurar de um projeto de dll](../debugger/how-to-debug-from-a-dll-project.md).

> [!NOTE]
> As caixas de diálogo e os comandos que você vê podem ser diferentes dos descritos neste artigo, dependendo de suas configurações ou edição do Visual Studio. Para alterar as configurações, escolha **ferramentas**  >  **importar e exportar configurações**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

## <a name="enable-mixed-mode-debugging-for-a-native-calling-app"></a>Habilitar a depuração de modo misto para um aplicativo de chamada nativo

1. Selecione o projeto C++ no **Gerenciador de soluções** e clique no ícone **Propriedades** , pressione **ALT** + **Enter**ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Na caixa de diálogo ** \<Project> páginas de propriedades** , expanda **Propriedades de configuração**e, em seguida, selecione **depuração**.

1. Defina **Tipo de Depurador** como **Misto** ou **Automático**.

1. Selecione **OK**.

   ![Habilitar depuração de modo misto](../debugger/media/dbg-mixed-mode-from-native.png "Habilitar depuração de modo misto")

## <a name="enable-mixed-mode-debugging-for-a-managed-calling-app"></a>Habilitar a depuração de modo misto para um aplicativo de chamada gerenciado

1. Selecione o projeto do C# ou do Visual Basic em **Gerenciador de soluções** e selecione o ícone **Propriedades** , pressione **ALT** + **Enter**ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Selecione a guia **depurar** e, em seguida, selecione **Habilitar depuração de código nativo**.

1. Feche a página Propriedades para salvar as alterações.

   ![Habilitar depuração de código nativo](../debugger/media/dbg-mixed-mode-from-csharp.png "Habilitar depuração de código nativo")

> [!NOTE]
> Na maioria das versões do Visual Studio começando com o Visual Studio 2017, você precisa usar o arquivo *launchSettings.json* em vez das propriedades do projeto para habilitar a depuração de modo misto de um código nativo em um aplicativo .NET Core. Para obter detalhes, consulte [depurar código gerenciado e nativo](../debugger/how-to-debug-managed-and-native-code.md).

## <a name="see-also"></a>Veja também

- [Como depurar de um projeto de DLL](../debugger/how-to-debug-from-a-dll-project.md)