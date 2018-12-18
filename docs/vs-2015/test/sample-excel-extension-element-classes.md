---
title: 'Extensão do Excel de amostra: classes de elemento | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c251098-00aa-49cf-9e37-5717c0c6b3f1
caps.latest.revision: 11
ms.author: gewarren
manager: douge
ms.openlocfilehash: fb5085bdd9a79330f7c4f73fb39993af63eb0a78
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49811940"
---
# <a name="sample-excel-extension-element-classes"></a>Extensão do Excel de amostra: classes de elemento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A extensão usa classes derivadas de <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> e representam o controle de Planilha e o controle de Célula no [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)].  
  
 O elemento base para essa extensão é o `ExcelElement`. As classes `ExcelWorksheetElement` e `ExcelCellElement` herdam desse elemento  
  
## <a name="element-and-elementinformation-classes"></a>Classes Element e ElementInformation  
 A `Element` é a classe base de todos os elementos de interface do usuário para a extensão do Excel e é herdada da classe <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>. `ElementInformation` é a classe base para o elemento de classes de informações na amostra e não tem nenhum membro.  
  
#### <a name="simple-properties-and-methods"></a>Propriedades e métodos simples  
 Esses membros retornam valores simples, como o valor da propriedade `Name` ou da `ClassName` e o código é claro e fácil de ler. Alguns valores são retornados usando a classe `Utility`, que será discutido mais tarde. Outros retornam `null` porque não são relevantes para esta extensão de amostra. Dois membros são mais interessantes que os outros: a <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A> propriedade e o método <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.CacheProperties%2A>.  
  
#### <a name="queryid-property"></a>QueryId Property  
 Essa propriedade retornará uma condição que consiste em pares de nome-valor de propriedade que identificam exclusivamente o controle durante a reprodução. Para cada classe de controle derivada, o desenvolvedor deve substituir essa propriedade para retornar um objeto <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement> que o Framework pode usar para localizar o controle na interface do usuário.  
  
#### <a name="cacheproperties-method"></a>Método CacheProperties  
 Este método é chamado pela estrutura de teste durante o processo de gravação para dizer ao elemento para salvar um instantâneo das propriedades importantes. Isso mantém as propriedades disponíveis, mesmo quando o controle de interface do usuário real não está mais na tela.  
  
## <a name="worksheetelement-and-worksheetinformation-classes"></a>Classes WorksheetElement e WorksheetInformation  
 A classe `WorksheetElement` representa uma planilha do Excel na estrutura de testes e herda a classe base `Element`. Três propriedades são substituídas para fornecer informações específicas sobre o objeto Planilha do Excel: <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ClassName%2A>, <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ControlTypeName%2A> e <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.Name%2A>.  
  
 O <xref:System.Runtime.InteropServices.ComVisibleAttribute> também é aplicado a essa classe para torná-la visível ao COM.  
  
 A classe `WorksheetInformation` representa informações sobre uma planilha do Excel. Ela tem apenas um membro, a propriedade `SheetName`, que é suficiente para este amostra.  
  
## <a name="cellelement-and-cellinformation-classes"></a>Classes CellElement e CellInformation  
 A classe `CellElement` representa uma célula do Excel, herdada da classe base `Element`. O único membro substituído é a propriedade <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A>, que retorna um <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement> que usa as propriedades `RowIndex` e `ColumnIndex` para identificar a célula.  
  
## <a name="utilities-and-excelutilities-classes"></a>Classes Utilities e ExcelUtilities  
 A classe `ExcelUtilities` interna fornece alguns valores de constantes, tal como o nome da tecnologia e um método que determina se o identificador de janela fornecido representa uma planilha do Excel.  
  
 A classe `Utilities` tem métodos auxiliares que retornam uma variedade de informações sobre a interface do usuário. Alguns métodos usam chamadas diretas em DLLs do sistema externo, como **USER32.DLL** e **OLEACC.DLL**, para obter os identificadores de janela da interface do usuário<strong>.</strong>  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Runtime.InteropServices.ComVisibleAttribute>   
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement>   
 [Estendendo testes de IU codificados e gravações da ação para dar suporte ao Microsoft Excel](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)



