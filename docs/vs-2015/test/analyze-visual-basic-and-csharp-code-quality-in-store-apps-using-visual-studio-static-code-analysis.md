---
title: Analisar o Visual Basic e C# código de qualidade em aplicativos da Store usando a análise de código estático
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb.express
ms.assetid: cab553fc-19a9-4cbf-858e-8200258ffe50
caps.latest.revision: 16
author: erickson-doug
ms.author: gewarren
manager: douge
ms.openlocfilehash: a3a3d753f9e2dd3b046159d191149b7af062fe16
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53063200"
---
# <a name="analyze-visual-basic-and-c-code-quality-in-store-apps-using-visual-studio-static-code-analysis"></a>Analisar a qualidade do código do Visual Basic e C# em aplicativos da Store usando a análise de código estático do Visual Studio

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")

 A ferramenta de análise de código Visual Studio Express examina seu código em busca de um conjunto de defeitos e violações comuns das práticas recomendadas de programação. Os avisos da análise de código diferem dos erros e avisos do compilador porque a ferramenta de análise de código procura por padrões de código específicos que são válidos, mas ainda podem criar problemas para você ou outras pessoas que usem o seu código. A análise de código também pode localizar os defeitos no seu código que são difíceis de descobrir com testes. A execução da ferramenta de análise de código a intervalos regulares durante o processo de desenvolvimento pode melhorar a qualidade do seu aplicativo concluído.

> [!NOTE]
>  No Visual Studio Ultimate, Visual Studio Premium e Visual Studio Professional, você pode usar a funcionalidade completa da análise de código. Consulte [Analisando a qualidade do aplicativo usando as ferramentas de análise de código](http://msdn.microsoft.com/library/dd264897.aspx) na Biblioteca MSDN.

## <a name="in-this-topic"></a>Neste tópico
 Estes são os assuntos tratados:

 [Executando a análise de código](../test/analyze-visual-basic-and-csharp-code-quality-in-store-apps-using-visual-studio-static-code-analysis.md#BKMK_Run)

 [Analisando e resolvendo avisos da análise de código](../test/analyze-visual-basic-and-csharp-code-quality-in-store-apps-using-visual-studio-static-code-analysis.md#BKMK_Analyze)

 [Suprimindo avisos da análise de código](../test/analyze-visual-basic-and-csharp-code-quality-in-store-apps-using-visual-studio-static-code-analysis.md#BKMK_Suppress)

 [Pesquisando e filtrando resultados de análise de código](../test/analyze-visual-basic-and-csharp-code-quality-in-store-apps-using-visual-studio-static-code-analysis.md#BKMK_Search)

 [Avisos de análise de código em Visual Basic e C#](../test/analyze-visual-basic-and-csharp-code-quality-in-store-apps-using-visual-studio-static-code-analysis.md#BKMK_Warnings)

##  <a name="BKMK_Run"></a> Executando análise de código
 Para executar a análise de código em sua solução do Visual Studio:

- No menu **Compilar**, escolha **Executar Análise de Código na Solução**.

  Para executar a análise de código automaticamente cada vez que você compilar um projeto:

1. Clique com o botão direito do mouse no nome do projeto no Gerenciador de Soluções e escolha **Propriedades**.

2. Na página de propriedades do projeto, escolha **Análise de Código** e depois **Habilitar Análise de Código no Build (define a constante CODEANALYSIS)**.

   A solução é compilada e a análise de código é executada. Os resultados aparecem na janela Análise de Código.

   ![Janela Análise de Código](../test/media/ca-managed-collapsed.png "CA_Managed_Collapsed")

##  <a name="BKMK_Analyze"></a> Analisando e resolvendo avisos da análise de código
 Para analisar um aviso específico, clique no respectivo título na janela Análise de Código. O aviso se expande para exibir informações detalhadas sobre o problema.

 ![Aviso de análise de código expandido](../test/media/ca-managed-callouts.png "CA_Managed_Callouts")

 Quando você expande um aviso, a linha de código que o causou é realçada no editor de códigos do Visual Studio.

 ![Realce de texto da análise de código](../test/media/ca-managed-sourceline.png "CA_Managed_SourceLine")

 Depois de entender o problema, você pode resolvê-lo no seu código. Em seguida, torne a executar a análise de código para verificar se o aviso não aparece mais na janela Análise de Código e se a sua correção não gerou novos avisos.

> [!TIP]
>  Você pode executar a análise de código novamente na janela Análise de Código. Clique no botão **Analisar** e escolha o escopo da análise. A análise pode ser executada na solução inteira ou em um projeto selecionado.

##  <a name="BKMK_Suppress"></a> Suprimindo avisos da análise de código
 Há ocasiões em que você pode decidir não corrigir um aviso de análise de código. Você pode decidir que resolver o aviso exige recodificação demais considerando a probabilidade de que o problema ocorrerá em qualquer implementação do seu código no mundo real. Ou você pode achar que a análise usada no aviso é inadequada nesse contexto específico. É possível suprimir avisos individuais para que não apareçam mais na janela Análise de Código.

 Para suprimir um aviso:

1. Se as informações detalhadas não estiverem exibidas, clique no título do aviso para expandi-lo.

2. Escolha o link **Ações** na parte inferior do aviso.

3. Aponte para **Suprimir Mensagem** e escolha **Na Origem** ou **No Arquivo de Supressão**.

   - **Na Origem** insere um atributo `SuppressMessage` no arquivo de origem acima do método que gerou o aviso. Isso facilita a descoberta da supressão.

   - **No Arquivo de Supressão** adiciona um atributo `SuppressMessage` ao arquivo **GlobalSuppressions.cs** do projeto. Isso pode simplificar o gerenciamento das supressões. Observe que o atributo `SuppressMessage` adicionado a **GlobalSuppression.cs** também afeta o método que gerou o aviso. Ele não suprime o aviso globalmente.

     Sua decisão sobre suprimir o aviso no arquivo de origem ou no arquivo de supressão depende do seu estilo de codificação e das suas necessidades.

##  <a name="BKMK_Search"></a> Pesquisando e filtrando resultados de análise de código
 Você pode pesquisar listas longas de mensagens de aviso e pode filtrar avisos em soluções multiprojeto.

 ![Pesquisar e filtrar a janela de análise de código](../test/media/ca-searchfilter.png "CA_SearchFilter")

 No [!INCLUDE[vs_dev11_expwin_long](../includes/vs-dev11-expwin-long-md.md)], todos os avisos de análise de código têm o nível de severidade Aviso.

##  <a name="BKMK_Warnings"></a> Avisos de análise de código em Visual Basic e C#
 A análise de código gera os seguintes avisos:

 [CA1001: os tipos com campos descartáveis devem ser descartáveis](http://msdn.microsoft.com/library/ms182172.aspx)

 [CA1821: remova os finalizadores vazios](http://msdn.microsoft.com/library/bb264476.aspx)

 [CA2213: os campos descartáveis devem ser descartados](http://msdn.microsoft.com/library/ms182328.aspx)

 [CA2229: implementar construtores de serialização](http://msdn.microsoft.com/library/ms182343.aspx)

 [CA2231: o operador de sobrecarga é igual ao substituir ValueType.Equals](http://msdn.microsoft.com/library/ms182359.aspx)
