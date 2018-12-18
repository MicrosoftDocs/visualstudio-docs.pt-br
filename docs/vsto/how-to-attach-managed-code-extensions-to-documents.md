---
title: 'Como: anexar extensões para documentos de código gerenciado'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], attaching
- documents [Office development in Visual Studio], managed code extensions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c6e39f27caf9d321bb83666d72114a9675091f03
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257031"
---
# <a name="how-to-attach-managed-code-extensions-to-documents"></a>Como: anexar extensões para documentos de código gerenciado
  Você pode anexar a um assembly de personalização a um documento existente do Microsoft Office Word ou uma pasta de trabalho do Microsoft Office Excel. O documento ou pasta de trabalho pode ser qualquer formato que oferece suporte a projetos do Microsoft Office e as ferramentas de desenvolvimento no Visual Studio. Para obter mais informações, consulte [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md).  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Para anexar uma personalização a um documento do Word ou Excel, use o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> método da <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe. Porque o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe é projetada para ser executado em um computador que não tenha o Microsoft Office instalado, você pode usar esse método em soluções que não estão diretamente relacionadas ao desenvolvimento do Microsoft Office (como um console ou aplicativo Windows Forms).  
  
> [!NOTE]  
>  A personalização não conseguirá carregar se o código espera que os controles que não tenha o documento especificado.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como eu faço para: anexar ou desanexar um assembly do VSTO a partir de um documento do Word?](http://go.microsoft.com/fwlink/?LinkId=136782).  
  
### <a name="to-attach-managed-code-extensions-to-a-document"></a>Para anexar extensões de código gerenciado a um documento  
  
1.  Em um projeto que não requer o Microsoft Office, como um aplicativo de console ou um projeto do Windows Forms, adicione uma referência para o *ServerDocument* e  *Dll* assemblies.  
  
2.  Adicione o seguinte **importações** ou **usando** instruções na parte superior do arquivo de código.  
  
     [!code-csharp[Trin_VstcoreDeployment#4](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#4)]
     [!code-vb[Trin_VstcoreDeployment#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#4)]  
  
3.  Chamar estático <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> método.  
  
     O seguinte exemplo de código usa o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> de sobrecarga. Essa sobrecarga toma o caminho completo do documento e uma <xref:System.Uri> que especifica o local do manifesto de implantação para a personalização que você deseja anexar ao documento. Este exemplo supõe que um documento do Word denominado **WordDocument1.docx** está na área de trabalho, e que o manifesto de implantação está localizado em uma pasta chamada **publicar** que também está na área de trabalho.  
  
     [!code-csharp[Trin_VstcoreDeployment#3](../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs#3)]
     [!code-vb[Trin_VstcoreDeployment#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb#3)]  
  
4.  Compile o projeto e executar o aplicativo no computador em que você deseja anexar a personalização. O computador deve ter o Visual Studio 2010 Tools for Office Runtime instalado.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)   
 [Como: remover as extensões de código gerenciado de documentos](../vsto/how-to-remove-managed-code-extensions-from-documents.md)   
 [Manifestos de aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md)  
  