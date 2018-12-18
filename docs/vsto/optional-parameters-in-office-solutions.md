---
title: Parâmetros opcionais em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d4a9737ae9e256cdc9862c0d7725e9bffda5b633
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882568"
---
# <a name="optional-parameters-in-office-solutions"></a>Parâmetros opcionais em soluções do Office
  Muitos dos métodos nos modelos de objeto dos aplicativos do Microsoft Office aceitam parâmetros opcionais. Se você usar o Visual Basic para desenvolver uma solução do Office no Visual Studio, você não precisa passar um valor para parâmetros opcionais, porque os valores padrão são usados automaticamente para cada parâmetro ausente. Na maioria dos casos, você também pode omitir parâmetros opcionais em projetos do Visual c#. No entanto, não é possível omitir opcional **ref** parâmetros da `ThisDocument` classe em projetos de nível de documento do Word.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Para obter mais informações sobre como trabalhar com parâmetros opcionais em projetos do Visual c# e Visual Basic, consulte [argumentos nomeados e opcionais &#40;C&#35; guia de programação do&#41; ](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments) e [ &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters).  
  
> [!NOTE]  
>  Em versões anteriores do Visual Studio, você deve passar um valor para cada parâmetro opcional em projetos do Visual c#. Para sua conveniência, esses projetos incluem uma variável global chamada `missing` que você pode passar para um parâmetro opcional quando você deseja usar o valor padrão do parâmetro. Projetos Visual c# para o Office no Visual Studio ainda incluem o `missing` variável, mas você normalmente não é necessário usá-lo ao desenvolver soluções do Office no [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)], exceto quando você chama métodos com opcional **ref** parâmetros no `ThisDocument` classe nos projetos em nível de documento para Word.  
  
## <a name="example-in-excel"></a>Exemplo no Excel  
 O <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceite o valor padrão de outras pessoas, conforme mostrado no exemplo de código a seguir. Este exemplo requer um projeto de nível de documento com uma classe de planilha denominada `Sheet1`.  
  
 [!code-csharp[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs#1)]
 [!code-vb[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb#1)]  
  
## <a name="example-in-word"></a>Exemplo no Word  
 O <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> método tem muitos parâmetros opcionais. Você pode especificar valores para alguns parâmetros e aceite o valor padrão de outras pessoas, conforme mostrado no exemplo de código a seguir.  
  
 [!code-vb[Trin_VstrefGeneralWord#1](../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstrefGeneralWord#1](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#1)]  
  
## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Use parâmetros opcionais dos métodos na classe ThisDocument em projetos do Visual c# em nível de documento para Word  
 O modelo de objeto do Word contém vários métodos com opcional **ref** parâmetros que aceitam <xref:System.Object> valores. No entanto, não é possível omitir opcional **ref** parâmetros de métodos de gerado `ThisDocument` classe no Visual c# projetos no nível de documento para Word. Visual c# permite que você omita opcional **ref** parâmetros apenas para os métodos das interfaces, classes não. Por exemplo, o exemplo de código a seguir não é compilado, porque você não pode omitir opcional **ref** parâmetros da <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método da `ThisDocument` classe.  
  
 [!code-csharp[Trin_VstrefGeneralWord#3](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#3)]  
  
 Quando você chama métodos do `ThisDocument` de classe, siga estas diretrizes:  
  
- Para aceitar o valor padrão de um recurso opcional **ref** parâmetro, passe o `missing` variável ao parâmetro. O `missing` variável é definido automaticamente em projetos do Office do Visual c# e é atribuído ao valor <xref:System.Type.Missing> no código do projeto gerado.  
  
- Para especificar seu próprio valor para um recurso opcional **ref** parâmetro, declarar um objeto que é atribuído ao valor que você deseja especificar e, em seguida, passar o objeto para o parâmetro.  
  
  O exemplo de código a seguir demonstra como chamar o <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> método, especificando um valor para o *ignoreUppercase* parâmetro e aceitar o valor padrão para os outros parâmetros.  
  
  [!code-csharp[Trin_VstrefGeneralWord#4](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#4)]  
  
  Se você quiser escrever um código que omite opcional **ref** parâmetros de um método na `ThisDocument` classe, você pode também chamar o mesmo método no <xref:Microsoft.Office.Interop.Word.Document> objeto retornado pelo <xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> propriedade e omitir a parâmetros do método. Você pode fazer isso porque <xref:Microsoft.Office.Interop.Word.Document> é uma interface, em vez de uma classe.  
  
  [!code-csharp[Trin_VstrefGeneralWord#5](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#5)]  
  
  Para obter mais informações sobre parâmetros de tipo de valor e referência, consulte [passar argumentos por valor e por referência &#40;Visual Basic&#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (para Visual Basic) e [passar parâmetros &#40;C&#35; Guia de programação do&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)  
  
  