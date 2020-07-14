---
title: Criar ou atualizar políticas de check-in de análise de código padrão
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.policyeditor
helpviewer_keywords:
- code analysis, migrating check-in policy
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7167368128cb5946118a7692c50c15109feb79a0
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371892"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>Como criar ou atualizar políticas de check-in de análise do código padrão

Você pode exigir que a análise de código seja executada em todos os projetos de código em um projeto DevOps do Azure usando a política de check-in de análise de código. Exigir análise de código pode melhorar a qualidade do código que é verificado na base de código.

> [!NOTE]
> Esse recurso estará disponível somente se você estiver usando Team Foundation Server.

As políticas de check-in de análise de código são definidas nas configurações do projeto e se aplicam a cada projeto de código. As execuções de análise de código são configuradas para projetos de código no arquivo de projeto (. xxproj) para o projeto de código. As execuções de análise de código são executadas no computador local. Quando você habilita uma política de check-in de análise de código, os arquivos em um projeto de código que deverão ser verificados devem ser compilados após a última edição e uma execução de análise de código que contém, no mínimo, as regras nas configurações do projeto devem ser executadas no computador onde as alterações foram feitas.

- Para código gerenciado, você define a política de check-in especificando um *conjunto de regras* que contém um subconjunto das regras de análise de código.

- Para código C/C++, no Visual Studio 2017 versão 15,6 e anterior, a política de check-in requer que todas as regras de análise de código sejam executadas. Você pode adicionar diretivas de pré-processador para desabilitar regras específicas para os projetos de código individuais em seu projeto DevOps do Azure. No 15,7 e posterior, você pode usar **/analyze: RuleSet** para especificar quais regras executar. Para obter mais informações, consulte [usando conjuntos de regras para especificar as regras de C++ a serem executadas](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run).

Depois de especificar uma política de check-in para código gerenciado, os membros da equipe podem sincronizar suas configurações de análise de código para projetos de código para as configurações de política de projeto DevOps do Azure.

## <a name="to-open-the-check-in-policy-editor"></a>Para abrir o editor de diretiva de check-in

1. Em Team Explorer, clique com o botão direito do mouse no nome do projeto, aponte para **configurações do projeto**e clique em **controle do código-fonte**.

1. Na caixa de diálogo **controle do código-fonte** , selecione a guia **política de check-in** .

1. Realize um dos seguintes procedimentos:

    - Clique em **Adicionar** para criar uma nova política de check-in.

    - Clique duas vezes no item **análise de código** existente na lista **tipo de política** para alterar a política.

## <a name="to-set-policy-options"></a>Para definir opções de política

Marque ou desmarque as seguintes opções:

|Opção|Descrição|
|------------|-----------------|
|**Impor check-in para conter somente arquivos que fazem parte da solução atual.**|A análise de código pode ser executada somente em arquivos especificados nos arquivos de configuração da solução e do projeto. Essa política garante que todo o código que faz parte de uma solução seja analisado.|
|**Impor análise de código C/C++ (/Analyze)**|Requer que todos os projetos C ou C++ sejam compilados com a opção de compilador/analyze para executar a análise de código antes que eles possam ser verificados.|
|**Impor análise de código para código gerenciado**|Requer que todos os projetos gerenciados executem a análise de código e compilem antes que possam ser verificados.|

## <a name="to-specify-a-managed-rule-set"></a>Para especificar um conjunto de regras gerenciadas

Na lista **executar este conjunto de regras** , use um dos seguintes métodos:

- Selecione um conjunto de regras padrão da Microsoft.

- Selecione um conjunto de regras personalizado clicando em **\<Select Rule Set from Source Control...>** . Em seguida, digite o caminho de controle de versão do conjunto de regras no navegador de controle do código-fonte. A sintaxe de um caminho de controle de versão é:

   **$/** `TeamProjectName` **/** `VersionControlPath`

Para obter mais informações sobre como criar e implementar um conjunto de regras de política de check-in personalizado, consulte [implementar políticas de check-in personalizadas para código gerenciado](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md).

## <a name="see-also"></a>Veja também

- [Implementar políticas de check-in de análise de código personalizadas para código gerenciado](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)
