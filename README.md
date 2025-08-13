# Safecracker Pro 🔐

Projeto final da disciplina **Sistemas Digitais** do **Centro de Informática (CIn) - UFPE**.

O **Safecracker Pro** é um sistema digital de cofre eletrônico implementado em **SystemVerilog** para FPGA, com programação e verificação de senha, bloqueio temporário após tentativas incorretas e interface via botões, switches e LEDs.

## 🎯 Funcionalidades

- **Modo Programação**: Definição de uma nova senha de 3 dígitos (cada dígito representado por 4 bits).
- **Modo Abertura**: Inserção da senha para destravar o cofre.
- **Bloqueio de Segurança**: Bloqueio temporário após 3 tentativas incorretas.
- **Indicação por LEDs**:
  - **LEDs verdes** → Cofre destravado.
  - **LEDs vermelhos** → Tentativa incorreta ou bloqueio ativo.
- **Senha inicial de teste**: `7, 13, 13` (em decimal).

## ⚙️ Especificações Técnicas

- **Plataforma**: FPGA (ex.: Altera/Intel DE1-SoC)
- **Clock**: 50 MHz
- **Linguagem**: SystemVerilog
- **Codificação de Estados**: One-hot
- **Entradas**:
  - `btn[3:0]` → Botões (KEY3..KEY0)
  - `sw[0]` → Switch para entrar no modo de programação
- **Saídas**:
  - `unlocked` → 1 quando o cofre está destravado
  - `LEDG[8:0]` → LEDs verdes
  - `LEDR[17:0]` → LEDs vermelhos

## 🔌 Mapeamento de Controles

| Componente     | Função |
|----------------|--------|
| **SW0**        | Ativa modo de programação |
| **KEY3..KEY0** | Digitação de dígitos (4 bits) |
| **LEDG**       | Indicam desbloqueio |
| **LEDR**       | Indicam erro ou bloqueio |

## ⏳ Lógica de Bloqueio

Após **3 tentativas incorretas**, o sistema entra em estado de bloqueio por **10 segundos**, indicado por todos os LEDs vermelhos acesos.

## 📂 Estrutura do Código

- **Máquina de Estados** (`state_t`):
  - `S_IDLE` → Estado inicial/espera
  - `S_PROGRAM` → Programação da senha
  - `S_WAIT_BTN` → Aguardando entrada do usuário
  - `S_CHECK` → Verificação da senha
  - `S_UNLOCKED` → Cofre destravado
  - `S_LOCKED` → Bloqueio temporário
- **Sincronização de Entradas**: Flip-flops duplos para evitar bouncing.
- **Detecção de Bordas**: Borda de descida para botões ativos-baixos.
- **Armazenamento de Senha**: Vetor de 12 bits (3×4 bits).

## 🚀 Como Rodar

1. Abra o projeto no **Intel Quartus Prime**.
2. Configure o dispositivo alvo (por exemplo, Cyclone V - DE1-SoC).
3. Compile (`Ctrl+L`) o projeto.
4. Carregue no FPGA.
5. Siga a lógica de programação e teste da senha usando os botões e switches.

## 👥 Autores

Projeto desenvolvido por Lucas Mendonça, Guilherme Valença, Daniel Acioly e Gustavo Leão como trabalho final da disciplina de Sistemas Digitais.

---
