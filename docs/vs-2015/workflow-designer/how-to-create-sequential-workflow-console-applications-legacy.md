---
title: 'Como: criar aplicativos de Console do fluxo de trabalho sequencial (herdado) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- workflows, console applications
- sequential workflows, console applications
- console applications, sequential workflow
ms.assetid: 9f7be7fa-551f-42c6-a9bb-f5ae8ab83625
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: e467e4a574263eaa35640bc99f99c1f599a74df9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49306313"
---
# <a name="how-to-create-sequential-workflow-console-applications-legacy"></a>Como: Criar aplicativos de console sequenciais de fluxo de trabalho (o legados)
Siga estas etapas para criar um projeto de aplicativo de console sequencial de fluxo de trabalho usando [!INCLUDE[wfd1](../includes/wfd1-md.md)] herdado fornecido por [!INCLUDE[vs2010](../includes/vs2010-md.md)]. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
### <a name="to-create-a-sequential-workflow-console-application"></a>Para criar um aplicativo de console sequencial de fluxo de trabalho  
  
1.  Inicie o Visual Studio.  
  
2.  No menu **Arquivo**, aponte para **Novo** e selecione **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  Selecione o **.NET Framework 3.0** opção ou o **.NET Framework 3.5** opção na lista suspensa na parte superior da lista da **novo projeto** janela para acessar o designer herdado.  
  
    > [!NOTE]
    >  A opção padrão na [!INCLUDE[vs2010](../includes/vs2010-md.md)] está **.NET Framework 4**. Essa opção é usada criar aplicativos de [!INCLUDE[wf](../includes/wf-md.md)] que direcionam [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] e usa o designer herdado.  
  
4.  No **tipos de projeto** painel, selecione projetos do Visual c# ou projetos do Visual Basic (sob **outras linguagens**) e, em seguida, selecione **fluxo de trabalho**.  
  
5.  No **modelos** painel, selecione **Sequential Workflow Console Application**.  
  
6.  No **nome** , digite um nome descritivo para seu projeto para torná-lo mais fácil identificar.  
  
7.  No **local** , digite o diretório no qual você deseja salvar seu projeto, ou clique em **procurar** para navegar até ele.  
  
     O designer do Windows Forms abre e exibe o Form1 do projeto que você criou.  
  
8.  Clique em **OK**.  
  
     Designer de Fluxo de Trabalho abre e exibe a superfície de design de fluxo de trabalho de fluxo de trabalho sequencial que você criou.  
  
9. Arraste uma atividade do **caixa de ferramentas** para a superfície de design na **soltar atividade** designado área.  
  
## <a name="see-also"></a>Consulte também  
 [Criando projetos herdados de fluxo de trabalho](../workflow-designer/creating-legacy-workflow-projects.md)   
 [Desenvolvendo fluxos de trabalho](http://msdn.microsoft.com/en-us/557bcb1f-a7ab-49f6-8df7-2706b7001301)