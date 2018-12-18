---
title: Escolhendo uma estratégia de atualização do ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- application updates, ClickOnce
- updates, ClickOnce
- ClickOnce deployment, update strategies
ms.assetid: d8b6e7bb-4ea0-47f3-91cd-48580bdceccc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a4da8dddc667b032c6c284dc62197ff05a1a328f
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39081791"
---
# <a name="choose-a-clickonce-update-strategy"></a>Escolha uma estratégia de atualização do ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] pode fornecer atualizações automáticas para o aplicativo. Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo lê periodicamente o seu arquivo de manifesto de implantação para ver se há atualizações do aplicativo estão disponíveis. Se disponível, a nova versão do aplicativo será baixada e executada. Para proporcionar eficiência, somente os arquivos que foram alterados serão baixados.  
  
 Ao criar um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], será necessário determinar qual estratégia o aplicativo usará para verificar se há atualizações disponíveis. Há três estratégias básicas que você pode usar: verificar se há atualizações na inicialização do aplicativo, verificar se há atualizações após a inicialização do aplicativo (executada em um thread em segundo plano) ou fornecer uma interface do usuário para atualizações.  
  
 Além disso, você poderá determinar a frequência com que o aplicativo verificará se há atualizações e fazer as atualizações necessárias.  
  
> [!NOTE]
>  Atualizações de aplicativos necessitam de conectividade de rede. Se uma conexão de rede não estiver presente, o aplicativo será executado sem verificar se há atualizações, independentemente da estratégia de atualização que você escolher.  
  
> [!NOTE]
>  No .NET Framework 2.0 e no .NET Framework 3.0, sempre que seu aplicativo verificar se as atualizações, antes ou após a inicialização ou por meio de \<xref:System.Deployment.Application > APIs, você deve definir `deploymentProvider` no manifesto de implantação. O `deploymentProvider` elemento corresponde no Visual Studio para o **atualizar local** campo o **atualizações** caixa de diálogo do **publicar** guia. Essa regra é consentida no .NET Framework 3.5. Para obter mais informações, consulte [implantação de ClickOnce aplicativos para teste e servidores de produção sem Resigning](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md).  
  
## <a name="check-for-updates-after-application-startup"></a>Verifique se há atualizações após a inicialização do aplicativo  
 Ao usar esta estratégia, o aplicativo tentará localizar e ler o arquivo de manifesto de implantação em segundo plano enquanto estiver em execução. Se uma atualização estiver disponível, na próxima vez que o usuário executar o aplicativo, o download e a instalação da atualização serão solicitados.  
  
 Essa estratégia funciona melhor para conexões de rede com largura da banda baixa ou aplicativos maiores que podem exigir downloads longos.  
  
 Para habilitar essa estratégia de atualização, clique em **depois que o aplicativo é iniciado** na **escolha quando o aplicativo deve verificar por atualizações** seção o **atualizações do aplicativo** caixa de diálogo. Em seguida, especifique um intervalo de atualização na seção **especifique a frequência com que o aplicativo deve verificar por atualizações**.  
  
 Isso é o mesmo que alterar o **atualização** elemento na implantação de manifesto da seguinte maneira:  
  
```xml  
<!-- When to check for updates -->  
<subscription>  
   <update>  
      <expiration maximumAge="6" unit="hours" />  
   </update>  
</subscription>  
```  
  
## <a name="check-for-updates-before-application-startup"></a>Verificar se há atualizações antes da inicialização do aplicativo  
 A estratégia padrão é tentar localizar e ler o arquivo de manifesto de implantação antes do início do aplicativo. Ao usar essa estratégia, o aplicativo tentará localizar e ler o arquivo de manifesto de implantação sempre que o usuário iniciar o aplicativo. Se uma atualização estiver disponível, ela será baixada e iniciada. Caso contrário, a versão existente do aplicativo será iniciada.  
  
 Essa estratégia funciona melhor para conexões de rede de alta largura da banda; o atraso para iniciar o aplicativo pode ser inaceitavelmente longo em conexões de baixa largura de banda.  
  
 Para habilitar essa estratégia de atualização, clique em **antes de iniciar o aplicativo** na **escolha quando o aplicativo deve verificar por atualizações** seção o **atualizações do aplicativo** caixa de diálogo.  
  
 Isso é o mesmo que alterar o **atualização** elemento na implantação de manifesto da seguinte maneira:  
  
```xml  
<!-- When to check for updates -->  
<subscription>  
   <update>  
      <beforeApplicationStartup />  
   </update>  
</subscription>  
```  
  
## <a name="make-updates-required"></a>Fazer as atualizações necessárias  
 Talvez haja ocasiões em que você deseje exigir que usuários executem uma versão atualizada de seu aplicativo. Por exemplo, você pode fazer uma alteração em um recurso externo como um serviço Web que impeça o funcionamento correto da versão anterior de seu aplicativo. Nesse caso, talvez você deseje marcar sua atualização como obrigatória e evitar que os usuários executem a versão anterior.  
  
> [!NOTE]
>  Embora você possa exigir atualizações por meio de outras estratégias de atualização, verificando **antes de iniciar o aplicativo** é a única maneira de garantir que uma versão mais antiga não pode ser executada. Quando a atualização obrigatória for detectada na inicialização, o usuário deverá aceitar a atualização ou fechar o aplicativo.  
  
 Para marcar uma atualização como requerido, clique em **especificar uma versão mínima necessária para este aplicativo** na **aplicativo atualiza** caixa de diálogo caixa e, em seguida, especifique a versão de publicação (**principal**, **Secundárias**, **Build**, **revisão**), que especifica o menor número de versão do aplicativo que pode ser instalado.  
  
 Isso é o mesmo que definir a **minimumRequiredVersion** atributo da **implantação** elemento no manifesto de implantação; por exemplo:  
  
```xml  
<deployment install="true" minimumRequiredVersion="1.0.0.0">  
```  
  
## <a name="specify-update-intervals"></a>Especifique os intervalos de atualização  
 Você também pode especificar a frequência com que o aplicativo verificará se há atualizações. Para fazer isso, especifique a verificação de atualizações pelo aplicativo após a inicialização como descrito em "Verificando se há atualizações após a inicialização do aplicativo" anteriormente neste tópico.  
  
 Para especificar o intervalo de atualização, defina as **especifique a frequência com que o aplicativo deve verificar se há atualizações** propriedades na **atualizações de aplicativos** caixa de diálogo.  
  
 Isso é o mesmo que definir a **maximumAge** e **unidade** atributos do **atualização** elemento no manifesto de implantação.  
  
 Por exemplo, talvez você deseje verificar sempre que o aplicativo é executado, uma vez por semana ou uma vez por mês. Se uma conexão de rede não estiver presente na hora especificada, a verificação de atualização será executada na próxima vez que o aplicativo for executado.  
  
## <a name="provide-a-user-interface-for-updates"></a>Fornecer uma interface do usuário para atualizações  
 Ao usar esta estratégia, o desenvolvedor de aplicativos fornece uma interface que permite ao usuário escolher quando ou com que frequência o aplicativo verificará se há atualizações. Por exemplo, você pode fornecer um comando "Verificar se Há Atualizações" ou uma caixa de diálogo "Configurações de Atualização" que contenha escolhas para intervalos de atualização diferentes. O [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] APIs de implantação fornecem uma estrutura para a programação de sua própria interface de usuário de atualização. Para obter mais informações, consulte o namespace de <xref:System.Deployment.Application>.  
  
 Se seu aplicativo usar APIs de implantação para controlar sua própria lógica de atualização, você deverá bloquear a verificação de atualização como descrito em "Bloqueando verificação de atualizações" na seção a seguir.  
  
 Essa estratégia funciona melhor quando você necessita de estratégias de atualização diferentes para usuários diferentes.  
  
## <a name="block-update-checking"></a>Bloquear a verificação de atualização  
 Também é possível evitar que seu aplicativo verifique se há atualizações. Por exemplo, você pode ter um aplicativo simples que nunca será atualizado, mas deseje usufruir dessa facilidade de instalação fornecida pela implantação de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)].  
  
 Você também deve bloquear a atualização verificando se seu aplicativo usa APIs de implantação para executar suas próprias atualizações; consulte "Fornecer uma interface do usuário para atualizações" no início deste tópico.  
  
 Para bloquear a verificação de atualização, desmarque a **o aplicativo deve verificar por atualizações** caixa de seleção na caixa de diálogo atualizações do aplicativo.  
  
 Você também pode bloquear a verificação de atualizações ao remover a marca `<Subscription>` do manifesto de implantação.  
  
## <a name="permission-elevation-and-updates"></a>Atualizações e elevação de permissões  
 Se uma nova versão de um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] exigir um nível mais alto de confiança para execução do que a versão anterior, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] perguntará ao usuário se ele deseja que o aplicativo receba esse nível mais alto de confiança. Se o usuário recusar a concessão do nível mais alto de confiança, a atualização não será instalada. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] solicitará que o usuário instale o aplicativo novamente quando ele for reiniciado na próxima vez. Se o usuário recusar conceder o nível mais alto de confiança neste momento, e a atualização não estiver marcada como o necessário, a versão antiga do aplicativo será executada. No entanto, se a atualização for necessária, o aplicativo não será executado novamente até que o usuário aceite o nível mais alto de confiança.  
  
 Nenhum aviso sobre níveis de confiança ocorrerá se você usar a Implantação de Aplicativo de Confiança. Para obter mais informações, consulte [visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md).  
  
## <a name="see-also"></a>Consulte também  
 \<XRef:System.Deployment.Application >   
 [Implantação e segurança do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Como o ClickOnce executa atualizações de aplicativos](../deployment/how-clickonce-performs-application-updates.md)   
 [Como: gerenciar atualizações para um aplicativo ClickOnce](../deployment/how-to-manage-updates-for-a-clickonce-application.md)