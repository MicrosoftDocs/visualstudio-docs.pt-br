---
title: 'Como: alterar o namespace de uma linguagem específica de domínio'
ms.date: 10/31/2018
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, namespace
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ff7c73694cb53f7fbea21514feeaab4abce3f29
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542669"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>Como: alterar o namespace de uma linguagem específica de domínio

Você pode alterar o namespace de uma linguagem específica de domínio. Faça a alteração no **Gerenciador de DSL**, nas propriedades do projeto de pacote DSL e nas informações do assembly.

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>Para alterar o namespace de uma linguagem específica de domínio

1. No **Gerenciador de DSL**, selecione o nó **DSL** .

2. Na janela **Propriedades** , altere a propriedade **namespace** .

3. Salve a solução e transforme os modelos.

4. No menu **projeto** , escolha **Propriedades de DSL**.

   As propriedades do seu projeto são exibidas.

5. Selecione a guia **aplicativo** .

6. Altere a propriedade de **namespace padrão** para o novo nome de namespace.

7. Se você também quiser alterar o nome do assembly, altere a propriedade do **nome do assembly.**

8. Se você alterou o nome do assembly, abra DslPackage\Package.tt e atualize esta linha:

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. Se você tiver escrito qualquer código personalizado, certifique-se de alterar o namespace e as referências de classe nos arquivos de código.

10. Redefina a instância experimental do Visual Studio.

    1. Exclua ** \\ \Users**_{Your Name}_**\AppData\Local\Microsoft\VisualStudio \\ \* exp**.

    2. No menu **Iniciar** do Windows, escolha **todos os programas**  >  **Microsoft Visual Studio**  >  **ferramentas**SDK  >  **do 2010 redefinam a instância experimental**.

11. No menu **Compilar** , escolha **Recompilar solução**.

## <a name="see-also"></a>Confira também

[Glossário de ferramentas de linguagem específica de domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)