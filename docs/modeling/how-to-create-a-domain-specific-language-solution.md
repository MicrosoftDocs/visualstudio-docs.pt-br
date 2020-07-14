---
title: Como criar uma solução de linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 844f3eb97ed9e07aa8125688d2bfe8944249b008
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541785"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>Como criar uma solução de linguagem específica do domínio
Uma DSL (linguagem específica do domínio) é criada usando uma solução especializada do Visual Studio.

## <a name="prerequisites"></a>Pré-requisitos

Para poder iniciar este procedimento, instale estes componentes:

- Visual Studio
- SDK do Visual Studio (instalado como parte da carga de trabalho de **desenvolvimento de extensão do Visual Studio** )
- SDK de modelagem (instalado como um componente do Visual Studio)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução de linguagem específica de domínio

1. Inicie o assistente de DSL criando um novo projeto de **Designer de linguagem específica de domínio** .

   > [!NOTE]
   > Preferivelmente, o nome que você escolher para o projeto deve ser um identificador válido do Visual C# porque ele pode ser usado para gerar código.

   ::: moniker range="vs-2017"

   ![Criar caixa de diálogo DSL](../modeling/media/create_dsldialog.png)

   ::: moniker-end

2. Escolha um modelo DSL.

    Na página **selecionar opções de linguagem específicas de domínio** , selecione um dos modelos de solução, como **linguagem mínima**. Escolha um modelo que seja semelhante à DSL que você deseja criar.

    Para obter mais informações sobre modelos de solução, consulte [escolhendo um modelo de solução de linguagem específica de domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).

3. Insira uma extensão de nome de **arquivo** na página extensão de arquivos. Ele deve ser exclusivo em seu computador e em todos os computadores nos quais você deseja instalar a DSL. Você deve ver a mensagem **nenhum aplicativo ou editor do Visual Studio usam essa extensão**.

   - Se você usou a extensão de nome de arquivo em DSLs experimentais anteriores que não foram totalmente instaladas, você pode limpá-las usando a ferramenta **redefinir a instância experimental** , que pode ser encontrada no menu do SDK do Visual Studio.

   - Se outra extensão do Visual Studio que usa essa extensão de arquivo tiver sido totalmente instalada em seu computador, considere desinstalá-la. No menu **ferramentas** , clique em **Gerenciador de extensões**.

4. Inspecione e, se necessário, ajuste, os campos nas páginas restantes do assistente. Quando estiver satisfeito com as configurações, clique em **concluir**. Para obter mais informações sobre as configurações, consulte [Designer de DSL páginas do assistente](#settings).

    O assistente cria uma solução que tem dois projetos, chamados **DSL** e **DslPackage**.

   > [!NOTE]
   > Se você vir uma mensagem que alerta você não executar modelos de texto de fontes não confiáveis, clique em **OK**. Você pode definir que essa mensagem não apareça novamente.

## <a name="the-dsl-designer-wizard-pages"></a><a name="settings"></a>As páginas do assistente de Designer de DSL
 Você pode deixar vários campos inalterados de seus valores padrão. No entanto, certifique-se de definir o campo extensão de arquivo.

### <a name="solution-settings-page"></a>Página de configurações da solução
 **Em qual modelo você gostaria de basear sua linguagem específica de domínio?**
Escolha um modelo que seja semelhante à DSL que você deseja criar. Os diferentes modelos fornecem pontos de partida convenientes. Quando você seleciona um modelo de solução, o assistente exibe uma descrição. Para obter mais informações sobre modelos de solução, consulte [escolhendo um modelo de solução de linguagem específica de domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).

 **Como você deseja nomear sua linguagem específica de domínio?**
O padrão é o nome da solução. O código é gerado a partir desse valor. Ele deve ser válido como um nome de classe C#.

### <a name="file-extension-page"></a>Página extensão de arquivo
 **Qual extensão os arquivos de modelo devem usar?**
Digite uma nova extensão de arquivo.

 Verifique se essa extensão de arquivo ainda não foi registrada para uso neste computador, da seguinte maneira:

 Procure em **outras ferramentas e aplicativos registrados para lidar com essa extensão**. Se você vir a mensagem **nenhum aplicativo ou editor do Visual Studio usa essa extensão**, você pode usar essa extensão de arquivo.

 Se você vir uma lista de ferramentas ou pacotes, siga um destes procedimentos:

- Digite uma extensão de arquivo diferente.

     \- ou –

- Redefina a instância experimental do Visual Studio. Isso cancelará o registro de todas as DSLs que você criou anteriormente. No menu **Iniciar** , clique em **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas**e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**. Você pode recompilar todas as outras DSLs que deseja usar novamente.

     \- ou –

- Se uma extensão do Visual Studio que usa essa extensão de arquivo tiver sido totalmente instalada em seu computador, desinstale-a. No menu **ferramentas** , clique em **Gerenciador de extensões**.

### <a name="product-settings-page"></a>Página de configurações do produto
 **Qual é o nome do produto ao qual a nova linguagem específica de domínio pertence?**
O padrão é o nome DSL.

 Esse valor é usado no Windows Explorer (ou explorador de arquivos) para descrever os arquivos que têm essa extensão de arquivo.

 **Qual é o nome da empresa à qual o produto pertence?**
O nome da sua empresa.

 Esse valor é incorporado às propriedades de AssemblyInfo do seu pacote de DSL.

 **Qual é o namespace raiz para projetos nesta solução?**
O padrão é um nome composto por seus nomes de produtos e da empresa.

### <a name="signing-page"></a>Página Assinatura
 **Criar um arquivo de chave de nome forte** A opção padrão é criar uma nova chave para assinar seu assembly DSL.

 **Usar chave de nome forte existente** Use esta opção se você quiser integrar sua DSL com outro assembly.

 Para obter mais informações sobre nomes fortes, consulte [criando e usando assemblies de nome forte](/dotnet/standard/assembly/create-use-strong-named).

## <a name="see-also"></a>Confira também

- [Como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
