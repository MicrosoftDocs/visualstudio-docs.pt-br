---
title: 'Como: criar ou atualizar as políticas do Check-in de análise de código padrão | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codeanalysis.policyeditor
helpviewer_keywords:
- code analysis, migrating check-in policy
ms.assetid: 458eb3b8-bb5e-4056-82b7-7079ce9c4089
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6821d218c22f2d83108205d8753fc2d5beac4f28
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939430"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>Como criar ou atualizar políticas de check-in de análise do código padrão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode exigir que a análise de código ser executado em todos os projetos de código em um projeto de equipe usando a análise de código check-in de política. Exigir que a análise de código pode melhorar a qualidade do código que é verificado na base de código.  
  
> [!NOTE]
>  Esse recurso está disponível apenas se você estiver usando o Team Foundation Server.  
  
 Políticas do check-in de análise de código são definidas nas configurações do projeto de equipe e se aplicam a cada projeto de código no projeto de equipe. Execuções de análise de código são configuradas para projetos de código no arquivo de projeto (xxproj) para o projeto de código. Execuções de análise de código são executadas no computador local. Quando você habilitar uma política de check-in do análise código, arquivos em um projeto de código são check-in devem ser compilados após sua última edição e uma análise de código que contém, no mínimo, as regras nas configurações do projeto de equipe devem ser executadas no computador em que o c foram feitas alterações pendentes.  
  
- Para código gerenciado, você deve definir a política de check-in, especificando um *conjunto de regras* que contém um subconjunto de regras de análise de código.  
  
- Para código C/C++, a política de check-in requer que todas as regras de análise de código sejam executadas. Você pode adicionar diretivas de pré-processador para desabilitar regras específicas para os projetos de código individuais no seu projeto de equipe.  
  
  Depois de especificar uma política de check-in para código gerenciado, os membros da equipe podem sincronizar suas configurações de análise de código para projetos de código para as configurações de política de projeto de equipe.  
  
### <a name="to-open-the-check-in-policy-editor"></a>Para abrir o editor de política de check-in  
  
1.  No Team Explorer, clique com botão direito no nome do projeto de equipe, aponte para **configurações de projeto de equipe**e, em seguida, clique em **controle do código-fonte**.  
  
2.  No **controle de origem** caixa de diálogo, selecione o **política de Check-in** guia.  
  
3.  Realize um dos seguintes procedimentos:  
  
    -   Clique em **adicionar** para criar uma nova política de check-in.  
  
    -   Clique duas vezes em existente **análise de código** item o **tipo de política** lista para alterar a política.  
  
### <a name="to-set-policy-options"></a>Para definir opções de política  
  
-   Marque ou desmarque as opções a seguir:  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |**Impor o check-in contenha somente os arquivos que fazem parte da solução atual.**|Análise de código pode executar somente em arquivos especificados em arquivos de configuração de solução e projeto. Essa política garante que todo o código que faz parte de uma solução é analisado.|  
    |**Impor análise de código C/C++ (/Analyze)**|Requer que todos os projetos de C ou C++ compilados com o / opção analyze do compilador para executar a análise de código antes que eles podem fazer check-in.|  
    |**Impor análise de código para código gerenciado**|Requer que todos os projetos gerenciados executar análise de código e criar antes que eles podem fazer check-in.|  
  
-  
  
### <a name="to-specify-a-managed-rule-set"></a>Para especificar um conjunto de regras gerenciado  
  
-   Dos **executar este conjunto de regras** lista, use um dos seguintes métodos:  
  
    -   Selecione um conjunto de regras padrão do Microsoft.  
  
    -   Para selecionar um conjunto de regras personalizadas, clique em  **\<Selecionar conjunto de regras de controle do código-fonte... >** e, em seguida, digite o caminho de controle de versão da regra definida no navegador de controle do código-fonte. A sintaxe de um caminho de controle de versão é:  
  
    -   **$/** `TeamProjectName` **/** `VersionControlPath`  
  
    -   Para obter mais informações sobre como criar e implementar uma regra de política de check-in personalizado definido, consulte [políticas de Check-in personalizadas implementando para código gerenciado](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criando e usando políticas de check-in de análise de código](../code-quality/creating-and-using-code-analysis-check-in-policies.md)



