---
title: Opções de usuário da solução (. Suo) arquivo | Microsoft Docs
description: Saiba mais sobre o arquivo de opções de usuário da solução (. suo), que contém opções de solução por usuário em um arquivo de armazenamento estruturado armazenado em um formato binário.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a38eb865cf003f7a2f9bafde7b6e527ce24f2bd
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899609"
---
# <a name="solution-user-options-suo-file"></a>Arquivo .Suo (Solution User Options)
O arquivo de opções de usuário da solução (. suo) contém opções de solução por usuário. Esse arquivo não deve ser verificado no controle do código-fonte.

 O arquivo de opções de usuário da solução (. suo) é um arquivo de armazenamento estruturado ou composto, armazenado em um formato binário. Você salva as informações do usuário em fluxos com o nome do fluxo sendo a chave que será usada para identificar as informações no arquivo. suo. O arquivo de opções de usuário da solução é usado para armazenar as configurações de preferência do usuário e é criado automaticamente quando o Visual Studio salva uma solução.

 Quando o ambiente abre um arquivo. suo, ele enumera todos os VSPackages carregados no momento. Se um VSPackage implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> interface, o ambiente chamará o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> método no VSPackage solicitando que ele carregue todos os seus dados do arquivo. suo.

 É responsabilidade do VSPackage saber quais fluxos podem ter sido gravados no arquivo. suo. Para cada fluxo que ele escreveu, o VSPackage chama de volta para o ambiente por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> para carregar um fluxo específico que é identificado pela chave, que é o nome do fluxo. Em seguida, o ambiente chama de volta para o VSPackage para ler esse fluxo específico passando o nome do fluxo e um `IStream` ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> método.

 Nesse ponto, outra chamada é feita para `LoadUserOptions` ver se há outra seção do arquivo. suo que deve ser lida. Esse processo continua até que todos os fluxos de dados no arquivo. suo tenham sido lidos e processados pelo ambiente.

 Quando a solução é salva ou fechada, o ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> método com um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> método. Um valor `IStream` que contém as informações binárias a serem salvas é passado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> método, que, em seguida, grava as informações no arquivo. suo e chama o `SaveUserOptions` método novamente para ver se há outro fluxo de informações a ser gravado no arquivo. suo.

 Esses dois métodos, `SaveUserOptions` e `WriteUserOptions` , são chamados recursivamente para cada fluxo de informações a ser salvo no arquivo. suo, passando o ponteiro para `IVsSolutionPersistence` . Eles são chamados recursivamente para permitir a gravação de vários fluxos no arquivo. suo. Dessa forma, as informações do usuário são mantidas com a solução e há garantia de que estejam lá na próxima vez em que a solução for aberta.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [Soluções](../../extensibility/internals/solutions-overview.md)
