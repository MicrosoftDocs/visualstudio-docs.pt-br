---
title: Benefício WhiteSource Bolt | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 01/11/2017
ms.topic: Get-Started-Article
description: Saiba como ativar a assinatura do WhiteSource Bolt incluída em sua assinatura do Visual Studio.
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: 981d6a655a203a7d44728fa7d12761fba2918d76
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49935766"
---
#  <a name="whitesource-bolt-in-visual-studio-subscriptions"></a>WhiteSource Bolt em assinaturas do Visual Studio

Encontre e corrija vulnerabilidades de software livre e gere relatórios de licença e inventário abrangentes de todos os componentes de software livre em seu build. Algumas assinaturas do Visual Studio incluem seis meses de acesso gratuito.

## <a name="activation-steps"></a>Etapas de ativação

1. Para ativar o benefício WhiteSource Bolt, entre em [https://my.visualstudio.com/benefits](https://my.visualstudio.com/benefits?wt.mc_id=o~msft~docs).

2. Localize o bloco WhiteSource Bolt na seção de Ferramentas e clique no link **Obter Código** na parte inferior do bloco do benefício.
   > [!div class="mx-imgBorder"]
   > ![Bloco do benefício WhiteSource Bolt](_img/vs-whitesource/vs-whitesource-tile.png)

3. Você receberá uma notificação exibindo o código de ativação.  **Copie o código para a área de transferência** e, em seguida, clique em **Ativar**.
   > [!div class="mx-imgBorder"]
   > ![Código do benefício WhiteSource](_img/vs-whitesource/vs-whitesource-code.png)

4. Na página da Web do WhiteSource, clique no botão **Ativar** ou role para baixo até a seção da página **Ativar sua conta**.
   > [!div class="mx-imgBorder"]
   > ![Ativar o benefício WhiteSource](_img/vs-whitesource/vs-whitesource-activate-page-cropped.png)

5. Na seção da página **Ativar sua conta**, você será guiado para realizar quatro etapas:

   - [Instalar](https://marketplace.visualstudio.com/items?itemName=whitesource.ws-bolt) a extensão WhiteSource Bolt do Microsoft Visual Studio Marketplace. Se você não tem permissões para instalar extensões, confira [Instalar extensões gratuitas para o Azure DevOps Services](/azure/devops/marketplace/install-vsts-extension?view=vsts).


~~~
Click the green **Install** button if you are using Azure DevOps Services, or the **Download** button for Team Foundation Server.  For this example, we will use Azure DevOps Services.
> [!div class="mx-imgBorder"]
> ![WhiteSource Benefit Install Extension](_img\vs-whitesource\vs-whitesource-download-install.png)

- Next, select the Azure DevOps organization you want to use and click **Confirm**.  (If you have not yet set up Azure DevOps Services, visit the [Benefits](https://my.visualstudio.com/benefits) page and activate your Azure DevOps Services benefit.)

> [!div class="mx-imgBorder"]
> ![WhiteSource Benefit Confirm Account](_img\vs-whitesource\vs-whitesource-confirm-account.png)

- You’ll receive a confirmation that the extension is installed and ready to use.  Click **Get started** to return to the WhiteSource Bolt page and continue.
> [!div class="mx-imgBorder"]
> ![WhiteSource Benefit Install Complete](_img\vs-whitesource\vs-whitesource-install-complete.png)
~~~

5. Abra o painel do projeto do Azure DevOps, clique no menu **Azure Pipelines** e escolha **WhiteSource Bolt**.
   > [!div class="mx-imgBorder"]
   > ![Adicionar extensão do benefício WhiteSource](_img/vs-whitesource/vs-whitesource-installed-cropped.png)

6. Cole o código de ativação no bloco do benefício WhiteSource Bolt e clique em **Ativar**. Cada código de ativação pode ser usado para ativar um único projeto.
   > [!div class="mx-imgBorder"]
   > ![Código de ativação do benefício WhiteSource](_img/vs-whitesource/vs-whitesource-activate-code-cropped.png)

7. Agora a ativação está concluída e você terá 180 dias restantes na sua assinatura.

8. Será necessário adicionar a extensão do WhiteSource Bolt como uma das etapas de build.  Há um vídeo disponível na [página do WhiteSource Bolt](https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate) que mostra como fazer isso.

9. Depois de executar o build, os seguintes relatórios e painéis abrangentes serão gerados automaticamente:
    - Painel de vulnerabilidades de segurança
    - Relatório de vulnerabilidades de segurança
    - Relatório de bibliotecas desatualizadas
    - Painel de riscos e conformidade de licença
    - Relatório de inventário

## <a name="eligibility"></a>Qualificação

| Nível de Assinatura                                                 |     Canais                                            | Benefício                                                          | Renovável?    |
|--------------------------------------------------------------------|---------------------------------------------------------|------------------------------------------------------------------|---------------|
| Visual Studio Enterprise (Padrão, nuvem anual)   | VL, Azure, Retail, NFR<sup>1</sup> selecionado | Seis meses       |  Sim          |
| Visual Studio Professional (Padrão, nuvem anual) | VL, Azure, Retail                                       | Indisponível                                                           |NA         |
| Visual Studio Test Professional (Padrão)                         | VL, Retail                                              | Não disponível                                             |  NA         |
| Plataformas MSDN (Padrão)                                          | VL, Retail                                              | Não disponível                                              | NA         |
| Visual Studio Dev Essentials | NA  | Não disponível |NA |
| Visual Studio Enterprise, Visual Studio Professional (nuvem mensal) | Azure                                       | Não disponível                                                           |NA|

<sup>1</sup>  *Inclui: Microsoft Partner Network (Enterprise).  Exclui: NFR (Proibida a Revenda), VSIP (Visual Studio Industry Partner), FTE, MCT Software & Services Developer, BizSpark, Imagine, MVP (Microsoft Valued Professional), RD (diretor regional), MCT Software & Services, Microsoft Partner Network (Professional).*

Não tem certeza de qual assinatura você está usando?  Conecte-se ao [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs) para ver todas as assinaturas atribuídas ao seu endereço de email. Se não vir todas as suas assinaturas, talvez você tenha uma ou mais atribuídas a outro endereço de email.  Você precisará entrar com esse endereço de email para ver as assinaturas.

## <a name="support-resources"></a>Recursos de suporte

-  Precisa de ajuda com o WhiteSource Bolt?  Converse com um representante do Bolt WhiteSource em https://www.whitesourcesoftware.com/vse_whitesource_bolt/
-  Para obter assistência com vendas, assinaturas, contas e cobrança para Assinaturas do Visual Studio, entre em contato com o [Suporte a Assinaturas](https://visualstudio.microsoft.com/subscriptions/support/) do Visual Studio.
-  Tem alguma pergunta sobre o IDE do Visual Studio, o Azure DevOps Services ou outros produtos ou serviços do Visual Studio?  Acesse o [Suporte do Visual Studio](https://visualstudio.microsoft.com/support/).