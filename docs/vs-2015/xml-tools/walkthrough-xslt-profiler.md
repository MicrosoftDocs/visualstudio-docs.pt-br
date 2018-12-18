---
title: 'Passo a passo: Profiler XSLT | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 87387c9a-2e89-4801-ad51-83740cd6ea25
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4f401d253c81385dc197e912a7f9cc7d6156e393
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49229444"
---
# <a name="walkthrough-xslt-profiler"></a>Passo a passo: Profiler XSLT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O profiler XSLT criar relatórios de desempenho detalhados XSLT que a medida da ajuda, avalia, e problemas de desempenho relacionados de destino no código XSLT. O profiler XSLT inclui dicas úteis para XSL e otimizações de folha de estilos XSLT. Para aplicativos que requerem XSLT máximo desempenho, essa ferramenta pode ser essencial.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 O seguinte explicação passo a passo requer a versão 4,0 do Visual Studio 2010 and.NET Framework. O profiler XSLT só está disponível com a equipe do Microsoft Visual Studio o sistema com Ferramentas de design de Perfil instalado.  
  
### <a name="create-the-performance-report"></a>Crie o relatório de desempenho  
  
1.  Abrir um documento XSLT no Visual Studio.  
  
2.  Clique no **perfil XSLT** opção está disponível no menu XML.  
  
3.  Fornecer um documento XML de entrada. Se um documento XML ele já não estiver aberto, você será solicitado para o arquivo.  
  
4.  Inicia a análise, e uma barra de progresso exibem o progresso no editor.  
  
5.  A saída XSLT são visíveis no painel de saída.  
  
6.  Após extremidades de uma sessão de desempenho, verifique o relatório de desempenho. Os dados salvos em um relatório de desempenho permitem que você exiba e analisar o desempenho XSLT.  
  
### <a name="get-all-the-available-views"></a>Obter todos os modos disponíveis  
  
1.  Clique no **modo de exibição atual** lista suspensa para obter todos os modos de exibição disponíveis.  
  
2.  Selecione o **modo de exibição de resumo** opção a **modo de exibição atual** lista suspensa. Por padrão, um relatório de desempenho é exibido na **modo de exibição resumo**. Esta exibição é um ponto de partida para determinar problemas de desempenho com documentos XSLT. O **modo de exibição resumo** relaciona os pontos de dados a seguir:  
  
    -   A maioria chamaram funções  
  
    -   Funções com a maioria de trabalho individual  
  
    -   Funções que usam o tempo os mais longa de executar  
  
3.  Por padrão, há três colunas para cada ponto de dados: o nome da função, o número de chamadas o valor absoluto, e um valor percentual de função chamado para chamadas de função total. De cada data point-in a **modo de exibição de resumo**, você pode navegar para exibições mais detalhadas clicando nos pontos de dados de função.  
  
4.  Selecione o **exibição da função** opção a **modo de exibição atual** lista suspensa. O **exibição da função** lista funções chamadas durante a criação de perfil. Você pode classificar os dados em um nome de coluna. As colunas exibidas por padrão são:  
  
    -   **Nome da Função**  
  
    -   **Tempo Inclusivo Decorrido**  
  
    -   **Tempo Exclusivo Decorrido**  
  
    -   **Tempo Inclusivo do Aplicativo**  
  
    -   **Tempo Exclusivo do Aplicativo**  
  
    -   **Número de Chamadas**  
  
5.  Todas as colunas de tempo são exibidas em valores absolutos e em porcentagens. O termo **exclusivo** refere-se ao tempo total de uma função executar gasta não incluem o tempo gasto por outras funções chamado durante a execução dessa função.  
  
6.  O termo **inclusivo** refere-se ao tempo total gasto em execução, incluindo o tempo de execução de todas as funções que chamou e se qualquer uma das funções chamados chamaram outras funções.  
  
### <a name="select-callercallee-view"></a>O modo de seleção do chamador/receptor  
  
1.  Selecione **chamador/receptor** exibir na **modo de exibição atual** lista suspensa.  
  
2.  O **chamador/receptor** exibição tem três partes distintas:  
  
    -   **Funções que chamaram**: todas as funções que chamaram uma função particular são listadas na parte superior do modo de exibição.  
  
    -   **Função atual**: A função específica que foi chamada está listada na parte do meio da exibição.  
  
    -   **Funções que foram chamadas pela** : todas as funções que foram chamadas pela função particular são listadas na parte inferior do modo de exibição.  
  
3.  Se uma função chamada `SyncToNavigator` aparece na parte média de exibição, todas as funções que chamaram a função de `SyncToNavigator` aparecem na parte superior de exibição, e em todas as funções que foram chamados por `SyncToNavigator` aparecem na parte de fundo de exibição.  
  
4.  Você pode alterar a função na parte média de exibição clicando duas vezes em algumas das funções listadas em duas outras partes de exibição. A exibição é atualizado para refletir automaticamente as alterações.  
  
5.  Você também pode classificar os dados clicando em nomes de coluna.  
  
### <a name="select-calltree-view"></a>Selecione o modo de CallTree  
  
1.  Selecione **modo de exibição de árvore de chamadas** na **modo de exibição atual** lista suspensa. Esta exibição é um modo de exibição de árvore de execução do programa.  
  
2.  O **modo de exibição de árvore de chamadas** mostra a raiz da árvore como o nome do processo. As funções são os nós de árvore. Esta exibição permite que você fure em rastreamentos específicos de chamada e analise que os rastreamentos têm o maior impacto de desempenho. A exibição é semelhante a **modo de exibição de pilha de chamadas** disponível durante a depuração. Além das colunas na **exibição da função**, no **modo de exibição de árvore de chamadas**, há uma coluna adicional para exibir o **nome do módulo**.  
  
3.  Selecione **marcas** na **modo de exibição atual** lista suspensa.  
  
4.  Com o profiler de SLT, há marcas que aparece no fluxo da coleção de dados com um comentário associado. As marcas são locais no código que têm contadores. Quando você indica que o profiler XSLT para coletar contadores de desempenho XSLT, os contadores obtém como cada vez que uma dessas marcas é executado. Os dados são exibidos em uma tabela que contém o **ID de marca**, **nome da marca** (**Iniciar programa**, **finalizar programa**) e o  **Time Stamp**. As marcas não são agregadas e exibidos em ordem cronológica na **exibição de marcas** de relatório de desempenho.  
  
### <a name="select-modules-in-the-current-view"></a>Módulos selecionados na exibição atual  
  
1.  Selecione **módulos** na **modo de exibição atual** lista suspensa.  
  
2.  Exibição de módulos é uma lista plana das funções agregadas para o nível de módulo. Expandir ou recolher o nome do módulo para exibir ou fechar a exibição de dados de desempenho do módulo. Você pode classificar os dados em um nome de coluna. Por padrão, há valores absolutos e números de porcentagem para **tempo incluindo decorridos**, **tempo exclusivo decorrido**, **tempo inclusivo do aplicativo**, **Tempo exclusivo do aplicativo**, e **número de chamadas**.  
  
3.  Selecione **processo** na **modo de exibição atual** lista suspensa.  
  
4.  A exibição processo exibe uma tabela que inclui o **ID do processo**, **nome do processo**, **inicie tempo**e o **hora de término**. Os dados podem ser classificados clicando em nomes de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: usando a hierarquia XSLT](../xml-tools/walkthrough-using-xslt-hierarchy.md)



