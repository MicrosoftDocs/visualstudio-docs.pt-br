---
title: 'Como: expor o código para VBA em um projeto do Visual c#'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f00f668c3eac9a39251d0a4e19f98ed597c373db
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873481"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>Como: expor o código para VBA em um projeto do Visual c#
  Você pode expor o código em um projeto Visual c# para o Visual Basic para código Applications (VBA) se você quiser que os dois tipos de código para interagir entre si.  
  
 O processo do Visual c# é diferente do processo do Visual Basic. Para obter mais informações, consulte [como: expor o código para VBA em um projeto do Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md).  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="expose-code-in-a-visual-c-project"></a>Expor o código em um projeto do Visual c#  
 Para habilitar o código do VBA chamar o código em um projeto do Visual c#, modifique o código para que fique visível para COM e, em seguida, defina a **ReferenceAssemblyFromVbaProject** propriedade **verdadeira** no designer.  
  
 Para um passo a passo que demonstra como chamar um método em um projeto do Visual c# do VBA, consulte [instruções passo a passo: chamar o código de VBA em um Visual C&#35; projeto](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md).  
  
### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>Para expor o código em um projeto do Visual c# para VBA  
  
1. Abra ou crie um projeto de nível de documento que se baseia em um documento do Word, a pasta de trabalho do Excel ou o modelo do Excel que dá suporte a macros e que já contenha código VBA.  
  
    Para obter mais informações sobre os formatos de arquivo do documento que dão suporte a macros, consulte [combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md).  
  
   > [!NOTE]  
   >  Esse recurso não pode ser usado em projetos de modelo do Word.  
  
2. Certifique-se de que o código VBA no documento tem permissão para executar sem avisar o usuário para habilitar as macros. Você pode confiar em código VBA de execução, adicionando o local do projeto do Office para a lista de locais confiáveis nas configurações do Centro de confiabilidade para Word ou Excel.  
  
3. Adicionar o membro que você deseja expor ao VBA para uma classe pública em seu projeto e declarar o novo membro como **público**.  
  
4. Aplicar o seguinte <xref:System.Runtime.InteropServices.ComVisibleAttribute> e <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> atributos à classe que você está expondo ao VBA. Esses atributos torná-la visível para COM, mas sem gerar uma interface de classe.  
  
   ```csharp  
   [System.Runtime.InteropServices.ComVisible(true)]  
   [System.Runtime.InteropServices.ClassInterface(  
       System.Runtime.InteropServices.ClassInterfaceType.None)]  
   ```  
  
5. Substituir a **GetAutomationObject** método de uma classe de item de host em seu projeto para retornar uma instância da classe que você está expondo ao VBA:  
  
   - Se você estiver expondo uma classe de item de host ao VBA, substituir os **GetAutomationObject** método que pertence a essa classe e retorna a instância atual da classe.  
  
     ```csharp  
     protected override object GetAutomationObject()  
     {  
         return this;  
     }  
     ```  
  
   - Se você estiver expondo uma classe que não é um item de host ao VBA, substituir os **GetAutomationObject** método de qualquer host de itens em seu projeto e retornar uma instância da classe de item de não-host. Por exemplo, o código a seguir pressupõe que você está expondo uma classe chamada `DocumentUtilities` ao VBA.  
  
     ```csharp  
     protected override object GetAutomationObject()  
     {  
         return new DocumentUtilities();  
     }  
     ```  
  
     Para obter mais informações sobre itens de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
6. Extrai uma interface de classe que você está expondo ao VBA. No **extrair Interface** caixa de diálogo, selecione os membros públicos que você deseja incluir na declaração de interface. Para obter mais informações, consulte [refatoração Extrair interface](../ide/reference/extract-interface.md).
  
7. Adicione a **pública** palavra-chave para a declaração de interface.  
  
8. Tornar a interface visível para COM, adicionando a seguinte <xref:System.Runtime.InteropServices.ComVisibleAttribute> de atributo para a interface.  
  
   ```csharp  
   [System.Runtime.InteropServices.ComVisible(true)]  
   ```  
  
9. Abrir o documento (para o Word) ou a planilha (para Excel) no designer de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
10. No **propriedades** janela, selecione a **ReferenceAssemblyFromVbaProject** propriedade e altere o valor para **verdadeiro**.  
  
    > [!NOTE]  
    >  Se a pasta de trabalho ou o documento ainda não contiver código VBA ou se o código do VBA no documento não é confiável para ser executado, você receberá uma mensagem de erro ao definir a **ReferenceAssemblyFromVbaProject** propriedade **True**. Isso ocorre porque o Visual Studio não é possível modificar o projeto do VBA no documento nessa situação.  
  
11. Clique em **Okey** na mensagem que é exibida. Esta mensagem lembra você de que, se você adicionar o VBA de código para a pasta de trabalho ou ao executar o projeto a partir de documento [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], o código do VBA serão perdido na próxima vez que você compila o projeto. Isso ocorre porque o documento na compilação de pasta é substituída sempre que você compilar o projeto de saída.  
  
     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar no assembly. O Visual Studio também adiciona um método chamado `GetManagedClass` para o projeto do VBA. Você pode chamar esse método em qualquer lugar no projeto VBA para acessar a classe que é exposto ao VBA.  
  
12. Compile o projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md)   
 [Passo a passo: Chamar o código de VBA em um Visual C&#35; projeto](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)   
 [Como: expor o código para VBA em um projeto do Visual Basic](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)  
  
  