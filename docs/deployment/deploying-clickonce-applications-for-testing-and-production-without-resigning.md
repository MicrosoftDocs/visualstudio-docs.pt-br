---
title: Implantando aplicativos ClickOnce para teste e os servidores de produção sem assinar novamente | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: abfa170fe0f30cbc4fac941a6d77d0ac8b407f7f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846584"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>Implantar aplicativos ClickOnce para servidores de teste e produção sem assinar novamente
Este artigo descreve um recurso do ClickOnce, introduzida no .NET Framework versão 3.5, o que permite a implantação de aplicativos ClickOnce a partir de vários locais de rede sem assinar novamente ou alterar o ClickOnce manifestos.  
  
> [!NOTE]
>  Assinar novamente ainda é o método preferencial para implantar novas versões de aplicativos. Sempre que possível, use o método resigning. Para obter mais informações, consulte [ *Mage.exe* (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool).  
  
 ISVs e desenvolvedores de terceiros podem aceitar esse recurso, tornando mais fácil para seus clientes atualizar seus aplicativos. Esse recurso pode ser usado nas seguintes situações:  
  
-   Ao atualizar um aplicativo, não para a primeira instalação de um aplicativo.  
  
-   Quando há apenas uma configuração do aplicativo em um computador. Por exemplo, se um aplicativo estiver configurado para apontar para dois bancos de dados diferentes, você não pode usar esse recurso.  
  
## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>Excluir deploymentProvider de manifestos de implantação  
 No .NET Framework 2.0 e o .NET Framework 3.0, qualquer aplicativo ClickOnce que é instalado no sistema para disponibilidade offline deve listar uma `deploymentProvider` em seu manifesto de implantação. O `deploymentProvider` é conhecido como o local de atualização; é o local em que o ClickOnce verifica se há atualizações de aplicativo. Esse requisito, juntamente com a necessidade de editores de aplicativo assinar suas implantações, dificultou para uma empresa atualizar um aplicativo ClickOnce de um fornecedor ou de terceiros. Ele também torna mais difícil de implantar o mesmo aplicativo de vários locais na mesma rede.  
  
 Com as alterações que foram feitas ao ClickOnce no .NET Framework 3.5, é possível que um terceiro fornecer um aplicativo ClickOnce para outra organização, que, em seguida, pode implantar o aplicativo em sua própria rede.  
  
 Para tirar proveito desse recurso, os desenvolvedores de aplicativos ClickOnce devem excluir `deploymentProvider` da implantação de manifestos. Esse requisito significa que você deve excluir o `-providerUrl` manifestos de argumento quando você cria a implantação com Mage.exe. Ou, se você estiver gerando manifestos de implantação com MageUI.exe, você deve garantir que o **local inicie** caixa de texto a **manifesto do aplicativo** guia for deixada em branco.  
  
## <a name="deploymentprovider-and-application-updates"></a>atualizações de aplicativo e deploymentProvider  
 Começando com o .NET Framework 3.5, você não precisa especificar um `deploymentProvider` em seu manifesto de implantação para implantar um aplicativo ClickOnce para uso online e offline. Essa alteração permite o cenário em que você precisa empacotar e assinar a implantação por conta própria, mas permitir que outras empresas para implantar o aplicativo em suas redes.  
  
 O ponto importante a lembrar é que os aplicativos que excluem um `deploymentProvider` não é possível alterar seu local de instalação durante as atualizações, até que eles são fornecidos em uma atualização que inclui o `deploymentProvider` marcar novamente.  
  
 Aqui estão dois exemplos para esclarecer esse ponto. No primeiro exemplo, você publica um aplicativo ClickOnce que não tem nenhum `deploymentProvider` marca e você solicitar aos usuários para instalá-lo do http://www.adatum.com/MyApplication/. Se você decidir que deseja publicar a próxima atualização do aplicativo do http://subdomain.adatum.com/MyApplication/, você não tem como indicando isso no manifesto de implantação que reside no http://www.adatum.com/MyApplication/. Você pode fazer uma das duas coisas:  
  
- Peça aos usuários que desinstalar a versão anterior e instale a nova versão do novo local.  
  
- Incluir uma atualização no http://www.adatum.com/MyApplication/ que inclui um `deploymentProvider` apontando para http://www.adatum.com/MyApplication/. Em seguida, solte outra atualização posterior com `deploymentProvider` apontando para http://subdomain.adatum.com/MyApplication/.  
  
  No segundo exemplo, você publica um aplicativo ClickOnce que especifica `deploymentProvider`, e você decidir, em seguida, removê-lo. Uma vez a nova versão sem `deploymentProvider` é baixado para os clientes, você não pode redirecionar o caminho usado para atualizações, até que uma versão do aplicativo que tenha `deploymentProvider` restaurado. Assim como acontece com o primeiro exemplo, `deploymentProvider` inicialmente deve apontar para o local de atualização atual, não seu novo local. Nesse caso, se você tentar inserir uma `deploymentProvider` que se refere à http://subdomain.adatum.com/MyApplication/, a próxima atualização falhará.  
  
## <a name="create-a-deployment"></a>Criar uma implantação  
 Para obter orientação passo a passo sobre a criação de implantações que podem ser implantadas de diferentes locais da rede, consulte [passo a passo: implantar manualmente um aplicativo ClickOnce que não requer nova assinatura e que preserva informações de identidade visual](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md).  
  
## <a name="see-also"></a>Consulte também  
 [*Mage.exe* (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)   
 [*MageUI.exe* (Manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)