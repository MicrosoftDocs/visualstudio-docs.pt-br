---
title: Proteger aplicativos ClickOnce | Microsoft Docs
ms.date: 02/17/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce security
- ClickOnce deployment, security
- deploying applications, ClickOnce security
ms.assetid: a05b5f2f-d1f2-471a-8096-8b11f7554265
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d99cbf4aaa30e1afb95a98743c223edee94d98fe
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85286291"
---
# <a name="secure-clickonce-applications"></a>Proteger aplicativos ClickOnce
Os aplicativos [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] estão sujeitos às restrições de segurança de acesso a código no .NET Framework para ajudar a limitar o acesso que o código tem a recursos e operações protegidos. Por esse motivo, é importante compreender as implicações de segurança de acesso a código para desenvolver seus aplicativos [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] adequadamente. Seus aplicativos podem usar o modo Confiança Total ou zonas parciais, como as zonas da Internet e intranet, para limitar o acesso.

 Além disso, o ClickOnce usa certificados para verificar a autenticidade do editor do aplicativo e assinar os manifestos do aplicativo e de implantação para provar que os arquivos não foram violados. Assinar é uma etapa opcional, o que facilita alterar os arquivos do aplicativo depois que os manifestos são gerados. No entanto, sem manifestos assinados, é difícil assegurar que o instalador do aplicativo não seja violado em ataques de segurança a intermediários. Por isso, recomendamos assinar seus manifestos do aplicativo e de implantação para ajudar a proteger seus aplicativos.

## <a name="zones"></a>Zonas
 Os aplicativos que são implantados usando a tecnologia [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] são restritos a um conjunto de permissões e ações definidas pela zona de segurança. As zonas de segurança são definidas no Internet Explorer e baseadas no local do aplicativo. A tabela a seguir lista as permissões padrão com base no local de implantação:

|Local da implantação|Zona de segurança|
|-------------------------|-------------------|
|Executar da Web|Zona da Internet|
|Instalar da Web|Zona da Internet|
|Instalar do compartilhamento de arquivos de rede|Zona de Intranet Local|
|Instalar de CD-ROM|Confiança Total|

 As permissões padrão são baseadas no local do qual a versão original do aplicativo foi implantada; as atualizações para o aplicativo herdarão as permissões. Se o aplicativo estiver configurado para verificar se há atualizações de um local na Web ou rede e uma versão mais recente estiver disponível, a instalação original poderá receber permissões para a zona da Internet ou intranet em vez de permissões de confiança total. Para evitar solicitações aos usuários, um administrador de sistema poderá especificar uma política de implantação ClickOnce que defina um editor de aplicativos específico como uma fonte confiável. Para computadores nos quais esta política é implantada, as permissões serão concedidas automaticamente e o usuário não será interpelado. Para saber mais, veja [Visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md). Para configurar a implantação do aplicativo de confiança, o certificado poderá ser instalado no computador ou em nível corporativo. Para saber mais, veja [Como adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md).

## <a name="code-access-security-policies"></a>Políticas de segurança de acesso a código
 As permissões para um aplicativo são determinadas pelas configurações no elemento [ \<trustInfo> Element](../deployment/trustinfo-element-clickonce-application.md) do manifesto do aplicativo. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] gerencia automaticamente essas informações com base nas configurações na página de propriedades de **Segurança** do projeto. Um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] recebe apenas as permissões específicas que ele solicita. Por exemplo, onde o acesso ao arquivo exige permissões de confiança total, se o aplicativo solicitar permissão de acesso a arquivos, ele receberá apenas permissão de acesso a arquivos, não permissões de confiança total. Ao desenvolver seu aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], certifique-se de solicitar apenas as permissões específicas que o aplicativo precisa. Na maioria dos casos, você pode usar zonas da Internet ou intranet local para limitar seu aplicativo à confiança parcial. Para saber mais, veja [Como definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md). Se seu aplicativo exigir permissões personalizadas, você poderá criar uma zona personalizada. Para saber mais, veja [Como definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md).

 Incluir uma permissão que não faça parte do conjunto de permissões padrão para a zona da qual o aplicativo será implantado fará com que o usuário final seja solicitado a conceder permissão no momento da instalação ou atualização. Para evitar solicitações aos usuários, um administrador de sistema poderá especificar uma política de implantação ClickOnce que defina um editor de aplicativos específico como uma fonte confiável. Em computadores onde esta política é implantada, permissões serão concedidas automaticamente e o usuário não será interpelado.

 Como um desenvolvedor, você é responsável por garantir que seu aplicativo seja executado com as permissões apropriadas. Se o aplicativo solicitar permissões fora de uma zona durante o tempo de execução, uma exceção de segurança poderá aparecer. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]permite que você depure seu aplicativo na zona de segurança de destino e fornece ajuda para desenvolver aplicativos seguros. Para obter mais informações, consulte [depurar aplicativos ClickOnce que usam System. Deployment. Application](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md).

 Para saber mais sobre a segurança de acesso do código e o ClickOnce, veja [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md).

## <a name="code-signing-certificates"></a>Certificados de assinatura de código
 Para publicar um aplicativo usando a implantação de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], você pode assinar os manifestos do aplicativo e de implantação para o aplicativo ao usar um par de chaves pública/privada. As ferramentas para assinar um manifesto estão disponíveis na página **Assinando** do **Designer de Projeto**. Para saber mais, veja [Página de Assinatura, Designer de Projeto](../ide/reference/signing-page-project-designer.md).

 Depois que os manifestos são assinados, as informações do editor baseadas na assinatura Authenticode serão exibidas para o usuário na caixa de diálogo de permissões durante a instalação, para mostrar que o aplicativo é oriundo de uma fonte confiável.

 Para saber mais sobre ClickOnce e certificados, veja [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md).

## <a name="aspnet-form-based-authentication"></a>Autenticação baseada em formulários ASP.NET
 Se você desejar controlar quais implantações cada usuário pode acessar, não habilite acesso anônimo aos aplicativos [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantados em um servidor Web. Em vez disso, habilite acesso de usuários às implantações instaladas com base em uma identidade de usuário usando a autenticação do Windows.

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] não dá suporte à autenticação baseada em formulários ASP.NET, pois ela usa cookies persistentes; eles representam um risco à segurança porque residem no cache do Internet Explorer e podem ser violados. Portanto, se você estiver implantando aplicativos [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], não haverá suporte a qualquer cenário de autenticação além da autenticação do Windows.

## <a name="pass-arguments"></a>Passar argumentos
 Uma consideração adicional sobre segurança ocorrerá se você tiver que passar argumentos para um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] permite que os desenvolvedores forneçam uma cadeia de caracteres de consulta para aplicativos implantados na Web. A cadeia de caracteres de consulta assume a forma de uma série de pares nome-valor no fim da URL utilizada para iniciar o aplicativo:

 `http://servername.adatum.com/WindowsApp1.application?username=joeuser`

 Por padrão, os argumentos da cadeia de caracteres de consulta estão desabilitados. Para habilitá-los, o atributo `trustUrlParameters` deverá ser definido no manifesto de implantação do aplicativo. Esse valor pode ser definido de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e MageUI.exe. Para obter etapas detalhadas sobre como habilitar a passagem de cadeias de caracteres de consulta, confira [Como recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce online](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md).

 Você nunca deve passar argumentos recuperados por meio de uma cadeia de caracteres de consulta a um banco de dados ou linha de comando sem verificar os argumentos para garantir que eles sejam seguros. Os argumentos inseguros são os que incluem caracteres de escape da linha de comando ou banco de dados que poderiam permitir que um usuário mal-intencionado manipulasse o seu aplicativo e executasse comandos arbitrários.

> [!NOTE]
> Os argumentos de cadeia de caracteres de consulta são a única maneira de passar argumentos para um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] na inicialização. Você não poderá passar argumentos para um aplicativo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] da linha de comando.

## <a name="deploying-obfuscated-assemblies"></a>Implantando assemblies ofuscados
 O Visual Studio inclui a versão gratuita da [PreEmptive Protection – Dotfuscator Community](../ide/dotfuscator/index.md), que pode ser usada para proteger os aplicativos ClickOnce por meio de ofuscação de código e medidas de proteção ativas.  Para obter detalhes, veja [Seção do ClickOnce do Guia do Usuário do Dotfuscator Community](https://www.preemptive.com/dotfuscator/ce/docs/help/5.27/advanced_clickonce.html).

## <a name="see-also"></a>Veja também
- [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)
- [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)
