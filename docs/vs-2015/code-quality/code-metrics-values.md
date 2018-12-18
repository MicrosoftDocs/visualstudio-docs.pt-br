---
title: Valores de métricas de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code metrics
- code analysis
- measure code quality
ms.assetid: bc38831e-2083-4ea4-8527-ee41499a342f
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 22c42cb215999fcc4415f4d7541b8f4b95ac2d29
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782954"
---
# <a name="code-metrics-values"></a>Valores de métricas do código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As métricas de código são um conjunto de medidas de software que fornecem aos desenvolvedores uma visão melhor do código que estão desenvolvendo. Ao tirar proveito das métricas de código, os desenvolvedores poderão entender quais tipos de e/ou os métodos devem ser reformulados ou mais minuciosamente. As equipes de desenvolvimento podem identificar possíveis riscos, entender o estado atual de um projeto e acompanhar o progresso durante o desenvolvimento de software.  
  
## <a name="software-measurements"></a>Medições de software  
 A lista a seguir mostra os resultados de métricas de código que [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] calcula:  
  
-   **Índice de facilidade de manutenção** – calcula um valor de índice entre 0 e 100 que representa a relativa facilidade de manutenção do código. Um valor alto significa melhor facilidade de manutenção. Classificações codificadas por cor podem ser usadas para identificar rapidamente pontos problemáticos em seu código. Uma classificação verde está entre 20 e 100 e indica que o código tem boa facilidade de manutenção. Uma classificação amarela é entre 10 e 19 e indica que o código é razoavelmente fácil de manter. Uma classificação vermelha é uma classificação entre 0 e 9 e indica pouca facilidade de manutenção.  
  
-   **A complexidade ciclomática** – mede a complexidade do código estrutural. Ele é criado pelo cálculo do número de diferentes caminhos de código no fluxo do programa. Um programa que tem o fluxo de controle complexo exigirá mais testes para obter boa cobertura do código e será menos capaz de manutenção.  
  
    > [!NOTE]
    >  Em alguns casos, o cálculo da complexidade ciclomática de um método em [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] difere das versões anteriores. Para obter mais informações, consulte "Alterações no Visual Studio 2010 seção de código complexidade cálculos" de [solução de problemas de métricas de código](../code-quality/troubleshooting-code-metrics-issues.md).  
  
-   **Profundidade de herança** – indica o número de definições de classe que estenda para a raiz da hierarquia de classe. Quanto mais a hierarquia mais difícil pode ser entender onde os campos e métodos particulares são definidos ou / e redefinido.  
  
-   **Classe acoplamento** – mede o acoplamento de classes exclusivos por meio de parâmetros, variáveis locais, tipos de retorno, chamadas de método, instanciações genéricas ou modelo, as classes base, implementações de interface, os campos definidos nos tipos externos, e decoração do atributo. Design de software BOM determina que tipos e métodos devem ter alta coesão e acoplamento de baixa. Acoplamento alta indica um design que é difícil a reutilização e a manter o devido à suas muitas interdependências em outros tipos.  
  
-   **Linhas de código** – indica o número aproximado de linhas de código. A contagem é baseada no código IL e, portanto, não o número exato de linhas no arquivo de código de origem. Uma contagem muito alta pode indicar que um tipo ou método está tentando fazer muito trabalho e deve ser dividido. Isso também pode indicar que o tipo ou método pode ser difícil de manter.  
  
## <a name="anonymous-methods"></a>Métodos anônimos  
 Uma *método anônimo* é apenas um método que não tem nome. Métodos anônimos são usados com mais frequência para passar um bloco de código como um parâmetro delegado. Resultados de métricas para um método anônimo que é declarada em um membro, como um método ou um acessador, estão associados com o membro que declara o método. Eles não são associados com o membro que chama o método.  
  
 Para obter mais informações sobre como as métricas de código trata os métodos anônimos, consulte [métodos anônimos e análise de código](../code-quality/anonymous-methods-and-code-analysis.md).  
  
## <a name="generated-code"></a>Código gerado  
 Alguns compiladores e ferramentas de software geram código que é adicionado a um projeto e que o desenvolvedor do projeto não vê ou não deve ser alterada. Em grande parte, as métricas de código ignora o código gerado quando ela calcula os valores das métricas. Isso permite que os valores das métricas refletir o que o desenvolvedor possa ver e alterar.  
  
 Código gerado para formulários do Windows não é ignorado, porque ele é o código que o desenvolvedor possa ver e alterar.  
  
## <a name="see-also"></a>Consulte também  
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)



