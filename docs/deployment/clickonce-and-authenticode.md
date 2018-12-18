---
title: ClickOnce e Authenticode | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- .pfx files
- ClickOnce deployment, Authenticode
- Authenticode, ClickOnce
- ClickOnce deployment, certificates
- ClickOnce deployment, security
ms.assetid: ab5b6712-f32a-4e33-842f-e88ab4818ccf
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bc0018533f089c2be3d0a94093bf41deadd9a74e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49907437"
---
# <a name="clickonce-and-authenticode"></a>ClickOnce e Authenticode
*Authenticode* é uma tecnologia da Microsoft que usa criptografia padrão do setor para assinar código do aplicativo com certificados digitais que verificam a autenticidade do Editor do aplicativo. Por meio de Authenticode para implantação de aplicativo, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] reduz o risco de um cavalo de Troia. Um cavalo de Troia é um vírus ou outro programa prejudicial que um terceiro mal-intencionado deturpe como um programa legítimo proveniente de uma fonte confiável e estabelecida. Assinatura [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantações com um certificado digital é uma etapa opcional para verificar que os assemblies e arquivos não são alterados.  
  
 As seções a seguir descrevem os diferentes tipos de certificados digitais usados em Authenticode, como os certificados são validados usando certificado autoridades (CAs), a função de carimbo de hora em certificados e os métodos de armazenamento disponível para certificados.  
  
## <a name="authenticode-and-code-signing"></a>Authenticode e assinatura de código  
 Um *certificado digital* é um arquivo que contém um pública/privada par de chaves criptográficas, juntamente com metadados que descrevem o publicador para quem o certificado foi emitido e a agência que emitiu o certificado.  
  
 Há vários tipos de certificados Authenticode. Cada um deles está configurado para diferentes tipos de assinatura. Para [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos, você deve ter um certificado Authenticode que é válido para assinatura de código. Se você tentar entrar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo com outro tipo de certificado, tais como um certificado digital de email, ele não funcionará. Para obter mais informações, consulte [Introdução à assinatura de código](http://go.microsoft.com/fwlink/?LinkId=179452).  
  
 Você pode obter um certificado de assinatura de código em uma destas três maneiras:  
  
- Compre um de um fornecedor de certificado.  
  
- Receba um de um grupo em sua organização responsável pela criação de certificados digitais.  
  
- Gerar seu próprio certificado usando o cmdlet New-SelfSignedCertificate do PowerShell ou usando *MakeCert.exe*, que é incluído com o [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)].  
  
### <a name="how-using-certificate-authorities-helps-users"></a>Como usar autoridades de certificação ajuda os usuários  
 Um certificado gerado usando New-SelfSignedCertificate ou o *MakeCert.exe* utilitário é comumente chamado de um *self-cert* ou uma *teste cert*. Esse tipo de certificado funciona quase da mesma forma que um *. snk* arquivo funciona no .NET Framework. Ele consiste exclusivamente em um par de chaves criptográficas pública/privada e não contém nenhuma informação verificável sobre o publicador. Você pode usar certificados de autoatendimento para implantar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos com alta confiança em uma intranet. No entanto, quando esses aplicativos são executados em um computador cliente, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] identificará como proveniente de um editor desconhecido. Por padrão, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos assinados com certificados de autoatendimento e implantados pela Internet não é possível utilizar a implantação de aplicativos confiáveis.  
  
 Por outro lado, se você receber um certificado de autoridade de certificação, como um fornecedor de certificado ou um departamento dentro de sua empresa, o certificado oferece mais segurança para seus usuários. Ele não só identifica o Editor de software assinado, mas ele verifica essa identidade examinando-se com a autoridade de certificação que assinou. Se a autoridade de certificação não é a autoridade raiz, Authenticode serão também "encadear" volta para a autoridade de raiz para verificar se a autoridade de certificação está autorizada para emitir certificados. Para maior segurança, você deve usar um certificado emitido por uma autoridade de certificação sempre que possível.  
  
 Para obter mais informações sobre como gerar certificados de autoatendimento, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) ou [MakeCert](/windows/desktop/SecCrypto/makecert).  
  
### <a name="timestamps"></a>Carimbos de hora  
 Os certificados usados para assinar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos expiram após um determinado período de tempo, normalmente doze meses. Para remover a necessidade de constantemente assinar novamente aplicativos com novos certificados, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] dá suporte ao carimbo de hora. Quando um aplicativo é assinado com um carimbo de hora, o seu certificado continuará a ser aceito, mesmo após a expiração, contanto que o carimbo de hora é válido. Isso permite que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos com certificados expirados, mas os carimbos de hora válidos, para baixar e executar. Ele também permite que aplicativos instalados com certificados expirados para continuar a baixar e instalar atualizações.  
  
 Para incluir um carimbo de hora em um servidor de aplicativos, um servidor de carimbo de hora deve estar disponível. Para obter informações sobre como selecionar um servidor de carimbo de hora, consulte [como: sinal de manifestos de aplicativo e implantação](../ide/how-to-sign-application-and-deployment-manifests.md).  
  
### <a name="update-expired-certificates"></a>Atualizar certificados expirados  
 Em versões anteriores do .NET Framework, a atualização de um aplicativo cujo certificado tivesse expirado pode causar que o aplicativo pare de funcionar. Para resolver esse problema, use um dos seguintes métodos:  
  
-   Atualize o .NET Framework para a versão 2.0 SP1 ou posterior no Windows XP, ou a versão 3.5 ou posterior no Windows Vista.  
  
-   Desinstalar o aplicativo e reinstale uma nova versão com um certificado válido.  
  
-   Crie um assembly de linha de comando que atualiza o certificado. Informações passo a passo sobre esse processo podem ser encontradas em [925521 de artigo de suporte do Microsoft](http://go.microsoft.com/fwlink/?LinkId=179454).  
  
### <a name="store-certificates"></a>Certificados de Store  
  
- Você pode armazenar certificados como uma *. pfx* arquivo em seu sistema de arquivos, ou você pode armazená-los dentro de um contêiner de chave. Um usuário em um domínio do Windows pode ter um número de contêineres de chave. Por padrão, *MakeCert.exe* irá armazenar certificados em seu contêiner de chave particular, a menos que você especifique que ela deve salvá-la em um *. pfx* em vez disso. *Mage.exe* e *MageUI.exe*, o [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] ferramentas para criar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantações, permitem que você use certificados armazenados de qualquer maneira.  
  
## <a name="see-also"></a>Consulte também  
 [Implantação e segurança do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md)   
 [Mage.exe (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)