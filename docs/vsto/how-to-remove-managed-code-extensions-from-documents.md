---
title: Como remover extensões de código gerenciado de documentos
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3b4f5cb3098289463cea7e650332583ec7b12258
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541304"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>Como remover extensões de código gerenciado de documentos
  Você pode remover programaticamente o assembly de personalização de um documento ou pasta de trabalho que faz parte de uma personalização em nível de documento para Microsoft Office Word ou Microsoft Office Excel. Os usuários podem abrir os documentos e exibir o conteúdo, mas qualquer interface do usuário personalizada (IU) que você adicionar aos documentos não será exibida e seu código não será executado.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Você pode remover o assembly de personalização usando um dos `RemoveCustomization` métodos fornecidos pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] . O método usado depende se você deseja remover a personalização em tempo de execução (ou seja, executando o código na personalização enquanto o documento do Word ou a pasta de trabalho do Excel está aberta) ou se deseja remover a personalização de um documento fechado ou de um documento que está em um servidor que não tem Microsoft Office instalado.

## <a name="to-remove-the-customization-assembly-at-run-time"></a>Para remover o assembly de personalização em tempo de execução

1. No código de personalização, chame o <xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> método (para Word) ou o <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> método (para Excel). Esse método deve ser chamado somente depois que a personalização não for mais necessária.

     O local em que você chama esse método em seu código depende de como sua personalização é usada. Por exemplo, se os clientes usarem os recursos de personalização até que estejam prontos para enviar o documento para outros clientes que só precisam do próprio documento (não a personalização), você poderá fornecer uma interface do usuário que chame `RemoveCustomization` quando o cliente clicar nele. Como alternativa, se a personalização popular o documento com dados quando ele for aberto pela primeira vez, mas a personalização não fornecer outros recursos que são acessados diretamente pelos clientes, você poderá chamar RemoveCustomization assim que a personalização terminar de inicializar o documento.

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>Para remover o assembly de personalização de um documento fechado ou de um documento em um servidor

1. Em um projeto que não requer Microsoft Office, como um aplicativo de console ou Windows Forms projeto, adicione uma referência ao assembly *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* .

2. Adicione as seguintes **importações** ou **use** a instrução na parte superior do seu arquivo de código.

     [!code-csharp[Trin_VstcoreDeployment#1](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#1)]
     [!code-vb[Trin_VstcoreDeployment#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#1)]

3. Chame o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> método estático da <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe e especifique o caminho do documento da solução para o parâmetro.

     O exemplo de código a seguir pressupõe que você está removendo a personalização de um documento chamado *WordDocument1.docx* que está na área de trabalho.

     [!code-csharp[Trin_VstcoreDeployment#2](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#2)]
     [!code-vb[Trin_VstcoreDeployment#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#2)]

4. Compile o projeto e execute o aplicativo no computador em que você deseja remover a personalização. O computador deve ter o tempo de execução do Visual Studio 2010 Tools for Office instalado.

## <a name="see-also"></a>Consulte também
- [Gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [Como: anexar extensões de código gerenciado a documentos](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
