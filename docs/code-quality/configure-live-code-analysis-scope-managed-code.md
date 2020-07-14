---
title: Configurar o escopo de análise de código ao vivo para código gerenciado
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 5b1e4362755bbbfa9ea220fcbdf92abf92723521
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462117"
---
# <a name="how-to-configure-live-code-analysis-scope-for-managed-code"></a>Como: configurar o escopo de análise de código ao vivo para código gerenciado

## <a name="what-is-live-code-analysis-for-managed-code"></a>O que é a "análise de código ao vivo" para código gerenciado?
O Visual Studio executa várias análises de código ao vivo, também chamadas de *análise em segundo plano*, enquanto você edita os arquivos de origem no editor. Algumas delas são necessárias para uma análise mínima de uma experiência aceitável de edição do IDE do Visual Studio. Alguns deles são para uma capacidade de resposta aprimorada para os recursos do IDE. Embora seja possível habilitar funcionalidades adicionais do IDE, como diagnóstico e correções de código de analisadores Roslyn. Com base na funcionalidade, essas análises podem ser agrupadas da seguinte maneira:

- **Computação em segundo plano de diagnóstico**: análise para computar erros, avisos e sugestões em arquivos de origem. Esses diagnósticos aparecem como entradas na lista de erros e como rabiscos no editor. Eles podem ser classificados em duas categorias:
    - Diagnóstico de compilador do C# e do Visual Basic
    - Diagnóstico do Roslyn Analyzer, que inclui:

        - Analisadores de IDE internos para sugestões de estilo de código e
        - Pacotes do analisador de terceiros [instalados](./install-roslyn-analyzers.md) para projetos na solução atual.

- **Outras análises em segundo plano**: análise para melhorar a capacidade de resposta e a interação do Visual Studio para recursos do IDE. Alguns exemplos dessas análises são:
    - Análise em segundo plano de arquivos abertos.
    - Compilação em segundo plano de projetos com arquivos abertos para obter símbolos para uma capacidade de resposta aprimorada de determinados recursos do IDE.
    - Criando caches de sintaxe e de símbolos.
    - Detectando a associação do designer para arquivos de origem, como formulários, controles, etc.

## <a name="default-analysis-scope"></a>Escopo de análise padrão

Por padrão, a análise de código ao vivo para computação em segundo plano de diagnóstico é executada para todos os arquivos que são _abertos_ no Visual Studio. Algumas das _outras análises em segundo plano_ mencionadas acima são executadas para todos os projetos, que têm pelo menos um arquivo aberto. Enquanto poucas análises em segundo plano são executadas para toda a solução.

## <a name="custom-analysis-scope"></a>Escopo de análise personalizada

O escopo padrão de cada análise em segundo plano foi ajustado para a melhor experiência do usuário, funcionalidade e desempenho para a maioria dos cenários e soluções de clientes. No entanto, há casos em que os clientes talvez queiram personalizar esse escopo para diminuir ou aumentar a análise em segundo plano. Por exemplo:

- Modo de economia de energia: se os usuários estiverem em execução na bateria do laptop, talvez desejam minimizar o consumo de energia para a vida útil da bateria. Nesse cenário, eles desejam minimizar a análise em segundo plano.
- Análise de código sob demanda: se os usuários preferem desativar a execução do analisador dinâmico e executar manualmente a análise de código sob demanda, eles desejam minimizar a análise em segundo plano. Consulte [como executar manualmente a análise de código sob demanda](./how-to-run-code-analysis-manually-for-managed-code.md).
- Análise de solução completa: se os usuários quiserem sempre ver todos os diagnósticos em todos os arquivos na solução, independentemente de estarem abertos ou não no editor. Nesse cenário, eles desejariam maximizar o escopo da análise em segundo plano para toda a solução.

A partir do Visual Studio 2019 versão 16,5, os usuários podem personalizar explicitamente o escopo de todas as análises de código ao vivo, incluindo a computação de diagnóstico, para projetos em C# e Visual Basic. Os escopos de análise disponíveis são:

- **Documento atual**: minimiza o escopo de análise de código ao vivo para execução somente para o arquivo atual ou visível no editor.
- **Documentos abertos**: escopo de análise de código ativo padrão, conforme descrito na seção acima.
- **Solução inteira**: maximiza o escopo de análise de código ao vivo para executar para todos os arquivos e projetos em toda a solução.

Você pode escolher um dos escopos de análise personalizados acima na caixa de diálogo ferramentas opções seguindo as etapas abaixo:

1. Para abrir a caixa de diálogo **Opções** , na barra de menus do Visual Studio, escolha **ferramentas**  >  **Opções**.

2. Na caixa de diálogo **Opções** , escolha **Editor de texto**  >  **C#** ou **básico**  >  **avançado**.

3. Selecione o **escopo de análise em segundo plano** desejado para personalizar o escopo de análise. Escolha **OK** quando terminar.

![Escopo da análise.](./media/background-analysis-scope.png)

> [!NOTE]
> Antes do Visual Studio 2019 versão 16,5, os usuários podem personalizar o escopo de análise para a computação de diagnóstico para toda a solução usando a caixa de seleção **Habilitar análise de solução completa** de **ferramentas**  >  **Opções**  >  **Editor de texto**  >  **C#** ou **Basic**  >  guia**avançado** básico. Não há suporte para minimizar o escopo da análise em segundo plano nas versões anteriores do Visual Studio.

## <a name="automatically-minimize-live-code-analysis-scope"></a>Minimizar automaticamente o escopo da análise de código dinâmico

Se o Visual Studio detectar que 200 MB ou menos de memória do sistema está disponível para ele, ele minimizará automaticamente o escopo da análise de código ao vivo para "documento atual". Se isso ocorrer, um alerta será exibido informando que o Visual Studio desabilitou alguns recursos. Um botão permite que você alterne de volta para o escopo de análise anterior, se desejar.

![Texto de alerta minimizando o escopo de análise](./media/fsa_alert.png)

## <a name="see-also"></a>Confira também

- [Suspensão automática de recursos](./automatic-feature-suspension.md)
- [Solicitação de recurso do modo de economia de energia](https://github.com/dotnet/roslyn/issues/38429)
