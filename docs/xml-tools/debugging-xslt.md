---
title: Maneiras de depurar código XSLT
ms.date: 03/05/2019
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: d8e3885aa895cec5ed080b7a8b4d22522d2e9edf
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815611"
---
# <a name="debugging-xslt"></a>Depuração do XSLT

Você pode depurar o código XSLT no Visual Studio. O depurador XSLT dá suporte à definição de pontos de interrupção, à exibição de Estados de execução XSLT e assim por diante. O depurador XSLT pode ser usado para depurar folhas de estilo XSLT ou aplicativos XSLT.

Você pode executar o código uma linha de cada vez, passando para, percorrendo ou saindo do código. Os comandos para usar a funcionalidade de depuração de código do depurador XSLT são os mesmos dos outros depuradores do Visual Studio.

Uma vez que você iniciar a depuração, o depurador XSLT abrir janelas para mostrar o documento de entrada e saída XSLT.

> [!NOTE]
> O depurador XSLT só está disponível nas edições Professional e Enterprise do Visual Studio.

## <a name="debug-from-the-xml-editor"></a>Depurar do editor de XML

Você pode iniciar o depurador quando tiver uma folha de estilos ou um arquivo XML de entrada aberto no editor. Isso permite que você depure enquanto cria a folha de estilos.

1. Abra a folha de estilos ou o arquivo XML no Visual Studio.

1. Selecione **Iniciar Depuração XSLT** no menu **XML** ou pressione **ALT** + **F5**.

## <a name="debug-from-an-app-that-uses-xslt"></a>Depurar de um aplicativo que usa XSLT

Você pode entrar no XSLT durante a depuração de um aplicativo. Quando você pressiona **F11** em uma <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> chamada, o depurador pode entrar no código XSLT.

> [!NOTE]
> Entrar em XSLT da classe de <xref:System.Xml.Xsl.XslTransform> não é suportado. A classe de <xref:System.Xml.Xsl.XslCompiledTransform> é o único processador XSLT que suporte em avançar XSLT a depuração.

### <a name="to-start-debugging-an-xslt-application"></a>Para iniciar a depuração de um aplicativo XSLT

1. Ao criar uma instância do objeto de <xref:System.Xml.Xsl.XslCompiledTransform> , defina o parâmetro de `enableDebug` a `true` em seu código. Isso informa o processador XSLT para criar informações de depuração quando o código é compilado.

1. Pressione **F11** para entrar no código XSLT.

   A folha de estilos XSLT é carregada em uma nova janela de documento e o depurador XSLT é iniciado.

   Como alternativa, você pode adicionar um ponto de quebra a folha de estilos e executar o aplicativo.

### <a name="example"></a>Exemplo

O código a seguir é um exemplo de um programa C# XSLT. Mostra como ativar depuração XSLT.

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Xsl;

namespace ConsoleApplication
{
  class Program
  {
    private const string sourceFile = @"c:\data\xsl_files\books.xml";
    private const string stylesheet = @"c:\data\xsl_files\below-average.xsl";
    private const string outputFile = @"c:\data\xsl_files\output.xml";

    static void Main(string[] args)
    {
      // Enable XSLT debugging.
      XslCompiledTransform xslt = new XslCompiledTransform(true);

      // Compile the style sheet.
      xslt.Load(stylesheet);

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="xslt-profiler"></a>Criador de perfil XSLT

O [XSLT Profiler](../xml-tools/xslt-profiler.md) é uma ferramenta que permite aos desenvolvedores medir, avaliar e direcionar problemas relacionados ao desempenho no código XSLT criando relatórios de desempenho XSLT detalhados. Para obter mais informações, consulte [XSLT Profiler](../xml-tools/xslt-profiler.md).

## <a name="see-also"></a>Veja também

- [Walkthrough: Depurar uma folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [Primeiro, veja o depurador do Visual Studio](../debugger/debugger-feature-tour.md)
- [Noções básicas de depuração: pontos de interrupção](../debugger/using-breakpoints.md)
