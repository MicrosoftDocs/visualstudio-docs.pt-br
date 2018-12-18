---
title: Use o Editor de conjunto de regras de análise de código
ms.date: 04/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.ruleseteditor
ms.assetid: 370c97bf-bb29-4b2f-b9ae-ba125bce7b2d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bdd80031530049b204c0befc445c1416aa08b43e
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000810"
---
# <a name="use-the-code-analysis-rule-set-editor"></a>Use o editor de conjunto de regras de análise de código

A regra de análise de código definido editor permite a que você especifica as regras que estão incluídas em uma regra personalizada definida e definir a gravidade das violações de regra.

A tabela a seguir mostra as opções de gravidade:

|Ação (severidade)|Descrição|
|-|-|
|Aviso|Gera um aviso na **Error List** e também no momento da compilação.|
|Erro|Gera um erro no **Error List** e também no momento da compilação.|
|Info|Gera uma mensagem na **Error List**.|
|Hidden|A violação não é visível para o usuário. O IDE é notificado da violação, no entanto.|
|Nenhum|A regra será suprimida. O comportamento é o mesmo como se a regra foi removida do conjunto de regras.|

O editor exibe as regras em uma estrutura de árvore que grupos de regras por uma regra de conjunto de campo que você especificar. Para adicionar ou remover as regras de um conjunto de regras, execute uma ou mais das seguintes etapas:

- Marque ou desmarque a caixa de seleção do nó de grupo para adicionar ou remover todas as regras do grupo. Quando você seleciona um grupo, todas as regras são definidas o **aviso** ação.

   > [!TIP]
   > Você pode alterar como as regras são agrupadas na **Group by** lista suspensa.

- Clique o **ação** campo de um grupo e, em seguida, especifique a ação a ser aplicado a todas as regras do grupo.

- Marque ou desmarque a caixa de seleção de uma regra individual. Quando você seleciona a caixa de seleção para uma regra, a regra é definida como a ação de aviso.

## <a name="toolbar"></a>Barra de ferramentas

Você pode usar a barra de ferramentas do editor de conjunto de regras para agrupar, filtrar e pesquisar os dados que aparecem na grade de conjunto de regras.

A tabela a seguir descreve os controles na barra de ferramentas do editor de conjunto de regras.

|Controle de barra de ferramentas|Descrição|
|---------------------|-----------------|
|**Expandir tudo**|Mostra as regras em todos os grupos.|
|**Recolher tudo**|Oculta as regras em todos os grupos.|
|**Group By**|Especifica o campo pelo qual as regras são agrupadas. Clique em  **\<None >** para mostrar as regras sem grupos.|
|**Opções de coluna**|Especifica os campos de regra a serem exibidos.|
|**Ocultar as regras que não se aplicam à solução atual**|Mostra ou oculta as regras que não são do mesmo tipo de destino como a solução.|
|**Mostrar regras que podem gerar erros de análise de código**|Mostra ou oculta as regras que são atribuídas a ação de erro.|
|**Mostrar regras que podem gerar avisos de análise de código**|Mostra ou oculta as regras que são atribuídas a ação de aviso.|
|**Mostrar regras que não estão habilitadas**|Mostra ou oculta as regras que são atribuídas a nenhuma ação.|
|**Adicionar ou remover conjuntos de regras filho**|Adiciona ou remove as regras nos conjuntos de regra selecionada.|
|**Pesquisar regras**|Pesquisa todos os valores de campo para a cadeia de caracteres que você especificar.|

## <a name="rule-set-fields"></a>Campos do conjunto de regras

Campos de conjunto de regra exibem informações sobre um conjunto de regras e podem ser usados para classificar e agrupar a lista de regras. Para exibir ou ocultar campos, selecione **opções de coluna** na regra de conjunto de ferramentas do editor e, em seguida, marque ou desmarque as caixas de seleção dos campos para mostrar ou ocultar.

A tabela a seguir descreve os campos de um conjunto de regras:

|Campo|Descrição|
|-----------|-----------------|
|**ID**|O identificador da regra.|
|**Categoria**|Além de sua participação em conjuntos de regras, regras de análise de código também são agrupadas por categoria. Para obter mais informações, consulte [avisos de análise de código](../code-quality/code-analysis-for-managed-code-warnings.md).|
|**Nome**|O título da regra.|
|**Namespace**|O namespace da regra.|
|**Tipo de destino**|Indica se a regra é para nativo, gerenciado ou código de banco de dados.|
|**Ação**|A ação executada quando a regra é violada em uma execução de análise de código. Você pode editar a **ação** campo.|
|**Conjuntos de regras de código-fonte**|O conjunto de regras que contém a regra.|

## <a name="sort-and-filter-rule-sets"></a>Classificar e filtrar conjuntos de regras

Os cabeçalhos de coluna da grade de conjunto de regras, você pode classificar e filtrar as regras pelos valores do campo.

- Para classificar a lista de conjunto de regra, clique no cabeçalho da coluna do campo pelo qual você deseja classificar. Se os conjuntos de regras são agrupados, cada grupo é classificado individualmente.

- Para filtrar os conjuntos de regras pelo valor de um campo, clique no botão de filtro no cabeçalho da coluna do campo pelo qual você deseja filtrar. Marque as caixas de seleção dos valores que você deseja mostrar e desmarque as caixas de seleção dos valores que você deseja ocultar.

## <a name="see-also"></a>Consulte também

- [Criar um conjunto de regras personalizado](../code-quality/how-to-create-a-custom-rule-set.md)