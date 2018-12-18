---
title: 'CA2210: Os Assemblies devem ter nomes fortes válidos | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1551cccb11fc33a21503e7030cfd671c953ee17d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49865811"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210: os assemblies devem ter nomes fortes válidos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um assembly não está assinado com um nome forte, o nome forte não pôde ser verificado ou o nome forte não é válido sem as configurações do registro atual do computador.

## <a name="rule-description"></a>Descrição da Regra
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

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 **Para criar um arquivo de chave**

 Use um dos procedimentos a seguir:

- Use a ferramenta de vinculador de Assembly (Al.exe) fornecida pelo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK.

- Para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] versão 1.0 ou 1.1, use o <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> ou <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName> atributo.

- Para o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)], use o `/keyfile` ou `/keycontainer` opção de compilador [/KEYFILE (especificar chave ou par de chaves para assinar um Assembly)](http://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06) ou [/KEYCONTAINER (especificar um contêiner de chave para assinar um Assembly)](http://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e) opção de vinculador em C++).

  **Para assinar o assembly com um nome forte no Visual Studio**

1. No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra sua solução.

2. Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **propriedades.**

3. Clique o **Signing** guia e, em seguida, selecione o **assinar o assembly** caixa de seleção.

4. Partir **escolher um arquivo de chave de nome forte**, selecione **New**.

    O **criar chave de nome forte** janela será exibida.

5. Na **nome do arquivo de chave**, digite um nome para sua chave de nome forte.

6. Escolha se deseja proteger a chave com uma senha e, em seguida, clique em **Okey**.

7. Na **Gerenciador de soluções**, clique em seu projeto e, em seguida, clique em **Build**.

   **Para assinar o assembly com um nome forte fora do Visual Studio**

-   Use a ferramenta de nome forte (Sn.exe) que é fornecida pelo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK. Para saber mais, veja [Sn.exe (Ferramenta de Nome Forte)](http://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso nessa regra somente se o assembly é usado em um ambiente em que viole o conteúdo não é uma preocupação.

## <a name="see-also"></a>Consulte também
 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
 [Como: assinar um Assembly com um nome forte](http://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67) [Sn.exe (ferramenta nome forte)](http://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)



