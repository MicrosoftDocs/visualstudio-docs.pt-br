---
title: 'CA1824: Marcar assemblies com NeutralResourcesLanguageAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1824
- MarkAssembliesWithNeutralResourcesLanguage
helpviewer_keywords:
- MarkAssembliesWithNeutralResourcesLanguage
- CA1824
ms.assetid: 10e97f8a-aa6e-47aa-b253-1e5d3a295d82
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 19077a63d5aa22bda3f968943703a82488e2745d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545282"
---
# <a name="ca1824-mark-assemblies-with-neutralresourceslanguageattribute"></a>CA1824: Marque assemblies com NeutralResourcesLanguageAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um assembly contém um recurso baseado em **resx**, mas não tem o <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName> aplicado a ele.

## <a name="rule-description"></a>Descrição da Regra
 O atributo **NeutralResourcesLanguage** informa o **ResourceManager** do idioma que foi usado para exibir os recursos da cultura neutra para um assembly. Quando ele pesquisa recursos na mesma cultura que o idioma de recursos neutros, o **ResourceManager** usa automaticamente os recursos que estão localizados no assembly principal. Ele faz isso em vez de procurar um assembly satélite que tenha a cultura da interface do usuário atual para o thread atual. Isso melhora o desempenho da pesquisa para o primeiro recurso carregado e pode reduzir o conjunto de trabalho.

## <a name="fixing-violations"></a>Corrigindo violações
 Para corrigir uma violação dessa regra, adicione o atributo ao assembly e especifique o idioma dos recursos da cultura neutra.

## <a name="specifying-the-language"></a>Especificando o idioma

#### <a name="to-specify-the-language-of-the-resource-of-the-neutral-culture"></a>Para especificar o idioma do recurso da cultura neutra

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em seu projeto e clique em **Propriedades**.

2. Na barra de navegação à esquerda, selecione **aplicativo**e clique em **informações do assembly**.

3. Na caixa de diálogo **informações do assembly** , selecione o idioma na lista suspensa **idioma neutro** .

4. Clique em **OK**.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É permitido suprimir um aviso dessa regra. No entanto, o desempenho da inicialização pode diminuir.
