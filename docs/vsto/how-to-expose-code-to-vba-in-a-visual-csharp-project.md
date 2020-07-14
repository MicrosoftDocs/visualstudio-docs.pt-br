---
title: 'Como: expor código ao VBA em um projeto C#'
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 21d7672d3c08012e75d73ee8bf4d9816b850eb2c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544827"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>Como: expor código ao VBA em um projeto do Visual C#
  Você pode expor o código em um projeto do Visual C# para Visual Basic for Applications (VBA), se desejar que os dois tipos de código interajam entre si.

 O processo do Visual C# é diferente do processo de Visual Basic. Para obter mais informações, consulte [como: expor código ao VBA em um projeto Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md).

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>Expor código em um projeto do Visual C#
 Para habilitar o código VBA para chamar o código em um projeto do Visual C#, modifique o código para que ele fique visível para COM e, em seguida, defina a propriedade **ReferenceAssemblyFromVbaProject** como **true** no designer.

 Para obter instruções que demonstram como chamar um método em um projeto do Visual C# a partir do VBA, consulte [Walkthrough: chamar código do VBA em um projeto do Visual C&#35;](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md).

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>Para expor o código em um projeto do Visual C# para o VBA

1. Abra ou crie um projeto de nível de documento baseado em um documento do Word, pasta de trabalho do Excel ou modelo do Excel que dê suporte a macros e que já contenha código VBA.

    Para obter mais informações sobre os formatos de arquivo de documento que dão suporte a macros, consulte [combinar VBA e personalizações em nível de documento](../vsto/combining-vba-and-document-level-customizations.md).

   > [!NOTE]
   > Este recurso não pode ser usado em projetos de modelo do Word.

2. Verifique se o código VBA no documento pode ser executado sem solicitar que o usuário habilite macros. Você pode confiar no código VBA para executar adicionando o local do projeto do Office à lista de locais confiáveis nas configurações da central de confiabilidade do Word ou Excel.

3. Adicione o membro que você deseja expor ao VBA para uma classe pública em seu projeto e declare o novo membro como **público**.

4. Aplique os seguintes <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributos e à classe que você está expondo ao VBA. Esses atributos tornam a classe visível para COM, mas sem gerar uma interface de classe.

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. Substitua o método **GetAutomationObject** de uma classe de item de host em seu projeto para retornar uma instância da classe que você está expondo ao VBA:

   - Se você estiver expondo uma classe de item de host para o VBA, substitua o método **GetAutomationObject** que pertence a essa classe e retorne a instância atual da classe.

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - Se você estiver expondo uma classe que não é um item de host para o VBA, substitua o método **GetAutomationObject** de qualquer item de host em seu projeto e retorne uma instância da classe de item não host. Por exemplo, o código a seguir pressupõe que você está expondo uma classe chamada `DocumentUtilities` para VBA.

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     Para obter mais informações sobre itens de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

6. Extraia uma interface da classe que você está expondo ao VBA. Na caixa de diálogo **extrair interface** , selecione os membros públicos que você deseja incluir na declaração de interface. Para obter mais informações, consulte [extrair refatoração de interface](../ide/reference/extract-interface.md).

7. Adicione a palavra-chave **Public** à declaração de interface.

8. Torne a interface visível para COM adicionando o atributo a seguir <xref:System.Runtime.InteropServices.ComVisibleAttribute> à interface.

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. Abra o documento (para Word) ou planilha (para Excel) no designer no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

10. Na janela **Propriedades** , selecione a propriedade **ReferenceAssemblyFromVbaProject** e altere o valor para **true**.

    > [!NOTE]
    > Se a pasta de trabalho ou o documento ainda não contiver código VBA ou se o código VBA no documento não for confiável para execução, você receberá uma mensagem de erro quando definir a propriedade **ReferenceAssemblyFromVbaProject** como **true**. Isso ocorre porque o Visual Studio não pode modificar o projeto do VBA no documento nessa situação.

11. Clique em **OK** na mensagem que é exibida. Essa mensagem o lembrará de que, se você adicionar código VBA à pasta de trabalho ou ao documento ao executar o projeto do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , o código VBA será perdido na próxima vez que você compilar o projeto. Isso ocorre porque o documento na pasta de saída da compilação é substituído toda vez que você cria o projeto.

     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar o assembly. O Visual Studio também adiciona um método chamado `GetManagedClass` ao projeto do VBA. Você pode chamar esse método de qualquer lugar no projeto do VBA para acessar a classe que você expôs ao VBA.

12. Compile o projeto.

## <a name="see-also"></a>Consulte também
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Combine personalizações do VBA e no nível do documento](../vsto/combining-vba-and-document-level-customizations.md)
- [Walkthrough: chamar o código do VBA em um projeto do Visual C&#35;](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [Como: expor código ao VBA em um projeto Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
