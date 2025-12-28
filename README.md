# Projeto_Modelagem_BD2

# 🧰 Sistema de Oficina Mecânica  
### Controle e Gerenciamento de Ordens de Serviço

Este projeto apresenta o modelo de banco de dados para um sistema de **oficina mecânica**, com foco na gestão de ordens de serviço, clientes, veículos, equipes de mecânicos, serviços e peças. O objetivo é fornecer uma estrutura relacional robusta para implementação em SGBDs como MySQL, PostgreSQL ou SQL Server.

---

## 📌 Visão Geral do Projeto

O sistema permite:

- Cadastro de clientes e seus veículos  
- Emissão e controle de ordens de serviço (OS)  
- Designação de equipes de mecânicos para cada OS  
- Registro de serviços e peças utilizados  
- Cálculo automático de valores por mão de obra e peças  
- Autorização formal do cliente para execução dos serviços  

---

## 🧱 Entidades e Atributos

### **Cliente**
| Campo | Tipo |
|-------|------|
| idCliente | INT |
| nome | VARCHAR(60) |
| endereco | VARCHAR(100) |
| telefone | VARCHAR(20) |

### **Veículo**
| Campo | Tipo |
|-------|------|
| idVeiculo | INT |
| placa | VARCHAR(10) |
| modelo | VARCHAR(45) |
| marca | VARCHAR(45) |
| ano | INT |
| Cliente_idCliente | INT |

### **Mecânico**
| Campo | Tipo |
|-------|------|
| idMecanico | INT |
| nome | VARCHAR(60) |
| endereco | VARCHAR(100) |
| especialidade | VARCHAR(45) |

### **Equipe**
| Campo | Tipo |
|-------|------|
| idEquipe | INT |
| nomeEquipe | VARCHAR(45) |

### **Equipe_Mecanico** (associação N:N)
| Campo | Tipo |
|-------|------|
| idEquipe | INT |
| idMecanico | INT |

### **Ordem de Serviço (OS)**
| Campo | Tipo |
|-------|------|
| idOS | INT |
| dataEmissao | DATE |
| dataConclusaoPrevista | DATE |
| valorTotal | DECIMAL(10,2) |
| status | ENUM(...) |
| Veiculo_idVeiculo | INT |
| Equipe_idEquipe | INT |

### **Serviço**
| Campo | Tipo |
|-------|------|
| idServico | INT |
| descricao | VARCHAR(100) |
| valorMaoDeObra | DECIMAL(10,2) |

### **OS_Servico** (serviços executados)
| Campo | Tipo |
|-------|------|
| idOS | INT |
| idServico | INT |
| quantidade | INT |
| valorCalculado | DECIMAL(10,2) |

### **Peça**
| Campo | Tipo |
|-------|------|
| idPeca | INT |
| descricao | VARCHAR(100) |
| valorUnitario | DECIMAL(10,2) |

### **OS_Peca** (peças utilizadas)
| Campo | Tipo |
|-------|------|
| idOS | INT |
| idPeca | INT |
| quantidade | INT |
| valorCalculado | DECIMAL(10,2) |

### **Autorização**
| Campo | Tipo |
|-------|------|
| idAutorizacao | INT |
| idOS | INT |
| dataAutorizacao | DATETIME |
| autorizado | ENUM('SIM','NAO') |

---

## 🔗 Relacionamentos

- **Cliente 1:N Veículo**  
- **Veículo 1:N Ordem de Serviço**  
- **Equipe 1:N Ordem de Serviço**  
- **Equipe N:N Mecânico**  
- **OS N:N Serviço**  
- **OS N:N Peça**  
- **OS 1:1 Autorização**  

---

## 🧩 Regras de Negócio

- Cada OS é vinculada a um veículo e a uma equipe de mecânicos  
- A equipe identifica os serviços e peças necessários  
- O cliente autoriza a execução da OS  
- O valor total da OS é calculado com base nos serviços e peças utilizados  
- A OS possui status e datas de emissão/conclusão  

---

## 📘 Como Usar Este Modelo

Você pode:

- Implementar o banco em MySQL, PostgreSQL ou SQL Server  
- Criar o DER com base nas tabelas acima  
- Expandir o sistema para incluir agendamento, histórico de serviços, faturamento etc.  


