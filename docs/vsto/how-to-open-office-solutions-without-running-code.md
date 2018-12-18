---
title: 'Como: soluções do Office abertos sem executar código'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], opening
- opening Office solutions
- bypassing assemblies
- solutions [Office development in Visual Studio], opening
- assemblies [Office development in Visual Studio], bypassing
- Office documents [Office development in Visual Studio, opening without running code
- documents [Office development in Visual Studio], opening without running code
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f7ced7b38a4f32d96b397e7f9eebb1d40be03ae3
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254982"
---
# <a name="how-to-open-office-solutions-without-running-code"></a>Como: soluções do Office abertos sem executar código
  Uma solução do Microsoft Office criada com extensões de código gerenciado é executado, mesmo se a configuração de segurança no aplicativo do Office do usuário final é definida como alta. Isso ocorre porque a segurança de código do assembly .NET é gerenciada pelo Microsoft .NET Framework, não pelo Microsoft Office.  
  
 No entanto, há vezes quando você talvez queira abrir um documento sem executar o código. Por exemplo, código executado quando o documento é aberto pode alterar o conteúdo, mas você deseja atualizar a aparência do documento antes das alterações de código-lo. Ou você talvez queira enviar o documento com determinadas informações nele para alguém, e você não deseja que o código para executar e, possivelmente, alterar o conteúdo.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Há várias maneiras de abrir um documento ou pasta de trabalho que contém as extensões de código gerenciado sem executar o código do assembly.  
  
## <a name="to-bypass-the-assembly-by-using-the-shift-key"></a>Para ignorar o assembly usando a tecla Shift  
  
-   Abrir documentos e pastas de trabalho do **arquivo** menu enquanto mantém pressionada a **Shift** chave para evitar que o Word e Excel da geração de eventos de inicialização enquanto está abrindo o documento.  
  
    > [!NOTE]  
    >  Se você abrir um documento ou pasta de trabalho da **guia de Introdução** painel de tarefas, mantendo pressionada **Shift** não ignora o código. Além disso, mantendo pressionada a tecla SHIFT não impedir que eventos que está sendo gerado depois que o documento está aberto.  
  
     Esse método é útil se você quiser abrir um documento para fazer alterações sem o código em execução e alterar o documento pela primeira vez.  
  
## <a name="to-bypass-an-assembly-by-renaming-or-removing-it"></a>Para ignorar a um assembly renomeando ou removê-lo  
  
-   Se você tiver as permissões necessárias no computador onde o assembly está localizado, você pode renomear ou remover o assembly para que o documento ou pasta de trabalho não é possível encontrá-lo. Isso resulta em um erro que está sendo gerado sempre que o documento do Office é aberto.  
  
     Se a solução é usada por várias pessoas, esse método impede que a solução em execução para todos eles. Isso pode ser útil se um problema for encontrado no código ou em um servidor referenciado e você deseja parar todos os usuários de executá-lo.  
  
## <a name="see-also"></a>Consulte também  
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Manifestos de aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md)  
  
  