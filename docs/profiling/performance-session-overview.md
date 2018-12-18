---
title: Visão Geral da Sessão de Desempenho | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, performance session
- performance sessions
ms.assetid: 35752f95-a57a-4def-b64d-cf4899669e99
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a385b425ee8dead7df0faad302e6cf270b739034
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49828527"
---
# <a name="performance-session-overview"></a>Visão geral da sessão de desempenho
Esta visão geral explica as noções básicas de criação de perfil. Desenvolvedores pouco familiarizados com o trabalho de desempenho verão como as Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] podem ajudá-los a se tornarem rapidamente produtivos e a aumentar o desempenho do seu código. Desenvolvedores experientes na criação de perfis podem obter uma visão geral dos processos e recursos específicos das Ferramentas de Criação de Perfil.  
  
 As Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ajudam a identificar problemas de desempenho no código-fonte e a comparar o desempenho das soluções possíveis. Os assistentes e as e configurações padrão das Ferramentas de Criação de Perfil podem fornecer insight imediato sobre muitos problemas de desempenho. Os recursos e as opções das Ferramentas de Criação de Perfil fornecem controle preciso sobre o processo de criação de perfil. Esse controle inclui o direcionamento preciso de seções de código, a coleção de informações de tempo de nível de bloco e a inclusão de dados adicionais de desempenho do processador e do sistema em seus dados.  
  
 As etapas a seguir constituem o processo básico de como usar as Ferramentas de Criação de Perfil:  
  
1. Configure a sessão de desempenho, especificando o método de coleta e os dados que você deseja coletar.  
  
2. Colete os dados de criação de perfil executando o aplicativo na sessão de desempenho.  
  
3. Analisar os dados e identificar problemas de desempenho.  
  
4. Modifique o código no IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para aumentar o desempenho do código do aplicativo  
  
5. Colete dados de criação de perfil no código alterado e compare os dados de criação de perfil dos dados originais e alterados.  
  
6. Gere um relatório que documenta o aumento no desempenho.  
  
   Para trabalhar com as informações fornecidas pela criação de perfil, você deve ter informações de símbolo disponíveis para os binários que você deseja analisar e para os binários do sistema operacional Windows.  
  
## <a name="configure-the-performance-session"></a>Configurar a sessão de desempenho  
 Para configurar uma sessão de criação de perfil, selecione o método de criação de perfil que você deseja usar e os dados que você deseja coletar. O **Assistente de Desempenho** das Ferramentas de Criação de Perfil podem orientá-lo pela configuração básica e você pode usar as páginas de propriedade da Sessão de Desempenho para adicionar mais opções:  
  
- Os métodos de criação de perfil incluem amostragem, rastreamento e alocação de memória.  
  
- Os valores de dados incluem tempo, processador e contadores de desempenho do sistema operacional e eventos de aplicativo, tais como falhas de página e transições de kernel.  
  
  Você pode configurar uma sessão de desempenho em um projeto [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] como parte da solução do projeto ou binários arbitrários de perfil por meio do IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Você pode especificar as propriedades de sessão nas páginas de propriedade da Sessão de Desempenho ou pode usar o Assistente de Criação de Perfil.  
  
## <a name="collect-profiling-data"></a>Coletar dados de criação de perfil  
 Inicie a coleta dos dados de criação de perfil no **Gerenciador de Desempenho**. Você pode pausar e retomar a criação de perfil para limitar a quantidade de dados coletados. Você também pode anexar a um processo que já está em execução.  
  
 Assim que o aplicativo for iniciado, a janela **Controle de Coleta de Dados** aparece no IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Da janela **Controle de Coleta de Dados**, você pode analisar partes específicas do seu aplicativo pausando e retomando o processo de coleta. Você também pode usar a janela do **Controle de Coleta de Dados** para inserir marcas nos dados coletados. Marcas são pontos de dados definido pelo usuário que são mostradas nas exibições de perfil e que podem ser usadas para filtrar os dados de criação de perfil.  
  
 Quando o aplicativo de destino é desligado, as Ferramentas de Criação de Perfil geram um arquivo de dados de criação de perfil (*.vsp) e exibem a exibição do Relatório de Resumo no IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
## <a name="analyze-the-data-and-identify-performance-issues"></a>Analisar os dados e identificar problemas de desempenho  
 Quando você encerra uma execução de criação de perfil, os dados são analisados e um resumo é exibido nas janelas de exibição **Relatório de Desempenho** das Ferramentas de Criação de Perfil. Os dados de criação de perfil são coletados para a pilha de chamadas e as funções individuais do aplicativo de destino. Exibições de relatório mostram análise de desempenho para intervalos de dados dos processos, threads, módulos, funções e linhas de código-fonte do aplicativo. Valores de dados de criação de perfil para uma função incluem o seguinte:  
  
- O tempo total gasto na função e em funções filho que foram chamadas pela função (valores inclusivos).  
  
- O tempo gasto para executar apenas o código na função (valores exclusivos).  
  
  As mais de doze exibições diferentes permitem analisar os dados de criação de perfil da maneira mais eficiente. As personalizações de exibição permitem filtrar e classificar os dados para localizar as funções que podem estar causando problemas de desempenho. A filtragem de afunilamento fornece realce imediato dos caminhos mais ativos nas exibições de Árvore de Chamadas e Módulo.  
  
## <a name="modify-the-application-code"></a>Modificar o código do aplicativo  
 Após isolar um ou mais problemas de desempenho relevantes, você pode modificar o código usando o IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e, em seguida, coletar dados de criação de perfil para suas alterações.  
  
## <a name="collect-profiling-data-again-and-compare-the-data-between-the-profiling-runs"></a>Coletar dados de criação de perfil novamente e comparar os dados entre as execuções de criação de perfil  
 A Exibição de Relatório de Comparação de Ferramentas de Criação de Perfil exibem a diferença no desempenho do módulo, função ou linha entre os dois arquivos de dados de criação de perfil selecionados. Você pode especificar os valores de dados de criação de perfil que deseja comparar e mudar entre a exibição de Comparação e as exibições dos arquivos individuais.  
  
## <a name="generate-a-report-of-the-results"></a>Gerar um relatório dos resultados  
 Você pode colar linhas de qualquer exibição de relatório de desempenho em emails e planilhas, bem como pode gerar relatórios que contêm os dados para uma ou mais exibições.  
  
## <a name="see-also"></a>Consulte também  
 [Visões gerais](../profiling/overviews-performance-tools.md)   
 [Passo a passo: identificar problemas de desempenho](../profiling/walkthrough-identifying-performance-problems.md)