---
title: Guia do administrador do Visual Studio
titleSuffix: ''
description: Saiba mais sobre como implantar o Visual Studio em um ambiente corporativo.
ms.custom: seodec18
ms.date: 05/29/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 358614cae2001f46588bb447d97a863cf19b8036
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159458"
---
# <a name="visual-studio-2017-administrator-guide"></a>Guia do administrador do Visual Studio 2017

Em ambientes corporativos, é comum que administradores de sistema implantem instalações para os usuários finais de um compartilhamento de rede ou usando software de gerenciamento de sistemas. Projetamos o mecanismo de instalação do Visual Studio para dar suporte à implantação corporativa, permitindo que os administradores de sistema tenham a capacidade de criar um local de instalação de rede, pré-configurar padrões de instalação, implantar chaves de produto durante o processo de instalação e gerenciar atualizações de produto depois de uma implementação com êxito. Este guia do administrador fornece orientações com base em cenários para implantações corporativas em ambientes de rede.

## <a name="deploy-visual-studio-2017-in-an-enterprise-environment"></a>Implantar o Visual Studio 2017 em um ambiente empresarial

Você pode implantar o Visual Studio 2017 para estações de trabalho cliente, contanto que cada computador de destino atenda a [requisitos mínimos de instalação](/visualstudio/productinfo/vs2017-system-requirements-vs). Se você estiver implantando por meio de softwares como o System Center ou por meio de um arquivo em lotes, normalmente é preciso percorrer as etapas a seguir:

1. [Crie um compartilhamento de rede que contenha os arquivos de produto do Visual Studio](create-a-network-installation-of-visual-studio.md) para um local de rede.

2. [Selecione as cargas de trabalho e os componentes](workload-and-component-ids.md) que deseja instalar.

3. [Crie um arquivo de resposta](automated-installation-with-response-file.md) que contenha opções de instalação padrão. Ou, como alternativa, [compile um script de instalação](use-command-line-parameters-to-install-visual-studio.md) que use parâmetros de linha de comando para controlar a instalação.

4. Opcionalmente, [aplique uma chave de produto de licença de volume](automatically-apply-product-keys-when-deploying-visual-studio.md) como parte do script de instalação para que os usuários não precisem ativar o software separadamente.

5. Atualize o layout de rede para [controlar quando as atualizações de produto serão entregues aos usuários finais](controlling-updates-to-visual-studio-deployments.md).

6. Como alternativa, defina as chaves do Registro para [controlar o que é armazenado em cache nas estações de trabalho cliente](set-defaults-for-enterprise-deployments.md).

7. Usa a tecnologia de implantação de sua escolha para executar o script gerado nas etapas anteriores em suas estações de trabalho do desenvolvedor de destino.

8. [Atualize seu local de rede com as atualizações mais recentes](update-a-network-installation-of-visual-studio.md) do Visual Studio ao executar o comando usado na etapa 1 regularmente para adicionar componentes atualizados.

> [!IMPORTANT]
> Observe que as instalações de um compartilhamento de rede se “lembrarão” do seu local de origem. Isso significa que um reparo de um computador cliente pode ter que retornar para o compartilhamento de rede do qual o cliente foi instalado originalmente. Escolha cuidadosamente seu local de rede para que ele se alinhe com o tempo de vida esperado de execução de clientes do Visual Studio 2017 na sua organização.

## <a name="use-visual-studio-tools"></a>Usar ferramentas do Visual Studio

Temos várias ferramentas disponíveis para ajudar você a [detectar e gerenciar instâncias do Visual Studio instaladas](tools-for-managing-visual-studio-instances.md) em computadores cliente.

> [!TIP]
> Além da documentação no guia do administrador, uma boa fonte de informações sobre a instalação do Visual Studio 2017 é o [blog de Heath Stewart](https://blogs.msdn.microsoft.com/heaths/tag/vs2017/).

## <a name="specify-customer-feedback-settings"></a>Especificar configurações de comentários do cliente

Por padrão, a instalação do Visual Studio habilita os comentários do cliente. Quando você habilita a Política de Grupo, é possível configurar o Visual Studio para desabilitar os comentários do cliente em computadores individuais. Para fazer isso, defina uma política baseada no Registro na seguinte chave:

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SQM**

Entrada = **OptIn**

Valor = (DWORD)
* **0** é recusado
* **1** é aceito

Para obter mais informações sobre configurações dos comentários do cliente, confira a página [Programa de Aperfeiçoamento da Experiência do Usuário do Visual Studio](../ide/visual-studio-experience-improvement-program.md).

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio 2017](install-visual-studio.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio 2017](use-command-line-parameters-to-install-visual-studio.md)
  * [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md)
  * [Referência de ID de componente e carga de trabalho](workload-and-component-ids.md)
* [Criar uma instalação em rede do Visual Studio](create-a-network-installation-of-visual-studio.md)
  * [Instalar os certificados necessários para instalação offline do Visual Studio](install-certificates-for-visual-studio-offline.md)
* [Automatizar o Visual Studio com um arquivo de resposta](automated-installation-with-response-file.md)
* [Chaves de produto automaticamente durante a implantação do Visual Studio](automatically-apply-product-keys-when-deploying-visual-studio.md)
* [Definir padrões para implantações empresariais do Visual Studio](set-defaults-for-enterprise-deployments.md)
* [Desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md)
* [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
* [Atualizações de controle para implantações do Visual Studio](controlling-updates-to-visual-studio-deployments.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
