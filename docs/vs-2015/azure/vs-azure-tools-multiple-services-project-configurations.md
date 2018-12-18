---
title: Configurando seu projeto do Azure usando várias configurações de serviço | Microsoft Docs
description: Saiba como configurar um projeto de serviço de nuvem do Azure alterando os arquivos servicedefinition. Csdef, local. cscfg e ServiceConfiguration.
author: ghogen
manager: douge
assetId: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: f309c2a960d011601a9fdd41e29d767c667de838
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001311"
---
# <a name="configuring-your-azure-project-in-visual-studio-to-use-multiple-service-configurations"></a>Configurando seu projeto do Azure no Visual Studio para usar várias configurações de serviço

Um projeto de serviço de nuvem do Azure no Visual Studio inclui três arquivos de configuração: `ServiceDefinition.csdef`, `ServiceConfiguration.Local.cscfg`, e `ServiceConfiguration.Cloud.cscfg`:

- `ServiceDefinition.csdef` é implantado no Azure para descrever os requisitos do serviço de nuvem e suas funções e para fornecer configurações que se aplicam a todas as instâncias. As configurações podem ser lidas em tempo de execução usando a API de tempo de execução de hospedagem do Azure Service. Esse arquivo pode ser atualizado no Azure apenas quando o serviço de nuvem é interrompido.
- `ServiceConfiguration.Local.cscfg` e `ServiceConfiguration.Cloud.cscfg` fornecer valores para as configurações na definição de arquivo e especificam o número de instâncias a serem executadas para cada função. O arquivo "Local" contém valores usados na depuração local; o arquivo "Nuvem" é implantado no Azure como `ServiceConfiguration.cscfg` e fornece configurações para o ambiente de servidor. Esse arquivo pode ser atualizado enquanto o serviço de nuvem está em execução no Azure.

As definições de configuração são gerenciadas e modificadas no Visual Studio usando páginas de propriedades para a função aplicável (a função com o botão direito e selecione **propriedades**, ou clique duas vezes em função). As alterações podem ser definidas para qualquer configuração que é escolhida na **configuração do serviço** lista suspensa. As propriedades de funções web e de trabalho são semelhantes, exceto onde descritos nas seções a seguir.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Para obter informações sobre os esquemas subjacentes para a definição de serviço e os arquivos de configuração de serviço, consulte o [esquema XML. csdef](/azure/cloud-services/schema-csdef-file.md) e [esquema XML. cscfg](/azure/cloud-services/schema-cscfg-file.md) artigos. Para obter mais informações sobre a configuração de serviço, consulte [como configurar os serviços de nuvem](/azure/cloud-services/cloud-services-how-to-configure-portal).


## <a name="configuration-page"></a>Página de configuração

### <a name="service-configuration"></a>Configuração de serviço

Seleciona quais `ServiceConfiguration.*.cscfg` arquivo é afetado pelas alterações. Por padrão, há variantes de Local e a nuvem, e você pode usar o **gerenciar...**  comando para copiar, renomear e remover arquivos de configuração. Esses arquivos são adicionados ao seu projeto de serviço de nuvem e aparecem em **Gerenciador de soluções**. No entanto, renomear ou remover configurações pode ser feito somente por este controle.

### <a name="instances"></a>Instâncias

Defina as **instância** propriedade de contagem para o número de instâncias de serviço deve ser executado para esta função.

Defina a **tamanho da VM** propriedade a ser **Extra pequena**, **pequeno**, **médio**, **grande**, ou **Extra grande**.  Para obter mais informações, consulte [tamanhos para serviços de nuvem](/azure/cloud-services/cloud-services-sizes-specs).

### <a name="startup-action-web-role-only"></a>Ação de inicialização (somente função Web)

Defina essa propriedade para especificar que o Visual Studio deve iniciar um navegador da web para os pontos de extremidade HTTP ou os pontos de extremidade HTTPS ou ambos ao iniciar a depuração.

O **ponto de extremidade HTTPS** opção só estará disponível se você já definiu um ponto de extremidade HTTPS para sua função. Você pode definir um ponto de extremidade HTTPS na **pontos de extremidade** página de propriedades.

Se você já tiver adicionado um ponto de extremidade HTTPS, a opção de ponto de extremidade HTTPS é habilitada por padrão e o Visual Studio iniciará um navegador para esse ponto de extremidade quando você inicia a depuração, além de um navegador para seu ponto de extremidade HTTP, supondo que as duas opções de inicialização estão habilitadas.

### <a name="diagnostics"></a>Diagnóstico

Por padrão, os diagnósticos são habilitados para a função Web. A conta de armazenamento e o projeto de serviço nuvem do Azure são definidos para usar o emulador de armazenamento local. Quando você estiver pronto para implantar no Azure, você pode selecionar o botão de construtor (**...** ) para usar o armazenamento do Azure. Você pode transferir os dados de diagnóstico para a conta de armazenamento sob demanda ou em intervalos agendados automaticamente. Para obter mais informações sobre o diagnóstico do Azure, consulte [habilitando o diagnóstico nos serviços de nuvem do Azure e máquinas virtuais](/azure/cloud-services/cloud-services-dotnet-diagnostics).

## <a name="settings-page"></a>Página de configurações

Sobre o **configurações** página, você pode adicionar configurações para uma configuração como pares nome-valor. O código em execução na função pode ler os valores dos parâmetros de configuração em tempo de execução usando classes fornecidas pelo [biblioteca gerenciada do Azure](http://go.microsoft.com/fwlink?LinkID=171026), mais especificamente, o [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) método.

### <a name="configuring-a-connection-string-for-a-storage-account"></a>Configurando uma cadeia de conexão para uma conta de armazenamento

Uma cadeia de caracteres de conexão é uma configuração que fornece informações de conexão e autenticação para o emulador de armazenamento ou para uma conta de armazenamento do Azure. Sempre que o código em uma função acessa o armazenamento do Azure (blobs, filas ou tabelas), ele precisa de uma cadeia de caracteres de conexão.

> [!Note]
> Uma cadeia de conexão para a conta de armazenamento do Azure deve usar um formato definido (consulte [configurar cadeias de Conexão de armazenamento do Azure](/azure/storage/common/storage-configure-connection-string)).

Você pode definir a cadeia de caracteres de conexão para usar o armazenamento local conforme o necessário, em seguida, defina a uma conta de armazenamento do Azure quando você implanta o aplicativo de serviço de nuvem. Falha ao definir a cadeia de conexão corretamente pode fazer com que sua função não iniciar, ou para alternar entre os estados inicializando, ocupados e parando.

Para criar uma cadeia de caracteres de conexão, selecione **Adicionar configuração** e defina **tipo** como "Cadeia de caracteres de Conexão".

Para cadeias de caracteres de conexão nova ou existente, selecione **...** * à direita dos **valor** campo para abrir o **criar cadeia de Conexão de armazenamento** caixa de diálogo:

1. Sob **conecte-se usando**, escolha o **sua assinatura** opção para selecionar uma conta de armazenamento de uma assinatura. Visual Studio, em seguida, obtém as credenciais da conta de armazenamento automaticamente a partir de `.publishsettings` arquivo.
1. Selecionando **credenciais inseridas manualmente** permite que você especifique o nome da conta e chave diretamente usando as informações do portal do Azure. Para copiar a chave da conta:
    1. Navegue até a conta de armazenamento no portal do Azure e selecione **gerenciar chaves**.
    1. Para copiar a chave de conta, navegue até a conta de armazenamento no portal do Azure, selecione **Configurações > chaves de acesso**, em seguida, use o botão Copiar para copiar a chave de acesso primária para a área de transferência.
1. Selecione uma das opções de conexão. **Especifique os pontos de extremidade personalizados** pede que você especifique URLs específicas para blobs, tabelas e filas. Pontos de extremidade personalizados permitem que você use [domínios personalizados](/azure/storage/blobs/storage-custom-domain-name.md) e para controlar o acesso mais exatamente. Ver [configurar cadeias de Conexão do armazenamento do Azure](/azure/storage/common/storage-configure-connection-string).
1. Selecione **Okey**, em seguida, **arquivo > Salvar** para atualizar a configuração com a nova cadeia de caracteres de conexão.

Novamente, quando você publica seu aplicativo no Azure, escolha a configuração do serviço que contém a conta de armazenamento do Azure para a cadeia de caracteres de conexão. Depois que seu aplicativo é publicado, verifique se que o aplicativo funciona conforme o esperado nos serviços de armazenamento do Azure.

Para obter mais informações sobre como atualizar as configurações de serviço, consulte a seção [gerenciar cadeias de conexão para contas de armazenamento](vs-azure-tools-configure-roles-for-cloud-service.md#manage-connection-strings-for-storage-accounts).

## <a name="endpoints-page"></a>Página pontos de extremidade

Uma função web geralmente tem um único ponto de extremidade HTTP na porta 80. Por outro lado, uma função de trabalho pode ter qualquer número de pontos de extremidade HTTP, HTTPS ou TCP. Pontos de extremidade podem ser pontos de extremidade de entrada, que estão disponíveis para clientes externos, ou pontos de extremidade internos, que estão disponíveis para outras funções que são executadas no serviço.

- Para disponibilizar um ponto de extremidade HTTP para clientes externos e navegadores da Web, altere o tipo de ponto de extremidade para entrada e especifique um nome e um número de porta pública.
- Para disponibilizar um ponto de extremidade HTTPS para clientes externos e navegadores da Web, altere o tipo de ponto de extremidade para **entrada**e especifique um nome, um número de porta pública e um nome de certificado de gerenciamento. Você também deve definir o certificado na **certificados** página de propriedades antes de especificar um certificado de gerenciamento. 
- Para disponibilizar um ponto de extremidade para acesso interno por outras funções no serviço de nuvem, altere o tipo de ponto de extremidade para interno e especifique um nome e possíveis portas privadas para esse ponto de extremidade.

## <a name="local-storage-page"></a>Página armazenamento local

Você pode usar o **armazenamento Local** página de propriedades para reservar um ou mais recursos de armazenamento local para uma função. Um recurso de armazenamento local é um diretório reservado no sistema de arquivos da máquina virtual do Azure no qual uma instância de uma função está em execução.

## <a name="certificates-page"></a>Página certificados

O **certificados** página de propriedades adiciona informações sobre seus certificados para a configuração de serviço. Observe que os certificados não são empacotados com seu serviço; Você deve carregá-los separadamente no Azure por meio de [portal do Azure](http://portal.azure.com).

Adicionando um certificado aqui adiciona informações sobre seus certificados para a configuração de serviço. Certificados não são empacotados com o serviço; Você deve carregá-los separadamente no portal do Azure.

Para associar um certificado de sua função, forneça um nome para o certificado. Use esse nome para referir-se ao certificado quando você configura um ponto de extremidade HTTPS na **pontos de extremidade** página. Em seguida, especifique se o repositório de certificados está **computador Local** ou **usuário atual** e o nome do repositório. Por fim, insira a impressão digital do certificado. Se o certificado está no atual\pessoal (Meu) repositório, você pode inserir a impressão digital do certificado, selecionando o certificado em uma lista preenchida. Se ele residir em qualquer outro local, insira o valor de impressão digital manualmente.

Quando você adiciona um certificado do repositório de certificados, todos os certificados intermediários são automaticamente adicionados às definições de configuração para você. Além disso, esses certificados intermediários devem ser carregados para o Azure para configurar corretamente o serviço para SSL.

Qualquer certificado de gerenciamento que você associar seu serviço se aplicam ao seu serviço apenas quando ele está em execução na nuvem. Quando seu serviço estiver em execução no ambiente de desenvolvimento local, ele usa um certificado padrão que é gerenciado pelo emulador de computação.
