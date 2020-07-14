---
title: Sincronizar conjuntos de regras de projeto com a política de check-in
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.selecttfsruleset
ms.assetid: 9b02f934-2db6-41ec-aaff-9c31ceec2f04
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e27987f7fa298ddcedf52a9f01a80f57d3d329f
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371775"
---
# <a name="how-to-synchronize-code-project-rule-sets-with-an-azure-devops-project-check-in-policy"></a>Como: sincronizar conjuntos de regras de projeto de código com uma política de check-in do projeto DevOps do Azure

Sincronize as configurações de análise de código para projetos de código para a política de check-in do projeto DevOps do Azure especificando um conjunto de regras que contenha pelo menos as regras especificadas no conjunto de regras para a política de check-in. O líder do desenvolvedor pode informá-lo sobre o nome e o local do conjunto de regras para a política de check-in. Você pode usar uma das seguintes opções para garantir que a análise de código para o projeto Use o conjunto correto de regras:

- Se a política de check-in usar um dos conjuntos de regras internas da Microsoft, abra a caixa de diálogo Propriedades do projeto de código, exiba a página análise de código e selecione o conjunto de regras. Os conjuntos de regras padrão da Microsoft são instalados automaticamente com o Visual Studio são definidos como somente leitura e não devem ser editados. Se os conjuntos de regras não forem editados, as regras na política e nos conjuntos de regras locais têm a garantia de haver correspondência.

- Se a política de check-in usar um conjunto de regras personalizado, execute uma operação get no arquivo de conjunto de regras no controle de versão para criar uma cópia local. Em seguida, especifique o local local nas configurações de análise de código para o projeto de código. As regras têm a garantia de corresponder se o conjunto de regras para a política de check-in for atualizado.

     Se você mapear o local do controle de versão para uma pasta local que esteja na mesma relação com a raiz do projeto DevOps do Azure como seu projeto de código, o local da regra será definido usando um caminho relativo. O caminho relativo garante que a configuração do projeto de código para análise de código possa ser movida para outros computadores.

- Personalize uma cópia do conjunto de regras para a política de check-in de um projeto de código. Verifique se o novo conjunto de regras contém todas as regras na política de check-in e quaisquer outras regras que você queira incluir. Você deve verificar se o conjunto de regras inclui todas as regras no conjunto de regras para a política de check-in.

## <a name="to-specify-a-microsoft-standard-rule-set"></a>Para especificar um conjunto de regras padrão da Microsoft

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto de código e clique em **Propriedades**.

2. Clique em **Análise de código**.

::: moniker range="vs-2017"

3. Na lista **executar este conjunto de regras** , selecione o conjunto de regras da política de check-in.

::: moniker-end

::: moniker range=">=vs-2019"

3. Na lista **regras ativas** , selecione o conjunto de regras de política de check-in.

::: moniker-end

## <a name="to-specify-a-custom-check-in-policy-rule-set"></a>Para especificar um conjunto de regras de política de check-in personalizado

1. Se necessário, execute uma operação get no arquivo de conjunto de regras que especifica a política de check-in.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto de código e clique em **Propriedades**.

3. Clique em **Análise de código**.

::: moniker range="vs-2017"

4. Na lista **executar este conjunto de regras** , clique em **\<Browse>** .

::: moniker-end

::: moniker range=">=vs-2019"

4. Na lista **regras ativas** , clique em **\<Browse>** .

::: moniker-end

5. Na caixa de diálogo **abrir** , especifique o arquivo de conjunto de regras de política de check-in.

## <a name="to-create-a-custom-rule-set-for-a-code-project"></a>Para criar um conjunto de regras personalizado para um projeto de código

Para obter informações sobre como criar um conjunto de regras personalizadas, consulte [Personalizar um conjunto de regras](how-to-create-a-custom-rule-set.md).
