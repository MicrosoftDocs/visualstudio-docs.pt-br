---
title: A cadeia de caracteres de conexão contém credenciais com uma senha de texto não criptografado e não está usando segurança integrada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 501d85af-92e0-4471-b280-8a59c0688575
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f1ec13cab1b8c41225cb1934740b8dd3e7f59ac0
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49230861"
---
# <a name="the-connection-string-contains-credentials-with-a-clear-text-password-and-is-not-using-integrated-security"></a>A cadeia de conexão contém credenciais com uma senha de texto não criptografado e não estiver usando segurança integrada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Deseja salvar a cadeia de conexão no arquivo DBML atual e nos arquivos de configuração do aplicativo com essas informações confidenciais?  Clique em Não para salvar a cadeia de conexão sem as informações confidenciais.  
  
 Ao trabalhar com conexões de dados que incluem informações confidenciais (senhas que são incluídas na cadeia de conexão), você tem a opção de salvar a cadeia de conexão no arquivo DBML de um projeto e o arquivo de configuração do aplicativo com ou sem informações sigilosas.  
  
> [!WARNING]
>  Definir explicitamente o **Conexão** propriedades **configurações do aplicativo** propriedade a ser **False** adicionará a senha para o arquivo DBML.  
  
### <a name="to-save-the-connection-string-with-the-sensitive-information-in-the-projects-application-settings"></a>Para salvar a cadeia de conexão com informações sigilosas nas configurações de aplicativo do projeto  
  
-   Clique em **Sim**.  
  
     A cadeia de conexão é armazenada como uma configuração de aplicativo. A cadeia de conexão inclui informações sigilosas em texto sem formatação. O arquivo DBML não contém informações sigilosas.  
  
### <a name="to-save-the-connection-string-without-the-sensitive-information-in-the-projects-application-settings"></a>Para salvar a cadeia de conexão sem informações sigilosas nas configurações de aplicativo do projeto  
  
-   Clique em **Não**.  
  
     A cadeia de conexão é armazenada como uma configuração de aplicativo, mas a senha não é incluído.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)

