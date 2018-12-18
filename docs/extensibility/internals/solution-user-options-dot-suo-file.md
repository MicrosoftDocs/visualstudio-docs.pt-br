---
title: Opções de usuário de solução (. Arquivo suo) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0b96e3ad2ec29402dddc7354df46293b99bac3ec
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130841"
---
# <a name="solution-user-options-suo-file"></a>Opções de usuário de solução (. Arquivo suo)
O arquivo de opções (. suo) do usuário de solução contém opções de solução por usuário. Esse arquivo não deve fazer check-in de controle do código fonte.  
  
 O arquivo de opções (. suo) do usuário de solução é um armazenamento estruturado ou composto, um arquivo armazenado em um formato binário. Você pode salvar informações de usuário em fluxos com o nome do fluxo que está sendo a chave que será usada para identificar as informações no arquivo. suo. O arquivo de opções de usuário de solução é usado para armazenar as configurações de preferências do usuário e é criado automaticamente quando o Visual Studio salva uma solução.  
  
 Quando o ambiente de abre um arquivo. suo, enumera todos os VSPackages carregados atualmente. Se um VSPackage implementa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> interface, então o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> método sobre o VSPackage perguntando ao carregar todos os seus dados do arquivo. suo.  
  
 É responsabilidade do VSPackage saber o que o fluxos pode ter gravado no arquivo. suo. Para cada fluxo que escreveu, o VSPackage chama de volta para o ambiente por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> para carregar um fluxo específico que é identificado pela chave, que é o nome do fluxo. O ambiente, em seguida, chama o VSPackage para leitura nesse fluxo específico passando o nome do fluxo e um `IStream` ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> método.  
  
 Nesse ponto, a outra chamada é feita para `LoadUserOptions` para ver se há outra seção do arquivo. suo que deve ser lidos. Esse processo continua até que todos os fluxos de dados no arquivo. suo são lidos e processados pelo ambiente.  
  
 Quando a solução é salvo ou fechada, o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> método com um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> método. Um `IStream` que contém as informações de binárias a serem salvas é passado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> método, que grava as informações de arquivo. suo e chama o `SaveUserOptions` método novamente para ver se há outro fluxo de informações para gravar a. suo arquivo.  
  
 Esses dois métodos, `SaveUserOptions` e `WriteUserOptions`, são chamados recursivamente para cada fluxo de informações a serem salvas no arquivo. suo, passando o ponteiro para `IVsSolutionPersistence`. Eles são chamados recursivamente para permitir a gravação de vários fluxos para o arquivo. suo. Dessa forma, informações do usuário são mantidas com a solução em são garantidas como existe na próxima vez em que a solução é aberta.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>   
 [Soluções](../../extensibility/internals/solutions.md)