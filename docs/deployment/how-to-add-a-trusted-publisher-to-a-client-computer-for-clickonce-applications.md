---
title: 'Como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- trusted application deployment, Trusted Publishers
ms.assetid: 35fe324c-45a1-4509-b7be-5c18b4b1b4ab
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 05fec72b143ccd36cb0a07f17d4bea4b6319eb20
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39155308"
---
# <a name="how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications"></a>Como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce
Com a implantação de aplicativos confiáveis, você pode configurar computadores cliente para que seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos executados com um nível mais alto de confiança, sem avisar o usuário. Os procedimentos a seguir mostram como usar a ferramenta de linha de comando CertMgr.exe para adicionar um certificado de editor para o repositório de editores confiáveis em um computador cliente.  
  
 Os comandos usados variam um pouco dependendo se a autoridade de certificação (CA) que emitiu o certificado for parte de raiz confiável de um cliente. Se um computador de cliente do Windows fizer parte de um domínio, ele conterá, em uma lista, autoridades de certificação que são considerados raízes confiáveis. Geralmente, essa lista é configurada pelo administrador do sistema. Se seu certificado foi emitido por uma dessas raízes confiáveis ou por uma autoridade de certificação que se encadeie a um dessas raízes confiáveis, você pode adicionar o certificado ao repositório de raiz confiável do cliente. Se, por outro lado, o seu certificado não foi emitido por uma dessas raízes confiáveis, você deve adicionar o certificado para o repositório de raiz confiável do cliente e armazenamento de fornecedor confiável.  
  
> [!NOTE]
>  Você deve adicionar certificados dessa maneira em cada computador cliente para o qual você planeja implantar uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que requer permissões elevadas. Adicione os certificados manualmente ou por meio de um aplicativo que você distribuir aos seus clientes. Você só precisará configurar esses computadores de uma vez, após o qual você pode implantar qualquer quantidade de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos assinados com o mesmo certificado.  
  
 Você também pode adicionar um certificado para um armazenamento de forma programática, usando o <xref:System.Security.Cryptography.X509Certificates.X509Store> classe.  
  
 Para uma visão geral da implantação de aplicativos confiáveis, consulte [visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md).  
  
### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-the-trusted-root"></a>Para adicionar um certificado no repositório de editores confiáveis sob a raiz confiável  
  
1.  Obter um certificado digital de uma autoridade de certificação.  
  
2.  Exportar o certificado nos x. 509 Base64 (*. cer*) formato. Para obter mais informações sobre formatos de certificado, consulte [exportar um certificado](http://go.microsoft.com/fwlink/?LinkId=164793).  
  
3.  Do prompt de comando em computadores cliente, execute o seguinte comando:  
  
     **certmgr.exe-adicionar chaves públicas - c -s - r localMachine TrustedPublisher**  
  
### <a name="to-add-a-certificate-to-the-trusted-publishers-store-under-a-different-root"></a>Para adicionar um certificado ao repositório de editores confiáveis em uma raiz diferente  
  
1.  Obter um certificado digital de uma autoridade de certificação.  
  
2.  Exportar o certificado nos x. 509 Base64 (*. cer*) formato. Para obter mais informações sobre formatos de certificado, consulte [exportar um certificado](http://go.microsoft.com/fwlink/?LinkId=164793).  
  
3.  Do prompt de comando em computadores cliente, execute o seguinte comando:  
  
     **certmgr.exe-adicionar good.cer - c -s - r localMachine raiz**  
  
     **certmgr.exe-adicionar good.cer - c -s - r localMachine TrustedPublisher**  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Implantar um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)   
 [Visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md)   
 [Como: Habilitar configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)   
 [Como: definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [Como: definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Como: depurar um aplicativo ClickOnce com permissões restritas](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [Como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [Como: assinar novamente os manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md)   
 [Como: configurar o comportamento do prompt confiável do ClickOnce](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)