---
title: Implantando aplicativos ClickOnce para teste e os servidores de produção sem assinar novamente | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 2b2a26e847a23e8a4037958532889626a931341c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49840032"
---
# <a name="deploying-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>Implantando aplicativos ClickOnce para servidores de teste e produção sem assinar novamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico apresenta um novo recurso do ClickOnce, introduzida no .NET Framework versão 3.5, o que permite a implantação de aplicativos ClickOnce a partir de vários locais de rede sem assinar novamente ou alterar o ClickOnce manifestos.  
  
> [!NOTE]
>  Assinar novamente ainda é o método preferencial para implantar novas versões de aplicativos. Sempre que possível, use o método resigning. Para obter mais informações, consulte [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1).  
  
 ISVs e desenvolvedores de terceiros podem participar desse recurso, tornando mais fácil para seus clientes atualizar seus aplicativos. Esse recurso pode ser usado nas seguintes situações:  
  
-   Ao atualizar um aplicativo, não a primeira instalação de um aplicativo.  
  
-   Quando há apenas uma configuração do aplicativo em um computador. Por exemplo, se um aplicativo estiver configurado para apontar para dois bancos de dados diferentes, você não pode usar esse recurso.  
  
## <a name="excluding-deploymentprovider-from-deployment-manifests"></a>Excluindo deploymentProvider de manifestos de implantação  
 No .NET Framework 2.0 e o .NET Framework 3.0, qualquer aplicativo ClickOnce que é instalado no sistema para disponibilidade offline deve especificar um `deploymentProvider` em seu manifesto de implantação. O `deploymentProvider` é conhecido como o local de atualização; é o local em que verificará se há atualizações do aplicativo ClickOnce. Esse requisito, juntamente com a necessidade de editores de aplicativo assinar suas implantações, dificultou para uma empresa atualizar um aplicativo ClickOnce de um fornecedor ou outros terceiros. Ele também torna mais difícil de implantar o mesmo aplicativo de vários locais na mesma rede.  
  
 Com as alterações que foram feitas ao ClickOnce no .NET Framework 3.5, é possível que um terceiro fornecer um aplicativo ClickOnce para outra organização, que, em seguida, pode implantar o aplicativo em sua própria rede.  
  
 Para tirar proveito desse recurso, os desenvolvedores de aplicativos ClickOnce devem excluir `deploymentProvider` da implantação de manifestos. Isso significa que a exclusão do `-providerUrl` manifestos de argumento quando você cria a implantação com Mage.exe ou certificando-se a **local inicie** caixa de texto na **manifesto do aplicativo** guia for deixada em branco se você estão gerando manifestos de implantação com MageUI.exe.  
  
## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider e atualizações de aplicativos  
 Começando com o .NET Framework 3.5, você não precisa especificar um `deploymentProvider` em seu manifesto de implantação para implantar um aplicativo ClickOnce para uso online e offline. Isso dá suporte para o cenário em que você precisa empacotar e assinar a implantação por conta própria, mas permitir que outras empresas para implantar o aplicativo em suas redes.  
  
 O principal ponto a lembrar é que os aplicativos que excluem um `deploymentProvider` não é possível alterar seu local de instalação durante as atualizações, até que eles são fornecidos em uma atualização que inclui o `deploymentProvider` marcar novamente.  
  
 Aqui estão dois exemplos para esclarecer esse ponto. No primeiro exemplo, você publica um aplicativo ClickOnce que não tem nenhum `deploymentProvider` marca e você solicitar aos usuários para instalá-lo do http://www.adatum.com/MyApplication/. Se você decidir que deseja publicar a próxima atualização do aplicativo do http://subdomain.adatum.com/MyApplication/, você não terá nenhuma maneira de indicando isso no manifesto de implantação que reside no http://www.adatum.com/MyApplication/. Você pode fazer uma das duas coisas:  
  
- Peça aos usuários que desinstalar a versão anterior e instale a nova versão do novo local.  
  
- Incluir uma atualização no http://www.adatum.com/MyApplication/ que inclui um `deploymentProvider` apontando para http://www.adatum.com/MyApplication/. Em seguida, solte outra atualização posterior com `deploymentProvider` apontando para http://subdomain.adatum.com/MyApplication/.  
  
  No segundo exemplo, você publica um aplicativo ClickOnce que especifica `deploymentProvider`, e você decidir, em seguida, removê-lo. Uma vez a nova versão sem `deploymentProvider` tiver sido baixado para os clientes, você não poderá redirecionar o caminho usado para atualizações até uma versão do aplicativo que tenha `deploymentProvider` restaurado. Assim como acontece com o primeiro exemplo, `deploymentProvider` inicialmente deve apontar para o local de atualização atual, não seu novo local. Nesse caso, se você tentar inserir uma `deploymentProvider` que se refere à http://subdomain.adatum.com/MyApplication/, em seguida, a próxima atualização falhará.  
  
## <a name="creating-a-deployment"></a>Criar uma implantação  
 Para obter orientação passo a passo sobre a criação de implantações que podem ser implantadas de diferentes locais da rede, consulte [passo a passo: Implantando manualmente um aplicativo ClickOnce que faz não exigem assinando novamente e essas informações de preserva a identidade visual](../deployment/walkthrough-manually-deploying-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information.md).  
  
## <a name="see-also"></a>Consulte também  
 [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe (Manifest Generation and Editing Tool, cliente gráfico)](http://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)



