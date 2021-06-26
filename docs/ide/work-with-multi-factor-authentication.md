---
title: Usar contas que exigem autenticação multifafação
ms.date: 05/27/2020
ms.custom: SEO-VS-2020
ms.topic: conceptual
description: Saiba como usar o Visual Studio com contas que exigem autenticação multifafação.
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 9ac42ccff8c7bffcc22c453002aad1caf6935d28
ms.sourcegitcommit: e4630a3bb89b4d606fe2cbd709bc773c5b538b78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2021
ms.locfileid: "112975678"
---
# <a name="how-to-use-visual-studio-with-accounts-that-require-multi-factor-authentication"></a>Como usar o Visual Studio com contas que exigem autenticação multifafação

Ao colaborar com usuários convidados externos, é uma boa ideia proteger seus aplicativos e dados com políticas de **AC (acesso condicional),** como a **MFA (autenticação multifacional).**  

Depois de habilitados, os usuários convidados precisarão de mais do que apenas um nome de usuário e senha para acessar seus recursos e deverão atender aos requisitos de segurança adicionais. As políticas de MFA podem ser impostas no nível do locatário, aplicativo ou usuário convidado individual, da mesma maneira que podem ser habilitadas para membros da sua própria organização. 

## <a name="how-is-the-visual-studio-experience-affected-by-mfa-policies"></a>Como a experiência Visual Studio é afetada pelas políticas de MFA?
Versões do Visual Studio anteriores à 16.6 podem ter experiências de autenticação degradadas quando usadas com contas que habilitaram políticas de AC, como MFA, e estão associadas a dois ou mais locatários.

Esses problemas podem fazer com que sua instância Visual Studio solicitar a autenticação várias vezes por dia. Talvez seja preciso reinserar suas credenciais para locatários autenticados anteriormente, mesmo durante a mesma sessão Visual Studio.

## <a name="using-visual-studio-with-mfa-policies"></a>Usando Visual Studio com políticas de MFA
Na versão 16.6, adicionamos novos recursos ao Visual Studio 2019 que simplificam como os usuários podem acessar recursos protegidos por meio de políticas de AC, como MFA. Para usar esse fluxo de trabalho aprimorado, você precisará optar por usar o navegador da Web padrão do sistema como o mecanismo para adicionar e autenticar Visual Studio contas.  

> [!WARNING]
> Não usar esse fluxo de trabalho pode disparar uma experiência degradada, resultando em vários prompts de autenticação adicionais ao adicionar ou autenticar Visual Studio contas. 

### <a name="enabling-system-web-browser"></a>Habilitando o navegador da Web do sistema

> [!NOTE] 
> Para a melhor experiência, recomendamos limpar os dados padrão do navegador da Web do sistema antes de continuar com esse fluxo de trabalho. Além disso, se você tiver contas de trabalho ou de estudante em suas Windows 10 configurações em Acessar trabalho ou **escola,** verifique se elas estão autenticadas corretamente.

Para habilitar esse fluxo de trabalho, vá para a caixa de diálogo  Opções do Visual Studio **(Ferramentas > Opções...)**, selecione a guia Contas e escolha Navegador da **Web** do sistema na lista suspenso Adicionar e autenticar contas **usando:** . 

:::image type="content" source="media/select-system-web-browser.png" alt-text="Selecione navegador da Web do sistema no menu.":::

### <a name="sign-into-additional-accounts-with-mfapolicies"></a>Entrar em contas adicionais com políticas de MFA 
Depois que o fluxo de trabalho do navegador da Web do sistema for habilitado, você poderá entrar ou adicionar contas ao Visual Studio como faria normalmente, por meio da caixa de diálogo Configurações da Conta (Configurações de Conta > **Arquivo...)**.   
</br>
:::image type="content" source="media/add-personalization-account.png" alt-text="Adicione uma nova conta de personalização ao Visual Studio." border="false":::

Essa ação abrirá o navegador da Web padrão do sistema, solicitará que você entre em sua conta e valide qualquer política de MFA necessária.

Durante o processo de login, você pode receber um prompt adicional solicitando que você permaneça entre. Esse prompt provavelmente será a segunda vez que uma conta for usada para entrar. Para minimizar a necessidade de inserir suas credenciais, recomendamos que você selecione **Sim,** pois isso garante que suas credenciais sejam preservadas entre as sessões do navegador.

:::image type="content" source="media/kmsi.png" alt-text="Mantenha-se dentro?":::

Com base em suas atividades de desenvolvimento e na configuração de recursos, talvez você ainda seja solicitado a reinserar suas credenciais durante a sessão. Isso pode ocorrer quando você adiciona um novo recurso ou tenta acessar um recurso sem ter atendido anteriormente aos requisitos de autorização de CA/MFA.

## <a name="reauthenticating-an-account"></a>Reauthenticando uma conta  
Se houver um problema com sua conta, você Visual Studio solicitar que você reinsera suas credenciais de conta.  

:::image type="content" source="media/reauthenticate-account.png" alt-text="Autenticar sua conta de Visual Studio.":::

Clicar em **Reinserar suas** credenciais abrirá o navegador da Web padrão do sistema e tentará atualizar automaticamente suas credenciais. Se não tiver êxito, você será solicitado a entrar em sua conta e validar qualquer política de CA/MFA necessária.

> [!NOTE] 
> Para a melhor experiência, mantenha seu navegador aberto até que todas as políticas de CA/MFA sejam validadas para seus recursos. Fechar o navegador pode resultar na perda do estado de MFA criado anteriormente e pode solicitar prompts de autorização adicionais.

## <a name="how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio"></a>Como não usar um locatário de Azure Active Directory específico no Visual Studio

Visual Studio 2019 versão 16.6 oferece a flexibilidade de filtrar locatários individual ou globalmente, efetivamente hidding-los de Visual Studio. A filtragem elimina a necessidade de autenticação com esse locatário, mas também significa que você não poderá acessar nenhum recurso associado.

Essa funcionalidade é útil quando você tem vários locatários, mas deseja otimizar seu ambiente de desenvolvimento direcionando um subconjunto específico. Ele também pode ajudar em instâncias quando você não pode validar uma política de CA/MFA específica, pois você pode filtrar o locatário que está com problemas. 

### <a name="how-to-filter-out-all-tenants"></a>Como filtrar todos os locatários
Para filtrar globalmente todos os locatários, abra a caixa de diálogo Configurações da Conta (Configurações da Conta do > **arquivo...)** e desmarque a caixa de seleção Autenticar em todos os Diretórios **Azure Active.**

A desmarcação dessa opção garante que você se autentidade apenas com o locatário padrão da conta. Isso também significa que você não poderá acessar nenhum recurso associado a outros locatários em que sua conta possa ser um convidado.

### <a name="how-to-filter-out-individual-tenants"></a>Como filtrar locatários individuais
Para filtrar os locatários associados à sua conta Visual Studio, abra a caixa de diálogo Configurações da Conta (Configurações da Conta > **Arquivo...)** e clique em **Aplicar filtro**. 
</br>
</br>

:::image type="content" source="media/apply-filter.png" alt-text="Aplicar filtro." border="false":::

A **caixa de diálogo** Filtrar conta será exibida, permitindo que você selecione quais locatários deseja usar com sua conta. 

:::image type="content" source="media/select-filter-account.png" alt-text="Selecione conta para filtrar.":::

## <a name="see-also"></a>Confira também

- [Entrar no Visual Studio](signing-in-to-visual-studio.md)
- [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in)
- [Trabalhar com várias contas de usuário](work-with-multiple-user-accounts.md)
