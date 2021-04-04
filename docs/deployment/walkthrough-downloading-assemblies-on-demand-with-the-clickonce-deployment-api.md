---
title: Baixar assemblies sob demanda (API do ClickOnce)
description: Saiba como marcar determinados assemblies em seu aplicativo ClickOnce como opcionais e baixá-los quando o Common Language Runtime precisar deles.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 316be1f0a8fa881f781d983cfe9ed663e5907749
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216898"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api"></a>Walkthrough: baixar assemblies sob demanda com a API de implantação do ClickOnce
Por padrão, todos os assemblies incluídos em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo são baixados quando o aplicativo é executado pela primeira vez. No entanto, você pode ter partes do seu aplicativo que são usadas por um pequeno conjunto de usuários. Nesse caso, você deseja baixar um assembly somente quando você cria um de seus tipos. A instrução a seguir demonstra como marcar determinados assemblies em seu aplicativo como "opcional" e como baixá-los usando classes no <xref:System.Deployment.Application> namespace quando o Common Language Runtime (CLR) os exige.

> [!NOTE]
> Seu aplicativo terá que ser executado com confiança total para usar este procedimento.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará de um dos seguintes componentes para concluir este passo a passos:

- O SDK do Windows. O SDK do Windows pode ser baixado do centro de download da Microsoft.

- Visual Studio.

## <a name="create-the-projects"></a>Criar os projetos

#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>Para criar um projeto que usa um assembly sob demanda

1. Crie um diretório chamado ClickOnceOnDemand.

2. Abra o prompt de comando do SDK do Windows ou o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] prompt de comando.

3. Altere para o diretório ClickOnceOnDemand.

4. Gere um par de chaves pública/privada usando o seguinte comando:

   ```cmd
   sn -k TestKey.snk
   ```

5. Usando o bloco de notas ou outro editor de texto, defina uma classe chamada `DynamicClass` com uma única propriedade chamada `Message` .

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs" id="Snippet1":::

6. Salve o texto como um arquivo chamado *ClickOnceLibrary. cs* ou *ClickOnceLibrary. vb*, dependendo do idioma usado para o diretório *ClickOnceOnDemand* .

7. Compile o arquivo em um assembly.

   ```csharp
   csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs
   ```

   ```vb
   vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb
   ```

8. Para obter o token de chave pública para o assembly, use o seguinte comando:

   ```cmd
   sn -T ClickOnceLibrary.dll
   ```

9. Crie um novo arquivo usando seu editor de texto e insira o código a seguir. Esse código cria um aplicativo Windows Forms que baixa o assembly ClickOnceLibrary quando necessário.

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb" id="Snippet1":::

10. No código, localize a chamada para <xref:System.Reflection.Assembly.LoadFile%2A> .

11. Defina `PublicKeyToken` como o valor que você recuperou anteriormente.

12. Salve o arquivo como *Form1. cs* ou *Form1. vb*.

13. Compile-o em um executável usando o comando a seguir.

    ```csharp
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs
    ```

    ```vb
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb
    ```

## <a name="mark-assemblies-as-optional"></a>Marcar assemblies como opcionais

#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>Para marcar assemblies como opcionais em seu aplicativo ClickOnce usando MageUI.exe

1. Usando *MageUI.exe*, crie um manifesto do aplicativo conforme descrito em [passo a passos: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto do aplicativo:

    - Nomeie o manifesto do aplicativo `ClickOnceOnDemand` .

    - Na página **arquivos** , na linha *ClickOnceLibrary.dll* , defina a coluna **tipo de arquivo** como **nenhum**.

    - Na página **arquivos** , na linha *ClickOnceLibrary.dll* , digite `ClickOnceLibrary.dll` a coluna **grupo** .

2. Usando o *MageUI.exe*, crie um manifesto de implantação, conforme descrito em [Walkthrough: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Use as seguintes configurações para o manifesto de implantação:

    - Nomeie o manifesto de implantação `ClickOnceOnDemand` .

## <a name="testing-the-new-assembly"></a>Testando o novo assembly

#### <a name="to-test-your-on-demand-assembly"></a>Para testar seu assembly sob demanda

1. Carregue sua [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação em um servidor Web.

2. Inicie o aplicativo implantado com o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] de um navegador da Web, inserindo a URL para o manifesto de implantação. Se você chamar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo `ClickOnceOnDemand` e carregá-lo no diretório raiz de adatum.com, sua URL ficaria assim:

   ```
   http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application
   ```

3. Quando o formulário principal for exibido, pressione a <xref:System.Windows.Forms.Button> . Você deve ver uma cadeia de caracteres em uma janela de caixa de mensagem que lê "Olá, mundo!".

## <a name="see-also"></a>Confira também
- <xref:System.Deployment.Application.ApplicationDeployment>