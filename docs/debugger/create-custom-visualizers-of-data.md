---
title: Criar visualizadores de dados personalizados | Microsoft Docs
ms.date: 05/27/2020
ms.topic: conceptual
f1_keywords:
- vs.debug.visualizer.troubleshoot
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers
ms.assetid: c24c006f-f2ac-429f-89db-677fc0c6e1ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e184507415810f64060b0d2b2e92a825d642d2e
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280870"
---
# <a name="create-custom-data-visualizers"></a>Criar visualizadores de dados personalizados

 Um *Visualizador* faz parte da [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] interface do usuário do depurador que exibe uma variável ou objeto de uma maneira apropriada ao seu tipo de dados. Por exemplo, um visualizador de HTML interpreta uma cadeia de caracteres HTML e exibe o resultado como seria exibido em uma janela do navegador. Um visualizador de bitmap interpreta uma estrutura de bitmap e exibe o gráfico que ela representa. Alguns visualizadores permitem que você modifique e exiba os dados.

 O depurador do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] inclui seis visualizadores padrão. Os visualizadores de texto, HTML, XML e JSON funcionam em objetos de cadeia de caracteres. O Visualizador de árvore do WPF exibe as propriedades de uma árvore visual do objeto WPF. O Visualizador do conjunto de um funciona para objetos DataSet, DataView e DataTable.

Mais visualizadores podem estar disponíveis para download da Microsoft, de terceiros e da Comunidade. Você também pode escrever seus próprios visualizadores e instalá-los no [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] depurador.

No depurador, um visualizador é representado por um ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "Ícone do Visualizador"). Você pode selecionar o ícone em um **DataTip**, uma janela de **inspeção** do depurador ou uma caixa de diálogo **QuickWatch** e, em seguida, selecionar o visualizador apropriado para o objeto correspondente.

## <a name="write-custom-visualizers"></a>Escrever visualizadores personalizados

 > [!NOTE]
 > Para criar um visualizador personalizado para código nativo, consulte o exemplo do [Visualizador do depurador nativo do SQLite](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/SqliteVisualizer) . Os visualizadores personalizados não têm suporte para aplicativos UWP e Windows 8. x.

Você pode escrever um visualizador personalizado para um objeto de qualquer classe gerenciada com exceção de <xref:System.Object> ou <xref:System.Array>.

A arquitetura de um visualizador de depurador tem duas partes:

- O *lado do depurador* é executado no depurador do Visual Studio e cria e exibe a interface do usuário do visualizador.

- O *lado a ser depurado* é executado dentro do processo que o Visual Studio está depurando (o *lado a ser depurado*). O objeto de dados a ser visualizado (por exemplo, um objeto de cadeia de caracteres) existe no processo de depuração. O lado que está sendo depurado envia o objeto para o lado do depurador, que o exibe na interface do usuário que você criar.

O lado do depurador recebe o objeto de dados de um *provedor de objetos* que implementa a <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> interface. O lado que está sendo depurado envia o objeto por meio da *origem do objeto*, que é derivado de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> .

O provedor de objetos também pode enviar dados de volta para a origem do objeto, o que permite que você escreva um visualizador que possa editar dados. Você substitui o provedor de objetos para se comunicar com o avaliador de expressão e a origem do objeto.

O lado depurador e o lado do depurador se comunicam entre si por meio de <xref:System.IO.Stream> métodos que serializam um objeto de dados em um <xref:System.IO.Stream> e desserializam de <xref:System.IO.Stream> volta para um objeto de dados.

Você poderá gravar um visualizador para um tipo genérico somente se o tipo for um tipo aberto. Essa restrição é a mesma que a restrição ao usar o atributo `DebuggerTypeProxy`. Para obter detalhes, consulte [usar o atributo DebuggerTypeProxy](../debugger/using-debuggertypeproxy-attribute.md).

Os visualizadores personalizados podem ter considerações de segurança. Consulte [considerações de segurança do visualizador](../debugger/visualizer-security-considerations.md).

As etapas a seguir fornecem uma visão geral de alto nível da criação do visualizador. Para obter instruções detalhadas, consulte [instruções passo a passo: escrever um visualizador em C# ](../debugger/walkthrough-writing-a-visualizer-in-csharp.md) ou [passo a passo: escrever um visualizador em Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md).

### <a name="to-create-the-debugger-side"></a>Para criar o lado do depurador

Para criar a interface do usuário do visualizador no lado do depurador, você cria uma classe que herda de <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> e substitui o <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> método para exibir a interface. Você pode usar <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> para exibir Windows Forms, caixas de diálogo e controles em seu visualizador.

1. Use os métodos <xref:Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider> para obter o objeto visualizado no lado do depurador.

1. Crie uma classe que herda de <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer>.

1. Substitua o método <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer.Show%2A?displayProperty=fullName> para exibir sua interface. Use <xref:Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService> métodos para exibir Windows Forms, caixas de diálogo e controles em sua interface.

4. Aplicar <xref:System.Diagnostics.DebuggerVisualizerAttribute> , dando a ele o visualizador para exibir ( <xref:Microsoft.VisualStudio.DebuggerVisualizers.DialogDebuggerVisualizer> ).

### <a name="to-create-the-visualizer-object-source-for-the-debuggee-side"></a>Para criar a origem do objeto visualisador para o lado que está sendo depurado

No código do lado do depurador, edite o <xref:System.Diagnostics.DebuggerVisualizerAttribute> , dando a ele o tipo a ser visualizado (a origem do objeto do lado do depurador) ( <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> ). A `Target` propriedade define a origem do objeto. Se você omitir a origem do objeto, o visualizador usará uma fonte de objeto padrão.

::: moniker range=">=vs-2019"
O código do lado de depuração contém a origem do objeto que é visualizado. O objeto de dados pode substituir métodos de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> . Uma DLL do lado de depuração será necessária se você quiser criar um visualizador autônomo.
::: moniker-end

No código do lado do depurador:

- Para permitir que o visualizador edite objetos de dados, a origem do objeto deve herdar de <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> e substituir os `TransferData` `CreateReplacementObject` métodos ou.

- Se você precisar dar suporte a vários destinos em seu visualizador, poderá usar os seguintes monikers da estrutura de destino (TFMs) no arquivo de projeto do lado do depurador.

   ```xml
   <TargetFrameworks>net20;netstandard2.0;netcoreapp2.0</TargetFrameworks>
   ```

   Esses são os únicos TFMs com suporte.

## <a name="see-also"></a>Veja também

- [Passo a passo: Escrever um visualizador em C#](../debugger/walkthrough-writing-a-visualizer-in-csharp.md)
- [Passo a passo: Escrever um visualizador em Visual Basic](../debugger/walkthrough-writing-a-visualizer-in-visual-basic.md)
- [Como instalar um visualizador](../debugger/how-to-install-a-visualizer.md)
- [Como testar e depurar um visualizador](../debugger/how-to-test-and-debug-a-visualizer.md)
- [Referência da API do Visualizador](../debugger/visualizer-api-reference.md)
- [Exibir dados no depurador](../debugger/viewing-data-in-the-debugger.md)