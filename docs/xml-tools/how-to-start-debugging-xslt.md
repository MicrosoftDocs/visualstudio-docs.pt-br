---
title: 'Como: Iniciar a depuração XSLT'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: e499aea3793e5c496930fe255133d51361e6f394
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39178342"
---
# <a name="how-to-start-debugging-xslt"></a>Como: iniciar a depuração XSLT

O depurador XSLT pode ser usado para depurar uma folha de estilos XSLT ou um aplicativo XSLT. Para depurar, você pode executar a linha de código por vez em pisando, pisando sobre, ou pisando fora do código. Os comandos usar a funcionalidade do avançar são os mesmos para o depurador XSLT para que os outros depuradores do Visual Studio. Uma vez que você iniciar a depuração, o depurador XSLT abrir janelas para mostrar o documento de entrada e saída XSLT.

## <a name="xml-editor"></a>Editor de XML

Você pode iniciar o depurador do editor XML. Isso permite que você depure como você está criando a folha de estilos.

### <a name="to-start-debugging-from-a-style-sheet"></a>Para iniciar depuração de uma folha de estilos

1. Abra a folha de estilos no editor XML.

1. Selecione **depurar XSL** da **XML** menu.

### <a name="to-start-debugging-from-an-xml-input-document"></a>Para iniciar depuração de um documento de entrada XML

1. Abra o documento XML no editor XML.

1. Selecione **depurar XSL** da **XML** menu.

## <a name="xslt-from-other-languages"></a>XSLT de outras linguagens

Você também pode entrar em XSLT ao depurar um aplicativo. Quando você pressiona a tecla F11 em uma chamada de <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A?displayProperty=fullName> , o depurador pode entrar no código XSLT.

> [!NOTE]
> Entrar em XSLT da classe de <xref:System.Xml.Xsl.XslTransform> não é suportado. A classe de <xref:System.Xml.Xsl.XslCompiledTransform> é o único processador XSLT que suporte em avançar XSLT a depuração.

### <a name="to-start-debugging-an-xslt-application"></a>Para iniciar a depuração de um aplicativo XSLT

1. Ao criar uma instância do objeto de <xref:System.Xml.Xsl.XslCompiledTransform> , defina o parâmetro de `enableDebug` a `true` em seu código.

     Isso informa o processador XSLT para criar informações de depuração quando o código é compilado.

1. Pressione F11 para entrar no código XSLT.

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
    private const string stylesheet = @"c:\data\xsl_files\belowAvg.xsl";
    private const string outputFile = @"c:\data\xsl_files\output.xml";

    static void Main(string[] args)
    {
      // Enable XSLT debugging.
      XslCompiledTransform xslt = new XslCompiledTransform(true);

      // Compile the style sheet.
      xslt.Load(stylesheet)

      // Execute the XSLT transform.
      FileStream outputStream = new FileStream(outputFile, FileMode.Append);
      xslt.Transform(sourceFile, null, outputStream);
    }
  }
}
```

## <a name="see-also"></a>Consulte também

- [Passo a passo: Depurar uma folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
- [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)