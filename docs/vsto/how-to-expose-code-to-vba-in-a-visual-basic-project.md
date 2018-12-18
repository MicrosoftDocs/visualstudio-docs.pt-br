---
title: 'Como: expor o código para VBA em um projeto do Visual Basic'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7e4bc9f4227c11f8e34838a2785b27da62a0a6b8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839642"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>Como: expor o código para VBA em um projeto do Visual Basic
  Você pode expor o código em um [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto ao Visual Basic para código Applications (VBA), se você quiser que os dois tipos de código para interagir entre si.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 O processo do Visual Basic é diferente do processo Visual c#. Para obter mais informações, consulte [como: expor o código para VBA em um Visual C&#35; projeto](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md).  
  
 O processo é diferente para o código em uma classe de item de host para o código em outras classes:  
  
- [Expor o código em uma classe de item de host](#HostItemCode)  
  
- [Expor o código que não está em uma classe de item de host](#NonHostItem)  
  
  ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como o VSTO chame i: código do VBA?](http://go.microsoft.com/fwlink/?LinkId=136757).  
  
##  <a name="HostItemCode"></a> Expor o código em uma classe de item de host  
 Para habilitar o código do VBA chamar o código do Visual Basic em uma classe de item de host, defina as **EnableVbaCallers** propriedade do item de host para **verdadeiro**.  
  
 Para um passo a passo que demonstra como expor um método de uma classe de item de host e, em seguida, chame-o do VBA, consulte [instruções passo a passo: chamar o código do VBA em um projeto do Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md). Para obter mais informações sobre itens de host, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
#### <a name="to-expose-code-in-a-host-item-to-vba"></a>Para expor o código em um item de host para o VBA  
  
1.  Abra ou crie um nível de documento [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto com base em um documento do Word, a pasta de trabalho do Excel ou o modelo do Excel que dá suporte a macros e que já contenha código VBA.  
  
     Para obter mais informações sobre os formatos de arquivo do documento que dão suporte a macros, consulte [combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md).  
  
    > [!NOTE]  
    >  Esse recurso não pode ser usado em projetos de modelo do Word.  
  
2.  Certifique-se de que o código VBA no documento tem permissão para executar sem avisar o usuário para habilitar as macros. Você pode confiar em código VBA de execução, adicionando o local do projeto do Office para a lista de locais confiáveis nas configurações do Centro de confiabilidade para Word ou Excel.  
  
3.  Adicione a propriedade, método ou evento que você deseja expor ao VBA para uma das classes de item de host em seu projeto e declarar o novo membro como **público**. O nome da classe depende do aplicativo:  
  
    -   Em uma palavra projeto, a classe de item de host é chamada `ThisDocument` por padrão.  
  
    -   Em um projeto do Excel, as classes de item de host são nomeadas `ThisWorkbook`, `Sheet1`, `Sheet2`, e `Sheet3` por padrão.  
  
4.  Defina as **EnableVbaCallers** propriedade para o item de host para **verdadeiro**. Essa propriedade está disponível na **propriedades** janela quando o item de host é aberto no designer.  
  
     Depois de definir essa propriedade, o Visual Studio define automaticamente a **ReferenceAssemblyFromVbaProject** propriedade **verdadeiro**.  
  
    > [!NOTE]  
    >  Se a pasta de trabalho ou o documento ainda não contiver código VBA, ou se o código do VBA no documento não é confiável para ser executado, você receberá uma mensagem de erro ao definir a **EnableVbaCallers** propriedade **verdadeiro**. Isso ocorre porque o Visual Studio não é possível modificar o projeto do VBA no documento nessa situação.  
  
5.  Clique em **Okey** na mensagem que é exibida. Esta mensagem lembra você de que, se você adicionar o código do VBA para a pasta de trabalho ou o documento enquanto você está executando o projeto do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], o código do VBA serão perdido na próxima vez que você compilar o projeto. Isso ocorre porque o documento na pasta de saída de compilação é substituído sempre que você compilar o projeto.  
  
     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar no assembly. O Visual Studio também adiciona uma propriedade chamada `CallVSTOAssembly` para o `ThisDocument`, `ThisWorkbook`, `Sheet1`, `Sheet2`, ou `Sheet3` módulo no projeto do VBA. Você pode usar essa propriedade para acessar membros públicos da classe que é exposto ao VBA.  
  
6.  Compile o projeto.  
  
##  <a name="NonHostItem"></a> Expor o código que não está em uma classe de item de host  
 Para habilitar o código do VBA chamar o código do Visual Basic que não está em uma classe de item de host, modifique o código para que fique visível para o VBA.  
  
### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>Para expor o código que não está em uma classe de item de host para o VBA  
  
1.  Abra ou crie um nível de documento [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] projeto com base em um documento do Word, a pasta de trabalho do Excel ou o modelo do Excel que dá suporte a macros e que já contenha código VBA.  
  
     Para obter mais informações sobre os formatos de arquivo do documento que dão suporte a macros, consulte [combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md).  
  
    > [!NOTE]  
    >  Esse recurso não pode ser usado em projetos de modelo do Word.  
  
2.  Certifique-se de que o código VBA no documento tem permissão para executar sem avisar o usuário para habilitar as macros. Você pode confiar em código VBA de execução, adicionando o local do projeto do Office para a lista de locais confiáveis nas configurações do Centro de confiabilidade para Word ou Excel.  
  
3.  Adicionar o membro que você deseja expor ao VBA para uma classe pública em seu projeto e declarar o novo membro como **público**.  
  
4.  Aplicar o seguinte <xref:System.Runtime.InteropServices.ComVisibleAttribute> e <xref:Microsoft.VisualBasic.ComClassAttribute> atributos à classe que você está expondo ao VBA. Esses atributos torná-la visível ao VBA.  
  
    ```vb  
    <Microsoft.VisualBasic.ComClass()> _  
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _  
    ```  
  
5.  Substituir a **GetAutomationObject** método de uma classe de item de host em seu projeto para retornar uma instância da classe que você está expondo ao VBA. O exemplo de código a seguir pressupõe que você está expondo uma classe chamada `DocumentUtilities` ao VBA.  
  
    ```vb  
    Protected Overrides Function GetAutomationObject() As Object  
        Return New DocumentUtilities()  
    End Function  
    ```  
  
6.  Abrir o documento (para o Word) ou o designer de planilha (para Excel) em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
7.  No **propriedades** janela, selecione a **ReferenceAssemblyFromVbaProject** propriedade e altere o valor para **verdadeiro**.  
  
    > [!NOTE]  
    >  Se a pasta de trabalho ou o documento ainda não contiver código VBA, ou se o código do VBA no documento não é confiável para ser executado, você receberá uma mensagem de erro ao definir a **ReferenceAssemblyFromVbaProject** propriedade **True** . Isso ocorre porque o Visual Studio não é possível modificar o projeto do VBA no documento nessa situação.  
  
8.  Clique em **Okey** na mensagem que é exibida. Esta mensagem lembra você de que, se você adicionar o código do VBA para a pasta de trabalho ou o documento enquanto você está executando o projeto do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], o código do VBA serão perdido na próxima vez que você compilar o projeto. Isso ocorre porque o documento na pasta de saída de compilação é substituído sempre que você compilar o projeto.  
  
     Neste ponto, o Visual Studio configura o projeto para que o projeto do VBA possa chamar no assembly. O Visual Studio também adiciona um método chamado `GetManagedClass` para o projeto do VBA. Você pode chamar esse método em qualquer lugar no projeto VBA para acessar a classe que é exposto ao VBA.  
  
9. Compile o projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Combinar o VBA e personalizações no nível de documento](../vsto/combining-vba-and-document-level-customizations.md)   
 [Passo a passo: Chamar o código do VBA em um projeto do Visual Basic](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)   
 [Como: expor o código para VBA em um Visual C&#35; projeto](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)  
  
  