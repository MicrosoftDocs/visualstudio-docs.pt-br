---
title: Gerenciar assinatura de assembly e de manifesto
ms.date: 02/17/2017
ms.technology: vs-ide-deployment
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 6c1ef36b-25f7-4ad0-b29a-51801b7a5420
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a17ce633515979ca7a3fd3ac5a7e1d8802996944
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770409"
---
# <a name="manage-assembly-and-manifest-signing"></a>Gerenciar assinatura de assembly e de manifesto

A assinatura de nome forte fornece a um componente de software uma identidade global exclusiva. Nomes fortes são usados para assegurar que o assembly não possa ser falsificado por outra pessoa e para assegurar que as dependências do componente e as instruções de configuração sejam mapeadas para o componente e a versão do componente corretos.

Um nome forte consiste na identidade do assembly (nome de texto simples, número de versão e informações de cultura), além de um token de chave pública e uma assinatura digital.

Para obter informações sobre como assinar assemblies em projetos do Visual Basic e do C#, confira [Criar e usar assemblies de nomes fortes](/dotnet/framework/app-domains/create-and-use-strong-named-assemblies).

Para obter informações sobre como assinar assemblies em projetos C++, consulte [assemblies de nome forte (C++/CLI)](/cpp/dotnet/strong-name-assemblies-assembly-signing-cpp-cli).

> [!NOTE]
> A assinatura de nome forte não protege contra a engenharia reversa do assembly. Para se proteger contra a engenharia reversa, confira a [Dotfuscator Community](dotfuscator/index.md).

## <a name="asset-types-and-signing"></a>Tipos de ativo e assinatura

Você pode assinar os manifestos de aplicativo e assemblies do .NET:

- Executáveis (*.exe*)

- Manifestos de aplicativo (*.exe.manifest*)

- Manifestos de implantação (*.application*)

- Assemblies do componente compartilhado (*.dll*)

Assine os seguintes tipos de ativo:

1. assemblies, se você desejar implantá-los no cache de assembly global (GAC).

2. Manifestos de aplicativo e de implantação do ClickOnce. O Visual Studio permite a assinatura por padrão desses aplicativos.

3. Assemblies de interoperabilidade primários, que são usados para a interoperabilidade COM. O utilitário TLBIMP impõe uma nomenclatura forte ao criar um assembly de interoperabilidade primário com base em uma biblioteca de tipos COM.

Em geral, você não deve assinar executáveis. Um componente de nome forte não pode referenciar um componente que não tem um nome forte implantado com o aplicativo. O Visual Studio não assina executáveis do aplicativo, mas em vez disso, assina o manifesto do aplicativo, que aponta para o executável de nome fraco. Evite assinar componentes particulares do aplicativo, pois sua assinatura pode dificultar o gerenciamento de dependências.

## <a name="how-to-sign-an-assembly-in-visual-studio"></a>Como assinar um assembly no Visual Studio

Assine um aplicativo ou um componente usando a guia **Assinatura** da janela de propriedades do projeto (clique com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e selecione **Propriedades**). Selecione a guia **Assinatura** e, em seguida, marque a caixa de seleção **Assinar o assembly**.

Especifique um arquivo de chave. Se você optar por criar um arquivo de chave, os novos arquivos de chave sempre serão criados no formato *.pfx*. É necessário um nome e uma senha para o novo arquivo.

> [!WARNING]
> Você sempre deve proteger o arquivo de chave com uma senha para evitar o uso por outra pessoa. Também é possível proteger as chaves usando provedores ou repositórios de certificados.

Você também pode apontar para uma chave já criada. Para obter mais informações de como criar chaves, confira [Criar um par de chaves pública/privada](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair).

Se você só tiver acesso a uma chave pública, use a assinatura com atraso para adiar a atribuição da chave. Habilite a assinatura com atraso selecionando a caixa de seleção **Somente sinal de atraso**. Um projeto assinado com atraso não é executado e não pode ser depurado. No entanto, você pode ignorar a verificação durante o desenvolvimento usando a [ferramenta de nome forte Sn.exe](/dotnet/framework/tools/sn-exe-strong-name-tool) com a opção `-Vr`.

Para obter informações sobre manifestos de assinatura, consulte [como assinar manifestos de aplicativo e implantação](../ide/how-to-sign-application-and-deployment-manifests.md).

## <a name="see-also"></a>Confira também

- [Assemblies de nome forte](/dotnet/framework/app-domains/strong-named-assemblies)
- [Assemblies de nome forte (C++/CLI)](/cpp/dotnet/strong-name-assemblies-assembly-signing-cpp-cli)
