---
title: Parâmetros opcionais em soluções do Office
description: Saiba como você não precisa passar um valor para parâmetros opcionais porque os valores padrão são usados automaticamente para cada parâmetro ausente.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9c95842ac2c6d77a2312ac5c4c197ba22ed2020e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825414"
---
# <a name="optional-parameters-in-office-solutions"></a>Parâmetros opcionais em soluções do Office
  Muitos dos métodos nos modelos de objeto de Microsoft Office aplicativos aceitam parâmetros opcionais. Se você usar Visual Basic para desenvolver uma solução do Office no Visual Studio, não será necessário passar um valor para os parâmetros opcionais, porque os valores padrão são usados automaticamente para cada parâmetro ausente. Na maioria dos casos, você também pode omitir parâmetros opcionais em projetos do Visual C#. No entanto, você não pode omitir os parâmetros **ref** opcionais da `ThisDocument` classe em projetos do Word de nível de documento.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Para obter mais informações sobre como trabalhar com parâmetros opcionais em projetos do Visual C# e Visual Basic, consulte [argumentos nomeados e opcionais &#40;guia de programação C&#35;&#41;](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) e [parâmetros opcionais &#40;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)Visual Basic de&#41;.

> [!NOTE]
> Em versões anteriores do Visual Studio, você deve passar um valor para cada parâmetro opcional em projetos do Visual C#. Para sua conveniência, esses projetos incluem uma variável global chamada `missing` que você pode passar para um parâmetro opcional quando desejar usar o valor padrão do parâmetro. Os projetos do Visual C# para Office no Visual Studio ainda incluem a `missing` variável, mas você normalmente não precisa usá-la ao desenvolver soluções do Office no [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] , exceto quando você chama métodos com parâmetros **ref** opcionais na `ThisDocument` classe em projetos de nível de documento para o Word.

## <a name="example-in-excel"></a>Exemplo no Excel
 O <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceitar o valor padrão de outros, conforme mostrado no exemplo de código a seguir. Este exemplo requer um projeto de nível de documento com uma classe de planilha chamada `Sheet1` .

 :::code language="csharp" source="../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb" id="Snippet1":::

## <a name="example-in-word"></a>Exemplo no Word
 O <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceitar o valor padrão de outros, conforme mostrado no exemplo de código a seguir.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet1":::

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Usar parâmetros opcionais de métodos na classe ThisDocument em projetos de nível de documento do Visual C# para Word
 O modelo de objeto do Word contém muitos métodos com parâmetros **ref** opcionais que aceitam <xref:System.Object> valores. No entanto, você não pode omitir parâmetros **ref** opcionais de métodos da `ThisDocument` classe gerada em projetos de nível de documento do Visual C# para Word. O Visual C# permite omitir parâmetros **ref** opcionais somente para métodos de interfaces, não para classes. Por exemplo, o exemplo de código a seguir não compila, porque você não pode omitir parâmetros **ref** opcionais do <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método da `ThisDocument` classe.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet3":::

 Ao chamar métodos da `ThisDocument` classe, siga estas diretrizes:

- Para aceitar o valor padrão de um parâmetro **ref** opcional, passe a `missing` variável para o parâmetro. A `missing` variável é definida automaticamente em projetos do Office em Visual C# e é atribuída ao valor <xref:System.Type.Missing> no código do projeto gerado.

- Para especificar seu próprio valor para um parâmetro **ref** opcional, declare um objeto que é atribuído ao valor que você deseja especificar e, em seguida, passe o objeto para o parâmetro.

  O exemplo de código a seguir demonstra como chamar o <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método especificando um valor para o parâmetro *IgnoreUppercase* e aceitando o valor padrão para os outros parâmetros.

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet4":::

  Se você quiser escrever um código que omita os parâmetros **ref** opcionais de um método na `ThisDocument` classe, você pode chamar o mesmo método no <xref:Microsoft.Office.Interop.Word.Document> objeto retornado pela <xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> propriedade e omitir os parâmetros desse método. Você pode fazer isso porque <xref:Microsoft.Office.Interop.Word.Document> é uma interface, em vez de uma classe.

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet5":::

  Para obter mais informações sobre parâmetros de tipo de referência e valor, consulte [passar argumentos por valor e por referência &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (para Visual Basic) e [passar parâmetros &#40;guia de programação C&#35;&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters).

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
