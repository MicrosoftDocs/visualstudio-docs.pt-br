---
title: Configurar análise de código
ms.date: 04/04/2018
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a8c922f0fc952cede53b9961e2e772e71a19cbb9
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371944"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>Como: configurar a análise herdada para código gerenciado

No Visual Studio, você pode escolher em uma lista de conjuntos de [regras](../code-quality/rule-set-reference.md) de análise de código para aplicar a um projeto de código gerenciado. Por padrão, o conjunto de regras **Microsoft mínimo recomendado** é selecionado, mas você pode aplicar um conjunto de regras diferente, se desejar. Os conjuntos de regras podem ser aplicados a um ou vários projetos em uma solução.

> [!NOTE]
> Este artigo se aplica à análise herdada e não a [analisadores de código baseados em .net Compiler Platform](use-roslyn-analyzers.md).

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>Configurar um conjunto de regras para um projeto .NET Framework

1. Abra a guia **análise de código** nas páginas de propriedades do projeto. É possível fazer isso de qualquer uma destas maneiras:

   - Em **Gerenciador de soluções**, selecione o projeto. Na barra de menus, selecione **analisar**  >  **Configurar análise**  >  **de código \<projectname> para **.

   - Clique com o botão direito do mouse no projeto em **Gerenciador de soluções** e selecione **Propriedades**e, em seguida, selecione a guia **análise de código** .

2. Nas listas de **configuração** e **plataforma** , selecione a configuração de compilação e a plataforma de destino.

::: moniker range="vs-2017"

3. Para executar a análise de código toda vez que o projeto for criado usando a configuração selecionada, selecione **Habilitar análise de código na compilação**. Você também pode executar a análise de código manualmente selecionando **analisar**  >  **executar análise de código**  >  **executar \<projectname> análise de código em **.

::: moniker-end

::: moniker range=">=vs-2019"

3. Para executar a análise de código toda vez que o projeto é compilado usando a configuração selecionada, selecione **executar na compilação** na seção **analisadores binários** . Você também pode executar a análise de código herdada manualmente, consulte [como executar análise de código herdada manualmente para código gerenciado](how-to-run-legacy-code-analysis-manually-for-managed-code.md) para obter mais detalhes.

::: moniker-end

4. Para exibir avisos do código gerado, desmarque a caixa de seleção **suprimir resultados do código gerado** .

    > [!NOTE]
    > Essa opção não suprimi erros de análise de código e avisos do código gerado quando os erros e avisos aparecem em formulários e modelos. Você pode exibir e manter o código-fonte de um formulário ou modelo e ele não será substituído.

::: moniker range="vs-2017"

5. Na lista **executar este conjunto de regras** , siga um destes procedimentos:

::: moniker-end

::: moniker range=">=vs-2019"

5. Na lista **regras ativas** , siga um destes procedimentos:

::: moniker-end

   - Selecione o conjunto de regras que você deseja usar.

   - Selecione **\<Browse>** para localizar um conjunto de regras personalizadas existente que não esteja na lista.

   - Defina um [conjunto de regras personalizadas](../code-quality/how-to-create-a-custom-rule-set.md).

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>Especificar conjuntos de regras para vários projetos em uma solução

Por padrão, todos os projetos gerenciados de uma solução são atribuídos ao conjunto de regras de análise de código de *regras recomendadas mínimas da Microsoft* . Você pode alterar os conjuntos de regras que são atribuídos aos projetos de uma solução na caixa de diálogo **Propriedades** da solução.

1. Abra a solução no Visual Studio.

2. No menu **analisar** , selecione **Configurar análise de código para solução**.

3. Se necessário, expanda **Propriedades comuns**e selecione **configurações de análise de código**.

4. Você pode especificar um conjunto de regras para um ou mais projetos:

    - Para especificar um conjunto de regras para um projeto individual, selecione o nome do projeto.

    - Para especificar um conjunto de regras para vários projetos, mantenha a **tecla CTRL** pressionada e selecione os nomes dos projetos.

    - Para especificar todos os projetos na solução, mantenha pressionada a **tecla Shift** e clique na lista projeto.

5. Selecione o campo **conjunto de regras** de um projeto e, em seguida, selecione o nome do conjunto de regras que você deseja aplicar.

## <a name="see-also"></a>Veja também

- [Referência do conjunto de regras da análise de código](../code-quality/rule-set-reference.md)
