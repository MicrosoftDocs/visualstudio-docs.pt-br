---
title: Verificando e depurando o código do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- unit testing [SharePoint development in Visual Studio]
- IntelliTrace [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, IntelliTrace
- SharePoint development in Visual Studio, unit testing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 327e7be43fc60142fc50634ec61f6fd9499461e2
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118453"
---
# <a name="verify-and-debug-sharepoint-code"></a>Verificar e depurar o código do SharePoint
Usando o IntelliTrace e o teste de unidade, com mais facilidade você pode depurar suas soluções do SharePoint e certifique-se de que cada método neles funcione corretamente. Você pode usar esses recursos para projetos do SharePoint no Visual Studio, seguindo os mesmos procedimentos que para outros tipos de projetos.

## <a name="intellitrace"></a>IntelliTrace
Usando o IntelliTrace, você pode determinar não apenas o estado atual da sua solução do SharePoint, mas também eventos que ocorreram no passado e o contexto em que eles ocorreram. Você pode navegar e voltar para vários pontos no tempo em sua solução do SharePoint onde os eventos de interesse foram registrados e examine os estados e os valores das variáveis em cada ponto. Usando essa navegação dinâmica, você pode mais rapidamente e facilmente depurar suas soluções do SharePoint sem precisar definir muitos pontos de interrupção. Você também pode salvar a sessão de depuração em um log do IntelliTrace (*. itrace*) de arquivos, abri-lo mais tarde no Visual Studio Enterprise e realizar a depuração de pós-falha. O *. itrace* arquivo inclui informações detalhadas sobre quando e onde ocorreram erros específicos do SharePoint, para que você pode descobrir mais facilmente o que está causando os erros. As informações de *. itrace* arquivo é um subconjunto do log de erros completa que cria ULS log unificado do sistema () no SharePoint. Essas informações incluem eventos que são específicos para o SharePoint, como quando um perfil de usuário é aberto ou fechado, e quando as propriedades em um SharePoint project são carregados, lidas ou alteradas. Você pode configurar os eventos IntelliTrace registra. Para obter mais informações, consulte [usando dados salvo do IntelliTrace](/visualstudio/debugger/using-saved-intellitrace-data).

Quando ocorre um erro no SharePoint, a caixa de diálogo de erro exibe um identificador de "ID de correlação" para esse erro específico. Você também pode obter as IDs de correlação de eventos que são listados na *. itrace* arquivo. Para exibir uma lista de todos os eventos que ocorreram com uma ID de correlação fornecido, você pode inserir a ID na **análise** seção da página de resumo do IntelliTrace. Nesta seção, você pode optar por exibir somente os nomes dos eventos que ocorreram ou os nomes dos eventos, juntamente com suas informações de chamada, como o nome da função, os pontos de entrada e saída, parâmetros e valores de retorno.

Você pode obter eventos do Visual Studio no IntelliTrace escolhendo os **F5** chave. Para obter os eventos que são específicos para o SharePoint, no entanto, você deve coletar dados do IntelliTrace em soluções do SharePoint usando o Microsoft Monitoring Agent. Essa ferramenta coleta dados do IntelliTrace e cria *. itrace* arquivos para aplicativos que são implantados fora do Visual Studio. Para obter mais informações, consulte [recursos do IntelliTrace](/visualstudio/debugger/intellitrace-features) e [usando o coletor autônomo IntelliTrace](/visualstudio/debugger/using-the-intellitrace-stand-alone-collector).

## <a name="unit-test"></a>Teste de unidade
Você pode encontrar mais facilmente os erros em seu código executando testes de unidade, na qual você escreve e executa o código de teste dentro de métodos de teste. Esses métodos contêm variáveis vazias e uma instrução Assert que você pode usar para verificar a lógica e a funcionalidade do seu projeto com base no modelo de objeto do SharePoint. Para obter mais informações, consulte [Efetuar teste de unidade em seu código](/visualstudio/test/unit-test-your-code).

### <a name="support-for-microsoft-fakes-framework"></a>Suporte para o Microsoft Fakes framework
Suporte de projetos do SharePoint Microsoft Fakes, que é uma estrutura de isolamento em que você pode criar com base em delegado teste stubs e shims em aplicativos que são baseados no .NET Framework. Usando a estrutura do Fakes, você pode criar, manter e injetar implementações fictícias em seus testes de unidade. Esses stubs e shims isolam seus testes de unidade do ambiente. Você pode criar stubs para testar o código que consome as interfaces ou classes não seladas com métodos substituíveis. Você pode criar shims para redirecionar as chamadas embutido em código, para classes lacradas com métodos estáticos ou não pode ser substituído para uma implementação de shim alternativo. Você também pode usar delegados com tipos de shim e tipos de stub para personalizar dinamicamente o comportamento de membros individuais de stub. Para obter mais informações, consulte [isolando código em teste com Microsoft Fakes](/visualstudio/test/isolating-code-under-test-with-microsoft-fakes).

## <a name="related-articles"></a>Artigos relacionados

|Título|Descrição|
|-----------|-----------------|
|[IntelliTrace](/visualstudio/debugger/intellitrace)|Descreve como depurar soluções do Visual Studio com mais facilidade usando o IntelliTrace.|
|[Passo a passo: Depurar um aplicativo do SharePoint usando o IntelliTrace](../sharepoint/walkthrough-debugging-a-sharepoint-application-by-using-intellitrace.md)|Demonstra como localizar erros de codificação em um projeto do SharePoint usando o IntelliTrace.|
|[Efetuar teste de unidade em seu código](/visualstudio/test/unit-test-your-code)|Descreve como localizar erros lógicos em seu código usando testes de unidade.|

## <a name="see-also"></a>Consulte também
[Melhorar a qualidade do código](/visualstudio/test/improve-code-quality)
