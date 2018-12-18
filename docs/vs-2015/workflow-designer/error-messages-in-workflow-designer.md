---
title: Mensagens de erro no Designer de fluxo de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- WFDErrorMessages.UI
- System.Activities.Presentation.ErrorActivity.UI
- System.Activities.Presentation.View.ErrorView.UI
ms.assetid: 4d8bbc2e-34fc-477f-9140-4adfd70c34a0
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: efd6bc680be42f1074da8d2313b1a4b8e9307580
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894840"
---
# <a name="error-messages-in-workflow-designer"></a>Mensagens de erro em Designer de Fluxo de Trabalho
Este tópico descreve os tipos de mensagens de erro que podem ser encontrados ao trabalhar com [!INCLUDE[wfd1](../includes/wfd1-md.md)].  
  
## <a name="situations-in-which-errors-in-the-workflow-designer-occur"></a>Situações em que os erros no criador de Fluxo de Trabalho ocorrem  
 Erros em [!INCLUDE[wfd2](../includes/wfd2-md.md)] ocorrem nas seguintes situações:  
  
1. Há um erro em uma expressão.  
  
2. As restrições de validação de uma atividade não foram satisfeitas.  
  
3. Há erros no arquivo XAML que fazem com que uma atividade a falha carregue.  
  
4. Há erros no arquivo XAML que fazem com que o fluxo de trabalho a falha carregue.  
  
   As expressões inválidos e restrições insatisfeitas de validação não fazem com que o fluxo de trabalho a falha compile. Compilar seu fluxo de trabalho é bem-sucedido, mas <xref:System.Activities.InvalidWorkflowException> é lançada pelo tempo de execução. Se há erros no arquivo XAML, a compilação falhará.  
  
   Dentro de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], quando um fluxo de trabalho é carregado, os erros são exibidos na **lista de erros**. Para navegar até a atividade que é a origem do erro, clique duas vezes no erro na **Error List**.  
  
### <a name="expression-errors"></a>Erros de expressão  
 Uma expressão é inválido denotada por um círculo vermelho com um ponto de exclamação branco ao lado da expressão. Passa sobre este ícone exibe uma dica de ferramenta que descreve a fonte do erro. Dentro de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], clique na expressão para exibir a linha que enfatiza a fonte do erro. Passa sobre o texto alinhado exibe uma dica de ferramenta que descreve a fonte do erro.  
  
### <a name="activity-validation-errors"></a>Erros de validação de atividades  
 Quando as restrições de validação de uma atividade não forem atendidas, um círculo vermelho com um ponto de exclamação branco aparece no canto superior direito da atividade. Passa sobre este ícone exibe uma dica de ferramenta que descreve a fonte do erro.  
  
### <a name="xaml-load-errors"></a>Erros de carregamento XAML  
 Quando uma atividade não carrega, uma caixa vermelha com o texto “atividade não pôde ser carregada devido a erros no XAML” aparece. Isso geralmente ocorre quando o tipo de atividade não pode ser resolvido. A atividade inválido pode ser excluído no designer selecionando a caixa vermelha e excluindo a.  
  
### <a name="workflow-load-errors"></a>Erros de carregamento de fluxo de trabalho  
 Quando um fluxo de trabalho não carrega, o texto “Designer de Fluxo de Trabalho após problemas com seu documento” aparece na superfície de designer, junto com as informações de exceção que causou a falha de fluxo de trabalho para carregar. Isso geralmente ocorre quando o arquivo XAML não pode ser analisado.