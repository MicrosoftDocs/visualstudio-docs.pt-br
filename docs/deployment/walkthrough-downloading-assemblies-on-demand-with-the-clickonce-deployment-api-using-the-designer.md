---
title: Baixar assemblies sob demanda usando o designer (API do ClickOnce)
description: Saiba como marcar determinados assemblies em seu aplicativo ClickOnce como opcionais usando o designer e baixe-os quando o Common Language Runtime precisar deles.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- Windows applications, ClickOnce deployments
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: 59a0dd5f-1cab-4f2f-b780-0ab7399905d5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7bb30b26e859708d295a31bd45b310897e4bcaac
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216989"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>Walkthrough: baixar assemblies sob demanda com a API de implantação do ClickOnce usando o designer
Por padrão, todos os assemblies incluídos em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo são baixados quando o aplicativo é executado pela primeira vez. No entanto, pode haver partes do seu aplicativo que são usadas por um pequeno conjunto de usuários. Nesse caso, você deseja baixar um assembly somente quando você cria um de seus tipos. A instrução a seguir demonstra como marcar determinados assemblies em seu aplicativo como "opcional" e como baixá-los usando classes no <xref:System.Deployment.Application> namespace quando o Common Language Runtime os exige.

> [!NOTE]
> Seu aplicativo terá que ser executado com confiança total para usar este procedimento.

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar as configurações, clique em **Importar e exportar configurações** no menu **Ferramentas**. Para obter mais informações, confira [Redefinir as configurações](../ide/environment-settings.md#reset-settings).

## <a name="create-the-projects"></a>Criar os projetos

### <a name="to-create-a-project-that-uses-an-on-demand-assembly-with-visual-studio"></a>Para criar um projeto que usa um assembly sob demanda com o Visual Studio

1. Crie um novo projeto de Windows Forms no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . No menu **Arquivo**, aponte para **Adicionar** e clique em **Novo Projeto**. Escolha um projeto de **biblioteca de classes** na caixa de diálogo e nomeie-o `ClickOnceLibrary` .

   > [!NOTE]
   > Em Visual Basic, recomendamos que você modifique as propriedades do projeto para alterar o namespace raiz desse projeto para `Microsoft.Samples.ClickOnceOnDemand` ou para um namespace de sua escolha. Para simplificar, os dois projetos nesta explicação estão no mesmo namespace.

2. Defina uma classe chamada `DynamicClass` com uma única propriedade chamada `Message` .

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs" id="Snippet1":::

3. Selecione o projeto Windows Forms no **Gerenciador de soluções**. Adicione uma referência ao <xref:System.Deployment.Application> assembly e uma referência de projeto ao `ClickOnceLibrary` projeto.

   > [!NOTE]
   > Em Visual Basic, recomendamos que você modifique as propriedades do projeto para alterar o namespace raiz desse projeto para `Microsoft.Samples.ClickOnceOnDemand` ou para um namespace de sua escolha. Para simplificar, os dois projetos neste passo a passos estão localizados no mesmo namespace.

4. Clique com o botão direito do mouse no formulário, clique em **Exibir código** no menu e adicione as referências a seguir ao formulário.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet1":::

5. Adicione o código a seguir para baixar esse assembly sob demanda. Este código mostra como mapear um conjunto de assemblies para um nome de grupo usando uma <xref:System.Collections.DictionaryBase.Dictionary%2A> classe genérica. Como estamos baixando apenas um único assembly neste passo a passos, há apenas um assembly em nosso grupo. Em um aplicativo real, você provavelmente desejaria baixar todos os assemblies relacionados a um único recurso em seu aplicativo ao mesmo tempo. A tabela de mapeamento permite que você faça isso facilmente associando todas as DLLs que pertencem a um recurso com um nome de grupo de download.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet2":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet2":::

6. No menu **Exibir** , clique em **Caixa de Ferramentas**. Arraste um <xref:System.Windows.Forms.Button> da **caixa de ferramentas** para o formulário. Clique duas vezes no botão e adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet3":::

## <a name="mark-assemblies-as-optional"></a>Marcar assemblies como opcionais

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-visual-studio"></a>Para marcar assemblies como opcionais em seu aplicativo ClickOnce usando o Visual Studio

1. Clique com o botão direito do mouse no projeto Windows Forms no **Gerenciador de soluções** e clique em **Propriedades**. Selecione a guia **publicar** .

2. Clique no botão **arquivos de aplicativo** .

3. Localize a listagem para *ClickOnceLibrary.dll*. Defina a caixa suspensa **status de publicação** para **incluir**.

4. Expanda a caixa suspensa **grupo** e selecione **novo**. Digite o nome `ClickOnceLibrary` como o novo nome do grupo.

5. Continue Publicando seu aplicativo conforme descrito em [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-manifest-generation-and-editing-tool--graphical-client-mageuiexe"></a>Para marcar assemblies como opcionais em seu aplicativo ClickOnce usando Manifest Generation and Editing Tool – cliente gráfico (MageUI.exe)

1. Crie seus [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos conforme descrito em [passo a passos: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).

2. Antes de fechar MageUI.exe, selecione a guia que contém o manifesto do aplicativo da implantação e, nessa guia, selecione a guia **arquivos** .

3. Localize ClickOnceLibrary.dll na lista de arquivos de aplicativo e defina sua coluna de **tipo de arquivo** como **nenhum**. Para a coluna **grupo** , digite `ClickOnceLibrary.dll` .

## <a name="test-the-new-assembly"></a>Testar o novo assembly

Para testar seu assembly sob demanda:

1. Inicie o aplicativo implantado com o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] .

2. Quando o formulário principal for exibido, pressione a <xref:System.Windows.Forms.Button> . Você deve ver uma cadeia de caracteres em uma janela de caixa de mensagem que lê "Olá, mundo!"

## <a name="see-also"></a>Confira também

- <xref:System.Deployment.Application.ApplicationDeployment>
