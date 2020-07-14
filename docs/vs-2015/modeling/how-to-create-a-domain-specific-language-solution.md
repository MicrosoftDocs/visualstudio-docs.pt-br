---
title: 'Como: criar uma solução de linguagem específica de domínio | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
ms.assetid: e585b63b-34d2-405a-8d81-39ea22317975
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 227838334067d33c8a50c81d3a3c013c6baee356
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533075"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>Como criar uma solução de linguagem específica do domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma DSL (linguagem específica de domínio) é criada usando uma solução especializada [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

## <a name="prerequisites"></a>Pré-requisitos
 Antes de iniciar este procedimento, você deve primeiro instalar estes componentes:

|Produto|Link de download|
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[https://www.visualstudio.com/](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[SDK do Visual Studio](../extensibility/visual-studio-sdk.md)|
|SDK de Visualização e Modelagem do Visual Studio|[Download do SDK de modelagem](https://www.microsoft.com/download/details.aspx?id=48148)|

## <a name="creating-a-domain-specific-language-solution"></a>Criando uma solução de linguagem específica de domínio

#### <a name="to-create-a-domain-specific-language-solution"></a>Para criar uma solução de linguagem específica de domínio

1. Inicie o assistente de DSL.

   1. No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.

   2. A caixa de diálogo **Novo Projeto** aparecerá.

   3. Em **tipos de projeto**, expanda o nó **outros tipos de projeto** e clique em **extensibilidade**.

   4. Clique em **Designer de linguagem específica de domínio**.

   5. Na caixa **nome** , digite um nome para a solução. Clique em **OK**.

       O **Assistente de designer de linguagem específica de domínio** é exibido.

      > [!NOTE]
      > Preferivelmente, o nome que você digita deve ser um identificador válido do Visual C#, pois ele pode ser usado para gerar código.

      ![Criar caixa de diálogo DSL](../modeling/media/create-dsldialog.png "Create_DSLDialog")

2. Escolha um modelo DSL.

    Na página **selecionar opções de linguagem específicas de domínio** , selecione um dos modelos de solução, como **linguagem mínima**. Escolha um modelo que seja semelhante à DSL que você deseja criar.

    Para obter mais informações sobre modelos de solução, consulte [escolhendo um modelo de solução de linguagem específica de domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).

3. Insira uma extensão de nome de **arquivo** na página extensão de arquivos. Ele deve ser exclusivo em seu computador e em todos os computadores nos quais você deseja instalar a DSL. Você deve ver a mensagem **nenhum aplicativo ou editor do Visual Studio usam essa extensão**.

   - Se você tiver usado a extensão de nome de arquivo em DSLs experimentais anteriores que não foram totalmente instaladas, você poderá limpá-las usando a ferramenta **redefinir a instância experimental** , que pode ser encontrada no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] menu SDK.

   - Se outra [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que usa essa extensão de arquivo tiver sido totalmente instalada em seu computador, considere desinstalá-la. No menu **ferramentas** , clique em **Gerenciador de extensões**.

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

- Redefina a [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] instância experimental. Isso cancelará o registro de todas as DSLs que você criou anteriormente. No menu **Iniciar** , clique em **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas**e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**. Você pode recompilar todas as outras DSLs que deseja usar novamente.

     \- ou –

- Se uma [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão que usa essa extensão de arquivo tiver sido totalmente instalada em seu computador, desinstale-a. No menu **ferramentas** , clique em **Gerenciador de extensões**.

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

## <a name="see-also"></a>Consulte Também
 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md) [ferramentas de linguagem específica de domínio Glossário](/previous-versions/bb126564(v=vs.100))
