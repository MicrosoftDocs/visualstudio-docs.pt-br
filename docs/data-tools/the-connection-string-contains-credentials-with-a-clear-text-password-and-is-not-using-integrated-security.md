---
title: A cadeia de conexão contém credenciais com uma senha de texto não criptografado e não estiver usando segurança integrada
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 501d85af-92e0-4471-b280-8a59c0688575
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 201d01d5891b1d788245b2ce61b09f43a50731b1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281468"
---
# <a name="the-connection-string-contains-credentials-with-a-clear-text-password-and-is-not-using-integrated-security"></a>A cadeia de conexão contém credenciais com uma senha de texto não criptografado e não estiver usando segurança integrada

Deseja salvar a cadeia de conexão no arquivo DBML atual e nos arquivos de configuração do aplicativo com essas informações confidenciais?  Clique em **Não** para salvar a cadeia de conexão sem as informações confidenciais.

Ao trabalhar com conexões de dados que incluem informações confidenciais (senhas que são incluídas na cadeia de conexão), você tem a opção de salvar a cadeia de conexão no arquivo DBML de um projeto e o arquivo de configuração do aplicativo com ou sem informações sigilosas.

> [!WARNING]
> Explicitamente definindo a propriedade de **Configurações do Aplicativo** propriedades de **Conexão** a **False** adicionará a senha para o arquivo DBML.

## <a name="save-options"></a>Opções de salvamento

- Para salvar a cadeia de conexão com as informações confidenciais, escolha **Sim**.

   A cadeia de conexão é armazenada como uma configuração de aplicativo. A cadeia de conexão inclui informações sigilosas em texto sem formatação. O arquivo DBML não contém informações sigilosas.

- Para salvar a cadeia de conexão sem as informações confidenciais, escolha **não**.

   A cadeia de conexão é armazenada como uma configuração de aplicativo, mas a senha não é incluído.

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
