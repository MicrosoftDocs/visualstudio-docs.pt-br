---
title: 'Passo a passo: Capturando informações de gráficos | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 48f12f6e-57b4-48ec-a145-89fa71a42424
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 81e647f1e98a13a87c1b526630eee349fde3fd69
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49932917"
---
# <a name="walkthrough-capturing-graphics-information"></a>Passo a passo: capturando informações de gráficos
Este passo a passo demonstra como usar o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] diagnóstico de gráficos para capturar manualmente as informações gráficas de um aplicativo Direct3D.  
  
 Este passo a passo ilustra essas tarefas:  
  
-   Vinculando o diagnóstico de gráficos para seu aplicativo  
  
-   Capturando informações de gráficos  
  
## <a name="capturing-graphics-information"></a>Capturando informações de gráficos  
 Para usar as ferramentas de diagnóstico de gráficos, primeiro, você precisa capturar as informações gráficas nas quais ele confia. Para habilitar a captura, use o **iniciar diagnóstico** comando para conectar o diagnóstico de gráficos para seu aplicativo quando ele é iniciado.  
  
#### <a name="to-enable-the-capture-of-graphics-information-after-a-project-or-solution-is-loaded"></a>Para habilitar a captura de informações de gráfico depois de um projeto ou solução é carregada  
  
1. No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar um arquivo de projeto ou solução para o aplicativo que você deseja capturar informações de gráficos.  
  
2. Na barra de ferramentas de diagnóstico de gráficos, escolha **iniciar diagnóstico**.  
  
#### <a name="to-enable-the-capture-of-graphics-information-without-loading-a-project-or-solution"></a>Para habilitar a captura de informações de gráficos sem carregar um projeto ou solução  
  
1. Na barra de menus, escolha **Arquivo**, **Abrir**, **Projeto/Solução**. O **Abrir projeto** caixa de diálogo é exibida.  
  
2. Em vez de um arquivo de projeto ou solução, especifique o arquivo executável para o aplicativo que você deseja capturar informações de gráficos e, em seguida, escolha **aberto**.  
  
3. Na barra de menus, escolha **Debug**, **gráficos**, **iniciar diagnóstico**.  
  
   Depois de iniciar o aplicativo e é quadros de renderização, você pode capturar informações gráficas.  
  
#### <a name="to-capture-graphics-information"></a>Para capturar informações gráficas  
  
- Na barra de ferramentas de diagnóstico de gráficos, escolha o **capturar** botão. ![Ícone do botão de captura de elementos gráficos](media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics")  
  
   -ou-  
  
   Com o aplicativo no foco, pressionar **Print Screen**.  
  
  Cada vez que você capturar informações sobre um quadro, o diagnóstico de gráficos registra os eventos de Direct3D e o estado associado e adiciona esses dados para um log de gráficos. Um novo log de gráficos é criado para cada sessão de diagnóstico de gráficos. Para obter informações sobre logs de gráficos, consulte [visão geral](overview-of-visual-studio-graphics-diagnostics.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo demonstrou como capturar informações gráficas manualmente. Como próxima etapa, considere esta opção:  
  
-   Aprenda a analisar informações gráficas capturadas usando as ferramentas de diagnóstico de gráficos. Ver [visão geral](overview-of-visual-studio-graphics-diagnostics.md).  
  
## <a name="see-also"></a>Consulte também  
 [Capturando informações de gráficos](capturing-graphics-information.md)