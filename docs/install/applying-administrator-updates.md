---
title: Aplicar atualizações de administrador ao Visual Studio com Microsoft Endpoint Configuration Manager
titleSuffix: ''
description: Saiba como aplicar atualizações de administrador ao Visual Studio.
ms.date: 04/16/2021
ms.custom: ''
ms.topic: overview
ms.assetid: 9a3fdb28-db3d-4970-bc17-7417a985f0fb
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: c18c460ebcffdba93279aafec2f3d76503ab2383
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307681"
---
# <a name="applying-administrator-updates-that-use-microsoft-endpoint-configuration-manager"></a>Aplicando atualizações de administrador que usam Microsoft Endpoint Configuration Manager

Este documento descreve diferentes tipos e características de atualizações Visual Studio administrador. Abaixo, você encontrará informações sobre como e quando elas devem ser distribuídas em toda a sua organização, quais opções de configuração estão disponíveis e como exibir relatórios e solucionar problemas. Para obter mais informações sobre os pré-requisitos para usar atualizações de administrador, consulte [Habilitando atualizações de administrador.](../install/enabling-administrator-updates.md) As atualizações de administrador presumem Visual Studio já está instalado no computador. Aplicar atualizações de administrador não iniciará uma nova instalação.

## <a name="understanding-visual-studio-administrator-updates"></a>Noções básicas Visual Studio de administrador

O pacote de atualização do administrador do Visual Studio publicado no Microsoft Update para consumo pelo Catálogo da Microsoft e pelo WSUS contém informações de que o Gerenciador de Configurações precisa ser capaz de baixar e distribuir Visual Studio atualização para máquinas cliente. Ele também contém informações de que um administrador de IT precisa para decidir quais atualizações distribuir em toda a organização. Ele também pode ser usado para facilitar a manutenção de layouts de rede. Os Visual Studio pacotes de atualização do administrador não contêm informações suficientes para fazer uma nova instalação do produto, nem contêm nenhum dos binários reais do produto publicados na Rede de Distribuição de Conteúdo. Visual Studio atualizações de administrador são cumulativas, assim como as atualizações Visual Studio regulares. Você pode supor que qualquer atualização Visual Studio que tenha um número de versão de produto mais alto e uma data de lançamento posterior seja um superconjunto de uma versão mais antiga e inferior.

Visual Studio de administrador se aplicam Visual Studio versões de manutenção que estão sob suporte. Para obter mais informações sobre Visual Studio linhas de base de manutenção ainda estão em suporte durante um período de tempo específico, consulte Visual Studio ciclo de vida e [manutenção do produto](/visualstudio/productinfo/vs-servicing-vs). Todas as linhas de Visual Studio de manutenção com suporte serão mantidas seguras.  

## <a name="types-and-characteristics-of-administrator-updates"></a>Tipos e características de atualizações de administrador

Há três tipos de atualizações de administrador para Visual Studio:

* **As atualizações** de segurança são aplicáveis Visual Studio todas as edições do Visual Studio (por exemplo, Enterprise, Professional, Community etc.) e contêm alterações de nível de serviço limitadas, altamente direcionadas e compatíveis. As atualizações de segurança não avançarão um cliente para uma versão secundária posterior; eles foram projetados para fornecer correções para vulnerabilidades de segurança para um cliente que já está em um nível de versão secundária específico. As atualizações de segurança terão pelo menos uma correção de segurança, mas a correção de segurança pode ou não estar em um componente ou carga de trabalho instalado no computador cliente. Por exemplo, poderíamos corrigir uma vulnerabilidade de segurança nos componentes do .NET e rotular a atualização como uma atualização de segurança, mas ela não teria nenhum efeito significativo em um computador cliente que tivesse apenas componentes C++ instalados. As atualizações de segurança também podem conter outras correções de confiabilidade ou outras atualizações de componente necessárias. As atualizações de segurança são publicadas no MUC (Catálogo [Microsoft Update)](https://www.catalog.update.microsoft.com/Home.aspx) e Windows Server Update Services [,](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)em que são classificadas como "Atualizações de Segurança".
* **As atualizações de recursos** permitem que os administradores de IT avancem os computadores em sua organização para uma versão secundária mais recente do Visual Studio. As atualizações de recursos se aplicam Visual Studio edições que normalmente são encontradas em empresas, como SKUs enterprise, Professional e Ferramentas de Build. Todas as atualizações de recursos serão publicadas no Catálogo do Microsoft Update como "Feature Packs" e estão disponíveis para, opcionalmente, importar manualmente para Gerenciador de Configurações do [catálogo Microsoft Update](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog). As atualizações de recursos são cumulativas e conterão correções de segurança anteriores e de qualidade adicionais. Consulte a seção [opções de](#understanding-configuration-options) configuração abaixo para obter instruções sobre como configurar um computador cliente para permanecer em uma linha de base de serviço e impedir que as atualizações de recursos seja entregue a clientes específicos.
* **As atualizações** de qualidade também são aplicáveis apenas às edições Visual Studio que normalmente são encontradas em empresas e contêm alterações de nível de serviço limitadas, altamente direcionadas e compatíveis. As atualizações de qualidade não avançarão um cliente para uma versão secundária posterior; eles foram projetados para fornecer correções de desempenho e confiabilidade ou outras atualizações de componente necessárias para um cliente que já está em um nível de versão secundária específico. As atualizações de qualidade se acumulam junto com as atualizações de segurança e, portanto, conterão correções de segurança somente se a correção de segurança já tiver sido liberada independentemente. As atualizações de qualidade são publicadas no catálogo Microsoft Update como "Atualizações" e também estão disponíveis para importar manualmente para o Gerenciador de Configurações [.](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)

### <a name="decoding-the-titles-of-administrator-updates"></a>Decodificar os títulos das atualizações do administrador

O título de cada atualização de administrador descreve o intervalo de versão aplicável e a versão resultante da atualização.Por exemplo,

::: moniker range="vs-2017"

* A atualização Visual Studio **2017 versão 15.9.0 a 15.9.35** classificada como uma "Atualização de Segurança" será aplicada a qualquer edição do Visual Studio 2017 no cliente entre as versões 15.9.0 a 15.9.35 e atualizará essas edições do cliente para a versão 15.9.35.
* A atualização do **Visual Studio 2017 versão 15.0.0 a 15.9.0** classificada como um "Feature Pack" será aplicada às edições do Visual Studio 2017 licenciadas para uso empresarial no cliente entre todo o intervalo de versão do produto de 15.0.0 a 15.9.0 e atualizará essas edições do cliente para 15.9.0. A aplicação desse feature pack basicamente permite que os clientes recebam atualizações de segurança. 
* A atualização do **Visual Studio 2017 versão 15.9.0 a 15.9.37** classificada como simplesmente "Atualizações" se aplicará às edições do Visual Studio 2017 licenciadas para uso empresarial no cliente entre as versões 15.9.0 e 15.9.37 e atualizará essas edições do cliente para a versão 15.9.37.

::: moniker-end

::: moniker range="vs-2019"

* A atualização Visual Studio **2019 versão 16.7.0 a 16.7.12** classificada como uma "Atualização de Segurança" será aplicada a qualquer edição do Visual Studio 2019 no cliente entre as versões 16.7.0 a 16.7.12 e atualizará essas edições do cliente para a versão 16.7.12.  
* A atualização Visual Studio **2019 versão 16.0.0 a 16.9.0** classificada como um "Feature Pack" se aplicará às edições Visual Studio 2019 licenciadas para uso empresarial no cliente entre todo o intervalo de versão do produto de 16.0.0 a 16.9.0, e atualizará essas edições de cliente (que não foram configuradas para permanecer em uma linha de base de manutenção anterior) para 16.9.0. 
* A atualização do **Visual Studio 2019 versão 16.8.0 a 16.8.7** classificada como simplesmente "Atualizações" se aplicará às edições do Visual Studio 2019 licenciadas para uso empresarial no cliente entre as versões 16.8.0 a 16.8.7 e atualizará essas edições do cliente para a versão 16.8.7.

::: moniker-end

::: moniker range=">=vs-2022"

::: moniker-end

## <a name="using-configuration-manager-to-deploy-visual-studio-updates"></a>Usando Gerenciador de Configurações para implantar Visual Studio atualizações

### <a name="understanding-configuration-options"></a>Noções básicas sobre opções de configuração

Há algumas opções de configuração que podem ser usadas para adaptar as atualizações do administrador Visual Studio para que elas sejam compatíveis e alinhadas com as preferências e os requisitos de implantação da sua organização. As opções de configuração mais comuns estão listadas abaixo. Para ver uma lista completa de todos os comportamentos de atualização de administrador com suporte, consulte Usar [parâmetros](../install/use-command-line-parameters-to-install-visual-studio.md) de linha de comando para instalar o Visual Studio e preste atenção apenas àqueles que correspondem à ação de "atualização".

* **[Aceitação da atualização do administrador:](../install/enabling-administrator-updates.md#encoding-administrator-intent-on-the-client-machines)** essa chave do Registro é necessária para que o computador cliente receba atualizações de administrador. É uma chave em todo o computador, o que significa que ela se aplica a todas as instâncias de Visual Studio instaladas na caixa.
* **Visual Studio** de usuário: Visual Studio usuários podem usar uma chave do Registro **AdministratorUpdatesOptOut**  separada em todo o computador para não receber Visual Studio de administrador. A finalidade dessa chave é permitir que o usuário Visual Studio tenha algum controle sobre como ter atualizações aplicadas automaticamente ao computador. Para configurar o computador cliente para bloquear atualizações de administrador, de definido como **AdministradorUpdatesOptOut** REG_DWORD   chave como **1**. A ausência da chave ou um valor definido de **0** significa que o Visual Studio usuário deseja receber atualizações de administrador para Visual Studio.
    Observe que a chave **AdministratorUpdatesOptOut** para codificar a preferência do usuário é priorizada em relação à chave    **AdministratorUpdatesEnabled,** que codifica a intenção de administrador   de IT. Se **AdministratorUpdatesOptOut** for definido como 1 , a atualização será bloqueada no cliente, mesmo que a chave    **AdministratorUpdatesEnabled** também seja definida como ****    **1**.Essa ação pressuém que os administradores de IT podem acessar e monitorar quais desenvolvedores optaram por ressutar e que as duas partes podem discutir quais necessidades são mais importantes.Os administradores de IT sempre podem alterar qualquer chave sempre que quiserem.
* **Local dos bits de produto atualizados:** na maioria das vezes, os máquinas cliente baixam os bits de produto atualizados da Internet por meio da CDN da Microsoft. Esse cenário exige que os máquinas cliente tenham acesso à Internet. No entanto, algumas empresas restringem os máquinas cliente a instalar e atualizar apenas os bits de um local de layout de rede interno. Para garantir que as atualizações de administrador possam ser aplicadas usando bits atualizados que estão em um local de rede interno, as seguintes condições devem ser verdadeiras antes que a atualização do administrador possa ser implantada com êxito: 
  * O computador cliente deve ter, em algum momento, já executado o bootstrapper desse local de layout de rede. Idealmente, a instalação original do cliente teria ocorrido usando o bootstrapper do layout de rede, mas também é possível ter apenas instalado uma atualização usando um bootstrapper atualizado no mesmo local de rede. Qualquer uma dessas ações inseriria, no computador cliente, uma conexão com esse local de layout específico.
  * O local de layout de rede (ao qual o cliente está conectado) deve ser atualizado para conter os [bits](../install/update-a-network-installation-of-visual-studio.md) de produto atualizados que a atualização do administrador deseja implantar.

::: moniker range=">=vs-2019"

* **Manutenção de manutenção de** linha de base : conforme descrito acima, as atualizações de recursos do administrador avançam uma Visual Studio para uma versão secundária mais atual do produto. Às vezes, Visual Studio usuários precisam permanecer em um nível de linha de base de manutenção estável e seguro específico e querem controlar quando seus máquinas avançam para uma versão secundária mais atual. Para configurar um computador cliente para permanecer em uma linha de base de serviço e ignorar as atualizações de recursos de administrador indesejáveis enviadas a ele, você precisará criar e definir o valor de dados **baselineStickinessVersions2019** Reg_SZ como uma cadeia de caracteres que representa a linha de base preferencial à quais o computador cliente deve se ajustar e permanecer. A cadeia de caracteres pode conter uma versão de linha de base de manutenção **acessível, como 16.7.0**.  
     Se o valor do Registro estiver malformado, todas as atualizações de recursos do administrador serão impedidas de `BaselineStickinessVersions2019` serem instaladas no computador. Certifique-se de prestar atenção aos [períodos de tempo com suporte para Visual Studio atualizações de recursos.](/visualstudio/productinfo/vs-servicing-vs) Além disso, independentemente da presença ou do valor da chave, embora seja tecnicamente possível aplicar atualizações de recursos de administrador que atingiram o fim de seus tempos de vida, não recomendamos isso porque eles estarão sem suporte e, portanto, potencialmente `BaselineStickinessVersions2019` inseguros.

::: moniker-end

* **Force a atualização a ocorrer mesmo se Visual Studio estiver em uso:** Visual Studio deve ser fechado antes de instalar a atualização. Se Visual Studio estiver aberto ou estiver sendo usado, a instalação da atualização será anulada. Uma maneira fácil de garantir que o Visual Studio está fechado é configurar o Gerenciador de Confirmação para aplicar a atualização logo após uma reinicialização do computador. Você também pode usar o `--force` parâmetro para forçar o Visual Studio. Forçar Visual Studio fechar pode causar perda de trabalho, portanto, use-o com cuidado. Executar uma atualização de administrador no contexto do sistema padrão ignorará o sinalizador, portanto, você precisará configurar a Atualização do administrador para ser `–-force` executado no contexto do usuário.

### <a name="methods-for-configuring-an-administrator-update"></a>Métodos para configurar uma atualização de administrador

Há três métodos principais de configuração de atualizações de administrador: uma chave do Registro, um arquivo de configuração no computador cliente ou uma modificação do próprio pacote Gerenciador de Configurações implantação.   

* **Chave do Registro:** as atualizações do administrador pesquisam chaves específicas do Registro em qualquer um dos locais de Visual Studio padrão, conforme descrito em Definir padrões para [implantações corporativas.](../install/set-defaults-for-enterprise-deployments.md) As opções controladas por chaves do Registro são itens como **AdministratorUpdatesOptOut** Reg_DWORD, **AdministratorUpdatesOptOut** Reg_DWORD e   **BaselineStickinessVersions2019** Reg_SZ. O acesso de administrador no computador cliente é necessário para criar e definir o valor das chaves do Registro.

* **Arquivo de** configuração: algumas configurações podem ser preservadas no computador cliente em um arquivo de configuração opcional, que tem o benefício de defini-lo apenas uma vez e fazer com que ele se aplique a todas as atualizações futuras do administrador. A abordagem do arquivo de configuração se comporta como uma chave do Registro e é de todo o computador, o que significa que ela se aplicará a todas as Visual Studio instaladas no computador cliente. O local padrão para o arquivo de configuração está em `C:\ProgramData\Microsoft\VisualStudio\updates.config` . No entanto, se você quiser usar outro local para armazenar o arquivo, poderá fazer isso criando uma chave do Registro Reg_SZ chamada **UpdateConfigurationFile** e definindo o valor dessa chave para o caminho do arquivo de configuração. Essa chave do Registro pode ser colocada em qualquer um dos locais Visual Studio registro, conforme descrito em Definir padrões [para implantações corporativas.](../install/set-defaults-for-enterprise-deployments.md) Se você optar por adicionar um valor de Registro para um local de arquivo de configuração personalizado, ele procurará esse arquivo; se o arquivo não existir, uma exceção será lançada e a atualização falhará.

     O arquivo de configuração, que está no formato JSON, dá suporte à opção que é uma matriz de cadeias de caracteres separadas por vírgulas que especificam mais opções que você pode passar para o Visual Studio `installerUpdateArgs` instalador. Se o conteúdo do arquivo incluir um campo inválido ou uma opção sem suporte, a atualização falhará. Para obter mais informações, [consulte Usar parâmetros de linha de comando para instalar Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md).

   Aqui está um arquivo de configuração de exemplo:

  ```json
  "installerUpdateArgs" : ["--quiet", "--noWeb"], 
  "checkPendingReboot" :  "true" 
  ```

* Atualizar manualmente o pacote de atualizações de administrador no **SCCM:** os parâmetros de linha de comando de um pacote de atualização de administrador individual no SCCM também podem ser modificados manualmente.

## <a name="verification-reports-and-troubleshooting-error-codes"></a>Verificação, relatórios e códigos de erro de solução de problemas

### <a name="determining-that-visual-studio-was-updated"></a>Determinando que o Visual Studio foi atualizado

Você pode usar um dos seguintes métodos para verificar se a atualização do administrador foi instalada corretamente:

* No computador cliente, inicie o Visual Studio, selecione **ajuda**   >  **sobre** e verifique se o número de versão corresponde ao último número no título da atualização pretendida.
* Use a ferramenta **vswhere** no computador cliente para identificar as várias versões do Visual Studio no computador. Para obter mais informações, consulte [ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md).
* Cada tentativa de atualização administrativa gera vários arquivos de log no diretório da máquina cliente `%temp%` que captura o progresso da operação de atualização.Classifique a pasta por data e procure os arquivos que começam  `dd_updatedriver` ,  `dd_bootstrapper` ,  `dd_client` e  `dd_setup`   para as atualizações administrativas, o bootstrapper, o instalador do Visual Studio e o mecanismo de instalação, respectivamente.Verifique se esses arquivos de log contêm um 0, indicando que a atualização foi aplicada com êxito. Observe que esses arquivos de log também podem ser usados para verificar se o arquivo de configuração está sendo usado. Consulte a [ferramenta de coleta de logs do Visual Studio](https://www.microsoft.com/download/details.aspx?id=12493) para obter mais detalhes.

### <a name="error-codes-and-conditions"></a>Códigos de erro e condições

>[!IMPORTANT]
> Lembre-se de que o Visual Studio deve ser fechado antes da instalação da atualização. Se o Visual Studio estiver aberto ou sendo usado, a instalação da atualização será cancelada.

As atualizações administrativas podem retornar os seguintes códigos de retorno:  

| Código do erro | Definição                                                                                                                                                                                                  |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0          | A atualização administrativa foi instalada com êxito.                                                                                                                                                       |
| 1001       | Instalador do Visual Studio ou um processo de instalação relacionado está em execução. A atualização não é aplicada.                                                                                                                   |
| 1002       | Instalador do Visual Studio está em pausa. A atualização não é aplicada.                                                                                                                                               |
| 1003       | O Visual Studio está em execução. A atualização não é aplicada. Essa condição pode ser sobrerégua usando o `--force` sinalizador.                                                                                              |
| 1004       | Nenhuma Internet detectada.A atualização não pôde entrar em contato com o local da Internet que contém os arquivos atualizados. A atualização não é aplicada.                                                                          |
| 1005       | O  ****   valor do registro AdministratorUpdatesEnabled é definido como **0** ou não definido. A atualização não é aplicada.                                                                                            |
| 1006       | O  ****   valor do registro AdministratorUpdatesOptOut é definido como **1**. A atualização não é aplicada. A chave destina-se a computadores cliente que não devem ser atualizados pelo administrador.                     |
| 1007       | O Instalador do Visual Studio não está instalado.                                                                                                                                                               |
| 1008       | O valor do registro **BaselineStickinessVersions2019** não está em um formato legível. O valor do registro deve incluir **todas as** versões ou as válidas com o número de Build definido como 0 explicitamente, por exemplo, X. Y. 0. |
| 3010       | O sistema requer uma reinicialização.A atualização pode ou não ter sido aplicada. Reinicialize o computador e tente a atualização novamente.                                                                                |
| Outro      | Erro ao tentar aplicar a atualização.A atualização não é aplicada.                                                                                                                                   |

Para obter uma lista completa dos códigos de erro do cliente, consulte [usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md).

## <a name="feedback-and-support"></a>Comentários e suporte

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

Você pode usar os seguintes métodos para fornecer comentários sobre as atualizações do administrador do Visual Studio ou os problemas de relatório que afetam as atualizações:

* Consulte as diretrizes [solução de problemas de instalação e atualização do Visual Studio](../install/troubleshooting-installation-issues.md) .
* Faça perguntas à Comunidade na instalação do [Visual Studio Q&um fórum](/answers/topics/vs-setup.html).
* Vá para a [página de suporte do Visual Studio](https://visualstudio.microsoft.com/vs/support/)e verifique se o problema está listado nas perguntas frequentes.  Você também pode selecionar o botão [link de suporte](https://visualstudio.microsoft.com/vs/support/#talktous) para a ajuda do chat.
* [Forneça comentários sobre recursos ou relate um problema](https://aka.ms/vs/wsus/feedback) à equipe do Visual Studio sobre essa experiência de aplicação de atualizações do administrador.
* Entre em contato com o gerente técnico de conta da sua organização para a Microsoft.

## <a name="see-also"></a>Confira também

* [Habilitando atualizações do administrador](../install/enabling-administrator-updates.md)
* [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)
* [Ciclo de vida e manutenção do produto Visual Studio](/visualstudio/productinfo/vs-servicing-vs)
* [Notas sobre a versão do Visual Studio 2019](/visualstudio/releases/2019/release-notes)
* [Notas de versão do Visual Studio 2017](/visualstudio/releasenotes/vs2017-relnotes)
* [Instalar o Visual Studio](../install/install-visual-studio.md)
* [Usando parâmetros de linha de comando para instalar o Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md)
* [Criar uma instalação de rede do Visual Studio](../install/create-a-network-installation-of-visual-studio.md)
* [Como definir as configurações em um arquivo de resposta](../install/automated-installation-with-response-file.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](../install/controlling-updates-to-visual-studio-deployments.md)
* [Perguntas frequentes do catálogo de Microsoft Update](https://www.catalog.update.microsoft.com/faq.aspx)
* [Documentação do Microsoft Endpoint Configuration Manager (SCCM)](/mem/configmgr)
* [Importar atualizações do catálogo da Microsoft para o Configuration Manager](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Documentação do Windows Server Update Services (WSUS)](/windows-server/administration/windows-server-update-services/get-started-windows-server-update-services-wsus)
