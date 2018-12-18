---
title: Criar uma extensão com uma janela de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6170c5d418f1778af242bb4eb08cccffe0c031be
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499797"
---
# <a name="create-an-extension-with-a-tool-window"></a>Criar uma extensão com uma janela de ferramentas
Neste procedimento, você aprenderá a usar o modelo de projeto do VSIX e o **janela de ferramenta personalizada** modelo de item para criar uma extensão com uma janela de ferramentas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
### <a name="create-a-tool-window"></a>Criar uma janela de ferramentas  
  
1.  Crie um projeto do VSIX chamado **FirstWindow**. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c#** > **extensibilidade**.  
  
2.  Quando o projeto aberto, adicione um modelo de item da janela de ferramenta denominado **MyWindow**. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** > **Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **janela de ferramenta personalizada**. No **nome** campo na parte inferior da janela, altere o nome de arquivo da janela de ferramenta *MyWindow.cs*.  
  
3.  Compile o projeto e comece a depuração.  
  
     A instância experimental do Visual Studio é exibida. Para obter mais informações sobre a instância experimental, consulte [a instância experimental](../extensibility/the-experimental-instance.md).  
  
4.  Na instância experimental, vá para **modo de exibição** > **Other Windows**.  
  
     Você deve ver um item de menu **MyWindow**. Clique nele.  
  
     Você deverá ver uma janela de ferramenta com o título **MyWindow** e uma fala botão **Click Me!.**