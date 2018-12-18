---
title: 'Como: depurar o código-fonte do .NET Framework | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ce5e20524040d131a655da1567606ffbb0934a80
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725429"
---
# <a name="how-to-debug-net-framework-source"></a>Como depurar a origem do .NET Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A versão mais recente do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece novos recursos para [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] depuração. Para depurar [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] fonte, você deve ter acesso aos símbolos de depuração para o código. Você também precisará habilitar a depuração de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] código-fonte.  
  
 Você pode habilitar [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] passo a passo e o download do símbolo na **opções** caixa de diálogo. Ao habilitar a transferência de símbolo, você pode optar por baixar imediatamente os símbolos ou apenas habilitar a opção para uma transferência posterior. Se você não baixar os símbolos imediatamente, eles serão baixados da próxima vez em que você iniciar a depuração do seu aplicativo. Você também pode baixar um manual do **módulos** janela ou o **pilha de chamadas** janela.  
  
### <a name="to-enable-net-framework-source-debugging"></a>Para ativar a depuração de origem do .NET Framework  
  
1.  No menu **Ferramentas**, clique em **Opções**.  
  
2.  No **opções** caixa de diálogo, clique o **depuração** categoria.  
  
3.  No **gerais** , defina **habilitar o .NET Framework** depuração da origem.  
  
    1.  Se Apenas Meu Código tiver sido habilitado, uma caixa de diálogo de aviso mostrará que Apenas Meu Código está desabilitado agora. Clique em **OK**.  
  
    2.  Se você não tiver um local de cache de símbolo definido, outra caixa de diálogo de aviso informará que um local padrão de cache do símbolo foi definido agora. Clique em **OK**.  
  
4.  Sob o **Debugging** categoria, clique em **símbolos**.  
  
5.  Se você desejar alterar o local do cache de símbolos:  
  
    1.  Abra o **depuração** nó na caixa à esquerda.  
  
    2.  Sob o **Debugging** nó, clique em **símbolos**.  
  
    3.  Editar o local no **armazenar em Cache símbolos de servidores de símbolos para este diretório** ou clique em **procurar** para escolher um local.  
  
6.  Se você quiser baixar símbolos imediatamente, clique em **carregar símbolos usando os locais acima**.  
  
     Este botão não está disponível no modo de design.  
  
     Se você não optar por baixar símbolos agora, os símbolos serão baixados automaticamente da próxima vez em que você iniciar a depuração do seu programa.  
  
7.  Clique em **OK** para fechar a caixa de diálogo **Opções**.  
  
### <a name="to-load-framework-symbols-using-the-modules-window"></a>Para carregar símbolos de Framework usando a janela de módulos  
  
1.  No **módulos** janela, o botão direito do mouse, um módulo para o qual os símbolos não foram carregados. Você pode informar se os símbolos são carregados ou não examinando os **Status de símbolos** coluna.  
  
2.  Aponte para **carregar símbolos de** e clique em **servidores de símbolo Microsoft** baixar símbolos do servidor de símbolos públicos da Microsoft ou **caminho de símbolo** para carregar a partir de um diretório onde você armazenou símbolos anteriormente.  
  
### <a name="to-load-framework-symbols-using-the-call-stack-window"></a>Para carregar símbolos de Framework usando a janela de pilha de chamadas  
  
1.  No **pilha de chamadas** janela, o botão direito do mouse um quadro para o qual os símbolos não foram carregados. O quadro será esmaecido.  
  
2.  Aponte para **carregar símbolos de** e clique em **servidores de símbolo Microsoft** ou **caminho de símbolo**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)



