---
title: Aplicando atualizações do administrador ao Visual Studio com o Microsoft Endpoint Configuration Manager
titleSuffix: ''
description: Saiba como aplicar atualizações do administrador ao Visual Studio.
ms.date: 03/10/2021
ms.custom: ''
ms.topic: overview
ms.assetid: 9a3fdb28-db3d-4970-bc17-7417a985f0fb
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 78c2de8b1d1ffb28cc536b770bf6bd9a4ab0aa35
ms.sourcegitcommit: 00e16b9afe6b22ba0591e4d0d92690544e6d4357
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2021
ms.locfileid: "105617320"
---
# <a name="applying-administrator-updates-that-use-microsoft-endpoint-configuration-manager"></a>Aplicando atualizações do administrador que usam o Microsoft Endpoint Configuration Manager

Este documento descreve diferentes tipos e características das atualizações do administrador do Visual Studio. Abaixo, você encontrará informações sobre como e quando eles devem ser distribuídos em toda a sua organização, quais opções de configuração estão disponíveis e como exibir relatórios e solucionar problemas. Para obter mais informações sobre os pré-requisitos para usar atualizações do administrador, consulte [habilitando atualizações do administrador](../install/enabling-administrator-updates.md).

## <a name="understanding-visual-studio-administrator-updates"></a>Noções básicas sobre atualizações do administrador do Visual Studio 

O pacote de atualização do administrador do Visual Studio que é publicado no Microsoft Update para consumo pelo catálogo da Microsoft e pelo WSUS contém informações que o Configuration Manager precisa para poder baixar e distribuir a atualização para o Visual Studio para computadores cliente. Ele também contém informações de que um administrador de ti precisa para decidir quais atualizações devem ser distribuídas em toda a organização e facilita a manutenção de layouts de rede. Os pacotes de atualização do administrador do Visual Studio não contêm informações suficientes para fazer uma nova instalação do produto, nem eles contêm os binários de produto reais que são publicados na rede de distribuição de conteúdo. As atualizações do administrador do Visual Studio são cumulativas, assim como as atualizações regulares do Visual Studio. Você pode assumir que qualquer atualização do Visual Studio que tenha um número de versão do produto maior e uma data de lançamento posterior é um superconjunto de uma versão mais antiga e inferior. 

As atualizações do administrador do Visual Studio se aplicam às versões de serviço do Visual Studio que estão em suporte. Para obter mais informações sobre quais linhas de base de serviço do Visual Studio ainda estão em suporte durante um determinado período, consulte [ciclo de vida do produto e manutenção do Visual Studio](https://docs.microsoft.com/visualstudio/productinfo/vs-servicing-vs). Todas as linhas de base de serviço do Visual Studio com suporte serão mantidas seguras.  

## <a name="types-and-characteristics-of-administrator-updates"></a>Tipos e características de atualizações do administrador 

Há três tipos de atualizações de administrador para o Visual Studio:

* **As atualizações de segurança** são aplicáveis a todas as edições do Visual Studio (por exemplo, Enterprise, Professional, Community, etc.) e contêm alterações de nível de serviço limitadas, altamente direcionadas e compatíveis. As atualizações de segurança não avançarão um cliente para uma versão secundária posterior; Elas foram projetadas para fornecer correções de vulnerabilidades de segurança para um cliente que já está em um nível de versão secundário específico. As atualizações de segurança terão pelo menos uma correção de segurança nelas, mas a correção de segurança pode ou não estar em um componente ou carga de trabalho instalado no computador cliente. Por exemplo, poderíamos corrigir uma vulnerabilidade de segurança nos componentes do .NET, e podemos rotular a atualização como uma atualização de segurança, mas ela realmente não teria nenhum efeito significativo em um computador cliente que tinha apenas componentes do C++ instalados. As atualizações de segurança também podem conter outras correções de confiabilidade ou outras atualizações de componentes necessárias. As atualizações de segurança são publicadas no [Catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/Home.aspx) (MUC) e [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus), em que são classificadas como "atualizações de segurança".
 
* **As atualizações de recursos** permitem que os administradores de ti aprimorem os computadores da sua organização para uma versão secundária mais recente do Visual Studio 2019. As atualizações de recursos se aplicam apenas às edições do Visual Studio que normalmente são encontradas em empresas, como as SKUs Enterprise, Professional e Build Tools. Todas as atualizações de recursos serão publicadas no catálogo de Microsoft Update como "pacotes de recursos" e estarão disponíveis para serem [importados opcionalmente para o Configuration Manager do catálogo de Microsoft Update](https://docs.microsoft.com/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog). As atualizações de recursos são cumulativas e conterão qualidade adicional e correções de segurança anteriores. Consulte a [seção Opções de configuração](#understanding-configuration-options) abaixo para obter instruções sobre como configurar um computador cliente para permanecer em uma linha de base de serviço e impedir que atualizações de recursos sejam entregues a clientes específicos. 

* **As atualizações de qualidade** também são aplicáveis somente às edições do Visual Studio que normalmente são encontradas em empresas e contêm alterações de nível de serviço limitadas, altamente direcionadas e compatíveis. As atualizações de qualidade não avançarão um cliente para uma versão secundária posterior; Elas foram projetadas para fornecer correções de desempenho e confiabilidade ou outras atualizações de componentes necessárias para um cliente que já está em um nível de versão secundário específico. As atualizações de qualidade se acumulam junto com as atualizações de segurança e, portanto, só conterão correções de segurança se a correção de segurança já tiver sido liberada independentemente. As atualizações de qualidade são publicadas no catálogo de Microsoft Update como "Atualizações" e também estão disponíveis para serem [importados](https://docs.microsoft.com/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)opcionalmente para o Configuration Manager.

### <a name="decoding-the-titles-of-administrator-updates"></a>Decodificando os títulos de atualizações do administrador

O título de cada atualização do administrador descreve o intervalo de versão aplicável e a versão resultante da atualização.Por exemplo,

* O **visual studio 2019 versão 16.7.0 para 16.7.12 atualização** classificada como uma "atualização de segurança" se aplicará a qualquer edição do Visual Studio no cliente entre as versões 16.7.0 por meio de 16.7.12 e atualizará essas edições de cliente para 16.7.12.  

* O **visual studio 2019 versão 16.0.0 para 16.9.0 atualização** classificada como um "Feature Pack" será aplicado para selecionar as edições do Visual Studio no cliente entre o intervalo de versão do produto inteiro de 16.0.0 até 16.9.0 e atualizará essas edições de cliente (que não foram configuradas para permanecer em uma linha de base de manutenção anterior) para 16.9.0. 

* O **visual studio 2019 versão 16.8.0 para 16.8.7 atualização** classificada como simplesmente "Atualizações" se aplicará às edições Select Visual Studio no cliente entre as versões 16.8.0 por meio de 16.8.7 e atualizará essas edições de cliente para 16.8.7. 

## <a name="using-configuration-manager-to-deploy-visual-studio-updates"></a>Usando Configuration Manager para implantar atualizações do Visual Studio

### <a name="understanding-configuration-options"></a>Noções básicas sobre opções de configuração

Há algumas opções de configuração que podem ser usadas para personalizar as atualizações do administrador do Visual Studio para que elas sejam compatíveis e alinhadas com os requisitos de implantação da sua organização. As opções mais comuns são listadas abaixo.  Para obter uma lista completa de todos os parâmetros de linha de comando com suporte das atualizações do administrador, consulte [usar parâmetros de linha de comando para instalar a documentação do Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) e prestar atenção apenas aos que correspondem à ação de "atualização".

* **Aceitação de atualização do administrador**: essa chave do Registro descrita na [habilitação de atualizações do administrador](../install/enabling-administrator-updates.md) é necessária para que o computador cliente Receba atualizações do administrador. É uma chave em todo o computador, o que significa que ele se aplica a todas as instâncias do Visual Studio instaladas na caixa. 
 
* **Recusa do desenvolvedor**: os desenvolvedores podem usar uma chave **AdministratorUpdatesOptOut** separada em todo o computador   para *recusar* o recebimento de atualizações do administrador do Visual Studio. A finalidade dessa chave é codificar a intenção do usuário do Visual Studio. Para configurar o computador cliente para bloquear as atualizações do administrador, defina a chave de REG_DWORD **AdministratorUpdatesOptOut**   como **1**. A ausência da chave ou um valor definido de **0** significa que o usuário do Visual Studio deseja receber atualizações do administrador para o Visual Studio.

    Observe que a ****   chave AdministratorUpdatesOptOut (para a codificação da intenção do desenvolvedor) é priorizada sobre a chave **AdministratorUpdatesEnabled**   , que codifica a intenção do administrador de ti. Se **AdministratorUpdatesOptOut**   for definido como **1**, a atualização será bloqueada no cliente, mesmo que a chave **AdministratorUpdatesEnabled**   também seja definida como **1**.Essa ação pressupõe que os administradores de ti possam acessar e monitorar quais desenvolvedores optaram por recusar, e que as duas partes podem discutir as necessidades mais importantes.Os administradores de ti sempre podem alterar qualquer chave sempre que desejarem.
 
* **Local dos bits de produto atualizados**: na maioria das vezes, os computadores cliente baixam os bits de produto atualizados da Internet por meio da CDN da Microsoft. Esse cenário exige que os computadores cliente tenham acesso à Internet. No entanto, algumas empresas restringem os computadores cliente para instalar e atualizar apenas os bits de um local de layout de rede interno. Para garantir que as atualizações do administrador possam ser aplicadas a partir de um local de rede interno, as seguintes condições devem ser verdadeiras: 

  - O computador cliente deve ter instalado originalmente o produto de um local de layout de rede (ou seja, um cache de instalação local). 
  - Esse local de layout de rede (onde o cliente originalmente instalado) foi [atualizado para conter os bits de produto atualizados](../install/update-a-network-installation-of-visual-studio.md) especificados pela atualização do administrador. 
 
* **Forçar a atualização a ocorrer mesmo se o Visual Studio estiver em uso**: o Visual Studio deve ser fechado antes da instalação da atualização. Se o Visual Studio estiver aberto ou sendo usado, a instalação da atualização será anulada. Uma maneira fácil de garantir que o Visual Studio esteja fechado é configurar o Gerenciador de confirmação para aplicar a atualização logo após a reinicialização do computador. Você também pode usar o `--force` parâmetro para forçar o desligamento do Visual Studio. Forçar o Visual Studio a fechar pode causar perda de trabalho, portanto, use-o com cuidado. A execução de uma atualização de administrador no contexto do sistema padrão ignorará o `–-force` sinalizador, portanto, será necessário configurar a atualização do administrador para ser executada no contexto do usuário.
 
* **Manutenção da adesão da linha de base**: conforme descrito acima, as atualizações do administrador que são atualizações de recursos avançam em uma instalação do Visual Studio para uma versão secundária mais atual do produto. Às vezes, no entanto, as equipes de desenvolvimento gostam de permanecer em um nível específico de linha de base de serviço estável e seguro, e eles gostam de controlar quando seus clientes avançam para uma versão secundária mais atual. Para configurar um computador cliente para permanecer em uma linha de base de serviço e ignorar as atualizações de recursos de administrador indesejadas enviadas a ele, você precisará criar e definir o valor de dados de Reg_SZ **BaselineStickinessVersions2019** para uma cadeia de caracteres que represente as linhas de base permitidas que o computador cliente pode ajustar e permanecer.  A cadeia de caracteres pode conter uma sequência de versões de linha de base de serviço, separadas por vírgulas, como **16.4.0, 16.7.0**. Qualquer número de versões de linha de base de serviço pode ser incluído na cadeia de caracteres e a palavra **tudo**, que é a abreviação para fazer referência a todas as linhas de base de serviço com suporte, também tem suporte. 

     Se o `BaselineStickinessVersions2019` valor do registro estiver malformado, todas as atualizações do recurso serão impedidas de serem instaladas no computador. Além disso, preste atenção aos [períodos de tempo com suporte para atualizações de recursos do Visual Studio](https://docs.microsoft.com/visualstudio/productinfo/vs-servicing-vs). Embora seja tecnicamente possível aplicar atualizações de recursos que atingiram o término de seus tempos de vida, não recomendamos isso porque eles estarão fora de suporte e, portanto, potencialmente inseguros.

### <a name="methods-for-configuring-an-administrator-update"></a>Métodos para configurar uma atualização de administrador

Há três métodos principais de configuração de atualizações do administrador: uma chave do registro, um arquivo de configuração no computador cliente ou uma modificação do pacote de implantação Configuration Manager em si.   

* **Chave do registro**: as atualizações do administrador procuram chaves de registro específicas em qualquer um dos locais padrão do Visual Studio, conforme descrito na documentação [definir padrões para implantações corporativas]. As opções que são controladas por chaves do registro são itens como **AdministratorUpdatesOptOut** Reg_DWORD, **AdministratorUpdatesOptOut**   Reg_DWORD e **BaselineStickinessVersions2019** REG_SZ. O acesso de administrador no computador cliente é necessário para criar e definir o valor das chaves do registro. 
 
* **Arquivo de configuração**: algumas configurações podem ser preservadas no computador cliente em um arquivo de configuração opcional, que tem a vantagem de configurá-la apenas uma vez e fazer com que ela se aplique a todas as atualizações futuras do administrador. A abordagem do arquivo de configuração se comporta como uma chave do registro e tem todo o computador, o que significa que ela será aplicada a todas as instalações do Visual Studio instaladas no computador cliente. O local padrão para o arquivo de configuração está em `C:\ProgramData\Microsoft\VisualStudio\updates.config` . No entanto, se você quiser usar outro local para armazenar o arquivo, poderá fazê-lo criando uma chave de registro Reg_SZ chamada **UpdateConfigurationFile** e definindo o valor dessa chave como o caminho do arquivo de configuração. Essa chave do registro pode ser local em qualquer um dos locais do registro do Visual Studio, conforme descrito em [definir padrões para implantações corporativas](../install/set-defaults-for-enterprise-deployments.md). Se você optar por adicionar um valor de registro para um local de arquivo de configuração personalizado, ele procurará esse arquivo; Se o arquivo não existir, uma exceção será lançada e a atualização falhará.    
 
O arquivo de configuração, que está no formato JSON, dá suporte à opção `installerUpdateArgs` que é uma matriz de cadeias de caracteres separadas por vírgulas que especificam mais opções que podem ser passadas para o instalador do Visual Studio. Se o conteúdo do arquivo incluir um campo inválido ou uma opção sem suporte, a atualização falhará. Para obter mais informações, consulte [usar parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md).
 
Aqui está um exemplo de arquivo de configuração: 

```
“installerUpdateArgs” : [“--quiet”, “--noWeb”], 

“checkPendingReboot” :  “true” 
```

* **Atualizando manualmente o pacote de atualizações do administrador no SCCM**: os parâmetros de linha de comando de um pacote de atualização de administrador individual no SCCM também podem ser modificados manualmente.

## <a name="verification-reports-and-troubleshooting-error-codes"></a>Verificação, relatórios e códigos de erro de solução de problemas

### <a name="determining-that-visual-studio-was-updated"></a>Determinando que o Visual Studio foi atualizado

Você pode usar um dos seguintes métodos para verificar se a atualização do administrador foi instalada corretamente: 

* No computador cliente, inicie o Visual Studio 2019, selecione **ajuda**   >  **sobre** e verifique se o número de versão corresponde ao último número no título da atualização pretendida. 

* Use a ferramenta **vswhere** no computador cliente para identificar as várias versões do Visual Studio no computador. Para obter mais informações, consulte [ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md). 

* Cada tentativa de atualização administrativa gera vários arquivos de log no diretório da máquina cliente `%temp%` que captura o progresso da operação de atualização.Classifique a pasta por data e procure os arquivos que começam  `dd_updatedriver` ,  `dd_bootstrapper` ,  `dd_client` e  `dd_setup`   para as atualizações administrativas, o bootstrapper, o instalador do Visual Studio e o mecanismo de instalação, respectivamente.Verifique se esses arquivos de log contêm um 0, indicando que a atualização foi aplicada com êxito. Observe que esses arquivos de log também podem ser usados para verificar se o arquivo de configuração está sendo usado. Consulte a [ferramenta de coleta de logs do Visual Studio](https://www.microsoft.com/download/details.aspx?id=12493) para obter mais detalhes.     

### <a name="error-codes-and-conditions"></a>Códigos de erro e condições

>[!IMPORTANT]
> Lembre-se de que o Visual Studio deve ser fechado antes da instalação da atualização. Se o Visual Studio estiver aberto ou sendo usado, a instalação da atualização será cancelada.

As atualizações administrativas podem retornar os seguintes códigos de retorno:  

| Código do erro | Definição |
|--|:-|
| 0 | A atualização administrativa foi instalada com êxito. |
| 1001 | Instalador do Visual Studio ou um processo de instalação relacionado está em execução. A atualização não é aplicada. |
| 1002 | Instalador do Visual Studio está em pausa. A atualização não é aplicada. |
| 1003 | O Visual Studio está em execução. A atualização não é aplicada. Essa condição pode ser sobrerégua usando o `--force` sinalizador. |
| 1004 | Nenhuma Internet detectada.A atualização não pôde entrar em contato com o local da Internet que contém os arquivos atualizados. A atualização não é aplicada. |
| 1005 | O  ****   valor do registro AdministratorUpdatesEnabled é definido como **0** ou não definido. A atualização não é aplicada. |
| 1006 | O  ****   valor do registro AdministratorUpdatesOptOut é definido como **1**. A atualização não é aplicada. A chave destina-se a computadores cliente que não devem ser atualizados pelo administrador. |
| 1007 | O Instalador do Visual Studio não está instalado. |
| 1008 | O valor do registro **BaselineStickinessVersions2019** não está em um formato legível. O valor do registro deve incluir **todas as** versões ou as válidas com o número de Build definido como 0 explicitamente, por exemplo, X. Y. 0. |
| 3010 | O sistema requer uma reinicialização.A atualização pode ou não ter sido aplicada. Reinicialize o computador e tente a atualização novamente. |
| Outro | Erro ao tentar aplicar a atualização.A atualização não é aplicada. |

Para obter uma lista completa dos códigos de erro do cliente, consulte [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md). 

## <a name="feedback-and-support"></a>Comentários e suporte
[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

Você pode usar os seguintes métodos para fornecer comentários sobre as atualizações do administrador do Visual Studio ou os problemas de relatório que afetam as atualizações:
* Consulte as diretrizes [solução de problemas de instalação e atualização do Visual Studio](../install/troubleshooting-installation-issues.md) .
* Faça perguntas à Comunidade na configuração do [Visual Q&um fórum](https://docs.microsoft.com/answers/topics/vs-setup.html).
* Vá para a [página de suporte do Visual Studio](https://visualstudio.microsoft.com/vs/support/)e verifique se o problema está listado nas perguntas frequentes.  Você também pode selecionar o botão [link de suporte](https://visualstudio.microsoft.com/vs/support/#talktous) para a ajuda do chat.
* [Forneça comentários sobre recursos ou relate um problema](https://aka.ms/vs/wsus/feedback) à equipe do Visual Studio para essa experiência.
* Entre em contato com o gerente técnico de conta da sua organização para a Microsoft.

## <a name="see-also"></a>Consulte também
* [Habilitando atualizações do administrador](../install/enabling-administrator-updates.md)    
* [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)
* [Ciclo de vida e manutenção do produto Visual Studio](https://docs.microsoft.com/visualstudio/productinfo/vs-servicing-vs)
* [Notas sobre a versão do Visual Studio 2019](https://docs.microsoft.com/visualstudio/releases/2019/release-notes)
* [Notas de versão do Visual Studio 2017](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes)
* [Instalar o Visual Studio](../install/install-visual-studio.md)
* [Usando parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md)
* [Criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md)
* [Como definir as configurações em um arquivo de resposta](../install/automated-installation-with-response-file.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](../install/controlling-updates-to-visual-studio-deployments.md)
* [Perguntas frequentes do catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/faq.aspx)
* [Documentação do Microsoft Endpoint Configuration Manager (SCCM)](https://docs.microsoft.com/mem/configmgr)
* [Importar atualizações do catálogo da Microsoft para o Configuration Manager](https://docs.microsoft.com/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Documentação do Windows Server Update Services (WSUS)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started-windows-server-update-services-wsus)
