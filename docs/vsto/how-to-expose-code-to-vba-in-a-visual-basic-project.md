---
title: 'Como: expor código ao VBA em um projeto Visual Basic'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8aa29fca9905c9f1ed056949eec64ad967323462
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544840"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>Como: expor código ao VBA em um projeto Visual Basic
  Você pode expor o código em um [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto para Visual Basic for Applications (VBA) código se desejar que os dois tipos de código interajam entre si.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 O processo de Visual Basic é diferente do processo do Visual C#. Para obter mais informações, consulte [como: expor código ao VBA em um projeto do Visual C&#35;](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md).

 O processo é diferente para o código em uma classe de item de host do que para o código em outras classes:

- [Expor o código em uma classe de item de host](#HostItemCode)

- [Expor o código que não está em uma classe de item de host](#NonHostItem)

## <a name="expose-code-in-a-host-item-class"></a><a name="HostItemCode"></a>Expor o código em uma classe de item de host
 Para permitir que o código VBA chame Visual Basic código em uma classe de item de host, defina a propriedade **EnableVbaCallers** do item de host como **true**.

 Para obter instruções que demonstram como expor um método de uma classe de item de host e, em seguida, chamá-la do VBA, consulte [passo a passos: chamar código do VBA em um projeto Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md). Para obter mais informações sobre itens de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>Para expor o código em um item de host para o VBA

1. Abra ou crie um projeto de nível de documento [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] baseado em um documento do Word, pasta de trabalho do Excel ou modelo do Excel que dê suporte a macros e que já contenha código VBA.

     Para obter mais informações sobre os formatos de arquivo de documento que dão suporte a macros, consulte [combinar VBA e personalizações em nível de documento](../vsto/combining-vba-and-document-level-customizations.md).

    > [!NOTE]
    > Este recurso não pode ser usado em projetos de modelo do Word.

2. Verifique se o código VBA no documento pode ser executado sem solicitar que o usuário habilite macros. Você pode confiar no código VBA para executar adicionando o local do projeto do Office à lista de locais confiáveis nas configurações da central de confiabilidade do Word ou Excel.

3. Adicione a propriedade, o método ou o evento que você deseja expor ao VBA para uma das classes de item de host em seu projeto e declare o novo membro como **público**. O nome da classe depende do aplicativo:

    - Em um projeto do Word, a classe de item de host é denominada `ThisDocument` por padrão.

    - Em um projeto do Excel, as classes de item de host são nomeadas `ThisWorkbook` , `Sheet1` , `Sheet2` e `Sheet3` por padrão.

4. Defina a propriedade **EnableVbaCallers** para o item de host como **true**. Essa propriedade está disponível na janela **Propriedades** quando o item de host está aberto no designer.

     Depois de definir essa propriedade, o Visual Studio define automaticamente a propriedade **ReferenceAssemblyFromVbaProject** como **true**.

    > [!NOTE]
    > Se a pasta de trabalho ou o documento ainda não contiver código VBA, ou se o código VBA no documento não for confiável para execução, você receberá uma mensagem de erro quando definir a propriedade **EnableVbaCallers** como **true**. Isso ocorre porque o Visual Studio não pode modificar o projeto do VBA no documento nessa situação.

5. Clique em **OK** na mensagem que é exibida. Essa mensagem o lembrará de que, se você adicionar código VBA à pasta de trabalho ou ao documento enquanto estiver executando o projeto do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , o código VBA será perdido na próxima vez que você compilar o projeto. Isso ocorre porque o documento na pasta de saída da compilação é substituído toda vez que você cria o projeto.

     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar o assembly. O Visual Studio também adiciona uma propriedade chamada `CallVSTOAssembly` ao `ThisDocument` módulo,, `ThisWorkbook` `Sheet1` , `Sheet2` ou `Sheet3` no projeto do VBA. Você pode usar essa propriedade para acessar membros públicos da classe que você expôs ao VBA.

6. Compile o projeto.

## <a name="expose-code-that-is-not-in-a-host-item-class"></a><a name="NonHostItem"></a>Expor o código que não está em uma classe de item de host
 Para habilitar o código VBA para chamar Visual Basic código que não está em uma classe de item de host, modifique o código para que ele fique visível para o VBA.

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>Para expor o código que não está em uma classe de item de host para o VBA

1. Abra ou crie um projeto de nível de documento [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] baseado em um documento do Word, pasta de trabalho do Excel ou modelo do Excel que dê suporte a macros e que já contenha código VBA.

     Para obter mais informações sobre os formatos de arquivo de documento que dão suporte a macros, consulte [combinar VBA e personalizações em nível de documento](../vsto/combining-vba-and-document-level-customizations.md).

    > [!NOTE]
    > Este recurso não pode ser usado em projetos de modelo do Word.

2. Verifique se o código VBA no documento pode ser executado sem solicitar que o usuário habilite macros. Você pode confiar no código VBA para executar adicionando o local do projeto do Office à lista de locais confiáveis nas configurações da central de confiabilidade do Word ou Excel.

3. Adicione o membro que você deseja expor ao VBA para uma classe pública em seu projeto e declare o novo membro como **público**.

4. Aplique os seguintes <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:Microsoft.VisualBasic.ComClassAttribute> atributos e à classe que você está expondo ao VBA. Esses atributos tornam a classe visível para o VBA.

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. Substitua o método **GetAutomationObject** de uma classe de item de host em seu projeto para retornar uma instância da classe que você está expondo ao VBA. O exemplo de código a seguir pressupõe que você está expondo uma classe chamada `DocumentUtilities` para VBA.

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. Abra o documento (para Word) ou a planilha (para Excel) designer no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

7. Na janela **Propriedades** , selecione a propriedade **ReferenceAssemblyFromVbaProject** e altere o valor para **true**.

    > [!NOTE]
    > Se a pasta de trabalho ou o documento ainda não contiver código VBA, ou se o código VBA no documento não for confiável para execução, você receberá uma mensagem de erro quando definir a propriedade **ReferenceAssemblyFromVbaProject** como **true**. Isso ocorre porque o Visual Studio não pode modificar o projeto do VBA no documento nessa situação.

8. Clique em **OK** na mensagem que é exibida. Essa mensagem o lembrará de que, se você adicionar código VBA à pasta de trabalho ou ao documento enquanto estiver executando o projeto do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , o código VBA será perdido na próxima vez que você compilar o projeto. Isso ocorre porque o documento na pasta de saída da compilação é substituído toda vez que você cria o projeto.

     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar o assembly. O Visual Studio também adiciona um método chamado `GetManagedClass` ao projeto do VBA. Você pode chamar esse método de qualquer lugar no projeto do VBA para acessar a classe que você expôs ao VBA.

9. Compile o projeto.

## <a name="see-also"></a>Confira também
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Combine personalizações do VBA e no nível do documento](../vsto/combining-vba-and-document-level-customizations.md)
- [Walkthrough: chamar o código do VBA em um projeto Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [Como: expor código ao VBA em um projeto do Visual C&#35;](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
