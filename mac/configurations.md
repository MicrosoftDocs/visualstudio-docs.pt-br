---
title: Noções sobre configurações de build
description: Este artigo descreve as várias configurações de build no Visual Studio para Mac
author: conceptdev
ms.author: crdun
ms.date: 04/14/2017
ms.assetid: 78107CFA-9308-4293-A92A-9B552A259E15
ms.openlocfilehash: 7f130f5dec77e0a1965c68cf71e642fdb636832f
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296171"
---
# <a name="understanding-build-configurations"></a>Noções sobre configurações de build

## <a name="project-build-configurations"></a>Configurações de build do projeto

Os projetos costumam ter várias configurações e alternar entre elas permite produzir resultados diferentes no tempo de build. Por exemplo, uma Configuração de depuração gerará a saída de símbolos de depuração, permitindo que o depurador resolva nomes de funções, parâmetros ou variáveis do rastreamento de pilha do aplicativo com falha. Embora essas informações adicionais sejam úteis durante o desenvolvimento, elas levarão a um tamanho de arquivo inflado e não é ideal para distribuição.

Cada plataforma tem configurações específicas para seu build.

## <a name="solution-configurations"></a>Configurações da solução

Semelhante às configurações de projeto, as configurações da solução são usadas para criar configurações personalizadas para um projeto inteiro. Usando a guia **Mapeamentos de Configuração** no item **Build > Configurações** , você pode atribuir uma configuração de destino para cada item da solução, conforme ilustrado na imagem abaixo:

![Opções de mapeamento de configuração](media/projects-and-solutions-image3.png)

Para saber mais sobre configurações, veja o vídeo do [Configuration Manager](https://www.youtube.com/watch?v=tjSdkqYh5Vg) de James Montemagno.

## <a name="run-configuration"></a>Configuração de execução

Nas versões anteriores do Xamarin Studio, era possível selecionar a opção para configurar um projeto como um **Projeto de Inicialização**, que é o projeto que é executado/depurado usando o comando run/debug global. Isso era indicado por uma face de tipos em negrito do nome do projeto no painel do projeto.

No Visual Studio para Mac, em vez de configurar um projeto de inicialização, é possível definir uma _configuração de execução_. As configurações de execução são apresentadas em uma lista suspensa na barra de ferramentas, ao lado de seletor de configuração de build, conforme ilustrado abaixo:

![Lista suspensa Configuração de execução](media/projects-and-solutions-image8.png)

Uma configuração de execução é um conjunto de opções com um nome e várias configurações que são definidas em um projeto para finalidades diferentes. Configurações de execução são definidas no nível de projeto e um padrão será criado automaticamente para cada projeto executável, embora seja possível adicionar tantos quantos forem necessários. Certos tipos de projeto geram configurações de execução adicionais automaticamente. Por exemplo, os projetos watchOS podem gerar  _configurações de Visão geral e de Notificação._

As configurações podem ser compartilhadas com outros desenvolvedores (nesse caso elas serão armazenadas no arquivo .csproj) ou mantidas localmente (nesse caso elas serão armazenados em um arquivo .user).

### <a name="android-run-configurations"></a>Configurações de execução do Android

Configurações de execução em projetos Android permitem que você especifique quais atividade, serviços ou receptores de difusão iniciar ao executar ou depurar o projeto. Você pode passar dados extras intencionais e definir sinalizadores de intenção para poder testar seus componentes em diferentes condições de inicialização.

Atividades além de `MainLauncher` precisarão ter `Exported=true` adicionado ao atributo Atividade para a depuração em um dispositivo físico ou ter filtros de Intenção definidos.

## <a name="examples-of-data-that-might-be-included-in-run-configurations"></a>Exemplos de dados que podem ser incluídos em configurações de execução

A lista a seguir fornece alguns exemplos de dados que podem ser incluídos em configurações de execução:

* Projeto .NET regular
    * Aplicativo de inicialização alternativo
    * Argumentos iniciais
    * Diretório de trabalho
    * Variáveis de ambiente
    * Opções de tempo de execução mono (deve ser usado somente quando em execução no Mono)
* Projeto do Android
    * Ponto de entrada (atividade, serviço, receptor)
    * Dados e os argumentos de intenção
* Projeto do iOS
    * Modo (Normal, Fetch em segundo plano)
* Projeto de extensão de iOS
    * Aplicativo de inicialização: padrão ou personalizada
* Projeto do WatchKit
    * Modo (Visão rápida, Notificação)
    * Conteúdo da notificação

## <a name="see-also"></a>Consulte também

- [Noções sobre configurações de build (Visual Studio no Windows)](/visualstudio/ide/understanding-build-configurations)