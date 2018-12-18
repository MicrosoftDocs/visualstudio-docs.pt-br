---
title: 'Como: sincronizar conjuntos de regras do projeto de código com a política de Check-in do projeto de equipe | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.codeanalysis.selecttfsruleset
ms.assetid: 9b02f934-2db6-41ec-aaff-9c31ceec2f04
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 482f3107aeb7545951632f6841c43968067b1b2a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263114"
---
# <a name="how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy"></a>Como sincronizar conjuntos de regras do projeto de código com política de check-in do projeto de equipe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode sincronizar as configurações de análise de código para projetos de código para a política de check-in para o projeto de equipe, especificando um conjunto de regras que contenha pelo menos as regras que são especificadas na regra definida para a política de check-in. O líder de desenvolvimento pode informar o nome e o local da regra definida para a política de check-in. Você pode usar uma das opções a seguir para garantir que a análise de código para o projeto usa o conjunto correto de regras:  
  
-   Se a política de check-in usa um dos conjuntos de regra interna de Microsoft, abrir a caixa de diálogo Propriedades do projeto de código, exibir a página de análise de código e selecione a regra definida na página de análise de código das configurações de projeto de código. A Microsoft conjuntos de regras padrão são instalados automaticamente com o Visual Studio são definidos como somente leitura e não deve ser editado. Se os conjuntos de regras não são editados, as regras na política e conjuntos de regras locais são garantidas para corresponder.  
  
-   Se a política de check-in usa um conjunto de regras personalizadas, execute uma operação get no arquivo de conjunto de regras no controle de versão para criar uma cópia local. Em seguida, especifica esse local nas configurações de análise de código para o projeto de código. As regras são garantidas para correspondência se a regra definida para a política de check-in é atualizada.  
  
     Se você mapear o local do controle de versão em uma pasta local que está na mesma relação à raiz do projeto de equipe como seu projeto de código, o local da regra é definido usando um caminho relativo. O caminho relativo garante que a configuração de projeto de código para análise de código pode ser movida para outros computadores.  
  
-   Personalize uma cópia da regra definida para a política de check-in para um projeto de código. Certifique-se de que o novo conjunto de regras contém todas as regras na política de check-in e outras regras que você deseja incluir. Certifique-se de que seu conjunto de regras de inclui todas as regras na regra definida para a política de check-in.  
  
### <a name="to-specify-a-microsoft-standard-rule-set"></a>Para especificar uma regra padrão da Microsoft definido  
  
1.  Na **Gerenciador de soluções**, clique com botão direito no projeto de código e, em seguida, clique em **propriedades**.  
  
2.  Clique em **análise de código**.  
  
3.  No **executar este conjunto de regras** lista, clique no conjunto de regra de política de check-in.  
  
### <a name="to-specify-a-custom-check-in-policy-rule-set"></a>Para especificar um conjunto de regras de política de check-in personalizado  
  
1.  Se necessário, execute uma operação get no arquivo de conjunto de regra que especifica a política de check-in.  
  
2.  Na **Gerenciador de soluções**, clique com botão direito no projeto de código e, em seguida, clique em **propriedades**.  
  
3.  Clique em **análise de código**.  
  
4.  No **executar este conjunto de regras** , clique em  **\<procurar... >**.  
  
5.  No **abrir** caixa de diálogo, especifique o arquivo de conjunto de regra de política de check-in.  
  
### <a name="to-create-a-custom-rule-set-for-a-code-project"></a>Para criar uma regra personalizada definida para um projeto de código  
  
1.  Siga um dos procedimentos neste tópico para selecionar a política de check-in do projeto da equipe na página de análise de código da caixa de diálogo de configurações do projeto.  
  
2.  Clique em **aberto**.  
  
3.  Adicionar ou remover regras usando o editor de conjunto de regras.  
  
     Para obter mais informações, consulte [criação de conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md).  
  
4.  Salve a regra modificada definido como um arquivo. RuleSet no computador local ou em um caminho UNC.  
  
5.  Abrir a caixa de diálogo Propriedades do projeto de código e exibir o **análise de código** página.  
  
6.  No **executar este conjunto de regras** , clique em  **\<procurar... >**.  
  
7.  No **abrir** caixa de diálogo, especifique o arquivo de conjunto de regra.



