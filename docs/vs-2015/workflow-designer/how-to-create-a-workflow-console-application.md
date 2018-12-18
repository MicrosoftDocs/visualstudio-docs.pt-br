---
title: 'Como: criar um aplicativo de Console do fluxo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 51a2eea7-921c-49f1-b358-68afc27f1ee9
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: ad509e0e57f2c8996c13ffbe1d8f8890d2954dec
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49251661"
---
# <a name="how-to-create-a-workflow-console-application"></a>Como: Crie um aplicativo de console do fluxo de trabalho
[!INCLUDE[wf](../includes/wf-md.md)] permite que você crie fluxos de trabalho para executar o sistema ou processos humanos. [!INCLUDE[wfd1](../includes/wfd1-md.md)] fornece a superfície de design para criar esses fluxos de trabalho. [!INCLUDE[wfd2](../includes/wfd2-md.md)] pode ser usado para criar fluxos de trabalho dentro de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou pode ser integrado em outros aplicativos que rehost o designer.  
  
 Este tópico descreve como usar [!INCLUDE[wfd2](../includes/wfd2-md.md)] em [!INCLUDE[vs2010](../includes/vs2010-md.md)] para criar um fluxo de trabalho em um aplicativo de console.  
  
### <a name="to-create-a-workflow-console-application"></a>Para criar um aplicativo de console do fluxo de trabalho  
  
1.  Inicie o [!INCLUDE[vs2010](../includes/vs2010-md.md)].  
  
2.  Sobre o **arquivo** , aponte para **New**e, em seguida, selecione **projeto...** .  
  
     A caixa de diálogo **Novo Projeto** é aberta.  
  
3.  No **modelos instalados** painel, selecione **fluxo de trabalho** de qualquer um os **Visual c#** ou **Visual Basic** agrupamentos, dependendo do seu idioma de preferência.  
  
4.  No painel central, selecione **aplicativo de Console do fluxo de trabalho**.  
  
5.  No **nome** , digite um nome descritivo para seu projeto para torná-lo mais fácil identificar.  
  
6.  No **local** , digite o diretório no qual você deseja salvar seu projeto, ou clique em **procurar** para navegar até ele.  
  
7.  No **solução** , digite o nome para a nova solução. Clique em **Okey** para criar o aplicativo.  
  
    > [!NOTE]
    >  Se você deseja adicionar um aplicativo de console do fluxo de trabalho a uma solução existente, abra essa solução na [!INCLUDE[vs2010](../includes/vs2010-md.md)], clique com botão direito na solução **Gerenciador de soluções**e selecione **Add**, em seguida,  **Novo projeto...** Para abrir o **novo projeto** caixa de diálogo. Continuar conforme descrito acima neste procedimento.  
  
8.  O modelo de projeto cria uma definição de fluxo de trabalho em XAML e a definição de aplicativo de console está no código-fonte. [!INCLUDE[wfd2](../includes/wfd2-md.md)] abre e exibe a tela para o fluxo de trabalho que você criou.  
  
9. Para compor um fluxo de trabalho, arraste atividades ou outros itens de fluxo de trabalho do **caixa de ferramentas** à superfície de design do fluxo de trabalho.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um projeto de fluxo de trabalho](../workflow-designer/creating-a-workflow-project.md)