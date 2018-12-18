---
title: 'Como: criar associações de arquivo para um aplicativo ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: fd1bd7965f0277ce1d3d900be6ee10db097eeb3f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49909101"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>Como criar associações de arquivo para um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos podem ser associados com uma ou mais extensões de nome de arquivo, para que o aplicativo será iniciado automaticamente quando o usuário abre um arquivo desses tipos. Adicionando suporte à extensão de nome do arquivo para um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo é simples.  
  
### <a name="to-create-file-associations-for-a-clickonce-application"></a>Para criar associações de arquivo para um aplicativo ClickOnce  
  
1. Criar uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo normalmente, ou usar seu existente [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo.  
  
2. Abra o manifesto do aplicativo com um texto ou editor XML, como o bloco de notas.  
  
3. Encontre o elemento `assembly`. Para obter mais informações, consulte [ClickOnce Application Manifest](../deployment/clickonce-application-manifest.md) (Manifesto do aplicativo ClickOnce).  
  
4. Como um filho de `assembly` elemento, adicionar um `fileAssociation` elemento. O `fileAssociation` elemento tem quatro atributos:  
  
   - `extension`: A extensão de nome de arquivo que você deseja associar o aplicativo.  
  
   - `description`: Uma descrição do tipo de arquivo, que será exibido no shell do Windows.  
  
   - `progid`: Uma cadeia de caracteres que identifica exclusivamente o tipo de arquivo, para marcá-la no registro.  
  
   - `defaultIcon`: Um ícone a ser usado para esse tipo de arquivo. O ícone deve ser adicionado como um recurso de arquivo no manifesto do aplicativo. Para obter mais informações, consulte [Como incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).  
  
     Para obter um exemplo de `file` e `fileAssociation` elementos, consulte [ \<fileAssociation > elemento](../deployment/fileassociation-element-clickonce-application.md).  
  
5. Se você quiser associar mais de um tipo de arquivo com o aplicativo, adicionar mais `fileAssociation` elementos. Observe que o `progid` atributo deve ser diferente para cada um.  
  
6. Quando terminar com o manifesto do aplicativo, assine novamente o manifesto. Você pode fazer isso na linha de comando usando Mage.exe.  
  
    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`  
  
    Para obter mais informações, consulte [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)  
  
## <a name="see-also"></a>Consulte também  
 [\<fileAssociation > elemento](../deployment/fileassociation-element-clickonce-application.md)   
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)   
 [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)



