---
title: Como alterar o namespace de um idioma específico do domínio
description: Fornece informações sobre como alterar o namespace de um idioma específico do domínio.
ms.date: 10/31/2018
ms.topic: how-to
titleSuffix: ''
helpviewer_keywords:
- Domain-Specific Language, namespace
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: db9043c2a4c5abd19c839d2586709412d7607019
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387301"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>Como alterar o namespace de um idioma específico do domínio

Você pode alterar o namespace de um idioma específico do domínio. Faça a alteração no **DSL Explorer**, nas propriedades do projeto pacote Dsl e nas informações do assembly.

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>Para alterar o namespace de um idioma específico do domínio

1. No **DSL Explorer,** selecione o **nó Dsl.**

2. Na janela **Propriedades,** altere a **propriedade Namespace.**

3. Salve a solução e transforme os modelos.

4. No menu **Projeto,** escolha **Propriedades DSL**.

   As propriedades do projeto são exibidas.

5. Selecione a **guia Aplicativo.**

6. Altere **a propriedade namespace** Padrão para o novo nome do namespace.

7. Se você também quiser alterar o nome do assembly, altere a **propriedade Nome do assembly.**

8. Se você tiver alterado o nome do Assembly, abra DslPackage\Package.tt atualize esta linha:

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. Se você tiver escrito qualquer código personalizado, altere o namespace e as referências de classe nos arquivos de código.

10. Redefina a Visual Studio Experimental.

    1. Delete **\Users \\**_{your name}_**\AppData\Local\Microsoft\VisualStudio \\ \* Exp**.

    2. No menu Iniciar **do** Windows, escolha **Todos os Programas** Microsoft Visual Studio Ferramentas do  >  **SDK 2010**  >    >  **Redefinir a Instância Experimental**.

11. No menu **Build,** escolha **Recomar Solução**.

## <a name="see-also"></a>Confira também

[Glossário de ferramentas de linguagem específicas do domínio](/previous-versions/bb126564(v=vs.100))