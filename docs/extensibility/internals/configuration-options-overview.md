---
title: Visão geral das opções de configuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations
- configuration options, about configuration options
ms.assetid: f4ad4dd3-b39e-42df-ad89-d403cdf24a2b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fde39c346313dc66d5d94a5beb0e9e3b256ea436
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920184"
---
# <a name="configuration-options-overview"></a>Visão geral das opções de configuração
Projetos em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] pode dar suporte a várias configurações que podem ser criadas, depurado, execução e/ou implantado. Uma configuração é um tipo de build descrito com um conjunto de propriedades, normalmente os comutadores de compilador e locais de arquivos nomeado. Por padrão, novas soluções contêm duas configurações, *Debug* e *versão*. Essas configurações podem ser aplicadas usando suas configurações padrão, ou modificado para atender às suas necessidades específicas de solução e/ou projeto. Alguns pacotes podem ser criados de duas maneiras: como um editor de ActiveX ou como um componente no local. Projetos não é necessário dar suporte a várias configurações, no entanto. Se houver apenas uma configuração disponível, essa configuração é mapeada em todas as configurações da solução.  
  
 As configurações normalmente consistem em duas partes: o nome da configuração (como *Debug* ou *versão*) e as configurações de plataforma. Nome da plataforma de uma configuração identifica o ambiente que definir os destinos de configuração, como uma API ou a plataforma do sistema operacional. Os usuários do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não é possível criar uma plataforma; eles devem escolher dentre as opções um projeto de VSPackage permite. Quando um usuário instala um VSPackage, a plataforma de distribuição criada durante o desenvolvimento do pacote pode surgir em qualquer nome desejado da plataforma com base em quaisquer critérios definidos pelo criador do pacote. O usuário pode selecionar na lista de plataformas disponibilizados por meio de VSPackage quando as páginas de propriedades são instanciadas.  
  
 Nomes de plataforma são opcionais, pois nem todos os projetos suportam o conceito de plataformas. Quando uma configuração não tem um nome de plataforma, a cadeia de caracteres **n/d** é exibido na interface do usuário.  
  
 Cada solução tem seu próprio conjunto de configurações, apenas um dos quais pode estar ativo por vez. Uma configuração de solução é um conjunto de não mais de uma configuração de cada projeto. O requisito "não mais do que" é devido à opção para excluir um projeto de uma configuração de solução. Os usuários podem criar suas próprias configurações de solução personalizada.  
  
 A tabela a seguir ilustra a configuração de configurações típicas para um projeto. As linhas são rotuladas com nomes de configuração e as colunas com nomes de plataforma.  
  
|Nome da configuração|Plataforma: Win32|Plataforma: Win64|  
|------------------------|----------------------|----------------------|  
|*Depurar*|\<Configurações do Win32 de depuração >|\<Depurar configurações Win64 >|  
|*Versão*|\<Configurações do Win32 de versão >|\<Configurações de Win64 liberações >|  
|*MyConfig*|N/D|\<Configurações de MyConfig Win64 >|  
  
> [!NOTE]
>  Não é possível criar uma *MyConfig* configuração de solução que exclui uma plataforma Win32, a menos que o projeto de destino não dá suporte para Win32.  
  
 Alterando a configuração ativa para uma solução seleciona o conjunto de configurações de projeto que é criado, execute, depurado ou implantado na solução. Por exemplo, se você alterar a configuração da solução ativa da *Release* para *depurar*, todos os projetos na solução são criados automaticamente com a configuração do projeto indicada no configuração de depuração da solução. Configurações de projeto também são nomeadas *depurar* , a menos que o usuário tiver feito alterações manuais no Gerenciador de configuração do ambiente.  
  
 As propriedades de configuração da solução armazenadas para cada projeto incluem o nome do projeto, o nome de configuração do projeto, sinalizadores para indicar se deseja ou não para criar ou implantar e o nome da plataforma. Para obter mais informações, consulte [configuração da solução](../../extensibility/internals/solution-configuration.md).  
  
 O usuário pode exibir e definir parâmetros de configuração de solução selecionando a solução na hierarquia (Gerenciador de soluções) e abrindo as páginas de propriedades. Da mesma forma, você pode exibir e definir parâmetros de configuração do projeto selecionando um projeto no Solution Explorer e abrir as páginas de propriedades para o projeto.  
  
 O usuário também pode criar um projeto usando as definições de configuração de versão e todo o resto com definições de configuração de depuração, se necessário. Para obter mais informações, consulte [configuração do projeto para a construção](../../extensibility/internals/project-configuration-for-building.md).  
  
 O diagrama a seguir mostra como as interfaces que dão suporte a configurações de solução e projeto são implementadas:  
  
 ![Gráfico de configuração de interfaces](../../extensibility/internals/media/vsconfiginterfaces.gif "vsConfigInterfaces")  
Interfaces de configuração  
  
 Algumas notas relacionadas ao diagrama anterior:  
  
- `IDispatch` é marcado como opcional no objeto de configuração. Especificamente, é opcional para ter interfaces de configuração no objeto de navegação.  
  
- `IVsDebuggableProjectCfg` é marcado como opcional no objeto de configuração, mas é necessário para suporte à depuração.  
  
- `IVsProjectCfg2` é marcado como opcional no objeto de configuração, mas é necessário para suporte de agrupamento de saída.  
  
- O objeto de provedor de configuração é marcado como um objeto opcional, mas a opção é onde implementá-lo. Você pode implementar o objeto no objeto de projeto ou em um objeto separado.  
  
- `IVsCfgProvider2` é necessário para suporte de plataforma e a edição de configuração. `IVsCfgProvider` é suficiente se você não implementar essa funcionalidade.  
  
- Alguns desses objetos mostrados no diagrama como objetos separados podem ser combinados na mesma classe quando for prático com base em seus requisitos de design específico. Em outros tópicos desta seção, no entanto, os objetos e interfaces associadas a esses objetos serão discutidas acordo com o cenário apresentado no diagrama.  
  
- Determinados objetos são implementados separadamente. Por exemplo, o projeto e a construção da solução ocorrerem em threads separados e o objeto para gerenciar as vidas de compilação separadamente do objeto que descreve a configuração da compilação.  
  
  Para obter mais informações sobre as interfaces de objeto de configuração e interfaces de objeto de provedor de configuração no diagrama anterior, consulte [objeto de configuração do projeto](../../extensibility/internals/project-configuration-object.md). Além disso, [configuração do projeto para a construção](../../extensibility/internals/project-configuration-for-building.md) fornece mais informações sobre a dependência de construtor e a compilação da configuração interfaces de objeto, e [configuração do projeto para gerenciar a implantação](../../extensibility/internals/project-configuration-for-managing-deployment.md) ainda mais descreve as interfaces anexadas para o implantador de configuração e os objetos de dependência de implantação. Por fim, [configuração do projeto para saída](../../extensibility/internals/project-configuration-for-output.md) descreve o grupo de saída e as interfaces de objeto de saída e o uso de páginas de propriedades para exibir e definir propriedades dependentes de configuração.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>   
 [Configuração de projeto para criação](../../extensibility/internals/project-configuration-for-building.md)   
 [Configuração da solução](../../extensibility/internals/solution-configuration.md)