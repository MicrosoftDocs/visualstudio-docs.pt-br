---
title: Configurar um projeto do Azure com várias configurações de serviço
description: Saiba como configurar um projeto de serviço de nuvem do Azure alterando os arquivos ServiceDefinition.csdef, ServiceConfiguration.Local.cscfg e ServiceConfiguration.Cloud.cscfg.
author: ghogen
manager: jillfra
assetId: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: 8c9f65291d43a55ee75840591698c26fdde6e967
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280538"
---
# <a name="configuring-your-azure-project-in-visual-studio-to-use-multiple-service-configurations"></a>Configurando seu projeto do Azure no Visual Studio para usar várias configurações de serviço

Um projeto de serviço de nuvem do Azure no Visual Studio inclui três arquivos de configuração: `ServiceDefinition.csdef`, `ServiceConfiguration.Local.cscfg` e `ServiceConfiguration.Cloud.cscfg`:

- O `ServiceDefinition.csdef` é implantado no Azure para descrever os requisitos do serviço de nuvem e suas funções, e para fornecer as configurações que se aplicam a todas as instâncias. As configurações podem ser lidas em tempo de execução usando a API de tempo de execução de Hospedagem de serviço do Azure. Esse arquivo poderá ser atualizado no Azure somente quando o serviço de nuvem for interrompido.
- O `ServiceConfiguration.Local.cscfg` e o `ServiceConfiguration.Cloud.cscfg` fornecem valores para as configurações no arquivo de definição e especificam o número de instâncias a serem executadas para cada função. O arquivo "Local" contém os valores usados na depuração local; o arquivo "Nuvem" é implantado no Azure como `ServiceConfiguration.cscfg` e fornece as configurações para o ambiente do servidor. Esse arquivo pode ser atualizado enquanto o serviço de nuvem está em execução no Azure.

Os parâmetros de configuração são gerenciados e modificados no Visual Studio usando as páginas de propriedade para a função aplicável (clique com o botão direito na função e selecione **Propriedades** ou clique duas vezes na função). As alterações podem ser definidas para qualquer configuração que seja escolhida na lista suspensa **Configuração do serviço**. As propriedades para funções da Web e de trabalho são semelhantes, exceto onde estiver descrito nas seções a seguir.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Para obter informações sobre os esquemas subjacentes para a definição de serviço e os arquivos de configuração do serviço, consulte os artigos [Esquema XML .csdef](/azure/cloud-services/schema-csdef-file) e [Esquema XML .cscfg](/azure/cloud-services/schema-cscfg-file). Para saber mais sobre a configuração de serviço, veja [Como configurar Serviços de Nuvem](/azure/cloud-services/cloud-services-how-to-configure-portal).

## <a name="configuration-page"></a>Página Configuração

### <a name="service-configuration"></a>Configuração de Serviço

Seleciona qual arquivo do `ServiceConfiguration.*.cscfg` é afetado pelas alterações. Por padrão, há variantes de Local e Nuvem, e você pode usar o comando **Manage... ** para copiar, renomear e remover os arquivos de configuração. Esses arquivos são adicionados ao seu projeto de serviço de nuvem e aparecem no **Gerenciador de Soluções**. No entanto, renomear ou remover configurações pode ser feito somente por este controle.

### <a name="instances"></a>Instâncias

Definir a **instância** propriedade de contagem para o número de instâncias o serviço deve ser executado para esta função.

Defina a propriedade **Tamanho da VM** como **Extra Pequena**, **Pequena**, **Média**, **Grande** ou **Extra Grande**.  Para obter mais informações, consulte [tamanhos dos serviços de nuvem](/azure/cloud-services/cloud-services-sizes-specs).

### <a name="startup-action-web-role-only"></a>Ação de inicialização (somente função Web)

Defina essa propriedade para especificar que o Visual Studio deve iniciar um navegador da Web para os pontos de extremidade HTTP ou os pontos de extremidade HTTPS, ou ambos, quando você iniciar a depuração.

A opção de **ponto de extremidade https** só estará disponível se você já tiver definido um ponto de extremidade HTTPS para sua função. Você pode definir um ponto de extremidade HTTPS na página de propriedades **pontos de extremidade** .

Se você já tiver adicionado um ponto de extremidade HTTPS, a opção de ponto de extremidade HTTPS será habilitada por padrão e o Visual Studio iniciará um navegador para esse ponto de extremidade quando você iniciar a depuração, além de um navegador para o ponto de extremidade HTTP, supondo que as opções de inicialização estejam habilitadas.

### <a name="diagnostics"></a>Diagnósticos

Por padrão, o diagnóstico é habilitado para a função web. A conta de armazenamento e o projeto de serviço de nuvem do Azure são definidos para usar o emulador de armazenamento local. Quando você estiver pronto para implantar no Azure, selecione o botão de construtor (**...**) para usar o armazenamento do Azure. Você pode transferir os dados de diagnóstico para a conta de armazenamento sob demanda ou em intervalos agendados automaticamente. Para saber mais sobre o diagnóstico do Azure, veja [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure e nas Máquinas Virtuais](/azure/cloud-services/cloud-services-dotnet-diagnostics).

## <a name="settings-page"></a>Página Configurações

Na página **Configurações**, você pode adicionar as configurações a uma configuração como pares nome-valor. O código em execução na função pode ler os valores de suas definições de configuração em tempo de execução usando classes fornecidas pela [biblioteca gerenciada do Azure](/previous-versions/azure/dn602775(v=azure.11)), especificamente, o método [GetConfigurationSettingValue](/previous-versions/azure/reference/ee772857(v=azure.100)) .

### <a name="configuring-a-connection-string-for-a-storage-account"></a>Configurando uma cadeia de conexão para uma conta de armazenamento

Uma cadeia de conexão é uma configuração que fornece informações de conexão e autenticação para o emulador de armazenamento ou para uma conta de armazenamento do Azure. Sempre que o código em uma função acessar o armazenamento do Azure (blobs, filas ou tabelas), ele precisará de uma cadeia de conexão.

> [!Note]
> Uma cadeia de conexão para a conta de armazenamento do Azure deve usar um formato definido (veja [Configurar cadeias de conexão do armazenamento do Azure](/azure/storage/common/storage-configure-connection-string)).

Você pode definir a cadeia de conexão para usar o armazenamento local conforme o necessário, em seguida, definir para uma conta de armazenamento do Azure quando implantar o aplicativo no serviço de nuvem. A falha em definir a cadeia de conexão corretamente pode fazer sua função não iniciar, ou que ela alterne entre os estados inicializando, ocupado e parando.

Para criar uma cadeia de conexão, selecione **Adicionar Configuração** e defina **Tipo** como "Cadeia de Conexão".

Para cadeias de conexão novas ou existentes, selecione **... *** à direita do campo **Valor** para abrir a caixa de diálogo **Criar Cadeia de Conexão de Armazenamento**:

1. Em **Conectar usando**, escolha a opção **Sua assinatura** para selecionar uma conta de armazenamento de uma assinatura. O Visual Studio, em seguida, obtém as credenciais da conta de armazenamento automaticamente do arquivo `.publishsettings`.
1. Selecionar **Credenciais inseridas manualmente** permite que você especifique o nome da conta e a chave diretamente usando as informações do Portal do Azure. Para copiar a chave de conta:
    1. Navegue até a conta de armazenamento do Portal do Azure e selecione **Gerenciar Chaves**.
    1. Para copiar a chave de conta, navegue até a conta de armazenamento no portal do Azure, selecione **Configurações > Chaves de acesso** e, em seguida, use o botão Copiar para copiar a chave de acesso primária para a área de transferência.
1. Selecione uma das opções de conexão. **Especificar pontos de extremidade personalizados** solicitará que você especifique URLs específicas para blobs, tabelas e filas. Os pontos de extremidade personalizados permitem que você use [domínios personalizados](/azure/storage/blobs/storage-custom-domain-name) e controle o acesso mais exatamente. Veja [Configurar cadeias de conexão do Armazenamento do Azure](/azure/storage/common/storage-configure-connection-string).
1. Selecione **OK**, em seguida, **Arquivo > Salvar** para atualizar a configuração com a nova cadeia de conexão.

Novamente, quando você publica seu aplicativo no Azure, escolhe a configuração do serviço que contém a conta de armazenamento do Azure para a cadeia de conexão. Depois de publicar o aplicativo, verifique se ele funciona conforme esperado nos serviços de armazenamento do Azure.

Para obter mais informações sobre como atualizar as configurações de serviço, veja a seção [Gerenciar cadeias de conexão para contas de armazenamento](vs-azure-tools-configure-roles-for-cloud-service.md#manage-connection-strings-for-storage-accounts).

## <a name="endpoints-page"></a>Página Pontos de Extremidade

Uma função Web geralmente tem um único ponto de extremidade HTTP na porta 80. Uma função de trabalho, por outro lado, pode ter qualquer número de pontos de extremidade HTTP, HTTPS ou TCP. Pontos de extremidade podem ser pontos de extremidade de entrada, disponíveis a clientes externos, ou pontos de extremidade internos, disponíveis a outras funções em execução no serviço.

- Para disponibilizar um ponto de extremidade HTTP para clientes externos e navegadores da Web, altere o tipo de ponto de extremidade para entrada e especifique um nome e um número da porta pública.
- Para disponibilizar um ponto de extremidade HTTPS para clientes externos e navegadores da Web, altere o tipo de ponto de extremidade para **entrada**, e especifique um nome, um número da porta pública e um nome de certificado de gerenciamento. Você também deve definir o certificado na página de propriedades **Certificados** antes de especificar um certificado de gerenciamento.
- Para disponibilizar um ponto de extremidade para o acesso interno por outras funções no serviço de nuvem, altere o tipo de ponto de extremidade para interno e especifique um nome e possíveis portas privadas para esse ponto de extremidade.

## <a name="local-storage-page"></a>Página Armazenamento Local

Você pode usar a página de propriedades **Armazenamento Local** para reservar um ou mais recursos de armazenamento local para uma função. Um recurso de armazenamento local é um diretório reservado no sistema de arquivos da máquina virtual do Azure no qual uma instância de uma função está em execução.

## <a name="certificates-page"></a>Página Certificados

A página de propriedades **Certificados** adiciona informações sobre seus certificados para a configuração do serviço. Observe que os certificados não são fornecidos com o serviço; você deve carregá-los separadamente no Azure por meio do [portal do Azure](https://portal.azure.com).

Adicionar um certificado aqui adiciona informações sobre seus certificados para a configuração do serviço. Os certificados não são fornecidos com o serviço; você deve carregá-los separadamente por meio do Portal do Azure.

Para associar um certificado à sua função, forneça um nome para o certificado. Use esse nome para fazer referência ao certificado ao configurar um ponto de extremidade HTTPS na página **Pontos de Extremidade**. Em seguida, especifique se o repositório de certificados é **Computador Local** ou **Usuário Atual** e o nome do repositório. Finalmente, insira a impressão digital do certificado. Se o certificado estiver no repositório Usuário Atual\Pessoal (Meu), você pode inserir a impressão digital do certificado, selecionando o certificado em uma lista preenchida. Se ele residir em qualquer outro local, insira o valor de impressão digital manualmente.

Quando você adiciona um certificado do repositório de certificados, todos os certificados intermediários são adicionados automaticamente às definições de configuração para você. Além disso, esses certificados intermediários devem ser carregados no Azure para configurar corretamente o serviço para SSL.

Qualquer certificado de gerenciamento que você associar a seu serviço só se aplicará a esse serviço quando ele estiver em execução na nuvem. Quando o serviço é executado no ambiente de desenvolvimento local, ele usa um certificado padrão que é gerenciado pelo emulador de computação.
