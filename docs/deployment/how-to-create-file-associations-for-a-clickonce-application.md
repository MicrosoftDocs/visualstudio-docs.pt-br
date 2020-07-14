---
title: Como criar associações de arquivo para um aplicativo ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 76ecc41a852d80319f8a171ed590eb73680d92cc
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382491"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>Como criar associações de arquivo para um aplicativo ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]os aplicativos podem ser associados a uma ou mais extensões de nome de arquivo, para que o aplicativo seja iniciado automaticamente quando o usuário abrir um arquivo desses tipos. Adicionar suporte à extensão de nome de arquivo a um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é simples.

### <a name="to-create-file-associations-for-a-clickonce-application"></a>Para criar associações de arquivo para um aplicativo ClickOnce

1. Crie um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo normalmente ou use seu aplicativo existente [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] .

2. Abra o manifesto do aplicativo com um editor de texto ou XML, como o bloco de notas.

3. Localize o elemento `assembly`. Para obter mais informações, confira [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md).

4. Como um filho do `assembly` elemento, adicione um `fileAssociation` elemento. O `fileAssociation` elemento tem quatro atributos:

   - `extension`: A extensão de nome de arquivo que você deseja associar ao aplicativo.

   - `description`: Uma descrição do tipo de arquivo, que será exibido no Shell do Windows.

   - `progid`: Uma cadeia de caracteres que identifica exclusivamente o tipo de arquivo, para marcá-lo no registro.

   - `defaultIcon`: Um ícone a ser usado para esse tipo de arquivo. O ícone deve ser adicionado como um recurso de arquivo no manifesto do aplicativo. Para obter mais informações, consulte [como: incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).

     Para obter um exemplo dos `file` `fileAssociation` elementos e, consulte [ \<fileAssociation> Element](../deployment/fileassociation-element-clickonce-application.md).

5. Se você quiser associar mais de um tipo de arquivo ao aplicativo, adicione outros `fileAssociation` elementos. Observe que o `progid` atributo deve ser diferente para cada um.

6. Depois de concluir o manifesto do aplicativo, assine novamente o manifesto. Você pode fazer isso na linha de comando usando *Mage.exe*.

    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`

    Para obter mais informações, consulte [Mage.exe (manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool).

## <a name="see-also"></a>Veja também
- [\<fileAssociation>elementos](../deployment/fileassociation-element-clickonce-application.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
- [Mage.exe (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)