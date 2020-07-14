---
title: Criar um conjunto de regras de análise de código personalizado
ms.date: 11/02/2018
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81462db07941c73b847c009ef8353b00d28fff4f
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371905"
---
# <a name="customize-a-rule-set"></a>Personalizar um conjunto de regras

Você pode criar um conjunto de regras personalizadas para atender às necessidades específicas do projeto para análise de código.

## <a name="create-a-custom-rule-set-from-an-existing-rule-set"></a>Criar um conjunto de regras personalizado a partir de um conjunto de regras existente

Para criar um conjunto de regras personalizado, você pode abrir um conjunto de regras internas no **Editor de conjunto de regras**. A partir daí, você pode adicionar ou remover regras específicas e pode alterar a ação que ocorre quando uma regra é violada, &mdash; por exemplo, mostrar um aviso ou um erro.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e selecione **Propriedades**.

2. Nas páginas de **Propriedades** , selecione a guia **análise de código** .

::: moniker range="vs-2017"

3. Na lista suspensa **executar esta regra definida** , siga um destes procedimentos:

::: moniker-end

::: moniker range=">=vs-2019"

3. Na lista suspensa **regras ativas** , siga um destes procedimentos:

::: moniker-end

   - Selecione o conjunto de regras que você deseja personalizar.

     \- ou –

   - Selecione **\<Browse>** para especificar um conjunto de regras existente que não esteja na lista.

4. Selecione **abrir** para exibir as regras no editor de conjunto de regras.

> [!NOTE]
> Se você tiver um projeto do .NET Core ou .NET Standard, o processo será um pouco diferente porque não há nenhuma guia de propriedade de **análise de código** . siga as etapas para [copiar um conjunto de regras predefinidas para seu projeto e defini-lo como o conjunto de regras ativas](analyzer-rule-sets.md). Depois de copiar um conjunto de regras, você pode [editá-lo no editor de conjunto de regras do Visual Studio](working-in-the-code-analysis-rule-set-editor.md) abrindo-o em **Gerenciador de soluções**.

## <a name="create-a-new-rule-set"></a>Criar um novo conjunto de regras

Você pode criar um novo arquivo de conjunto de regras a partir da caixa de diálogo **novo arquivo** :

1. Selecione **arquivo**  >  **novo**  >  **arquivo**ou pressione **Ctrl** + **N**.

2. Na caixa de diálogo **novo arquivo** , selecione a categoria **geral** à esquerda e, em seguida, selecione **conjunto de regras de análise de código**.

3. Selecione **Abrir**.

   O novo arquivo *. RuleSet* é aberto no editor de conjunto de regras.

## <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>Criar um conjunto de regras personalizado de vários conjuntos de regras

> [!NOTE]
> O procedimento a seguir não se aplica a projetos do .NET Core, que não têm uma guia de propriedade de **análise de código** .

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e selecione **Propriedades**.

2. Nas páginas de **Propriedades** , selecione a guia **análise de código** .

::: moniker range="vs-2017"

3. Selecione **\<Choose multiple rule sets>** em **executar este conjunto de regras**.

::: moniker-end

::: moniker range=">=vs-2019"

3. Selecione uma **\<Choose multiple rule sets>** das **regras ativas**.

::: moniker-end

4. Na caixa de diálogo **Adicionar ou remover conjuntos de regras** , selecione os conjuntos de regras que deseja incluir no novo conjunto de regras.

   ![Caixa de diálogo Adicionar ou remover conjuntos de regras](media/add-remove-rule-sets.png)

5. Selecione **salvar como**, insira um nome para o arquivo *. RuleSet* e, em seguida, selecione **salvar**.

   O novo conjunto de regras é selecionado na lista **executar este conjunto de regras** .

6. Selecione **abrir** para abrir o novo conjunto de regras no editor de conjunto de regras.

## <a name="rule-precedence"></a>Precedência de regra

- Se a mesma regra estiver listada duas ou mais vezes em um conjunto de regras com severidades diferentes, o compilador gerará um erro. Por exemplo:

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- Se a mesma regra estiver listada duas ou mais vezes em um conjunto de regras com a *mesma* gravidade, você poderá ver o seguinte aviso no **lista de erros**:

   **CA0063: falha ao carregar o arquivo de conjunto \[ de regras ' Your]. RuleSet ' ou um de seus arquivos de conjunto de regras dependentes. O arquivo não está em conformidade com o esquema do conjunto de regras.**

- Se o conjunto de regras incluir uma regra filho definida usando uma marca **include** , e os conjuntos de regras filho e Parent listarem a mesma regra, mas com severidades diferentes, a severidade no conjunto de regras pai terá precedência. Por exemplo:

   ```xml
   <!-- Parent rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Include Path="classlibrary_child.ruleset" Action="Default" />
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" /> <!-- Overrides CA1021 severity from child rule set -->
     </Rules>
   </RuleSet>

   <!-- Child rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules from child" Description="Code analysis rules from child." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

## <a name="name-and-description"></a>Nome e descrição

Para alterar o nome de exibição de um conjunto de regras que está aberto no editor, abra a janela **Propriedades** selecionando janela **Exibir**  >  **Propriedades** na barra de menus. Insira o nome de exibição na caixa **nome** . Você também pode inserir uma descrição para o conjunto de regras.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um conjunto de regras, a próxima etapa é personalizar as regras adicionando ou removendo regras ou modificando a gravidade das violações de regra.

> [!div class="nextstepaction"]
> [Modificar regras no editor de conjunto de regras](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>Veja também

- [Como configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [Referência do conjunto de regras da análise de código](../code-quality/rule-set-reference.md)
