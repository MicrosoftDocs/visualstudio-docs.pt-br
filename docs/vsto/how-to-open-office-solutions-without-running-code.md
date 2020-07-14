---
title: 'Como: abrir soluções do Office sem executar código'
ms.date: 02/02/2017
ms.topic: how-to
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
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d84515c2c3159b61b96f77555b23eef0df0ae961
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543475"
---
# <a name="how-to-open-office-solutions-without-running-code"></a>Como: abrir soluções do Office sem executar código
  Uma solução Microsoft Office criada com extensões de código gerenciado é executada mesmo se a configuração de segurança no aplicativo do Office do usuário final estiver definida como alta. Isso ocorre porque a segurança do código do assembly .NET é gerenciada pelo Microsoft .NET Framework, não por Microsoft Office.

 No entanto, há ocasiões em que você talvez queira abrir um documento sem executar o código. Por exemplo, o código que é executado quando o documento é aberto pode alterar o conteúdo, mas você deseja atualizar a aparência do documento antes de o código alterá-lo. Ou talvez você queira enviar o documento com determinadas informações para alguém e não quer que o código seja executado e possivelmente alterar o conteúdo.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Há várias maneiras de abrir um documento ou pasta de trabalho que contém extensões de código gerenciado sem executar o código do assembly.

## <a name="to-bypass-the-assembly-by-using-the-shift-key"></a>Para ignorar o assembly usando a tecla Shift

- Abra documentos e pastas de trabalho no menu **arquivo** enquanto mantém a tecla **Shift** pressionada para impedir que o Word e o Excel prolançam eventos de inicialização enquanto o documento está sendo aberto.

    > [!NOTE]
    > Se você abrir um documento ou pasta de trabalho no painel de tarefas **introdução** , manter pressionada a **tecla Shift** não ignorará o código. Além disso, manter pressionada a tecla SHIFT não impede que os eventos sejam gerados depois que o documento é aberto.

     Esse método será útil se você quiser abrir um documento para fazer alterações sem o código em execução e alterar o documento primeiro.

## <a name="to-bypass-an-assembly-by-renaming-or-removing-it"></a>Para ignorar um assembly renomeando-o ou removendo-o

- Se você tiver as permissões necessárias no computador em que o assembly está localizado, poderá renomear ou remover o assembly para que o documento ou pasta de trabalho não possa localizá-lo. Isso resulta em um erro gerado toda vez que o documento do Office é aberto.

     Se a solução for usada por várias pessoas, esse método impedirá que a solução seja executada para todos eles. Isso pode ser útil se um problema for encontrado no código ou em um servidor referenciado e você quiser impedir que todos os usuários o executem.

## <a name="see-also"></a>Confira também
- [Proteger soluções do Office](../vsto/securing-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Manifestos de aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md)
