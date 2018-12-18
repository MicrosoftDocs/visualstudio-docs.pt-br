---
title: Combinar o VBA e personalizações no nível de documento
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.VBAInterop.InvalidAssemblyVersion
- VST.VBAInterop.ProjectLoadFailure
- VST.VBAInterop.MissingGUID
- VST.VBAInterop.EnableComCallers
- VST.VBAInterop.PersistVBACode
- VST.VBAInterop.ReferenceAssemblyFromVBA
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio]
- Office documents [Office development in Visual Studio], Visual Basic for Applications and
- VBA [Office development in Visual Studio], about VBA and document-level customizations
- managed code [Office development in Visual Studio], Visual Basic for Applications and
- document-level customizations [Office development in Visual Studio], Visual Basic for Applications and
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2243a3e03ed84325523f62d77ae3cc6d20f83bbb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878070"
---
# <a name="combine-vba-and-document-level-customizations"></a>Combinar o VBA e personalizações no nível de documento
  Você pode usar o Visual Basic para código Applications (VBA) em um documento que faz parte de uma personalização no nível de documento para o Microsoft Office Word ou Microsoft Office Excel. Você pode chamar o código do VBA no documento do assembly de personalização, ou você pode configurar seu projeto para habilitar o código do VBA no documento para chamar o código no assembly de personalização.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="behavior-of-vba-code-in-a-document-level-customization"></a>Comportamento do código VBA em uma personalização no nível de documento  
 Quando você abre seu projeto no Visual Studio, o documento é aberto no modo de design. Código do VBA não é executado quando o documento está no modo de design, para que possa trabalhar no documento e código sem executar o código do VBA.  
  
 Quando você executa a solução, manipuladores de eventos no VBA e o assembly de personalização acompanhar os eventos que são gerados no documento e execute os dois conjuntos de código. Não é possível determinar com antecedência qual código será executado antes das outras; Você deve determinar isso por meio de testes em cada caso individual. Você pode obter resultados inesperados se os dois conjuntos de código são não cuidadosamente coordenados e testados.  
  
## <a name="call-vba-code-from-the-customization-assembly"></a>Chamar o código do VBA do assembly de personalização  
 Você pode chamar macros em documentos do Word, e você pode chamar funções e macros em pastas de trabalho do Excel. Para fazer isso, use um dos seguintes métodos:  
  
- Para o Word, chame o <xref:Microsoft.Office.Interop.Word._Application.Run%2A>método da <xref:Microsoft.Office.Interop.Word.Application> classe.  
  
- Para Excel, chame o <xref:Microsoft.Office.Interop.Excel._Application.Run%2A> método da <xref:Microsoft.Office.Interop.Excel.Application> classe.  
  
  Para cada método, o primeiro parâmetro identifica o nome da macro ou função que você deseja chamar, e os parâmetros opcionais restantes especificam os parâmetros para passar para a macro ou função. O primeiro parâmetro pode ter formatos diferentes para Word e Excel:  
  
- Para o Word, o primeiro parâmetro é uma cadeia de caracteres que pode ser qualquer combinação de modelo, o módulo e o nome da macro. Se você especificar o nome do documento, seu código pode executar somente macros em documentos relacionados ao contexto atual — não apenas a qualquer macro em qualquer documento.  
  
- Para o Excel, o primeiro parâmetro pode ser uma cadeia de caracteres que especifica o nome da macro, um <xref:Microsoft.Office.Interop.Excel.Range> que indica onde está a função ou um identificador de registro para uma função de DLL (XLL) registrada. Se você passar uma cadeia de caracteres, a cadeia de caracteres será avaliada no contexto da planilha ativa.  
  
  O exemplo de código a seguir mostra como chamar uma macro denominada `MyMacro` de um projeto de nível de documento para Excel. Este exemplo supõe que `MyMacro` é definido em `Sheet1`.  
  
```vb  
Globals.Sheet1.Application.Run("MyMacro")  
```  
  
```csharp  
Globals.Sheet1.Application.Run("MyMacro", missing, missing, missing,  
    missing, missing, missing, missing, missing, missing, missing,  
    missing, missing, missing, missing, missing, missing, missing,  
    missing, missing, missing, missing, missing, missing, missing,   
    missing, missing, missing, missing, missing, missing);  
```  
  
> [!NOTE]  
>  Para obter informações sobre como usar global `missing` variável no lugar de parâmetros opcionais no Visual c#, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).  
  
## <a name="call-code-in-document-level-customizations-from-vba"></a>Chamar o código em personalizações no nível de documento do VBA  
 Você pode configurar um projeto de nível de documento para Word ou Excel para que esse código Visual Basic for Applications (VBA) no documento possa chamar o código no assembly de personalização. Isso é útil nos seguintes cenários:  
  
- Você deseja estender o código do VBA em um documento existente com o uso de recursos em uma personalização no nível de documento que está associada com o mesmo documento.  
  
- Você deseja disponibilizar serviços que você desenvolva em uma personalização no nível de documento para os usuários finais que podem acessar os serviços, escrevendo código VBA no documento.  
  
  As ferramentas de desenvolvimento do Office no Visual Studio fornecem um recurso semelhante para suplementos do VSTO. Se você estiver desenvolvendo um suplemento do VSTO, você pode chamar o código no seu suplemento do VSTO de outras soluções do Microsoft Office. Para obter mais informações, consulte [chamar o código no VSTO Add-ins de outras soluções do Office](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md).  
  
> [!NOTE]  
>  Esse recurso não pode ser usado em projetos de modelo do Word. Ele pode ser usado apenas no documento do Word, planilha do Excel ou projetos de modelo do Excel.  
  
## <a name="requirements"></a>Requisitos  
 Antes de habilitar o código do VBA chamar o assembly de personalização, seu projeto deve atender aos seguintes requisitos:  
  
-   O documento deve ter uma das seguintes extensões de nome de arquivo:  
  
    -   Para o Word: *docm* ou *. doc*  
  
    -   Para Excel: *. xlsm*, *. xltm*, *. xls*, ou *. xlt*  
  
-   O documento já deve conter um projeto do VBA que tem o código VBA nele.  
  
-   Código do VBA no documento deve ter permissão para executar sem avisar o usuário para habilitar as macros. Você pode confiar em código VBA de execução, adicionando o local do projeto do Office para a lista de locais confiáveis nas configurações do Centro de confiabilidade para Word ou Excel.  
  
-   O projeto do Office deve conter pelo menos uma classe pública que contém um ou mais membros públicos que você está expondo ao VBA.  
  
     Você pode expor métodos, propriedades e eventos ao VBA. A classe que você expõe pode ser uma classe de item de host (como `ThisDocument` para o Word, ou `ThisWorkbook` e `Sheet1` para Excel) ou outra classe que você define no seu projeto. Para obter mais informações sobre itens de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
## <a name="enable-vba-code-to-call-into-the-customization-assembly"></a>Habilitar o código do VBA chamar o assembly de personalização  
 Há duas maneiras diferentes que você pode expor os membros em um assembly de personalização ao código VBA no documento:  
  
- Você pode expor os membros de uma classe de item de host em um [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto VBA. Para fazer isso, defina a **EnableVbaCallers** propriedade do item de host para **True** no **propriedades** é janela enquanto o item de host (ou seja, o documento, planilha ou pasta de trabalho) aberto no designer. Visual Studio executa automaticamente todo o trabalho necessário para habilitar o código do VBA chamar membros da classe.  
  
- Você pode expor os membros em qualquer classe pública em um projeto do Visual c# ou classe de item de membros em um host não um [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto para o VBA. Essa opção fornece mais liberdade para escolher quais classes devem expor ao VBA, mas também requer mais etapas manuais.  
  
   Para fazer isso, você deve executar as seguintes etapas principais:  
  
  1.  Expor a classe a com.&lt;1}  
  
  2.  Substituir a **GetAutomationObject** método de uma classe de item de host em seu projeto para retornar uma instância da classe que você está expondo ao VBA.  
  
  3.  Defina as **ReferenceAssemblyFromVbaProject** propriedade de qualquer classe de item de host do projeto a **verdadeiro**. Isso insere a biblioteca de tipos do assembly de personalização no assembly e adiciona uma referência à biblioteca de tipos para o projeto do VBA no documento.  
  
  Para obter instruções detalhadas, consulte [como: expor o código para VBA em um projeto do Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md) e [como: expor o código para VBA em um Visual C&#35; projeto](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md).  
  
  O **EnableVbaCallers** e **ReferenceAssemblyFromVbaProject** propriedades estão disponíveis apenas no **propriedades** janela em tempo de design; eles não podem ser usados em tempo de execução . Para exibir as propriedades, abra o designer de um item de host em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para obter mais informações sobre as tarefas específicas que o Visual Studio executa quando você definir essas propriedades, consulte [tarefas executadas pelas propriedades do item de host](#PropertyTasks).  
  
> [!NOTE]  
>  Se a pasta de trabalho ou o documento ainda não contiver código VBA ou se o código do VBA no documento não é confiável para ser executado, você receberá uma mensagem de erro ao definir a **EnableVbaCallers** ou **ReferenceAssemblyFromVbaProject**  propriedade para **verdadeiro**. Isso ocorre porque o Visual Studio não é possível modificar o projeto do VBA no documento nessa situação.  
  
## <a name="use-members-in-vba-code-to-call-into-the-customization-assembly"></a>Usar membros no código do VBA para chamar o assembly de personalização  
 Depois de configurar seu projeto para habilitar o código do VBA chamar o assembly de personalização, o Visual Studio adiciona os seguintes membros para o projeto do VBA no documento:  
  
- Para todos os projetos, o Visual Studio adiciona um método global chamado `GetManagedClass`.  
  
- Para [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] classe do item no qual você expor os membros de um host de projetos usando o **EnableVbaCallers** propriedade, o Visual Studio também adiciona uma propriedade chamada `CallVSTOAssembly` para o `ThisDocument`, `ThisWorkbook`, `Sheet1`, `Sheet2`, ou `Sheet3` módulo no projeto do VBA.  
  
  Você pode usar o `CallVSTOAssembly` propriedade ou `GetManagedClass` método para acessar os membros públicos da classe que é exposta ao código do VBA no projeto.  
  
> [!NOTE]  
>  Embora você desenvolve e implanta sua solução, há várias cópias diferentes do documento onde você pode adicionar o código do VBA. Para obter mais informações, consulte [de código para o documento de diretrizes para adicionar o VBA](#Guidelines).  
  
### <a name="use-the-callvstoassembly-property-in-a-visual-basic-project"></a>Use a propriedade CallVSTOAssembly em um projeto do Visual Basic  
 Use o `CallVSTOAssembly` propriedade para acessar membros públicos que você adicionou à classe de item de host. Por exemplo, a macro VBA a seguir chama um método chamado `MyVSTOMethod` que é definido no `Sheet1` classe em um projeto de pasta de trabalho do Excel.  
  
```vb
Sub MyMacro()  
    Sheet1.CallVSTOAssembly.MyVSTOMethod()  
End Sub  
```  
  
 Essa propriedade é uma maneira mais conveniente para chamar o assembly de personalização que usar o `GetManagedClass` método diretamente. `CallVSTOAssembly` Retorna um objeto que representa o host de classe de item que é exposta ao VBA. Os membros e parâmetros de método do objeto retornado aparecem no IntelliSense.  
  
 O `CallVSTOAssembly` propriedade tem uma declaração que é semelhante ao código a seguir. Esse código supõe que você tenha exposto a `Sheet1` hospedar a classe de item em um projeto de pasta de trabalho do Excel chamado `ExcelWorkbook1` ao VBA.  
  
```vb 
Property Get CallVSTOAssembly() As ExcelWorkbook1.Sheet1  
    Set CallVSTOAssembly = GetManagedClass(Me)  
End Property  
```  
  
### <a name="use-the-getmanagedclass-method"></a>Use o método GetManagedClass  
 Usar global `GetManagedClass` método, passe para a classe de item de host que contém sua substituição do objeto VBA que corresponde a **GetAutomationObject** método. Em seguida, use o objeto retornado para acessar a classe que é exposto ao VBA.  
  
 Por exemplo, a macro VBA a seguir chama um método chamado `MyVSTOMethod` que é definido na `Sheet1` hospedar a classe de item em um projeto de pasta de trabalho do Excel denominado `ExcelWorkbook1`.  
  
```vb
Sub CallVSTOMethod  
    Dim VSTOSheet1 As ExcelWorkbook1.Sheet1  
    Set VSTOSheet1 = GetManagedClass(Sheet1)  
    VSTOSheet1.MyVSTOMethod  
End Sub  
```  
  
 O `GetManagedClass` método tem a seguinte declaração.  
  
```vb
GetManagedClass(pdispInteropObject Object) As Object  
```  
  
 Esse método retorna um objeto que representa a classe que é exposto ao VBA. Os membros e parâmetros de método do objeto retornado aparecem no IntelliSense.  
  
##  <a name="Guidelines"></a> Diretrizes para adicionar o código do VBA no documento  
 Há várias cópias diferentes do documento onde você pode adicionar código VBA que chama a personalização de nível de documento.  
  
 Ao desenvolver e testar sua solução, você pode escrever código VBA no documento que é aberta enquanto você depura ou executa seu projeto no Visual Studio (ou seja, o documento na pasta de saída de compilação). No entanto, qualquer código VBA adicionado a este documento será substituído na próxima vez que você compila o projeto, porque o Visual Studio substitui o documento na pasta de saída de compilação com uma cópia do documento da pasta do projeto principal.  
  
 Se você deseja salvar o código do VBA que você adiciona ao documento ao depurar ou executar a solução, copie o código do VBA para o documento na pasta do projeto. Para obter mais informações sobre o processo de compilação, consulte [compilar soluções do office](../vsto/building-office-solutions.md).  
  
 Quando você estiver pronto para implantar sua solução, há três locais de documento principal em que você pode adicionar o código do VBA.  
  
### <a name="in-the-project-folder-on-the-development-computer"></a>Na pasta do projeto no computador de desenvolvimento  
 Esse local é conveniente quando você tem controle completo sobre o código do VBA no documento e o código de personalização. Porque o documento estiver no computador de desenvolvimento, você pode facilmente modificar o código do VBA se você alterar o código de personalização. Código do VBA que você adicionar a essa cópia do documento permanece no documento quando você compila, depurar e publica sua solução.  
  
 É possível adicionar o código do VBA para o documento enquanto ele está aberto no designer. Você deve primeiro feche o documento no designer e, em seguida, abra o documento diretamente no Word ou Excel.  
  
> [!CAUTION]  
>  Se você adicionar o código do VBA que é executado quando o documento for aberto, em casos raros esse código pode corromper o documento ou impedir que ele seja aberto no designer.  
  
### <a name="in-the-publish-or-installation-folder"></a>Na pasta de instalação ou de publicação  
 Em alguns casos, ele pode ser adequado adicionar o código do VBA para o documento na pasta de instalação ou de publicação. Por exemplo, você pode escolher essa opção se o código do VBA é gravado e testado por um desenvolvedor diferente em um computador que não tenha instalado o Visual Studio.  
  
 Se os usuários instalam a solução diretamente a partir da pasta de publicação, você deve adicionar o código do VBA para o documento sempre que você publique a solução. Quando você publica a solução, o Visual Studio substitui o documento no local de publicação.  
  
 Se os usuários instalam a solução de uma pasta de instalação é diferente da pasta de publicação, você pode evitar adicionar o código do VBA no documento sempre que você publique a solução. Quando uma atualização de publicação está pronta para ser movida da pasta de publicação para a pasta de instalação, copie todos os arquivos para a pasta de instalação, exceto para o documento.  
  
### <a name="on-the-end-user-computer"></a>No computador do usuário final  
 Se os usuários finais são desenvolvedores VBA que estão chamando para os serviços que você fornece na personalização no nível de documento, você pode dizer a eles como chamar seu código usando o `CallVSTOAssembly` propriedade ou o `GetManagedClass` método em suas cópias do documento. Quando você publicar atualizações para a solução, o código do VBA no documento no computador do usuário final não será substituído, porque o documento não é modificado por publicar atualizações.  
  
##  <a name="PropertyTasks"></a> Tarefas executadas pelas propriedades do item de host  
 Quando você usa o **EnableVbaCallers** e **ReferenceAssemblyFromVbaProject** propriedades, o Visual Studio executa diferentes conjuntos de tarefas.  
  
### <a name="enablevbacallers"></a>EnableVbaCallers  
 Quando você define o **EnableVbaCallers** propriedade de um item de host **verdadeiro** em um projeto do Visual Basic, Visual Studio executa as seguintes tarefas:  
  
1. Ele adiciona o <xref:Microsoft.VisualBasic.ComClassAttribute> e <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributos para a classe de item de host.  
  
2. Ele substitui o **GetAutomationObject** método da classe de item de host.  
  
3. Ele define a **ReferenceAssemblyFromVbaProject** propriedade do item de host para **verdadeiro**.  
  
   Quando você define o **EnableVbaCallers** propriedade de volta para **falso**, Visual Studio executa as seguintes tarefas:  
  
4. Ele remove as <xref:Microsoft.VisualBasic.ComClassAttribute> e <xref:System.Runtime.InteropServices.ComVisibleAttribute> atributos do `ThisDocument` classe.  
  
5. Ele remove as **GetAutomationObject** método da classe de item de host.  
  
   > [!NOTE]  
   >  Visual Studio define automaticamente a **ReferenceAssemblyFromVbaProject** propriedade de volta para **falso**. Você pode definir essa propriedade **falsos** manualmente usando o **propriedades** janela.  
  
### <a name="referenceassemblyfromvbaproject"></a>ReferenceAssemblyFromVbaProject  
 Quando o **ReferenceAssemblyFromVbaProject** propriedade de qualquer item de host em um projeto do Visual Basic ou Visual c# é definida como **verdadeiro**, Visual Studio executa as seguintes tarefas:  
  
1. Ele gera uma biblioteca de tipos para o assembly de personalização e incorpora a biblioteca de tipos no assembly.  
  
2. Ele adiciona uma referência às bibliotecas de tipo a seguir no projeto VBA no documento:  
  
   -   A biblioteca de tipos para o assembly de personalização.  
  
   -   Os Microsoft Visual Studio Tools para Office biblioteca de tipos de 9.0 do mecanismo de execução. Esta biblioteca de tipos está incluída no [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)].  
  
   Quando o **ReferenceAssemblyFromVbaProject** propriedade é definida como **falso**, Visual Studio executa as seguintes tarefas:  
  
3. Ele remove as referências de biblioteca de tipo do projeto VBA no documento.  
  
4. Ele remove a biblioteca de tipos incorporados do assembly.  
  
## <a name="troubleshoot"></a>Solução de problemas
 A tabela a seguir lista alguns erros e sugestões para corrigir os erros comuns.  
  
|Erro|Sugestão|  
|-----------|----------------|  
|Depois de definir a **EnableVbaCallers** ou **ReferenceAssemblyFromVbaProject** propriedade, uma mensagem de erro indica que o documento não contém um projeto do VBA, ou você não tem permissão para acessar o Projeto do VBA no documento.|Certifique-se de que o documento no projeto contém pelo menos uma macro do VBA, o projeto do VBA tem confiança suficiente para ser executado e o projeto do VBA não está protegido por senha.|  
|Depois de definir a **EnableVbaCallers** ou **ReferenceAssemblyFromVbaProject** propriedade, uma mensagem de erro indica que o <xref:System.Runtime.InteropServices.GuidAttribute> declaração está ausente ou corrompido.|Certifique-se de que o <xref:System.Runtime.InteropServices.GuidAttribute> declaração está localizada em de *AssemblyInfo.cs* ou *AssemblyInfo* arquivo em seu projeto e que esse atributo é definido como um GUID válido.|  
|Depois de definir a **EnableVbaCallers** ou **ReferenceAssemblyFromVbaProject** propriedade, uma mensagem de erro informando de que o número de versão especificado pelo <xref:System.Reflection.AssemblyVersionAttribute> não é válido.|Certifique-se de que o <xref:System.Reflection.AssemblyVersionAttribute> declaração em de *AssemblyInfo.cs* ou *AssemblyInfo* arquivo em seu projeto é definido como um número de versão do assembly válido. Para obter informações sobre os números de versão do assembly válido, consulte o <xref:System.Reflection.AssemblyVersionAttribute> classe.|  
|Depois de renomear o assembly de personalização, código do VBA que chama o assembly de personalização deixará de funcionar.|Se você alterar o nome do assembly de personalização depois expô-lo ao código VBA, o link entre o projeto do VBA no documento e seu assembly de personalização é interrompido. Para corrigir esse problema, altere a **ReferenceFromVbaAssembly** propriedade em seu projeto para **falso** e, em seguida, de volta para **verdadeiro**e, em seguida, substitua todas as referências ao assembly antigo nome no código VBA com o novo nome do assembly.|  
  
## <a name="see-also"></a>Consulte também  
 [Como: expor o código para VBA em um projeto do Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)   
 [Como: expor o código para VBA em um Visual C&#35; projeto](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)   
 [Passo a passo: Chamar o código do VBA em um projeto do Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)   
 [Passo a passo: Chamar o código de VBA em um Visual C&#35; projeto](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Soluções VBA e do Office no Visual Studio comparadas](../vsto/vba-and-office-solutions-in-visual-studio-compared.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)  
  
  