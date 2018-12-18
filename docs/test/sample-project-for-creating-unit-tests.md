---
title: Código de exemplo para criar testes de unidade
description: Este artigo fornece um código de exemplo que pode ser usado com testes de unidade no Visual Studio.
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: sample
helpviewer_keywords:
- unit test sample [Visual Studio]
- unit tests, samples
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: deddf46a479e0ab8d4e0bebbaf3fffe4d90b622d
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51293441"
---
# <a name="sample-code-for-testing"></a>Código de exemplo para testes

Esse código de exemplo contém uma classe, *BankAccount*, com vários métodos que podem ser testados em testes de unidade.

O código é usado nos seguintes guias passo a passo:

- [Criar e executar testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md). Este passo a passo orienta você pelas etapas para criar e personalizar testes de unidade, executá-los e examinar os resultados de teste.
- [Usar o utilitário de teste de linha de comando](https://msdn.microsoft.com/Library/52c11992-9e94-4067-a4b7-59f19d69d867). Neste passo a passo, você usará o utilitário de linha de comando *MSTest.exe* para executar testes e exibir os resultados.

## <a name="sample-code"></a>Código de exemplo

O erro intencional apenas neste exemplo é que o método Debit em "m_balance += amount" deve ter um sinal de menos e não um sinal de mais antes do sinal de igual.

```csharp
using System;

namespace BankAccountNS
{
    /// <summary>
    /// Bank Account demo class.
    /// </summary>
    public class BankAccount
    {
        private string m_customerName;

        private double m_balance;

        private bool m_frozen = false;

        private BankAccount()
        {
        }

        public BankAccount(string customerName, double balance)
        {
            m_customerName = customerName;
            m_balance = balance;
        }

        public string CustomerName
        {
            get { return m_customerName; }
        }

        public double Balance
        {
            get { return m_balance; }
        }

        public void Debit(double amount)
        {
            if (m_frozen)
            {
                throw new Exception("Account frozen");
            }

            if (amount > m_balance)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            if (amount < 0)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            m_balance += amount; // intentionally incorrect code
        }

        public void Credit(double amount)
        {
            if (m_frozen)
            {
                throw new Exception("Account frozen");
            }

            if (amount < 0)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            m_balance += amount;
        }

        private void FreezeAccount()
        {
            m_frozen = true;
        }

        private void UnfreezeAccount()
        {
            m_frozen = false;
        }

        public static void Main()
        {
            BankAccount ba = new BankAccount("Mr. Bryan Walton", 11.99);

            ba.Credit(5.77);
            ba.Debit(11.22);
            Console.WriteLine("Current balance is ${0}", ba.Balance);
        }
    }
}
```

/* As empresas, as organizações, os produtos, os nomes de domínio, os endereços de email, os logotipos, as pessoas, os locais e os eventos de exemplo descritos aqui são fictícios. Nenhuma associação com nenhuma empresa, organização, produto, nome de domínio, endereço de email, logotipo, pessoa, locais ou eventos reais é intencional nem deve ser inferida. \*/

## <a name="create-the-project"></a>Criar o projeto

Para trabalhar com esse código, crie primeiro um projeto para ele no Visual Studio. Para criar o projeto, siga as etapas fornecidas em [Passo a passo: criar e executar testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#create-a-project-to-test).

## <a name="see-also"></a>Consulte também

- [Passo a passo: criar e executar testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)
- [Passo a passo: usar o utilitário de teste de linha de comando](https://msdn.microsoft.com/Library/52c11992-9e94-4067-a4b7-59f19d69d867)
