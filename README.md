# dio-desafio-projeto2-bootcamp-randstad-modulo5
Desafio de Projeto 2 - Módulo 5

# 🧰 Sistema de Controle e Gerenciamento de Ordens de Serviço – Oficina Mecânica

## 📖 Descrição do Projeto
Este projeto apresenta a **modelagem de banco de dados** para um sistema de controle e gerenciamento de **ordens de serviço (OS)** em uma **oficina mecânica**.  
O objetivo é representar, de forma estruturada, como as informações são armazenadas e relacionadas entre clientes, veículos, equipes, mecânicos, serviços e peças utilizadas nas ordens de serviço.

---

## 🧩 Narrativa do Caso
Clientes levam veículos à oficina mecânica para **conserto** ou **revisões periódicas**.  
Cada veículo é designado a uma **equipe de mecânicos**, responsável por identificar os serviços a serem executados e preencher uma **Ordem de Serviço (OS)** com data de entrega prevista.

A partir da OS, calcula-se o valor de cada serviço, **consultando uma tabela de referência de mão de obra**.  
Os valores das **peças utilizadas** também compõem o total da OS.  
Após a autorização do cliente, a mesma equipe **executa os serviços** até a conclusão.

Cada OS possui: **número, data de emissão, valor total, status e data de conclusão**.  
Os **mecânicos** têm código, nome, endereço e especialidade.

---

## 🧱 Modelo Entidade-Relacionamento (DER)

### 🔹 Entidades Principais

#### **Cliente**
- id_cliente (PK)
- nome
- endereco
- telefone
- email

#### **Veiculo**
- id_veiculo (PK)
- placa
- modelo
- marca
- ano
- id_cliente (FK)

#### **Equipe**
- id_equipe (PK)
- nome_equipe

#### **Mecanico**
- id_mecanico (PK)
- nome
- endereco
- especialidade
- id_equipe (FK)

#### **Ordem_Servico**
- id_os (PK)
- data_emissao
- data_conclusao
- valor_total
- status
- id_veiculo (FK)
- id_equipe (FK)

#### **Servico_Referencia**
- id_servico (PK)
- descricao
- valor_mao_obra

#### **OS_Servico**
- id_os (FK)
- id_servico (FK)
- quantidade
- valor_unitario
- valor_total

#### **Peca**
- id_peca (PK)
- descricao
- valor_unitario

#### **OS_Peca**
- id_os (FK)
- id_peca (FK)
- quantidade
- valor_total

---

## 🔗 Relacionamentos

| Entidade A | Entidade B | Tipo | Observação |
|-------------|-------------|------|-------------|
| Cliente | Veiculo | 1:N | Um cliente possui vários veículos |
| Veiculo | Ordem_Servico | 1:N | Um veículo pode gerar várias OS |
| Equipe | Ordem_Servico | 1:N | Uma equipe executa várias OS |
| Equipe | Mecanico | 1:N | Uma equipe tem vários mecânicos |
| Ordem_Servico | Servico_Referencia | N:N | Via tabela associativa OS_Servico |
| Ordem_Servico | Peca | N:N | Via tabela associativa OS_Peca |

---

## ⚙️ Regras e Observações
- O **valor total da OS** é composto pela soma dos **serviços e peças** associadas.  
- O **status da OS** pode assumir valores como: “Aberta”, “Em execução”, “Concluída” ou “Entregue”.  
- O **valor da mão de obra** é obtido a partir da tabela `Servico_Referencia`.  
- Cada **mecânico** pertence a uma **equipe** e executa serviços conforme sua **especialidade**.  
- Uma **tabela de referência de mão de obra** foi criada para padronizar os valores de serviços.

---

## 🧮 Objetivo do DER
O **Diagrama Entidade-Relacionamento (DER)** visa demonstrar:
- O fluxo de informações da oficina;
- A rastreabilidade das ordens de serviço;
- A composição de custos de peças e serviços;
- A responsabilidade das equipes e mecânicos.

---

## 🛠️ Ferramentas Utilizadas
- **Diagrama:** MySQL Workbench / Draw.io / Lucidchart  
- **Modelagem:** MER → DER  
- **Linguagem SQL:** Padrão ANSI SQL  
- **Documentação:** Markdown (`README.md`)

---

