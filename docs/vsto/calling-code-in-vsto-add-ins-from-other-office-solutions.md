---
title: Chamar o código no VSTO Add-ins de outras soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9290fcdd705f6f38b4b7e91e46d5b635f1e309ff
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248092"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>Chamar o código no VSTO Add-ins de outras soluções do Office
  Você pode expor um objeto no seu suplemento do VSTO para outras soluções, incluindo outras soluções do Microsoft Office. Isso é útil se o suplemento do VSTO fornece um serviço que você deseja habilitar usar outras soluções. Por exemplo, se você tiver um suplemento do VSTO para o Microsoft Office Excel que executa cálculos nos dados financeiros de um serviço Web, outras soluções podem executar esses cálculos chamando o suplemento do VSTO do Excel em tempo de execução.  
  
 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]  
  
 Há duas etapas principais nesse processo:  
  
-   No seu suplemento VSTO, expor um objeto para outras soluções.  
  
-   Em outra solução, acesse o objeto exposto pelo seu suplemento do VSTO e chamam membros do objeto.  
  
## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>Tipos de soluções que podem chamar o código em um suplemento  
 Você pode expor um objeto em um suplemento do VSTO para os seguintes tipos de soluções:  
  
-   Código Visual Basic for Applications (VBA) em um documento que é carregado no processo do aplicativo como o suplemento do VSTO.  
  
-   Personalizações no nível do documento que são carregadas no mesmo processo de aplicativo como o suplemento do VSTO.  
  
-   Outros suplementos do VSTO criados usando os modelos de projeto do Office no Visual Studio.  
  
-   COM o VSTO Add-ins (ou seja, suplementos do VSTO que implementam o <xref:Extensibility.IDTExtensibility2> diretamente da interface).  
  
-   Qualquer solução que está em execução em um processo diferente de seu suplemento do VSTO (esses tipos de soluções também são nomeados *clientes fora do processo*). Isso inclui aplicativos que automatizam um aplicativo do Office, como um aplicativo Windows Forms ou console e VSTO Add-ins que são carregados em um processo diferente.  
  
## <a name="expose-objects-to-other-solutions"></a>Expor objetos a outras soluções  
 Para expor um objeto no seu suplemento do VSTO para outras soluções, execute as seguintes etapas no seu suplemento do VSTO:  
  
1.  Defina uma classe que você deseja expor para outras soluções.  
  
2.  Substituir a <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método no `ThisAddIn` classe. Retorne uma instância da classe que você deseja expor para outras soluções.  
  
### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>Definir a classe que você deseja expor para outras soluções  
 No mínimo, a classe que você deseja expor deve ser pública, ele deve ter o <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributo definido como **verdadeira**, e ela deve expor os [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface.  
  
 A maneira recomendada para expor a [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface é executar as seguintes etapas:  
  
1. Defina uma interface que declara os membros que você deseja expor para outras soluções. Você pode definir essa interface em seu projeto de suplemento do VSTO. No entanto, você talvez queira definir essa interface em um projeto de biblioteca de classe separada, se você quiser expor a classe para as soluções não VBA, para que as soluções que chamam o suplemento do VSTO podem fazer referência a interface sem fazer referência ao seu projeto de suplemento do VSTO.  
  
2. Aplicar a <xref:System.Runtime.InteropServices.ComVisibleAttribute> de atributos para essa interface e defina esse atributo como **verdadeiro**.  
  
3. Modificar sua classe para implementar essa interface.  
  
4. Aplicar a <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> à sua classe de atributo e definir esse atributo para o **None** valor da <xref:System.Runtime.InteropServices.ClassInterfaceType> enumeração.  
  
5. Se você quiser expor essa classe para clientes fora do processo, você talvez precise também faça o seguinte:  
  
   -   Derive a classe de <xref:System.Runtime.InteropServices.StandardOleMarshalObject>. Para obter mais informações, consulte [expor classes para clientes fora do processo](#outofproc).  
  
   -   Defina as **registrar para interoperabilidade COM** propriedade no projeto em que você define a interface. Esta propriedade é necessária apenas se você quiser permitir que os clientes usam associação inicial para chamar o suplemento do VSTO.  
  
   O exemplo de código a seguir demonstra uma `AddInUtilities` classe com um `ImportData` método que pode ser chamado por outras soluções. Para ver esse código no contexto de um passo a passo maior, consulte [passo a passo: Chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).  
  
   [!code-csharp[Trin_AddInInteropWalkthrough #3](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#3)]
   [!code-vb[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#3)]  
  
### <a name="expose-classes-to-vba"></a>Exponha classes ao VBA  
 Quando você executa as etapas fornecidas acima, o código VBA pode chamar apenas os métodos que você declara na interface do. Código do VBA não é possível chamar quaisquer outros métodos em sua classe, incluindo os métodos que sua classe obtém de classes base como <xref:System.Object>.  
  
 Como alternativa, você pode expor os [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) interface, definindo o <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> de atributo para o valor de AutoDispatch ou AutoDual o <xref:System.Runtime.InteropServices.ClassInterfaceType> enumeração. Se você expuser a interface, você não precisa declarar os métodos em uma interface separada. No entanto, código do VBA pode chamar quaisquer métodos públicos e não estáticos em sua classe, incluindo métodos obtidos de classes base, como <xref:System.Object>. Além disso, out-of-process clientes que usam associação inicial não é possível chamar sua classe.  
  
###  <a name="outofproc"></a> Exponha classes para clientes fora do processo  
 Se você quiser expor uma classe no seu suplemento do VSTO para clientes fora do processo, você deve derivar a classe de <xref:System.Runtime.InteropServices.StandardOleMarshalObject> para garantir que clientes fora do processo podem chamar seu suplemento do VSTO objeto exposto. Caso contrário, as tentativas de obter uma instância de seu objeto exposto em um cliente fora do processo podem falhar inesperadamente.  
  
 Essa falha ocorre porque todas as chamadas para o modelo de objeto de um aplicativo do Office devem ser feitas no thread da interface do usuário principal, mas as chamadas de um cliente fora de processo para seu objeto chegará em um thread arbitrário de (chamada de procedimento remoto) do RPC. O mecanismo de empacotamento COM o .NET Framework não mudará threads e, em vez disso, ele tentará realizar marshaling da chamada para seu objeto no thread RPC de entrada, em vez do thread de interface do usuário principal. Se o objeto é uma instância de uma classe que deriva de <xref:System.Runtime.InteropServices.StandardOleMarshalObject>, chamadas de entrada para seu objeto são empacotadas automaticamente para o thread em que foi criado o objeto exposto, que será o thread de interface do usuário principal do aplicativo host.  
  
 Para obter mais informações sobre o uso de threads em soluções do Office, consulte [suporte a Threading no Office](../vsto/threading-support-in-office.md).  
  
### <a name="override-the-requestcomaddinautomationservice-method"></a>Substitua o método RequestComAddInAutomationService  
 O exemplo de código a seguir demonstra como substituir <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> no `ThisAddIn` classe no seu suplemento do VSTO. O exemplo supõe que você definiu uma classe chamada `AddInUtilities` que você deseja expor para outras soluções. Para ver esse código no contexto de um passo a passo maior, consulte [passo a passo: Chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).  
  
 [!code-csharp[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs#1)]
 [!code-vb[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb#1)]  
  
 Quando o suplemento do VSTO é carregado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] chama o <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> método. O tempo de execução atribui o objeto retornado para a propriedade COMAddIn.Object de um <xref:Microsoft.Office.Core.COMAddIn> objeto que representa o suplemento do VSTO. Isso <xref:Microsoft.Office.Core.COMAddIn> objeto está disponível para outras soluções do Office e para soluções que automatizam o Office.  
  
## <a name="access-objects-from-other-solutions"></a>Acessar objetos de outras soluções  
 Para chamar o objeto exposto no seu suplemento do VSTO, execute as seguintes etapas na solução de cliente:  
  
1. Obter o <xref:Microsoft.Office.Core.COMAddIn> objeto que representa o exposto suplemento VSTO. Os clientes podem acessar todos os VSTO Add-ins disponíveis usando o `Application.COMAddIns` propriedade no modelo de objeto de aplicativo do Office host.  
  
2. Acessar a propriedade COMAddIn.Object do <xref:Microsoft.Office.Core.COMAddIn> objeto. Essa propriedade retorna o objeto exposto do que o suplemento do VSTO.  
  
3. Chame os membros do objeto exposto.  
  
   A maneira que você use o valor de retorno da propriedade COMAddIn.Object é diferente para os clientes do VBA e não VBA. Para clientes fora do processo, o código adicional é necessário para evitar uma possível condição de corrida.  
  
### <a name="access-objects-from-vba-solutions"></a>Objetos de acesso de soluções do VBA  
 O exemplo de código a seguir demonstra como usar o VBA para chamar um método que é exposto por um suplemento do VSTO. Essa macro VBA chama um método chamado `ImportData` que está definido em um suplemento VSTO chamado **ExcelImportData**. Para ver esse código no contexto de um passo a passo maior, consulte [passo a passo: Chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md).  
  
```vb
Sub CallVSTOMethod()  
    Dim addIn As COMAddIn  
    Dim automationObject As Object  
    Set addIn = Application.COMAddIns("ExcelImportData")  
    Set automationObject = addIn.Object  
    automationObject.ImportData  
End Sub  
```  
  
### <a name="access-objects-from-non-vba-solutions"></a>Objetos de acesso de soluções não VBA  
 Em uma solução não VBA, você deve converter o valor da propriedade COMAddIn.Object para a interface que ele implementa e, em seguida, você pode chamar os métodos expostos no objeto de interface. O exemplo de código a seguir demonstra como chamar o `ImportData` método a partir de um outro suplemento VSTO que foi criado usando as ferramentas de desenvolvedor do Office no Visual Studio.  
  
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
  
 Neste exemplo, se você tentar converter o valor da propriedade COMAddIn.Object para o `AddInUtilities` classe em vez de `IAddInUtilities` interface, o código gerará uma <xref:System.InvalidCastException>.  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md)   
 [Passo a passo: Chamar o código em um suplemento do VSTO do VBA](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Como: Criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Arquitetura de suplementos do VSTO](../vsto/architecture-of-vsto-add-ins.md)   
 [Personalizar os recursos de interface do usuário usando interfaces de extensibilidade](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)  
  
  
