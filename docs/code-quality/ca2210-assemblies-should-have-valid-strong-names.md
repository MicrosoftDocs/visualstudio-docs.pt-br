---
title: 'CA2210: os assemblies devem ter nomes fortes válidos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bd22b0e28859ea153466b58f5f27ab458f5aa529
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47858938"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210: os assemblies devem ter nomes fortes válidos

|||
|-|-|
|NomeDoTipo|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um assembly não está assinado com um nome forte, o nome forte não pôde ser verificado ou o nome forte não é válido sem as configurações do registro atual do computador.

## <a name="rule-description"></a>Descrição da regra

Esta regra recupera e verifica o nome forte de um assembly. Ocorre uma violação se qualquer uma das seguintes opções for verdadeira:

- O assembly não tem um nome forte.

- O assembly foi alterado depois de entrar.

- O assembly é assinado com atraso.

- O assembly foi assinado incorretamente ou a assinatura falhou.

- O assembly requer configurações do registro para passar pela verificação. Por exemplo, a ferramenta de nome forte (Sn.exe) foi usada para ignorar a verificação para o assembly.

O nome forte protege clientes do carregamento desconhecido de um assembly adulterado. Os assemblies sem nomes fortes não devem ser implantados fora de cenários muito limitados. Se você compartilhar ou distribuir assemblies não assinados corretamente, o assembly poderá ser adulterado, o Common Language Runtime poderá não carregar o assembly ou o usuário talvez precise desabilitar a verificação em seu computador. Um assembly sem um nome forte tem das seguintes desvantagens:

- Não não possível verificar suas origens.

- O common language runtime não pode avisar os usuários se o conteúdo do assembly tiver sido alterado.

- Ele não pode ser carregado no cache de assembly global.

Observe que, para carregar e analisar um assembly assinado com atraso, você deve desabilitar verificação para o assembly.

## <a name="how-to-fix-violations"></a>Como corrigir violações

### <a name="create-a-key-file"></a>Criar um arquivo de chave

Use um dos procedimentos a seguir:

- Use a ferramenta de vinculador de Assembly (Al.exe) fornecida pelo SDK do .NET Framework.

- Para o .NET Framework v 1.0 ou 1.1, use o <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> ou <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName> atributo.

- Para o [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)], use o `/keyfile` ou `/keycontainer` opção de compilador [/KEYFILE (especificar chave ou par de chaves para assinar um Assembly)](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly) ou [/KEYCONTAINER (especificar um contêiner de chave para assinar um Assembly)](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly) opção de vinculador em C++).

### <a name="sign-your-assembly-with-a-strong-name-in-visual-studio"></a>Assinar o assembly com um nome forte no Visual Studio

1. No Visual Studio, abra sua solução.

2. Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **propriedades.**

3. Clique o **Signing** guia e, em seguida, selecione o **assinar o assembly** caixa de seleção.

4. Partir **escolher um arquivo de chave de nome forte**, selecione **New**.

   O **criar chave de nome forte** janela será exibida.

5. Na **nome do arquivo de chave**, digite um nome para sua chave de nome forte.

6. Escolha se deseja proteger a chave com uma senha e, em seguida, clique em **Okey**.

7. Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **Build**.

### <a name="sign-your-assembly-with-a-strong-name-outside-visual-studio"></a>Assinar o assembly com um nome forte fora do Visual Studio

Use a ferramenta de nome forte (Sn.exe) que é fornecida pelo SDK do .NET Framework. Para saber mais, veja [Sn.exe (Ferramenta de Nome Forte)](/dotnet/framework/tools/sn-exe-strong-name-tool).

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprimir um aviso nessa regra somente se o assembly é usado em um ambiente em que viole o conteúdo não é uma preocupação.

## <a name="see-also"></a>Consulte também

- <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>
- <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
- [Como assinar um assembly com um nome forte](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [Sn.exe (Ferramenta Nome Forte)](/dotnet/framework/tools/sn-exe-strong-name-tool)