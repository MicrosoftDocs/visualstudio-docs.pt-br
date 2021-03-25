---
title: Decisões de design de tipo de projeto | Microsoft Docs
description: Saiba mais sobre o item, a persistência de arquivo de projeto e as decisões de design mecânico de compromisso a serem tomadas antes de estender o Visual Studio criando um novo tipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f1a90082b0ba9d18336463b26cf72acea39851b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064303"
---
# <a name="project-type-design-decisions"></a>Decisões de design do tipo de projeto
Antes de criar um novo tipo de projeto, você deve tomar várias decisões de design em relação ao tipo de projeto. Você deve decidir quais tipos de itens seus projetos conterão, como os arquivos de projeto serão persistidos e qual modelo de compromisso será usado.

## <a name="project-items"></a>Itens de projeto
 Seu projeto usará arquivos ou objetos abstratos? Se você usar arquivos, eles serão arquivos baseados em referência ou em diretório? Os arquivos ou objetos abstratos serão locais ou remotos?

 Os itens em um projeto podem ser arquivos, ou podem ser objetos mais abstratos, como objetos em um repositório de banco de dados ou conexões de data pela Internet. Se os itens forem arquivos, o projeto poderá ser um projeto baseado em referência ou em diretório.

 Em projetos baseados em referência, os itens podem aparecer em mais de um projeto. No entanto, o arquivo real que um item representa está localizado em apenas um diretório. Em projetos baseados em diretório, existem todos os itens de projeto na estrutura de diretório.

 Os itens locais são armazenados no mesmo computador em que o aplicativo está instalado. Os itens remotos podem ser armazenados em um servidor separado em uma rede local ou em outro lugar na Internet.

## <a name="project-file-persistence"></a>Persistência de arquivo de projeto
 Os dados serão armazenados em sistemas de arquivos simples comuns ou no armazenamento estruturado? Os arquivos serão abertos usando um editor padrão ou um editor específico do projeto?

 Para manter seus dados, a maioria dos aplicativos salva seus dados em um arquivo e, em seguida, lê-los novamente quando um usuário precisar revisar ou alterar as informações.

 O armazenamento estruturado, também chamado de arquivos compostos, é usado normalmente quando vários objetos COM (Component Object Model) precisam armazenar seus dados persistentes em um único arquivo. Com o armazenamento estruturado, vários componentes de software diferentes podem compartilhar um único arquivo de disco.

 Você tem várias opções a serem consideradas relativas à persistência para os itens em seu projeto. Você pode executar qualquer uma das seguintes opções:

- Salve cada arquivo individualmente quando ele tiver sido alterado.

- Capturar várias transações em uma única operação de **salvamento** .

- Salve os arquivos localmente e, em seguida, publique em um servidor ou use outra abordagem para salvar itens de projeto quando o item representar uma conexão de dados com um objeto remoto.

  Para obter mais informações sobre persistência, consulte [persistência do projeto](../../extensibility/internals/project-persistence.md) e [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).

## <a name="project-commitment-model"></a>Modelo de compromisso do projeto
 Os objetos de dados persistidos serão abertos em modo direto ou em modo transacionado?

 Quando os objetos de dados são abertos no modo direto, as alterações feitas nos dados são incorporadas imediatamente ou quando o usuário salva o arquivo manualmente.

 Quando os objetos de dados são abertos usando o modo transacionado, as alterações são salvas em um local temporário na memória e não são confirmadas até que o usuário opte manualmente por salvar o arquivo. Nesse momento, todas as alterações devem ocorrer juntas ou nenhuma alteração será feita.

## <a name="see-also"></a>Confira também
- [Lista de verificação: Criando tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)
- [Persistência de projeto](../../extensibility/internals/project-persistence.md)
- [Elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md)
- [Componentes principais do projeto modelo](../../extensibility/internals/project-model-core-components.md)
- [Criando tipos de projeto](../../extensibility/internals/creating-project-types.md)
