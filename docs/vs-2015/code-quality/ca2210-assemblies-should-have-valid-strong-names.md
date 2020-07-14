---
title: 'CA2210: assemblies devem ter nomes fortes válidos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8f800a550717abfabdfb9296fc8f6de49d127d73
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548194"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210: Assemblies devem ter nomes fortes válidos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um assembly não está assinado com um nome forte, o nome forte não pôde ser verificado ou o nome forte não seria válido sem as configurações atuais do registro do computador.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra recupera e verifica o nome forte de um assembly. Uma violação ocorrerá se qualquer uma das seguintes opções for verdadeira:

- O assembly não tem um nome forte.

- O assembly foi alterado após a assinatura.

- O assembly é assinado com atraso.

- O assembly foi assinado incorretamente ou a assinatura falhou.

- O assembly requer que as configurações do registro passem na verificação. Por exemplo, a ferramenta de nome forte (Sn.exe) foi usada para ignorar a verificação para o assembly.

  O nome forte protege clientes do carregamento desconhecido de um assembly adulterado. Os assemblies sem nomes fortes não devem ser implantados fora de cenários muito limitados. Se você compartilhar ou distribuir assemblies não assinados corretamente, o assembly poderá ser adulterado, o Common Language Runtime poderá não carregar o assembly ou o usuário talvez precise desabilitar a verificação em seu computador. Um assembly sem um nome forte tem as seguintes desvantagens:

- Suas origens não podem ser verificadas.

- O Common Language Runtime não pode avisar os usuários se o conteúdo do assembly tiver sido alterado.

- Ele não pode ser carregado no cache de assembly global.

  Observe que para carregar e analisar um assembly com assinatura atrasada, você deve desabilitar a verificação para o assembly.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 **Para criar um arquivo de chave**

 Use um dos seguintes procedimentos:

- Use a ferramenta do vinculador de assembly (Al.exe) fornecida pelo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK.

- Para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] v 1.0 ou v 1.1, use o <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> atributo ou <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName> .

- Para o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] , use a `/keyfile` opção de `/keycontainer` compilador ou [/keyfile (especifique chave ou par de chaves para assinar um assembly)](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06) ou [/keycontainer (especifique um contêiner de chave para assinar um assembly)](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e) opção de vinculador em C++).

  **Para assinar seu assembly com um nome forte no Visual Studio**

1. No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra sua solução.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e clique em **Propriedades.**

3. Clique na guia **assinatura** e marque a caixa de seleção **assinar o assembly** .

4. Em **escolher um arquivo de chave de nome forte**, selecione **novo**.

    A janela **criar chave de nome forte** será exibida.

5. Em **nome do arquivo de chave**, digite um nome para a chave de nome forte.

6. Escolha se deseja proteger a chave com uma senha e clique em **OK**.

7. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e clique em **Compilar**.

   **Para assinar seu assembly com um nome forte fora do Visual Studio**

- Use a ferramenta de nome forte (Sn.exe) fornecida pelo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK. Para obter mais informações, consulte [Sn.exe (Strong Name Tool)](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Apenas suprimir um aviso dessa regra se o assembly for usado em um ambiente em que a violação do conteúdo não seja uma preocupação.

## <a name="see-also"></a>Consulte Também
 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
 [Como assinar um assembly com um nome forte](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67) [Sn.exe (ferramenta de nome forte)](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)
