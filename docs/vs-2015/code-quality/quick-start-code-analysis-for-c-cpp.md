---
title: 'Início rápido: Análise de código para C / C++ | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- C/C++ code analysis
- code analysis,C/C++
ms.assetid: 6110b8ba-0af6-4acd-b1ba-bb0551f90e44
caps.latest.revision: 10
author: mikeblome
ms.author: mblome
manager: ghogen
ms.openlocfilehash: 56f14abab372a6a6e533675b070d420a4dfc7a5e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758189"
---
# <a name="quick-start-code-analysis-for-cc"></a>Início Rápido: análise de código para C/C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode melhorar a qualidade do seu aplicativo, executando a análise de código regularmente em código C ou C++. Isso pode ajudá-lo a localizar problemas mais comuns, violações de boa prática de programação ou defeitos que são difíceis de descobrir por meio de testes. Os avisos da análise de código diferem dos erros e avisos do compilador porque a análise de código procura por padrões de código específicos que são válidos, mas que ainda podem criar problemas para você ou outras pessoas que usam seu código.  
  
## <a name="in-this-topic"></a>Neste tópico  
  
-   [Configurar conjuntos de regras para um projeto](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_ConfigureRuleSets)  
  
-   [Executar análise de código](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Run)  
  
-   [Analisar e resolver avisos da análise de código](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Analyze)  
  
-   [Suprimindo avisos da análise de código](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Suppress)  
  
-   [Criando itens de trabalho para o código avisos de análise](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Creating_work_items_for_code_analysis_warnings)  
  
-   [Pesquisando e filtrando resultados de análise de código](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Search)  
  
##  <a name="BKMK_ConfigureRuleSets"></a> Configurar conjuntos de regras para um projeto  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o nome do projeto e, em seguida, escolha **propriedades**.  
  
2.  As etapas a seguir são opcionais:  
  
    1.  No **Configuration** e **plataforma** listas, escolha a plataforma de destino e a configuração de compilação.  
  
    2.  Por padrão, a análise de código não relate os avisos de código que é gerado automaticamente por ferramentas externas. Para exibir avisos do código gerado, desmarque a **Suprimir resultados do código gerado** caixa de seleção.  
  
        > [!NOTE]
        >  Essa opção não suprime erros de análise de código e avisos do código gerado quando os erros e avisos que aparecem em formulários e modelos. Você pode exibir e manter o código-fonte para um formulário ou um modelo.  
  
3.  Para executar análise de código sempre que o projeto é compilado usando a configuração selecionada, selecione a **habilitar a análise de código para C/C++ no Build** caixa de seleção. Você também pode executar a análise de código manualmente abrindo o **Analyze** menu e, em seguida, escolhendo **executar análise de código na** *ProjectName*.  
  
4.  No **executar este conjunto de regras** lista, siga um destes procedimentos:  
  
    -   Escolha o conjunto de regras que você deseja usar.  
  
    -   Escolher  **\<procurar... >** especificar uma regra personalizada existente definida que não está na lista.  
  
    -   Defina um conjunto de regras personalizadas.  
  
         Para obter mais informações, consulte [criação de conjuntos de regras personalizado](../code-quality/creating-custom-code-analysis-rule-sets.md).  
  
### <a name="standard-cc-rule-sets"></a>Conjuntos de regras do C/C++ padrão  
 O Visual Studio inclui dois conjuntos de regras para código nativo padrão:  
  
|Conjunto de regras|Descrição|  
|--------------|-----------------|  
|Regras recomendadas mínimas do Microsoft Native|Esse conjunto de regras enfoca os problemas mais críticos do código nativo, inclusive falhas potenciais de segurança e falhas do aplicativo. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos nativos.|  
|Regras recomendadas nativo do Microsoft|Esse conjunto de regras abrange uma ampla gama de problemas. Ele inclui todas as regras em Microsoft Native mínimo recomendado regras.|  
  
##  <a name="BKMK_Run"></a> Executar análise de código  
 Na página de análise de código das páginas de propriedades do projeto, você pode configurar a análise de código para executar cada vez que você compila seu projeto. Você também pode executar a análise de código manualmente.  
  
 Para executar análise de código em uma solução:  
  
- No menu **Compilar**, escolha **Executar Análise de Código na Solução**.  
  
  Para executar análise de código em um projeto:  
  
- No Gerenciador de soluções, escolha o nome do projeto.  
  
- Sobre o **compilar** menu, escolha **executar análise de código na** *nome do projeto*.  
  
  A solução ou projeto é compilada e análise de código é executado. Os resultados aparecem na janela Análise de Código.  
  
##  <a name="BKMK_Analyze"></a> Analisar e resolver avisos da análise de código  
 Para analisar um aviso específico, escolha o título do aviso na janela Análise de Código. O aviso se expande para exibir informações adicionais sobre o problema. Quando possível, a análise de código exibe os números de linha e a lógica de análise que levou ao aviso. Para obter informações detalhadas sobre o aviso, incluindo soluções possíveis para o problema, escolha a id do aviso para exibir o tópico da Ajuda na biblioteca MSND para a mensagem.  
  
 Quando você expande um aviso, a linha de código que o causou é realçada no editor de códigos do Visual Studio.  
  
 Depois de entender o problema, você pode resolvê-lo no seu código. Em seguida, torne a executar a análise de código para verificar se o aviso não aparece mais na janela Análise de Código e se a sua correção não gerou novos avisos.  
  
> [!TIP]
>  Você pode executar a análise de código novamente na janela Análise de Código. Escolha o **analisar** botão e escolha o escopo da análise. A análise pode ser executada na solução inteira ou em um projeto selecionado.  
  
##  <a name="BKMK_Suppress"></a> Suprimindo avisos da análise de código  
 Há ocasiões em que você pode decidir não corrigir um aviso de análise de código. Você pode decidir que resolver o aviso exige recodificação demais considerando a probabilidade de que o problema ocorrerá em qualquer implementação do seu código no mundo real. Ou você pode achar que a análise usada no aviso é inadequada nesse contexto específico. É possível suprimir avisos individuais para que não apareçam mais na janela Análise de Código.  
  
 Para suprimir um aviso:  
  
1. Se as informações detalhadas não for exibidas, escolha o título do aviso para expandi-lo.  
  
2. Escolha o link **Ações** na parte inferior do aviso.  
  
3. Escolher **suprimir mensagem** e, em seguida, escolha **na origem**.  
  
   Suprimir uma mensagem insere `#pragma warning (disable:`*WarningId*`)`, que suprime o aviso para a linha de código.  
  
##  <a name="BKMK_Creating_work_items_for_code_analysis_warnings"></a> Criando itens de trabalho para o código avisos de análise  
 Você pode usar o recurso de rastreamento de item de trabalho para registrar bugs de dentro do Visual Studio. Para usar esse recurso, você deve se conectar a uma instância do Team Foundation Server.  
  
 **Para criar um item de trabalho para um ou mais avisos de código C/C++**  
  
1.  Na janela análise de código, expanda e selecione os avisos  
  
2.  No menu de atalho para os avisos, escolha **Criar Item de trabalho**e, em seguida, escolha o tipo de item de trabalho.  
  
3.  Visual Studio cria um único item de trabalho para os avisos selecionados e exibe o item de trabalho em uma janela de documento do IDE.  
  
4.  Adicione informações adicionais e, em seguida, escolha **Salvar Item de trabalho**.  
  
##  <a name="BKMK_Search"></a> Pesquisando e filtrando resultados de análise de código  
 Você pode pesquisar listas longas de mensagens de aviso e pode filtrar avisos em soluções multiprojeto.  
  
1.  **Para filtrar avisos por título ou identificação de aviso**: insira a palavra-chave em de **filtro** caixa de texto.  
  
2.  **Para filtrar avisos por projeto**: em uma solução multiprojeto, escolha um ou mais projetos na lista na parte superior direita da janela análise de código. Escolha o nome da solução para exibir todos os avisos.  
  
3.  **Para filtrar avisos por gravidade**: por padrão, mensagens de análise de código são atribuídas a severidade **aviso**. Você pode atribuir a gravidade de uma ou mais mensagens, como **erro** em uma regra personalizada definida. Escolha **aviso** ou **erro** para exibir apenas as mensagens que são atribuídas a severidade do respectiva. Escolher **todos os** para exibir todas as mensagens.



