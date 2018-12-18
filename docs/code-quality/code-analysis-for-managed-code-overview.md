---
title: Análise estática de código para código gerenciado
ms.date: 03/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 96f00e6080cb10778a92aaa860422da8366be54d
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389306"
---
# <a name="overview-of-static-code-analysis-for-managed-code-in-visual-studio"></a>Visão geral da análise de código estático para código gerenciado no Visual Studio

Visual Studio 2017 pode executar a análise de código gerenciado de duas maneiras: com *FxCop* análise estática de assemblies gerenciados e com os mais modernos *analisadores de Roslyn*. Este tópico aborda a análise de código estático do FxCop. Para saber mais sobre a análise de código usando analisadores de código, consulte [analisadores de visão geral do Roslyn](../code-quality/roslyn-analyzers-overview.md).

Análise de código para código gerenciado analisa os assemblies gerenciados e relata informações sobre assemblies, como violações de programação e regras de design estabelecidas nas diretrizes de Design do Microsoft .NET Framework.

A ferramenta de análise representa as verificações que executa durante uma análise como mensagens de aviso. Mensagens de aviso identificam quaisquer problemas de programação e design relevantes e, quando é possíveis, forneça informações sobre como corrigir o problema.

> [!NOTE]
> Não há suporte para a análise de código estático para projetos do .NET Core e .NET Standard no Visual Studio. Se você executar a análise de código em um projeto .NET Core ou .NET Standard como parte do msbuild, você verá um erro semelhante ao **erro: CA0055: não foi possível identificar a plataforma para \<your.dll >**. Para analisar o código em projetos do .NET Core ou .NET Standard, use [analisadores de Roslyn](../code-quality/roslyn-analyzers-overview.md) em vez disso.

## <a name="ide-integrated-development-environment-integration"></a>Integração de IDE (ambiente de desenvolvimento integrado)

Você pode executar a análise de código em seu projeto automaticamente ou manualmente.

Para executar a análise de código sempre que você compila um projeto, selecione **habilitar a análise de código no Build** na página de propriedades do projeto. Para obter mais informações, consulte [como: habilitar e desabilitar análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md).

Para executar a análise de código manualmente em um projeto, na barra de menus, escolha **Analyze** > **executar análise de código** > **executar análise de código em \<projeto >**.

## <a name="rule-sets"></a>Conjuntos de regras

Regras de análise de código para código gerenciado são agrupadas em [conjuntos de regra](../code-quality/using-rule-sets-to-group-code-analysis-rules.md). Você pode usar um dos conjuntos de regra padrão Microsoft, ou você pode [criar um conjunto de regras personalizado](../code-quality/how-to-create-a-custom-rule-set.md) para atender a uma necessidade específica.

## <a name="suppress-warnings"></a>Suprimir avisos

Com frequência, é útil indicar que um aviso é não aplicáveis. Isso informa o desenvolvedor e outras pessoas que podem examinar o código mais tarde, que um aviso foi investigado e então suprimido ou ignorado.

Supressão de código-fonte de avisos é implementada por meio de atributos personalizados. Para suprimir um aviso, adicione o atributo `SuppressMessage` no código-fonte, conforme mostrado no exemplo a seguir:

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
Public class MyClass
{
   // code
}
```

Para obter mais informações, consulte [suprimir avisos](../code-quality/in-source-suppression-overview.md).

> [!NOTE]
> Se você migrar um projeto para Visual Studio 2017, você pode encontrar, de repente, com um grande número de avisos da análise de código. Se você não estiver pronto para corrigir os avisos e quer se tornar produtivo imediatamente, você poderá *linha de base* o estado de análise do seu projeto. Dos **Analyze** menu, selecione **executar análise de código e suprimir problemas ativos**.

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>Executar análise de código como parte da política de check-in

Como uma organização, você talvez queira exigem que todos os check-ins satisfaçam determinadas políticas. Em particular, você deseja certificar-se de que você siga essas políticas:

- Não há nenhum erro de compilação no check-in do código.

- Análise de código é executada como parte da compilação mais recente.

Você pode fazer isso com a especificação de políticas de check-in. Para obter mais informações, consulte [aprimorando a qualidade do código com políticas de Check-in do projeto](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md).

## <a name="team-build-integration"></a>Integração do Team build

Você pode usar os recursos integrados do sistema de compilação para executar a ferramenta de análise como parte do processo de compilação. Para obter mais informações, confira [Azure Pipelines](/azure/devops/pipelines/index?view=vsts).

## <a name="see-also"></a>Consulte também

- [Visão geral dos analisadores de Roslyn](../code-quality/roslyn-analyzers-overview.md)
- [Usando conjuntos de regras para agrupar regras de análise de código](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [Como habilitar e desabilitar a análise de código automática](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
