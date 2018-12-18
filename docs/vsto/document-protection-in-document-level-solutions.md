---
title: Proteção de documento em soluções de nível de documento
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio], restricted permissions
- documents [Office development in Visual Studio], restricted permissions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 22c8f135770fbd427d361b9c9b113da3b20e609a
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34447863"
---
# <a name="document-protection-in-document-level-solutions"></a>Proteção de documento em soluções de nível de documento
  Você pode usar os recursos de proteção do Microsoft Office Word e Microsoft Office Excel em projetos no nível de documento. Esses recursos impedir que usuários não autorizados façam alterações protegidos partes de um documento.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Usando o Excel, você pode ativar a proteção e desativar enquanto a pasta de trabalho estiver aberta no designer. Usando o Word, você pode ativar proteção somente fora do designer. Em tempo de execução, você pode habilitar ou desabilitar a proteção por meio de programação para Word e Excel.  
  
 Quando a proteção de documento está habilitada em um documento que está aberto no designer, todos os controles são removidos do **caixa de ferramentas** ou ficam disponíveis, e você não pode arrastar desde o **fontes de dados** janela do documento.  
  
## <a name="serverdocument-and-protected-documents"></a>ServerDocument e documentos protegidos  
 Se um documento está protegido, o cache de dados não pode ser acessado de fora do documento. Não é possível usar o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> de classe para recuperar ou manipular dados armazenados em cache em um documento protegido, ou usar outros métodos do <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ServerDocument> classe.  
  
## <a name="word-document-protection-in-the-designer"></a>Proteção de documentos do Word no designer  
 Se você adicionar proteção a um documento do Word ou o modelo enquanto ele está aberto no Visual Studio, você não pode iniciar a imposição de proteção no designer. O documento está no modo de design enquanto ele está aberto no Visual Studio e execução deverá ser no modo antes de iniciar a imposição de proteção.  
  
 No entanto, se você criar um projeto que usa um documento do Word existente que tem proteção habilitada, o documento é protegido ao abrir no designer. Você não pode editar as partes protegidas do documento, mas ainda é possível escrever código no Editor de códigos para automatizar o documento. Você também não é possível compilar o projeto se a proteção está habilitada, enquanto o documento está aberto no Visual Studio.  
  
 Você pode desativar proteção, enquanto o documento está aberto no designer de forma que você pode editar o documento e compilar o projeto. Você não pode desativar a proteção para a cópia no designer enquanto você está depurando; o documento que é aberta durante a depuração é uma cópia separada de uma aberta no designer (a cópia de saída é armazenada no *\bin* diretório para o Visual Basic e o *\bin\debug* diretório c#).  
  
 Você pode habilitar a proteção na cópia do documento que é aberto no designer de fechar o projeto no Visual Studio, abrindo a cópia do documento que está no diretório do projeto e ativar a proteção.  
  
## <a name="enforce-word-document-protection-on-build"></a>Aplicar a proteção de documento do Word na compilação  
 Visual Studio inicia a imposição de proteção de documentos do Word e modelos durante o processo de compilação, para que a proteção é habilitada quando o documento é aberto para depuração. O documento está protegido com uma senha vazia.  
  
 A proteção é habilitado durante a compilação assim que se houver código no documento <xref:Microsoft.Office.Tools.Word.Document.Startup> eventos que podem causar exceções ou alterar o comportamento do aplicativo, esse código pode ser depurado corretamente. Se você habilitar a proteção depois que o documento for aberto, o código de inicialização não pode ser depurado ou testado.  
  
## <a name="setting-the-password"></a>Definir a senha  
 O Visual Studio automaticamente habilita a proteção, mas não fornece nenhuma senha por padrão. Se você quiser que a proteção de documento para ter uma senha, você deve adicioná-lo antes de implantar sua solução. Adicionar uma senha permite que você permitir que os usuários autorizados remover a proteção de documento. sem uma senha, não pode ser facilmente remover a proteção. Para obter detalhes sobre como definir uma senha, consulte a Ajuda no aplicativo do Office específico.  
  
## <a name="see-also"></a>Consulte também  
 [Como: programaticamente proteger documentos e partes de documentos](../vsto/how-to-programmatically-protect-documents-and-parts-of-documents.md)   
 [Explicações passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Gerenciamento de direitos de informação e visão geral de extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Como: permitir que o código seja executado atrás de documentos com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  