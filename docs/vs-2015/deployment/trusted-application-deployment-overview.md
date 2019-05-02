---
title: Trusted Application Deployment Overview | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- ClickOnce deployment, security
- trusted application deployment
ms.assetid: b24a1702-8fbe-45b1-87a0-9618a0708f1d
caps.latest.revision: 33
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 869a756b1995a1ae5de3736fcee4ccede6cb46e5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427107"
---
# <a name="trusted-application-deployment-overview"></a>Visão geral da implantação de aplicativos confiáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico fornece uma visão geral de como implantar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos que têm permissões elevadas, usando a tecnologia de implantação de aplicativos confiáveis.  
  
 Confiável para implantação do aplicativo, parte do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] tecnologia de implantação, torna mais fácil para as organizações de qualquer tamanho para conceder permissões adicionais a um aplicativo gerenciado de maneira mais seguro sem nenhum aviso ao usuário. Com a implantação de aplicativo confiável, uma organização pode simplesmente configurar um computador cliente para ter uma lista de editores confiáveis, que são identificados usando certificados Authenticode. Depois disso, qualquer [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo assinado por um destes trusted publishers recebe um nível mais alto de confiança.  
  
> [!NOTE]
> Confiável para que implantação de aplicativo requer uma configuração única de um computador do usuário. Em ambientes de área de trabalho gerenciados, essa configuração pode ser executada por meio da política global. Se isso é não o que você deseja para seu aplicativo, use a elevação de permissões. Para obter mais informações, consulte [Securing ClickOnce Applications](../deployment/securing-clickonce-applications.md) (Protegendo aplicativos ClickOnce).  
  
## <a name="trusted-application-deployment-basics"></a>Noções básicas sobre a implantação do aplicativo confiável  
 A tabela a seguir mostra os objetos e as funções que estão envolvidas na implantação de aplicativos confiáveis.  
  
|Objeto ou função|Descrição|  
|--------------------|-----------------|  
|administrador|A entidade organizacional responsável por atualizar e manter os computadores cliente|  
|Gerenciador de confiança|O subsistema de dentro do common language runtime (CLR) responsável pela aplicação de segurança do aplicativo cliente.|  
|editor|A entidade que grava e mantém o aplicativo.|  
|implantador|A entidade que empacota e distribui o aplicativo aos usuários.|  
|certificado|Uma assinatura criptográfica que consiste em uma chave pública e privada; Geralmente, emitidos por uma autoridade de certificação (CA) que pode comprovar sua autenticidade.|  
|Certificado Authenticode|Um certificado com o embedded metadados que descrevem, entre outras coisas, os usos para o qual o certificado pode ser empregado.|  
|autoridade de certificação|Uma organização que verifica a identidade de editores e emite os certificados são inseridos com metadados do publicador.|  
|autoridade raiz|Uma autoridade de certificação que autoriza a outras autoridades de certificação para emitir certificados.|  
|contêiner de chave|Um espaço de armazenamento lógico no Microsoft Windows para o armazenamento de certificados.|  
|fornecedor confiável|Um publicador cujo certificado Authenticode foi adicionado a uma lista de certificados confiáveis (CTL) em um computador cliente.|  
  
 Em organizações maiores, o publicador e o implantador são frequentemente duas entidades separadas:  
  
- O publicador é o grupo que cria o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo.  
  
- O implantador é o grupo, normalmente o departamento de TI (tecnologia) de informações, que distribui [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo em computadores de área de trabalho corporativa.  
  
  Você deve seguir estas etapas para tirar proveito da implantação de aplicativos confiáveis:  
  
1. Obter um certificado para o publicador.  
  
2. Adicione o publicador para o repositório de editores confiáveis em todos os clientes.  
  
3. Crie seu aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].  
  
4. Assinar o manifesto de implantação com o certificado do Editor.  
  
5. Publica a implantação do aplicativo em computadores cliente.  
  
### <a name="obtain-a-certificate-for-the-publisher"></a>Obter um certificado para o publicador  
 Certificados digitais são um componente principal do sistema de segurança e autenticação do Microsoft Authenticode. Authenticode é uma parte padrão do sistema operacional Windows. Todos os [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos devem ser assinados com um certificado digital, independentemente se eles participarem de implantação de aplicativos confiáveis. Para obter uma explicação completa de como funciona com o Authenticode [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], consulte [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md).  
  
### <a name="add-the-publisher-to-the-trusted-publishers-store"></a>Adicionar o publicador para a Store de editores confiáveis  
 Para sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo para receber um nível mais alto de confiança, você deve adicionar o certificado como um editor confiável para cada computador cliente no qual o aplicativo será executado. Para executar essa tarefa é uma configuração única. Depois de concluído, você pode implantar tantos [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos assinados com seu certificado de editor como deseja, e eles serão executados com confiança alta.  
  
 Se você estiver implantando seu aplicativo em um ambiente gerenciado da área de trabalho; Por exemplo, uma intranet corporativa executando o sistema operacional Windows; Você pode adicionar editores confiáveis ao armazenamento de um cliente, criando uma nova lista de certificados confiáveis (CTL) com a política de grupo. Para obter mais informações, consulte [criar uma lista de certificados confiáveis para um objeto de diretiva de grupo](http://go.microsoft.com/fwlink/?LinkId=102576).  
  
 Se você não estiver implantando seu aplicativo em um ambiente gerenciado de área de trabalho, você tem as seguintes opções para adicionar um certificado para o repositório fornecedores confiáveis:  
  
- O namespace <xref:System.Security.Cryptography?displayProperty=fullName>.  
  
- CertMgr.exe, que é um componente do Internet Explorer e, portanto, existe no Windows 98 e todas as versões posteriores. Para obter mais informações, consulte [Certmgr.exe (ferramenta de Gerenciador de certificados)](http://msdn.microsoft.com/library/7e953b43-1374-4bbc-814f-53ca1b6b52bb).  
  
### <a name="create-a-clickonce-application"></a>Criar um aplicativo ClickOnce  
 Um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo é um [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] aplicativo cliente combinado com os arquivos de manifesto que descrevem o aplicativo e fornecem parâmetros de instalação. Você pode ativar o seu programa em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo usando o **Publish** no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Como alternativa, você pode gerar todos os arquivos necessários para o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação usando as ferramentas que estão incluídas com o [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]. Para obter etapas detalhadas sobre [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação, consulte [passo a passo: Como implantar manualmente aplicativos ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  
  
 Implantação de aplicativo confiável é específica para [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]e só pode ser usado com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos.  
  
### <a name="sign-the-deployment"></a>Se a implantação  
 Depois de obter seu certificado, você deve usá-lo para assinar a sua implantação. Se você estiver implantando seu aplicativo usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Assistente de publicação, o assistente irá gerar automaticamente um certificado de teste para que você se você não especificou um certificado por conta própria. Você também pode usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela do Designer de projeto, no entanto, para fornecer um certificado fornecido por uma autoridade de certificação.  Consulte também [como: Publicar um aplicativo ClickOnce usando o Assistente de publicação](http://msdn.microsoft.com/library/31kztyey\(v=vs.110\)) ou [como: Publicar um aplicativo ClickOnce usando o assistente de publicação](http://msdn.microsoft.com/library/31kztyey\(v=vs.110\)).  
  
> [!CAUTION]
> Não é recomendável que o aplicativo ser implantado com um certificado de teste.  
  
 Você também pode assinar o aplicativo usando as ferramentas Mage.exe ou MageUI.exe SDK. Para obter mais informações, confira [Passo a passo: Como implantar manualmente aplicativos ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Para obter uma lista completa das opções de linha de comando relacionados à entrada de implantação, consulte [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1).  
  
### <a name="publish-the-application"></a>Publicar o aplicativo  
 Assim que você entrar com sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos, o aplicativo está pronto para publicar seu local de instalação. O local de instalação pode ser um servidor Web, um compartilhamento de arquivos ou no disco local. Quando um cliente acessa o manifesto de implantação pela primeira vez, o Gerenciador de confiança deve escolher se o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo recebeu autoridade ou não sejam executadas em um nível mais alto de confiança por instalado confiável publicador. O Gerenciador de confiança torna essa opção, comparando o certificado usado para assinar a implantação com os certificados armazenados no publicador de confiáveis do cliente armazenar. Se o Gerenciador de confiança encontra uma correspondência, o aplicativo é executado com confiança alta.  
  
## <a name="trusted-application-deployment-and-permission-elevation"></a>Implantação de aplicativos confiáveis e elevação de permissões  
 Se o publicador atual não for um fornecedor confiável, o Gerenciador de confiança usará elevação de permissões para consultar o usuário sobre se ele quer conceder que permissões elevadas do seu aplicativo. No entanto, se a elevação de permissões é desabilitada pelo administrador, o aplicativo não pode obter permissão para executar. O aplicativo não será executado e nenhuma notificação será exibida ao usuário. Para obter mais informações sobre a elevação de permissões, consulte [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).  
  
## <a name="limitations-of-trusted-application-deployment"></a>Limitações da implantação de aplicativos confiáveis  
 Você pode usar a implantação de aplicativos confiáveis para conceder confiança elevada para [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos implantados pela Web ou por meio de um compartilhamento de arquivos da empresa. Você não precisa usar a implantação de aplicativos confiáveis para [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos distribuídos em um CD, porque, por padrão, esses aplicativos recebem confiança total.  
  
## <a name="see-also"></a>Consulte também  
 [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [Passo a passo: Como implantar manualmente aplicativos ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
