---
title: 'CA1824: marcar assemblies com NeutralResourcesLanguageAttribute'
ms.date: 03/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1824
- MarkAssembliesWithNeutralResourcesLanguage
helpviewer_keywords:
- MarkAssembliesWithNeutralResourcesLanguage
- CA1824
ms.assetid: 10e97f8a-aa6e-47aa-b253-1e5d3a295d82
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: beaef23dd5b3047d1d65b90fdd984dfdedd7e145
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31916381"
---
# <a name="ca1824-mark-assemblies-with-neutralresourceslanguageattribute"></a>CA1824: marcar assemblies com NeutralResourcesLanguageAttribute

|||
|-|-|
|NomeDoTipo|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não recentes|

## <a name="cause"></a>Causa

Um assembly contém um **ResX**-com base em recursos, mas não tem o <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName> aplicada a ele.

## <a name="rule-description"></a>Descrição da regra

O <xref:System.Resources.NeutralResourcesLanguageAttribute> atributo informa ao Gerenciador de recursos de cultura do padrão do aplicativo. Se os recursos da cultura padrão são inseridos no assembly de principal do aplicativo, e <xref:System.Resources.ResourceManager> tem que recuperar os recursos que pertencem à mesma cultura que a cultura padrão, o <xref:System.Resources.ResourceManager> usa automaticamente os recursos localizados no assembly principal em vez de procurar por um assembly satélite. Isso ignora a investigação do assembly normal, melhora o desempenho da pesquisa para o primeiro recurso carregado e pode reduzir o conjunto de trabalho.

> [!TIP]
> Consulte [empacotamento e implantação de recursos](/dotnet/framework/resources/packaging-and-deploying-resources-in-desktop-apps) para o processo que <xref:System.Resources.ResourceManager> usa para investigação para arquivos de recurso.

## <a name="fix-violations"></a>Corrigir as violações

Para corrigir uma violação desta regra, adicione o atributo para o assembly e especificar o idioma dos recursos de cultura neutra.

### <a name="to-specify-the-neutral-language-for-resources"></a>Para especificar o idioma neutro para recursos

1. Em **Solution Explorer**, clique com o botão direito e, em seguida, selecione **propriedades**.

2. Selecione o **aplicativo** guia e, em seguida, selecione **informações de Assembly**.

   > [!NOTE]
   > Se o projeto é um projeto .NET padrão ou no .NET Core, selecione o **pacote** guia.

3. Selecione o idioma do **idioma neutro** ou **idioma neutro Assembly** lista suspensa.

4. Selecione **OK**.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É permitido para suprimir um aviso dessa regra. No entanto, pode afetar o desempenho da inicialização.

## <a name="see-also"></a>Consulte também

- <xref:System.Resources.NeutralResourcesLanguageAttribute>
- [Recursos em aplicativos de área de trabalho (.NET)](/dotnet/framework/resources/)
- [CA1703 - cadeias de caracteres de recurso devem ter grafia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1701 - cadeia de caracteres de recurso palavras compostas devem ter maiusculas e minúsculas corretamente](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)