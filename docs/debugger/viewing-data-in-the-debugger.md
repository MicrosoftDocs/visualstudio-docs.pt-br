---
title: Criar exibições personalizadas de dados no depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 59e6c1879d5463682ee41d60e3928fce85c74a8d
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305137"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger"></a>Criar exibições personalizadas de dados no depurador do Visual Studio
O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] depurador fornece várias ferramentas para inspecionar e modificar o estado do programa. A maioria dessas ferramentas funciona somente no modo de interrupção.

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>Criar exibições personalizadas de dados em janelas de variáveis e DataTips
 Muitas da [janelas do depurador](../debugger/debugger-windows.md), como o **Autos** e **Assista** windows, permitem que você inspecione variáveis. Você pode personalizar tipos como nativos, os objetos gerenciados, e seus próprios tipos são mostrados nas janelas de variáveis do depurador e no [DataTips](../debugger/view-data-values-in-data-tips-in-the-code-editor.md). Para obter mais informações, consulte [criar exibições personalizadas de objetos nativos](../debugger/create-custom-views-of-native-objects.md) e [criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-dot-managed-objects.md).
  
## <a name="create-custom-visualizers"></a>Criar visualizadores personalizados  
 Os visualizadores permitem exibir o conteúdo de um objeto ou variável de forma significativa. No depurador do Visual Studio, um visualizador refere-se ao windows diferentes que podem ser abertos usando a Lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador") ícone. Por exemplo, o visualizador HTML mostra como uma cadeia de caracteres HTML seria interpretada e exibida em um navegador. Você pode acessar visualizadores a partir das DataTips, a **Watch** janela, o **Autos** janela e o **locais** janela. O **QuickWatch** caixa de diálogo também fornece um visualizador. Para obter mais informações, confira [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md).
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)   
 [Janela Comando](../ide/reference/command-window.md)   
 [Segurança do depurador](../debugger/debugger-security.md)