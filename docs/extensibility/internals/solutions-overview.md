---
title: Visão geral das soluções
description: Saiba mais sobre os internos de uma solução para os desenvolvedores de extensão que desejam trabalhar com soluções nas extensões do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 914f1744accc10eb55cfb0b321a04560c27bca05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069368"
---
# <a name="solutions-overview"></a>Visão geral das soluções

Uma solução é um agrupamento de um ou mais projetos que trabalham juntos para criar um aplicativo. As informações de projeto e status relacionadas à solução são armazenadas em dois arquivos de solução diferentes. O [arquivo da solução (. sln)](solution-dot-sln-file.md) é baseado em texto e pode ser colocado no controle do código-fonte e compartilhado entre os usuários. O [arquivo da opção de usuário da solução (. suo)](solution-user-options-dot-suo-file.md) é binário. Como resultado, o arquivo. suo não pode ser colocado no controle do código-fonte e contém informações específicas do usuário.

Qualquer VSPackage pode gravar em qualquer tipo de arquivo de solução. Devido à natureza dos arquivos, há duas interfaces diferentes implementadas para gravar nelas. A <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> interface grava informações de texto no arquivo. sln e a <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> interface grava fluxos binários no arquivo. suo.

> [!NOTE]
> Um projeto não precisa gravar explicitamente uma entrada para si mesmo no arquivo da solução; o ambiente manipula o para o projeto. Portanto, a menos que você queira adicionar mais conteúdo especificamente ao arquivo de solução, não é necessário registrar seu VSPackage dessa maneira.

Cada VSPackage com suporte à persistência de solução usa três interfaces, a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> interface, que é implementada pelo ambiente e chamada pelo VSPackage, e `IVsPersistSolutionProps` e `IVsPersistSolutionOpts` , que são implementadas pelo VSPackage. A `IVsPersistSolutionOpts` interface só precisa ser implementada se as informações particulares forem gravadas pelo VSPackage no arquivo. suo.

Quando uma solução é aberta, ocorre o processo a seguir.

1. O ambiente lê a solução.

2. Se o ambiente encontrar um `CLSID` , ele carregará o VSPackage correspondente.

3. Se um VSPackage for carregado, o ambiente chamará a `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> interface para a interface que o VSPackage exige.

   - Ao ler de um arquivo. sln, o ambiente chama `QueryInterface` para `IVsPersistSolutionProps` .

   - Ao ler de um arquivo. suo, o ambiente chama `QueryInterface` para `IVsPersistSolutionOpts` .

   Informações específicas relacionadas ao uso desses arquivos podem ser encontradas em [solução (. Sln)](../../extensibility/internals/solution-dot-sln-file.md) opções de [usuário de solução e arquivo (. Suo)](../../extensibility/internals/solution-user-options-dot-suo-file.md).

> [!NOTE]
> Se você quiser criar uma nova configuração de solução consistindo em duas configurações de projetos e excluindo uma terceira da compilação, será necessário usar a interface do usuário de páginas de propriedades ou automação. Você não pode alterar as configurações do Gerenciador de compilação de solução e suas propriedades diretamente, mas você pode manipular o Gerenciador de compilação da solução usando a `SolutionBuild` classe do DTE no modelo de automação. Para obter mais informações sobre como configurar soluções, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
