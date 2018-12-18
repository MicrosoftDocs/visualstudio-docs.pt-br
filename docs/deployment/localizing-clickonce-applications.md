---
title: Localizando aplicativos ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- WPF, ClickOnce applications
- ClickOnce deployment, globalization
- deploying applications [ClickOnce], localizing ClickOnce applications
- localization, ClickOnce deployment
- ClickOnce deployment, download on-demand
- ClickOnce deployment, localization
- Windows Forms, ClickOnce applications
- console applications, ClickOnce applications
ms.assetid: c92b193b-054d-4923-834b-d4226a4c7a1a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2a4234d8f6ee9fa946f2accfd50a587e6dbd8068
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49822095"
---
# <a name="localize-clickonce-applications"></a>Localizar aplicativos ClickOnce
Localização é o processo de tornar seu aplicativo apropriado para uma cultura específica. Esse processo envolve a tradução de texto de (UI) de interface do usuário para uma linguagem específica de região, usando a data correta e a formatação de moeda, ajustando o tamanho dos controles em um formulário, e controles de espelhamento da direita para a esquerda, se necessário.  
  
 Localizando seus resultados de aplicativo na criação de um ou mais assemblies de satélite. Cada assembly contém cadeias de caracteres, imagens e outros recursos específicos de uma determinada cultura de interface do usuário. (O arquivo executável principal do seu aplicativo contém as cadeias de caracteres para a cultura padrão para seu aplicativo.)  
  
 Este tópico descreve três maneiras de implantar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] para outras culturas:  
  
-   Inclua todos os assemblies de satélite em uma única implantação.  
  
-   Gere uma implantação para cada cultura, com um assembly satélite único incluído em cada um.  
  
-   Baixe os assemblies satélite por demanda.  
  
## <a name="including-all-satellite-assemblies-in-a-deployment"></a>Incluindo todos os Assemblies de satélite em uma implantação  
 Em vez de publicação de várias [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantações, você pode publicar um único [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação que contém todos os assemblies de satélite.  
  
 Esse método é o padrão no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Para usar este método em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], você não precisa fazer qualquer trabalho adicional.  
  
 Para usar esse método com *MageUI.exe*, você deve definir a cultura para seu aplicativo para **neutro** na *MageUI.exe*. Em seguida, você deverá incluir manualmente todos os assemblies de satélite em sua implantação. Na *MageUI.exe*, você pode adicionar os assemblies satélite usando o **popular** botão o **arquivos** guia do manifesto do aplicativo.  
  
 O benefício dessa abordagem é que ele cria uma única implantação e simplifica a sua história de implantação localizada. Em tempo de execução, o assembly satélite adequado será usado, dependendo da cultura padrão do sistema de operacional do Windows do usuário. Uma desvantagem dessa abordagem é que ele baixa todos os assemblies de satélite, sempre que o aplicativo é instalado ou atualizado em um computador cliente. Se seu aplicativo tiver um grande número de cadeias de caracteres ou seus clientes têm uma conexão de rede lenta, esse processo pode afetar o desempenho durante a atualização do aplicativo.  
  
> [!NOTE]
>  Essa abordagem supõe que o seu aplicativo se ajusta a altura, largura e a posição dos controles automaticamente para acomodar os tamanhos de cadeia de caracteres de texto diferente em diferentes culturas. Windows Forms contém uma variedade de controles e tecnologias que permitem que você cria um formulário para torná-lo facilmente localizável, incluindo o <xref:System.Windows.Forms.FlowLayoutPanel> e <xref:System.Windows.Forms.TableLayoutPanel> controles, bem como a <xref:System.Windows.Forms.Control.AutoSize%2A> propriedade.  Consulte também [como: suporte à localização em formulários do Windows usando AutoSize e o controle TableLayoutPanel](/previous-versions/visualstudio/visual-studio-2010/1zkt8b33(v=vs.100)).  
  
## <a name="generate-one-deployment-for-each-culture"></a>Gerar uma implantação para cada cultura  
 Essa estratégia de implantação, você gera várias implantações. Em cada implantação, você inclui apenas o assembly satélite necessário para uma cultura específica e você marcar a implantação como específico para aquela cultura.  
  
 Para usar este método em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], defina a **linguagem de publicação** propriedade no **publicar** guia para a região desejada. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] incluirá automaticamente o assembly de satélite necessário para a região que você selecionar e excluirá todos os outros assemblies de satélite da implantação.  
  
 Você pode fazer a mesma coisa usando o *MageUI.exe* ferramenta no Microsoft [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)]. Use o **popular** botão a **arquivos** guia do manifesto do aplicativo para excluir todos os outros assemblies de satélite do diretório do aplicativo e, em seguida, defina o **cultura**campo de **nome** guia para o manifesto de implantação no *MageUI.exe*. Essas etapas não incluem apenas o assembly satélite correto, mas também definem os `language` atributo a `assemblyIdentity` elemento em seu manifesto de implantação para a cultura correspondente.  
  
 Depois de publicar o aplicativo, você deve repetir esta etapa para cada cultura adicional suporta seu aplicativo. Certifique-se de que você publica em um diretório diferente do servidor Web ou o diretório de compartilhamento de arquivo cada vez, porque cada manifesto do aplicativo fará referência a um assembly satélite diferentes, e cada manifesto de implantação terá um valor diferente para o `language`atributo.  
  
## <a name="download-satellite-assemblies-on-demand"></a>Baixar os assemblies satélite por demanda  
 Se você decidir incluir todos os assemblies de satélite em uma única implantação, você pode melhorar o desempenho por meio de download sob demanda, que permite que você marcar assemblies como opcional. Os assemblies marcados não serão baixados quando o aplicativo é instalado ou atualizado. Você pode instalar os assemblies quando você precisar deles, chamando o <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> método no <xref:System.Deployment.Application.ApplicationDeployment> classe.  
  
 Baixando assemblies satélite sob demanda é ligeiramente diferente de baixar outros tipos de assemblies por demanda. Para obter mais informações e exemplos de código sobre como habilitar esse cenário usando o [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] ferramentas para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], consulte [passo a passo: baixando Assemblies de satélite por demanda com a API de implantação do ClickOnce](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md).  
  
 Você também pode habilitar esse cenário em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  Consulte também [instruções passo a passo: baixando Assemblies de satélite sob demanda com o ClickOnce Deployment API usando o Designer](/previous-versions/visualstudio/visual-studio-2012/ms366788(v=vs.110)) ou [passo a passo: baixando Assemblies de satélite por demanda com a API de implantação do ClickOnce Usando o Designer](/previous-versions/visualstudio/visual-studio-2013/ms366788(v=vs.120)).  
  
## <a name="testing-localized-clickonce-applications-before-deployment"></a>Teste de aplicativos ClickOnce localizados antes da implantação  
 Um assembly satélite será usado para um se somente de aplicativo do Windows Forms a <xref:System.Threading.Thread.CurrentUICulture%2A> propriedade para o thread principal do aplicativo é definida como a cultura do assembly satélite. Os clientes em mercados locais provavelmente já executará uma versão localizada do Windows com sua cultura definida como o padrão apropriado.  
  
 Você tem três opções para testar implantações localizadas antes de tornar seu aplicativo disponível aos clientes:  
  
- Você pode executar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo em apropriado as versões localizadas do Windows.  
  
- Você pode definir o <xref:System.Threading.Thread.CurrentUICulture%2A> propriedade por meio de programação em seu aplicativo. (Essa propriedade deve ser definida antes de chamar o <xref:System.Windows.Forms.Application.Run%2A> método.)  
  
## <a name="see-also"></a>Consulte também  
 [\<assemblyIdentity > elemento](../deployment/assemblyidentity-element-clickonce-deployment.md)   
 [Implantação e segurança do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Globalizar formulários do Windows](/dotnet/framework/winforms/advanced/globalizing-windows-forms)