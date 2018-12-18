---
title: 'Como: alterar o namespace de uma linguagem específica de domínio'
ms.date: 10/31/2018
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, namespace
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 47e13e8399cba7762ff7443e4fc4cbf3a89375a6
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966824"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>Como: alterar o namespace de uma linguagem específica de domínio

Você pode alterar o namespace de uma linguagem específica de domínio. Fazer a alteração no valor de **Gerenciador de DSL**, nas propriedades do projeto Dsl de pacote e as informações de assembly.

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>Para alterar o namespace de uma linguagem específica de domínio

1. Na **Gerenciador de DSL**, selecione o **Dsl** nó.

2. No **propriedades** janela, altere o **Namespace** propriedade.

3. Salve a solução e transformar os modelos.

4. Sobre o **Project** menu, escolha **Dsl propriedades**.

   As propriedades do projeto são exibidos.

5. Selecione o **aplicativo** guia.

6. Alterar o **namespace padrão** propriedade para o novo nome de namespace.

7. Se você também quiser alterar o nome do assembly, altere o **propriedade nome do Assembly.**

8. Se você tiver alterado o nome do Assembly, abra DslPackage\Package.tt e atualize essa linha:

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. Se você tiver gravado um código personalizado, certifique-se de alterar as referências de namespace e classe nos arquivos de código.

10. Redefina a instância Experimental do Visual Studio.

    1. Exclua **\Users\\**_{o nome}_**\AppData\Local\Microsoft\VisualStudio\\\*Exp**.

    2. Sobre o Windows **inicie** menu, escolha **todos os programas** > **SDK do Microsoft Visual Studio 2010** > **ferramentas**  >  **Redefinir a instância Experimental**.

11. Sobre o **construir** menu, escolha **recompilar solução**.

## <a name="see-also"></a>Consulte também

[Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)