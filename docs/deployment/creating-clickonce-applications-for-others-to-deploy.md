---
title: Criando aplicativos ClickOnce para implantar para outras pessoas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- preserved branding information
- useManifestForTrust element
- customer deployments [ClickOnce]
- multiple ClickOnce deployment and branding
- ClickOnce applications, previous .NET Framework versions
- application manifests [ClickOnce]
- <useManifestForTrust> element
- manifests [ClickOnce]
- trust applications, ClickOnce
- ClickOnce applications, deployed by others
- ClickOnce applications, previous .NET Framework
ms.assetid: d20766c7-4ef3-45ab-8aa0-3f15b61eccaa
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b74e8a988505c5386b444df27f7726a8ceb51a62
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870764"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>Criar aplicativos ClickOnce para implantar outras pessoas
Nem todos os desenvolvedores que estão criando implantações do ClickOnce planejam implantar os próprios aplicativos. Muitos deles apenas empacotar seu aplicativo usando o ClickOnce e, em seguida, entregar os arquivos para um cliente, como uma grande corporação. O cliente torna-se a um responsável por hospedar o aplicativo em sua rede. Este tópico discute alguns dos problemas inerentes a tais implantações em versões do .NET Framework anteriores à versão 3.5. Ele descreve, em seguida, uma nova solução fornecida usando o novo recurso de "usar o manifesto para relação de confiança" no .NET Framework 3.5. Por fim, ele conclui com estratégias recomendadas para a criação de implantações do ClickOnce para clientes que ainda estejam usando versões mais antigas do .NET Framework.  
  
## <a name="issues-involved-in-creating-deployments-for-customers"></a>Problemas envolvidos na criação de implantações para clientes  
 Vários problemas ocorrem quando você planeja fornecer uma implantação de um cliente. O primeiro problema diz respeito a assinatura de código. Para ser implantado em uma rede, o manifesto de implantação e o manifesto do aplicativo de uma implantação de ClickOnce devem ambos ser assinados com um certificado digital. Isso levanta a questão de se usar o certificado do desenvolvedor ou o certificado do cliente ao assinar os manifestos.  
  
 A questão de qual certificado usar é crítica, como identidade de um aplicativo ClickOnce se baseia na assinatura digital do manifesto de implantação. Se o desenvolvedor assina o manifesto de implantação, isso pode levar a conflitos se o cliente é uma grande empresa, e mais de uma divisão da empresa implanta uma versão personalizada do aplicativo.  
  
 Por exemplo, digamos que a Adventure Works tem um departamento financeiro e um departamento de recursos humanos. Ambos os departamentos de licença de um aplicativo ClickOnce da Microsoft Corporation, que gera relatórios dos dados armazenados em um banco de dados SQL. A Microsoft fornece a cada departamento com uma versão do aplicativo que é personalizado para seus dados. Se os aplicativos são assinados com o mesmo certificado Authenticode, um usuário que tenta usar os dois aplicativos seria encontrar um erro, como ClickOnce considere o segundo aplicativo como sendo idêntico ao primeiro. Nesse caso, o cliente pode apresentar efeitos colaterais indesejáveis e imprevisíveis que incluem a perda de todos os dados armazenados localmente pelo aplicativo.  
  
 Um problema adicional relacionado à assinatura de código é o `deploymentProvider` elemento no manifesto de implantação, que informa ao ClickOnce onde procurar por atualizações de aplicativo. Esse elemento deve ser adicionado ao manifesto de implantação antes de assinar a ele. Se esse elemento for adicionado posteriormente, o manifesto de implantação deve ser assinado novamente.  
  
### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>Exigem que o cliente assinar o manifesto de implantação  
 Uma solução para esse problema de implantações não exclusivo é ter o sinal do desenvolvedor o manifesto do aplicativo e o cliente entre o manifesto de implantação. Embora essa abordagem funciona, ele apresenta outros problemas. Uma vez que um certificado Authenticode deve permanecer um ativo protegido, o cliente não pode conceder apenas o certificado para o desenvolvedor assine a implantação. Embora o cliente possa assinar o manifesto de implantação em si, usando as ferramentas disponíveis gratuitamente com o SDK do .NET Framework, isso pode exigir conhecimento técnico mais do que o cliente está disposto ou é capaz de fornecer. Nesses casos, o desenvolvedor geralmente cria um aplicativo, site da Web ou outro mecanismo por meio do qual o cliente pode enviar sua versão do aplicativo para a assinatura.  
  
### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>O impacto de segurança do aplicativo ClickOnce de assinatura de cliente  
 Mesmo que o desenvolvedor e o cliente concordarem que o cliente deve assinar o manifesto de aplicativo, isso levanta outras questões que envolvem a identidade do aplicativo, especialmente à medida que ele se aplica a implantação de aplicativos confiáveis. (Para obter mais informações sobre esse recurso, consulte [visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md).) Digamos que a Adventure Works quer configurar seus computadores cliente para que qualquer aplicativo fornecido pelo Microsoft Corporation seja executado com confiança total. Se a Adventure Works assina o manifesto de implantação, o ClickOnce usará assinatura de segurança da Adventure Work para determinar o nível de confiança do aplicativo.  
  
## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>Criar implantações de cliente usando o manifesto do aplicativo para relação de confiança  
 ClickOnce no .NET Framework 3.5 contém um novo recurso que oferece uma nova solução de desenvolvedores e clientes para o cenário de como os manifestos devem ser assinados. O manifesto do aplicativo ClickOnce oferece suporte a um novo elemento chamado `<useManifestForTrust>` que permite que um desenvolvedor indicar que a assinatura digital do manifesto do aplicativo é o que deve ser usado para tomar decisões de confiança. O desenvolvedor usa ferramentas de empacotamento do ClickOnce — como *Mage.exe*, *MageUI.exe*e o Visual Studio — para incluir esse elemento no manifesto do aplicativo, bem como para inserir seu nome do publicador e o nome do aplicativo no manifesto.  
  
 Ao usar `<useManifestForTrust>`, o manifesto de implantação não precisa ser assinado com um certificado Authenticode emitido por uma autoridade de certificação. Em vez disso, ele pode ser assinado com o que é conhecido como um certificado autoassinado. Um certificado autoassinado é gerado pelo cliente ou o desenvolvedor por meio de ferramentas padrão do SDK do .NET Framework e, em seguida, aplicado ao manifesto de implantação usando as ferramentas de implantação do ClickOnce padrão. Para obter mais informações, consulte [MakeCert](/windows/desktop/SecCrypto/makecert).  
  
 Usando um certificado autoassinado para o manifesto de implantação apresenta várias vantagens. Eliminando a necessidade do cliente obter ou criar seu próprio certificado Authenticode, `<useManifestForTrust>` simplifica a implantação do cliente, permitindo que o desenvolvedor manter sua própria identidade de identidade visual do aplicativo. O resultado é um conjunto de implantações com sinal que são mais seguros e têm identidades de aplicativo exclusivo. Isso elimina o conflito em potencial que pode ocorrer na implantação do mesmo aplicativo para vários clientes.  
  
 Para obter informações passo a passo sobre como criar uma implantação do ClickOnce com `<useManifestForTrust>` habilitado, consulte [passo a passo: implantar manualmente um aplicativo ClickOnce que não requer nova assinatura e que preserva informações de identidade visual](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md).  
  
### <a name="how-application-manifest-for-trust-works-at-runtime"></a>Como o manifesto do aplicativo para confiança funciona em tempo de execução  
 Para obter uma melhor compreensão de como funciona usando o manifesto do aplicativo para relação de confiança em tempo de execução, considere o exemplo a seguir. Um aplicativo ClickOnce que tem como alvo o .NET Framework 3.5 é criado pela Microsoft. O manifesto do aplicativo usa o `<useManifestForTrust>` elemento e é assinado pela Microsoft. Adventure Works assina o manifesto de implantação usando um certificado autoassinado. Adventure Works que os clientes são configurados para confiar em qualquer aplicativo assinado pela Microsoft.  
  
 Quando um usuário clica em um link para o manifesto de implantação, o ClickOnce instala o aplicativo no computador do usuário. As informações de certificado e a implantação identificar exclusivamente o aplicativo ClickOnce no computador cliente. Se o usuário tenta instalar o mesmo aplicativo novamente de um local diferente, o ClickOnce pode usar essa identidade para determinar se o aplicativo já existe no cliente.  
  
 Em seguida, o ClickOnce examina o certificado Authenticode que é usado para assinar o manifesto do aplicativo, que determina o nível de confiança que o ClickOnce, será concedido. Uma vez que a Adventure Works tiver configurado seus clientes para confiar em qualquer aplicativo assinado pela Microsoft, esse aplicativo ClickOnce é concedido confiança total. Para obter mais informações, consulte [visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md).  
  
## <a name="create-customer-deployments-for-earlier-versions"></a>Criar implantações de cliente para versões anteriores  
 E se um desenvolvedor está implantando aplicativos ClickOnce para clientes que estão usando versões mais antigas do .NET Framework? As seções a seguir resumem várias soluções recomendadas, junto com as vantagens e desvantagens de cada um.  
  
### <a name="sign-deployments-on-behalf-of-customer"></a>Implantações de entrada em nome do cliente  
 É uma estratégia de implantação possíveis para o desenvolvedor criar um mecanismo para assinar as implantações em nome dos clientes, usando a chave privada do cliente. Isso impede que o desenvolvedor ter que gerenciar chaves privadas ou vários pacotes de implantação. O desenvolvedor apenas fornece a mesma implantação para cada cliente. Cabe ao cliente para personalizá-lo para seu ambiente usando o serviço de autenticação.  
  
 Uma desvantagem para esse método é o tempo e as despesas necessários para implementá-lo. Embora esse tipo de serviço pode ser criado usando as ferramentas fornecidas no SDK do .NET Framework, ele adicionará mais tempo de desenvolvimento para o ciclo de vida do produto.  
  
 Conforme observado no início deste tópico, a outra desvantagem é que a versão de cada cliente do aplicativo terá a mesma identidade de aplicativo, que pode levar a conflitos. Se esta for uma preocupação, o desenvolvedor pode alterar o campo de nome é usado ao gerar o manifesto de implantação para dar um nome exclusivo de cada aplicativo. Isso criará uma identidade separada para cada versão do aplicativo e eliminar possíveis conflitos de identidade. Este campo corresponde à `-Name` argumento para Mage.exe e o **nome** campo o **nome** guia no MageUI.exe.  
  
 Por exemplo, digamos que o desenvolvedor criou um aplicativo chamado Application1. Em vez de criar uma única implantação com o campo de nome definido para Application1, o desenvolvedor pode criar várias implantações com esse nome, como Application1-Clientea, Application1-Clienteb, uma variação específica do cliente e assim por diante.  
  
### <a name="deploy-using-a-setup-package"></a>Implantar usando um pacote de instalação  
 Uma estratégia de implantação possíveis a segunda é gerar um projeto Microsoft Setup para realizar a implantação inicial do aplicativo ClickOnce. Isso pode ser fornecida em um dos vários formatos diferentes: como uma implantação de MSI, como um executável de instalação (. EXE), ou como um arquivo de gabinete (. cab) junto com um script em lotes.  
  
 Usando essa técnica, o desenvolvedor seria fornecer ao cliente uma implantação que inclui os arquivos do aplicativo, o manifesto do aplicativo e um manifesto de implantação que serve como um modelo. O cliente executaria o programa de instalação, que solicitaria-los para uma URL de implantação (o servidor ou local do qual os usuários instalarão o aplicativo ClickOnce de compartilhamento de arquivos), bem como um certificado digital. O aplicativo de instalação também pode optar por solicitar opções adicionais de configuração de ClickOnce, como o intervalo de verificação de atualização. Depois que essas informações são reunidas, o programa de instalação seria gerar o manifesto de implantação real, assiná-lo e publicar o aplicativo ClickOnce para o local de servidor designado.  
  
 Há três maneiras de que o cliente possa assinar o manifesto de implantação nessa situação:  
  
1. O cliente pode usar um certificado válido emitido por uma autoridade de certificação (CA).  
  
2. Como uma variação dessa abordagem, o cliente pode escolher assinar seu manifesto de implantação com um certificado autoassinado. A desvantagem é que ele fará com que o aplicativo para exibir as palavras "Editor desconhecido" quando o usuário é perguntado se deseja instalá-lo. No entanto, a vantagem é que ele impede que os clientes menores de precisar gastar tempo e dinheiro necessário para um certificado emitido por uma autoridade de certificação.  
  
3. Por fim, o desenvolvedor pode incluir seu próprio certificado autoassinado no pacote de instalação. Isso apresenta os problemas potenciais com identidade do aplicativo discutida anteriormente neste tópico.  
  
   A desvantagem para o método de projeto de implantação de instalação é o tempo e as despesas necessários para compilar um aplicativo de implantação personalizada.  
  
### <a name="have-customer-generate-deployment-manifest"></a>Fazer com que o cliente gere o manifesto de implantação  
 Uma terceira estratégia de implantação possíveis para lidar é desativar apenas o aplicativo de arquivos e aplicativos de manifesto para o cliente. Nesse cenário, o cliente é responsável por usar o SDK do .NET Framework para gerar e assinar o manifesto de implantação.  
  
 A desvantagem desse método é que ele requer que o cliente para instalar as ferramentas do SDK do .NET Framework e para que um desenvolvedor ou administrador do sistema que é qualificada para usá-los. Alguns clientes podem exigir uma solução que requer pouco ou nenhum esforço técnico de sua parte.  
  
## <a name="see-also"></a>Consulte também  
 [Implantar aplicativos ClickOnce para servidores de teste e produção sem assinar novamente](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)   
 [Passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [Passo a passo: Implantando manualmente um aplicativo ClickOnce que não requer nova assinatura e que preserva informações de identidade Visual](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)