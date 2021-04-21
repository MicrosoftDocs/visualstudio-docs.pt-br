---
title: Chamar código em suplementos do VSTO de outras soluções do Office
description: Saiba como você pode expor um objeto em seu suplemento do VSTO a outras soluções, incluindo outras soluções de Microsoft Office.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2519c9d1a22eb6f5577a258fb9b465cfd7caafc2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826974"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>Chamar código em suplementos do VSTO de outras soluções do Office
  Você pode expor um objeto em seu suplemento do VSTO a outras soluções, incluindo outras soluções de Microsoft Office. Isso será útil se o suplemento do VSTO fornecer um serviço que você deseja permitir que outras soluções usem. Por exemplo, se você tiver um suplemento do VSTO para Microsoft Office Excel que executa cálculos em dados financeiros de um serviço Web, outras soluções poderão executar esses cálculos chamando o suplemento do VSTO do Excel em tempo de execução.

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 Há duas etapas principais neste processo:

- Em seu suplemento do VSTO, expor um objeto para outras soluções.

- Em outra solução, acesse o objeto exposto pelo seu suplemento do VSTO e chame os membros do objeto.

## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>Tipos de soluções que podem chamar o código em um suplemento
 Você pode expor um objeto em um suplemento do VSTO para os seguintes tipos de soluções:

- O código Visual Basic for Applications (VBA) em um documento que é carregado no mesmo processo de aplicativo que o suplemento do VSTO.

- Personalizações em nível de documento que são carregadas no mesmo processo de aplicativo que o suplemento do VSTO.

- Outros suplementos do VSTO criados usando os modelos de projeto do Office no Visual Studio.

- Suplementos do VSTO do COM (ou seja, suplementos do VSTO que implementam a <xref:Extensibility.IDTExtensibility2> interface diretamente).

- Qualquer solução que esteja sendo executada em um processo diferente do suplemento do VSTO (esses tipos de soluções também são denominadas *clientes fora do processo*). Isso inclui aplicativos que automatizam um aplicativo do Office, como um Windows Forms ou um aplicativo de console, além de suplementos do VSTO que são carregados em um processo diferente.

## <a name="expose-objects-to-other-solutions"></a>Expor objetos a outras soluções
 Para expor um objeto em seu suplemento do VSTO a outras soluções, execute as seguintes etapas em seu suplemento do VSTO:

1. Defina uma classe que você deseja expor a outras soluções.

2. Substitua o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método na `ThisAddIn` classe. Retorne uma instância da classe que você deseja expor a outras soluções.

### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>Definir a classe que você deseja expor a outras soluções
 No mínimo, a classe que você deseja expor deve ser pública, deve ter o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo definido como **true** e deve expor a interface [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) .

 A maneira recomendada para expor a interface [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) é executar as seguintes etapas:

1. Defina uma interface que declare os membros que você deseja expor a outras soluções. Você pode definir essa interface em seu projeto de suplemento do VSTO. No entanto, talvez você queira definir essa interface em um projeto de biblioteca de classes separado se quiser expor a classe a soluções não VBA, para que as soluções que chamam o suplemento do VSTO possam fazer referência à interface sem fazer referência ao seu projeto de suplemento do VSTO.

2. Aplique o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo a essa interface e defina esse atributo como **true**.

3. Modifique sua classe para implementar essa interface.

4. Aplique o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo à sua classe e defina esse atributo como o valor **None** da <xref:System.Runtime.InteropServices.ClassInterfaceType> enumeração.

5. Se você quiser expor essa classe a clientes fora do processo, talvez também seja necessário fazer o seguinte:

   - Derive a classe de <xref:System.Runtime.InteropServices.StandardOleMarshalObject> . Para obter mais informações, consulte [expor classes a clientes fora do processo](#outofproc).

   - Defina o **registro para a propriedade de interoperabilidade com** no projeto onde você define a interface. Essa propriedade só será necessária se você quiser permitir que os clientes usem a ligação antecipada para chamar o suplemento do VSTO.

   O exemplo de código a seguir demonstra uma `AddInUtilities` classe com um `ImportData` método que pode ser chamado por outras soluções. Para ver esse código no contexto de uma explicação detalhada, consulte [Walkthrough: chamar código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).

   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs" id="Snippet3":::
   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb" id="Snippet3":::

### <a name="expose-classes-to-vba"></a>Expor classes ao VBA
 Quando você executa as etapas fornecidas acima, o código VBA pode chamar somente os métodos que você declara na interface. O código VBA não pode chamar nenhum outro método em sua classe, incluindo métodos que sua classe obtém de classes base, como <xref:System.Object> .

 Como alternativa, você pode expor a interface [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) definindo o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributo para a autoexpedição ou o valor AutoDual da <xref:System.Runtime.InteropServices.ClassInterfaceType> enumeração. Se você expor a interface, não é necessário declarar os métodos em uma interface separada. No entanto, o código VBA pode chamar qualquer método público e não estático em sua classe, incluindo métodos obtidos de classes base, como <xref:System.Object> . Além disso, os clientes fora do processo que usam a ligação inicial não podem chamar sua classe.

### <a name="expose-classes-to-out-of-process-clients"></a><a name="outofproc"></a> Expor classes a clientes fora do processo
 Se você quiser expor uma classe em seu suplemento do VSTO para clientes fora do processo, você deve derivar a classe de <xref:System.Runtime.InteropServices.StandardOleMarshalObject> para garantir que os clientes fora do processo possam chamar seu objeto de suplemento do VSTO exposto. Caso contrário, as tentativas de obter uma instância do objeto exposto em um cliente fora do processo podem falhar inesperadamente.

 Essa falha ocorre porque todas as chamadas para o modelo de objeto de um aplicativo do Office devem ser feitas no thread da interface do usuário principal, mas as chamadas de um cliente fora do processo para o objeto chegarão em um thread de RPC arbitrário (chamada de procedimento remoto). O mecanismo de marshaling COM no .NET Framework não alternará os threads e, em vez disso, tentará realizar marshaling da chamada para seu objeto no thread RPC de entrada em vez do thread da interface do usuário principal. Se o objeto for uma instância de uma classe derivada de, as <xref:System.Runtime.InteropServices.StandardOleMarshalObject> chamadas de entrada para o objeto serão automaticamente empacotadas para o thread em que o objeto exposto foi criado, que será o principal thread de interface do usuário do aplicativo host.

 Para obter mais informações sobre como usar threads em soluções do Office, consulte [suporte a threads no Office](../vsto/threading-support-in-office.md).

### <a name="override-the-requestcomaddinautomationservice-method"></a>Substituir o método RequestComAddInAutomationService
 O exemplo de código a seguir demonstra como substituir <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> na `ThisAddIn` classe em seu suplemento do VSTO. O exemplo supõe que você definiu uma classe denominada `AddInUtilities` que deseja expor a outras soluções. Para ver esse código no contexto de uma explicação detalhada, consulte [Walkthrough: chamar código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb" id="Snippet1":::

 Quando o suplemento do VSTO é carregado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método. O tempo de execução atribui o objeto retornado à propriedade COMAddIn. Object de um <xref:Microsoft.Office.Core.COMAddIn> objeto que representa o suplemento do VSTO. Esse <xref:Microsoft.Office.Core.COMAddIn> objeto está disponível para outras soluções do Office e para soluções que automatizam o Office.

## <a name="access-objects-from-other-solutions"></a>Acessar objetos de outras soluções
 Para chamar o objeto exposto em seu suplemento do VSTO, execute as seguintes etapas na solução do cliente:

1. Obtenha o <xref:Microsoft.Office.Core.COMAddIn> objeto que representa o suplemento do VSTO exposto. Os clientes podem acessar todos os suplementos do VSTO disponíveis usando a `Application.COMAddIns` propriedade no modelo de objeto do aplicativo do Office host.

2. Acesse a propriedade COMAddIn. Object do <xref:Microsoft.Office.Core.COMAddIn> objeto. Essa propriedade retorna o objeto exposto do suplemento do VSTO.

3. Chame os membros do objeto exposto.

   A maneira como você usa o valor de retorno da propriedade COMAddIn. Object é diferente para clientes do VBA e para clientes não-VBA. Para clientes fora do processo, o código adicional é necessário para evitar uma possível condição de corrida.

### <a name="access-objects-from-vba-solutions"></a>Acessar objetos de soluções do VBA
 O exemplo de código a seguir demonstra como usar o VBA para chamar um método que é exposto por um suplemento do VSTO. Essa macro do VBA chama um método chamado `ImportData` que é definido em um suplemento do VSTO chamado **ExcelImportData**. Para ver esse código no contexto de uma explicação detalhada, consulte [Walkthrough: chamar código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).

```vb
Sub CallVSTOMethod()
    Dim addIn As COMAddIn
    Dim automationObject As Object
    Set addIn = Application.COMAddIns("ExcelImportData")
    Set automationObject = addIn.Object
    automationObject.ImportData
End Sub
```

### <a name="access-objects-from-non-vba-solutions"></a>Acessar objetos de soluções não VBA
 Em uma solução não VBA, você deve converter o valor da propriedade COMAddIn. Object na interface que ele implementa e, em seguida, você pode chamar os métodos expostos no objeto de interface. O exemplo de código a seguir demonstra como chamar o `ImportData` método de um suplemento diferente do VSTO criado usando as ferramentas de desenvolvedor do Office no Visual Studio.

```vb
Dim addIn As Office.COMAddIn = Globals.ThisAddIn.Application.COMAddIns.Item("ExcelImportData")
Dim utilities As ExcelImportData.IAddInUtilities = TryCast( _
    addIn.Object, ExcelImportData.IAddInUtilities)
utilities.ImportData()
```

```csharp
object addInName = "ExcelImportData";
Office.COMAddIn addIn = Globals.ThisAddIn.Application.COMAddIns.Item(ref addInName);
ExcelImportData.IAddInUtilities utilities = (ExcelImportData.IAddInUtilities)addIn.Object;
utilities.ImportData();
```

 Neste exemplo, se você tentar converter o valor da propriedade COMAddIn. Object para a `AddInUtilities` classe em vez da `IAddInUtilities` interface, o código gerará um <xref:System.InvalidCastException> .

## <a name="see-also"></a>Consulte também
- [Programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md)
- [Walkthrough: chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)
- [Personalizar recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
