---
title: Como coletar dados de desempenho para um site | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vsperf.url.url
- vsperf.chooseurl
- vs.performance.wizard.asppage
- vsperf.url.ok
- vsperf.url.cancel
helpviewer_keywords:
- Profiling Tools,profiling ASP.NET
- web sites, performance profiling
- ASP.NET, performance profilng
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c2f8169716bda09e3c4d89ce06dc907c726adee2
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330963"
---
# <a name="how-to-collect-performance-data-for-a-web-site"></a>Como coletar dados de desempenho de um site

Você pode usar o **Assistente de Desempenho** para coletar dados de desempenho de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]. É possível criar o perfil de um aplicativo Web que esteja aberto no Visual Studio ou criar um perfil de um site do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] que esteja localizado no computador local e não esteja aberto no IDE do Visual Studio.

> [!NOTE]
> O **Assistente de Desempenho** permite que você adicione dados de interação de camadas (TIP), dados de desempenho de JScript ou ambos os dados de criação de perfil coletados. A opção TIP coleta dados de processos do servidor. A criação de perfil do JScript coleta dados de scripts que são executados em um site da Web local ou remoto. Na maioria dos casos, você deve escolher apenas uma das opções.

 Dependendo das configurações de Permissões de Acesso do Usuário que um administrador tenha disponibilizado, um usuário individual pode ter ou não a permissão de segurança para criar uma sessão de criador de perfil no computador que hospeda o processo ASP.NET. Os exemplos a seguir ilustram possíveis diferenças entre os usuários:

- Alguns usuários poderão acessar recursos de criação de perfil avançados quando o Administrador tiver configurado o driver e o serviço para iniciar.

- Os usuários do domínio podem acessar apenas as amostras de criação de perfil.

- Alguns usuários podem negar acesso à criação de perfil para todos os outros usuários.

  Para obter mais informações, consulte [criação de perfil e segurança do Windows Vista](../profiling/profiling-and-windows-vista-security.md) e as opções de administrador na [VSPerfCmd](../profiling/vsperfcmd.md).

## <a name="to-profile-a-web-site-project"></a>Para criar o perfil de um projeto de site

1. Abra o projeto Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] no Visual Studio.

2. No menu **Analisar**, selecione **Criador de Perfil de Desempenho**, **Gerenciador de Desempenho** e, em seguida, **Iniciar**.

3. Na primeira página do assistente, selecione um método de criação de perfil e, em seguida, clique em **Avançar**. Para obter mais informações sobre métodos de criação de perfil, confira [Entender os métodos de coleta de desempenho](../profiling/understanding-performance-collection-methods.md). Observe que o método de criação de perfil do visualizador de simultaneidade não está disponível para aplicativos Web.

4. Na lista suspensa **Qual aplicativo você deseja direcionar para a criação de perfil?**, certifique-se de que o projeto atual esteja selecionado e, em seguida, clique em **Avançar**.

5. Na terceira página do assistente, você pode adicionar dados de TIP (criação de perfil de interação de camada) e/ou dados do JavaScript em execução nas páginas da Web.

    - Para coletar a interação da camada, selecione a caixa de seleção **Habilitar Criação de Perfil de Interação de Camada**.

    - Para coletar dados do JavaScript em execução nas páginas da Web, marque a caixa de seleção **perfil JavaScript** .

6. Clique em **Avançar**.

7. Na quarta página do assistente, clique em **Concluir**.

8. Uma sessão de desempenho é criada para o aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e o site é iniciado no navegador. Execute a funcionalidade para qual deseja criar o perfil e, em seguida, feche o navegador.

     O criador de perfil gera o arquivo de dados e demonstra a exibição dos dados de Resumo na janela principal do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

## <a name="to-profile-a-web-site-without-opening-a-project-in-visual-studio"></a>Para criar o perfil de um site sem abrir um projeto no Visual Studio

1. Abra o Visual Studio.

2. No menu **Analisar**, selecione **Criador de Perfil de Desempenho**, **Gerenciador de Desempenho** e, em seguida, **Iniciar**.

3. Na primeira página do assistente, selecione um método de criação de perfil e, em seguida, clique em **Avançar**. Para obter mais informações, consulte [Noções Básicas sobre Métodos de Coleta de Desempenho](../profiling/understanding-performance-collection-methods.md).

4. Na segunda página do assistente, selecione a opção **Criar Perfil de um aplicativo ASP.NET ou JavaScript** e, em seguida, clique em **Avançar**.

5. Na caixa **Qual URL ou Caminho executará seu aplicativo Web** na terceira página do assistente, insira a URL para a home page do aplicativo e, em seguida, clique em **Avançar**.

   - Para um site baseado em servidor (IIS), digite uma URL como **<`http://localhost/MySite/default.aspx`>** . Isso faz com que o aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] no computador local na raiz do aplicativo do MySite tenha seu perfil criado e a página default.aspx nesse site seja iniciada no Internet Explorer para iniciar a sessão.

   - Para um site da Web baseado em um arquivo, digite um caminho como file///**c:\WebSites\MySite\default.aspx**. Isso faz com que o aplicativo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] localizado em c:\webSites\MySite tenha seu perfil criado e a página `http://localhost:nnnn/MySite/default.aspx` seja iniciada no Internet Explorer para iniciar a sessão.

   - Para sites externos sobre os quais deseja coletar dados de JavaScript, digite a URL, por exemplo, `http://www.contoso.com`.

     Para obter mais informações, exiba as páginas de propriedades para um binário de destino de [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].

6. Na terceira página do assistente, você pode adicionar dados de TIP (criação de perfil de interação de camada) e/ou dados do JavaScript em execução nas páginas da Web.

    - Para coletar a interação da camada, selecione a caixa de seleção **Habilitar Criação de Perfil de Interação de Camada**.

    - Para coletar dados do JavaScript em execução nas páginas da Web, marque a caixa de seleção **Criar perfil de JavaScript**.

7. Clique em **Avançar**.

8. Na quarta página do assistente, clique em **Concluir**.

9. Uma sessão de desempenho é criada para o aplicativo ASP.NET e o site é iniciado no navegador. Execute a funcionalidade para qual deseja criar o perfil e, em seguida, feche o navegador.

     O criador de perfil gera o arquivo de dados e demonstra a exibição dos dados de Resumo na janela principal do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

## <a name="see-also"></a>Veja também

[Visões gerais](../profiling/overviews-performance-tools.md) 
 [Configurar sessões](../profiling/configuring-performance-sessions.md) 
 de desempenho [Entender os valores](../profiling/understanding-instrumentation-data-values.md) 
 de dados de instrumentação [Entender os valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)
