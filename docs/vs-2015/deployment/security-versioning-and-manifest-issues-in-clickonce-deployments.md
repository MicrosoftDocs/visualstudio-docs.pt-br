---
title: Segurança, controle de versão e problemas de manifesto em implantações do ClickOnce | Microsoft Docs
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
- versioning, ClickOnce applications
- ClickOnce applications, Windows Vista User Account Control
- ClickOnce applications, versioning issues
- security, ClickOnce applications
- Windows 7, ClickOnce deployments
- ClickOnce applications, manifest issues
- User Account Control, ClickOnce applications
- Windows Vista, ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, security issues
ms.assetid: d5d0c90b-ac1a-44e2-88dc-0d0ffd881624
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 77685b2eb6397d1edf9a342c25838fcefac2e619
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49289218"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>Problemas de segurança, controle de versão e manifesto em implantações do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Há uma variedade de problemas com a [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] segurança, controle de versão do aplicativo e manifesto sintaxe e semântica que pode causar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação não seja bem-sucedida.  
  
## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce e controle de conta de usuário do Windows Vista  
 No [!INCLUDE[windowsver](../includes/windowsver-md.md)], por padrão, aplicativos executem como usuário padrão, mesmo se o usuário atual está conectado com uma conta que tenha permissões de administrador. Se um aplicativo deve executar uma ação que requer permissões de administrador, ele informa o sistema operacional, que, em seguida, solicita que o usuário insira suas credenciais de administrador. Esse recurso, que é chamado de controle de conta de usuário (UAC), impede que os aplicativos façam alterações que podem afetar todo o sistema operacional sem aprovação explícita de um usuário. Os aplicativos de Windows declaram que exigem essa elevação de permissão, especificando o `requestedExecutionLevel` de atributo no `trustInfo` seção do seu manifesto do aplicativo.  
  
 Devido ao risco de expor os aplicativos a ataques de elevação de segurança, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos não é possível solicitar a elevação de permissões se UAC estiver ativado para o cliente. Qualquer [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo que tenta definir seus `requestedExecutionLevel` atributo `requireAdministrator` ou `highestAvailable` não instalará em [!INCLUDE[windowsver](../includes/windowsver-md.md)].  
  
 Em alguns casos, sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo pode tentar executar com permissões de administrador, devido à lógica de detecção do instalador em [!INCLUDE[windowsver](../includes/windowsver-md.md)]. Nesse caso, você pode definir as `requestedExecutionLevel` atributo no manifesto do aplicativo para `asInvoker`. Isso fará com que o aplicativo seja executado sem a elevação. [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] adiciona automaticamente esse atributo para todos os manifestos de aplicativo.  
  
 Se você estiver desenvolvendo um aplicativo que requer permissões de administrador para o tempo de vida inteiro do aplicativo, você deve considerar a implantação do aplicativo usando a tecnologia Windows Installer (MSI) em vez disso. Para obter mais informações, consulte [Noções básicas do Windows Installer](../extensibility/internals/windows-installer-basics.md).  
  
## <a name="online-application-quotas-and-partial-trust-applications"></a>Aplicativos de confiança parcial e cotas do aplicativo online  
 Se seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo é executada online, em vez de por meio de uma instalação, ele deve se ajustar dentro da cota definida separadamente para aplicativos online. Além disso, um aplicativo de rede que é executado em confiança parcial, como com um conjunto restrito de permissões de segurança, não pode ser maior do que a metade do tamanho da cota.  
  
 Para obter mais informações e instruções sobre como alterar a cota de inscrição online, consulte [visão geral de Cache do ClickOnce](../deployment/clickonce-cache-overview.md).  
  
## <a name="versioning-issues"></a>Problemas de controle de versão  
 Você pode enfrentar problemas se você atribuir nomes fortes para seu assembly e incrementa o número de versão do assembly para refletir uma atualização de aplicativo. Qualquer assembly compilado com uma referência a um assembly de nome forte deve em si ser recompilado ou o assembly será tentar referenciar a versão mais antiga. O assembly será tentar isso porque o assembly está usando o valor antigo da versão em sua solicitação de associação.  
  
 Por exemplo, digamos que você tenha um assembly de nome forte em seu próprio projeto com a versão 1.0.0.0. Depois de compilar o assembly, adicioná-lo como uma referência para o projeto que contém o aplicativo principal. Se você atualiza o assembly, incrementa a versão para 1.0.0.1 e tenta implantá-lo sem também recompilar o aplicativo, o aplicativo não poderá carregar o assembly em tempo de execução.  
  
 Esse erro pode ocorrer somente se você estiver editando sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] manifestos manualmente; esse erro não deverá ocorrer se você gerar a sua implantação usando [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)].  
  
## <a name="specifying-individual-net-framework-assemblies-in-the-manifest"></a>Especificando os Assemblies do Framework .NET individuais no manifesto  
 O aplicativo falhará ao carregar se você tiver editado manualmente uma [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação para fazer referência a uma versão mais antiga de um [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] assembly. Por exemplo, se você adicionou uma referência ao assembly System.Net para obter uma versão de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] antes da versão especificada no manifesto, em seguida, poderá ocorrer um erro. Em geral, você não deve tentar especificar referências ao indivíduo [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] assemblies, como a versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] em relação a qual seu aplicativo é executado é especificado como uma dependência no manifesto do aplicativo.  
  
## <a name="manifest-parsing-issues"></a>Problemas de análise de manifesto  
 Os arquivos de manifesto que são usados pelo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] são arquivos XML, e eles devem ser bem formado e é válido: eles devem obedecem às regras de sintaxe XML e usar apenas os elementos e atributos definidos no esquema XML relevante.  
  
 Algo que pode causar problemas em um arquivo de manifesto é selecionar um nome para seu aplicativo que contém um caractere especial, como uma marca de aspas simples ou dupla. O nome do aplicativo faz parte do seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] identidade. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Atualmente, não analisa as identidades que contenham caracteres especiais. Se seu aplicativo não conseguir ativar, certifique-se de que você estiver usando apenas alfabéticos e numéricos para o nome e tenta implantá-lo novamente.  
  
 Se você tiver editado manualmente seus manifestos de implantação ou de aplicativo, você pode ter acidentalmente corrompida-los. Manifesto corrompido impedirá que um correto [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] instalação. Você pode depurar esses erros em tempo de execução clicando **detalhes** na **ClickOnce erro** caixa de diálogo e ler a mensagem de erro no log. O log listará uma das seguintes mensagens:  
  
-   Uma descrição do erro de sintaxe e o número de linha e o caractere posição onde ocorreu o erro.  
  
-   O nome de um elemento ou atributo usado em violação do esquema do manifesto. Se você tiver adicionado o XML manualmente para seus manifestos, você precisará comparar suas adições para os esquemas de manifesto. Para obter mais informações, consulte [manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md) e [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md).  
  
-   Um conflito de ID. Referências de dependência nos manifestos de implantação e o aplicativo devem ser exclusivas em ambos os seus `name` e `publicKeyToken` atributos. Se corresponderem a ambos os atributos entre dois elementos dentro de um manifesto, análise de manifesto não terá êxito.  
  
## <a name="precautions-when-manually-changing-manifests-or-applications"></a>Precauções ao alterar manualmente os manifestos ou aplicativos  
 Quando você atualiza um manifesto de aplicativo, você deve reassinar o manifesto do aplicativo e o manifesto de implantação. O manifesto de implantação contém uma referência ao manifesto do aplicativo que inclui o hash do arquivo e sua assinatura digital.  
  
### <a name="precautions-with-deployment-provider-usage"></a>Precauções com o uso do provedor de implantação  
 O [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] o manifesto de implantação tem um `deploymentProvider` propriedade que aponta para o caminho completo do local de onde o aplicativo deve ser instalado e atendido:  
  
```  
<deploymentProvider codebase="http://myserver/myapp.application" />  
```  
  
 Esse caminho é definido quando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] cria o aplicativo e é obrigatório para aplicativos instalados. O caminho aponta para o local padrão onde o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] instalador instalará o aplicativo e procura por atualizações. Se você usar o **xcopy** comando para copiar um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo em um local diferente, mas não altere a `deploymentProvider` propriedade, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ainda farão referência volta para o local original quando ele tenta baixar o aplicativo.  
  
 Se você deseja mover ou copiar um aplicativo, você também deverá atualizar o `deploymentProvider` caminho, para que o cliente é instalado, na verdade, de um novo local. Atualizar esse caminho é principalmente uma preocupação, se você tiver instalado os aplicativos. Para aplicativos online sempre são iniciados por meio da URL original, definindo o `deploymentProvider` é opcional. Se `deploymentProvider` for definido, isso será respeitado; caso contrário, a URL usada para iniciar o aplicativo será usada como a URL base para baixar os arquivos de aplicativo.  
  
> [!NOTE]
>  Sempre que você atualiza o manifesto você deve também assiná-lo novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)   
 [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Escolhendo uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)



