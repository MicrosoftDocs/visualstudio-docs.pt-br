---
title: Criar um conjunto de regras de análise de código personalizado
ms.date: 11/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 061ceec7a513a0d4c92f06fad5ef730100dbfb8e
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000210"
---
# <a name="customize-a-rule-set"></a>Personalizar um conjunto de regras

Você pode criar uma regra personalizada definida para atender às necessidades específicas do projeto para análise de código.

## <a name="create-a-custom-rule-set"></a>Criar um conjunto de regras personalizado

Para criar uma regra personalizada definida, você pode abrir uma conjunto de regras internas do **editor de conjunto de regras**. A partir daí, você pode adicionar ou remover regras específicas, e você pode alterar a ação que ocorre quando uma regra é violada&mdash;Mostrar, por exemplo, um aviso ou erro.

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, em seguida, selecione **propriedades**.

2. Sobre o **propriedades** páginas, selecionadas a **análise de código** guia.

3. No **executar este conjunto de regras** lista suspensa, siga um destes procedimentos:

   - Selecione o conjunto de regras que você deseja personalizar.

     \- ou -

   - Selecione  **\<procurar... >** especificar uma regra existente definida que não está na lista.

4. Selecione **abrir** para exibir as regras no editor de conjunto de regras.

Você também pode criar um novo arquivo de conjunto de regras do **novo arquivo** caixa de diálogo:

1. Selecione **arquivo** > **New** > **arquivo**, ou pressione **Ctrl**+**N**.

2. No **novo arquivo** caixa de diálogo, selecione o **gerais** categoria à esquerda e, em seguida, selecione **conjunto de regras de análise de código**.

3. Selecione **Abrir**.

   O novo *RuleSet* arquivo é aberto no editor de conjunto de regras.

### <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>Criar uma regra personalizada definida de vários conjuntos de regra

1. No Gerenciador de soluções, clique com botão direito no projeto e, em seguida, selecione **propriedades**.

2. Sobre o **propriedades** páginas, selecionadas a **análise de código** guia.

3. Selecione  **\<escolher vários regra define... >** partir **executar este conjunto de regras**.

4. No **adicionar ou remover conjuntos de regras** caixa de diálogo, selecione os conjuntos de regras você deseja incluir em seu novo conjunto de regras.

   ![Adicionar ou remover a caixa de diálogo de conjuntos de regra](media/add-remove-rule-sets.png)

5. Selecione **Salvar como**, insira um nome para o *RuleSet* de arquivo e, em seguida, selecione **salvar**.

   O novo conjunto de regras é selecionado na **executar este conjunto de regras** lista.

6. Selecione **abrir** para abrir a nova regra definida no editor de conjunto de regras.

### <a name="rule-precedence"></a>Precedência de regra

- Se a mesma regra é listadas duas ou mais vezes em uma conjunto de regras com gravidades diferentes, o compilador gera um erro. Por exemplo:

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- Se a mesma regra é listadas duas ou mais vezes em uma regra definida com o *mesmo* gravidade, você poderá ver o seguinte aviso na **lista de erros**:

   **CA0063: Falha ao carregar o arquivo de conjunto de regras '\[seu] RuleSet ' ou uma de suas regras dependentes definida arquivos. O arquivo não estiver de acordo com o esquema do conjunto de regra.**

- Se o conjunto de regras inclui uma regra de filho definida usando um **Include** a mesma regra de lista de marca e os conjuntos de regras pai e filho ambos os mas com gravidades diferentes, em seguida, a gravidade no conjunto de regras pai terá precedência. Por exemplo:

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

Para alterar o nome de exibição de um conjunto de regras que é aberto no editor, abra o **propriedades** janela selecionando **exibição** > **janela propriedades** na barra de menus. Insira o nome de exibição na **nome** caixa. Você também pode inserir uma descrição para o conjunto de regras.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma regra definida, a próxima etapa é personalizar as regras, adicionando ou removendo regras ou modificando a gravidade das violações de regra.

> [!div class="nextstepaction"]
> [Modificar as regras no editor de conjunto de regras](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>Consulte também

- [Como configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [Referência do conjunto de regras de análise de código](../code-quality/rule-set-reference.md)