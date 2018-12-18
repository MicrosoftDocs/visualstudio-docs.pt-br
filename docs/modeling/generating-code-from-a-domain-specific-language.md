---
title: Gerando código a partir de uma linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 77d26595bd97a98ef9a4cd1f72c14739695bb755
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859842"
---
# <a name="generating-code-from-a-domain-specific-language"></a>Gerando código a partir de uma linguagem específica do domínio
Microsoft [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] fornece uma maneira eficiente para gerar código, documentos, arquivos de configuração e outros artefatos de dados representados em modelos. Usando [!INCLUDE[dsl](../modeling/includes/dsl_md.md)], você pode criar um conjunto de classes que representam seus dados e você pode escrever seus modelos de texto em classes cujos nomes e propriedades refletirem esses dados.

 Por exemplo, a Fabrikam tem um arquivo XML de nomes de clientes e endereços de email. Seus desenvolvedores criar um modelo no qual o cliente é uma classe, com as propriedades name e e-mail. Eles escreverem vários modelos de texto para processar os dados, incluindo desse fragmento que produz uma tabela de todos os clientes como parte de uma página HTML:

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

 Quando o banco de dados do cliente é processado, o arquivo XML é lido no armazenamento de modelos. Um *processador de diretriz*, criada usando [!INCLUDE[dsl](../modeling/includes/dsl_md.md)], torna a classe de cliente disponível para o código no modelo de texto. Muitos modelos de texto podem ser executados no mesmo repositório.

 Modelos de texto são essenciais para [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]. Eles são usados para gerar o código-fonte para os elementos de modelo de domínio, bem como para o VSPackage e os controles que são usados para integrar as ferramentas do Visual Studio.

 Esta seção discute algumas das maneiras de criar, modificar e depurar os modelos de texto usados em [!INCLUDE[dsl](../modeling/includes/dsl_md.md)].

## <a name="in-this-section"></a>Nesta seção
 [Acessando modelos por meio de modelos de texto](../modeling/accessing-models-from-text-templates.md)

 Fornece informações básicas sobre a referência a linguagem específica de domínio em modelos de texto.

 [Passo a passo: depurando um modelo (template) de texto que acessa um modelo](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)

 Descreve como fazer a solução de problemas e depuração em um modelo de texto que se refere a uma linguagem específica de domínio.

 [Passo a passo: conectando um host a um processador de diretriz gerado](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)

 Descreve como se conectar a um host personalizado para um processador de diretriz gerado.

 [O comando DslTextTransform](../modeling/the-dsltexttransform-command.md)

 Descreve o arquivo de comando que executa o executável TextTransform na linha de comando para modelos de texto que fazem referência a linguagens específicas de domínio.

## <a name="reference"></a>Referência
 [Gravando um modelo de texto T4](../modeling/writing-a-t4-text-template.md)

 Fornece a sintaxe de diretivas de modelo de texto e blocos de controle.

## <a name="related-sections"></a>Seções relacionadas
 [Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)

 Explica o processo de transformação do modelo de texto.

 [Geração de código em um processo de build](../modeling/code-generation-in-a-build-process.md)

 Leia este tópico se você estiver gerando arquivos de uma DSL em um servidor de compilação.