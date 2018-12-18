---
title: Configurar a análise de código
ms.date: 04/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: c94c1a82acfcabaa8bc6d73eb302b8760c5df2ec
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062416"
---
# <a name="how-to-configure-code-analysis-for-a-managed-code-project"></a>Como configurar a análise de código para um projeto de código gerenciado

No Visual Studio, você pode escolher de uma lista de análise de código [conjuntos de regra](../code-quality/rule-set-reference.md)) para aplicar a um projeto de código gerenciado. Por padrão, o **Microsoft mínimo recomendado regras** conjunto de regras é selecionado, mas você pode aplicar uma regra diferente, defina se desejado. Conjuntos de regras podem ser aplicados a um ou vários projetos em uma solução.

> [!TIP]
> Para obter informações sobre como configurar uma regra definida para aplicativos web ASP.NET, consulte [como: configurar a análise de código para um ASP.NET web Application](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md).

## <a name="to-configure-a-rule-set-for-a-net-framework-project"></a>Para configurar uma regra definida para um projeto do .NET Framework

1. Abra o **análise de código** guia nas páginas de propriedades do projeto. Você pode fazer isso em qualquer uma das seguintes maneiras:

   - Na **Gerenciador de soluções**, selecione o projeto. Na barra de menus, selecione **Analyze** > **configurar a análise de código** > **para \<projectname >**.

   - Clique com botão direito no projeto no **Gerenciador de soluções** e selecione **Properties**e, em seguida, selecione o **análise de código** guia.

1. No **Configuration** e **plataforma** listas, selecione a plataforma de destino e a configuração de compilação.

1. Para executar análise de código sempre que o projeto é compilado usando a configuração selecionada, selecione a **habilitar a análise de código no Build** caixa de seleção. Você também pode executar a análise de código manualmente selecionando **Analyze** > **executar análise de código** > **executar análise de código em \<projectname >**.

1. Por padrão, a análise de código não relate os avisos de código que é gerado automaticamente por ferramentas externas. Para exibir avisos do código gerado, desmarque a **Suprimir resultados do código gerado** caixa de seleção.

    > [!NOTE]
    > Essa opção não suprime erros de análise de código e avisos do código gerado quando os erros e avisos que aparecem em formulários e modelos. Você pode exibir e manter o código-fonte para um formulário ou um modelo, sem ter que ele é substituído.

1. No **executar este conjunto de regras** lista, siga um destes procedimentos:

    - Selecione o conjunto de regras que você deseja usar.

    - Selecione  **\<procurar... >** localizar o conjunto de uma regra personalizada existente que não está na lista.

    - Definir um [conjunto de regras personalizado](../code-quality/how-to-create-a-custom-rule-set.md).

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>Especificar conjuntos de regras para vários projetos em uma solução

Por padrão, todos os projetos gerenciados de uma solução são atribuídos a *Microsoft mínimo recomendado regras* conjunto de regras de análise de código. Você pode alterar os conjuntos de regras que são atribuídos aos projetos de uma solução com o **propriedades** caixa de diálogo para a solução.

1. Abra a solução no Visual Studio.

2. Sobre o **Analyze** menu, selecione **configurar a análise de código para solução**.

3. Se necessário, expanda **propriedades comuns**e, em seguida, selecione **configurações de análise de código**.

4. Você pode especificar uma regra definida para um ou mais projetos:

    - Para especificar uma regra definida para um projeto individual, selecione o nome do projeto.

    - Para especificar uma regra definida para vários projetos, mantenha pressionada **Ctrl** e selecione os nomes de projeto.

    - Para especificar todos os projetos na solução, mantenha pressionada **Shift** e clique na lista de projetos.

5. Selecione o **do conjunto de regras** campo de um projeto e, em seguida, selecione o nome da regra definida que você deseja aplicar.

## <a name="see-also"></a>Consulte também

- [Referência do conjunto de regras de análise de código](../code-quality/rule-set-reference.md)
- [Como: configurar a análise de código para um aplicativo web do ASP.NET](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)