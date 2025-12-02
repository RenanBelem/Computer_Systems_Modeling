## Projetos de Modelagem de Sistemas Computacionais

Este repositório abrange a modelagem de vários sistemas computacionais, para fins didáticos e de avaliação, utilizando diagramas UML de Máquina de Estados.

O principal artefato analisado é o **Laboratório 02 (LAB02)**, que detalha a dinâmica de três sistemas distintos.

---

## 📑 Sistemas Modelados (LAB02)

O Laboratório 02 (`LAB02.asta`, `LAB02_UML-ESTADOS-COMPONENTES-E-IMPLANTACAO.asta`, e imagens) utiliza diagramas de Máquina de Estados UML para ilustrar o ciclo de vida e o comportamento de diferentes componentes.

### 1. Sistema de Atendimento (Ex.: Caixa Eletrônico/ATM)
Este modelo descreve o ciclo de vida de um sistema de atendimento, como um caixa eletrônico, desde seu estado inicial até a conclusão de uma transação. 
* **Estado Inicial e Ciclo de Funcionamento:** O sistema começa no estado **Desligado**. A transição para **Ocioso** ocorre após ligar/começar e passar por um **Auto testando** com sucesso (semSucesso).
* **Estados de Manutenção:** A partir de **Ocioso**, uma falha (semSucesso) ou um evento de **serviço** pode levá-lo para **EmManutencao** ou **ForaDeServico**. Um evento de **serviço** em `EmManutencao` o move para `ForaDeServico` e, de lá, `semSucesso` o leva de volta ao estado inicial `Desligado`.
* **Submáquina de Atendimento (`AtendendoCliente`):** O estado `Ocioso` leva a uma sub-máquina quando um `cartaoInserido` é detectado. Esta sub-máquina modela o fluxo de uma transação:
    * **Entry/Exit Actions:** Ao entrar no estado `AtendendoCliente`, a ação é `ler cartão`; ao sair, é `devolver cartão`.
    * **Fluxo da Transação:** O cliente passa por **AutenticandoCliente**, **SelecionandoTransacao** e **ExecutandoTransacao**. O sistema retorna a `Ocioso` após a transação ou se for cancelada (`cancel`).

***

### 2. Sistema de Leilão (Com Lance e Autorização de Crédito)

Este modelo (diagrama de estado composto com *concurrent regions* - regiões concorrentes) descreve as ações e o fluxo de controle em um processo de leilão. 
O processo se inicia e bifurca (ação **fork**) em duas atividades que ocorrem em paralelo:

| Região Concorrente | Estados e Transições Principais |
| :--- | :--- |
| **Leiloando** (Oferta) | Inicia em **Recebendo lance**. O lance é **Avaliando lance**. Se for `[aceita]`, passa para **Aceitando lance**, gerando um *Trigger*. Se for `[rejeita, continua]`, volta a `Recebendo lance`. Se for `[rejeita, não querendo aumentar]`, o leilão é **Cancelado**. |
| **AutorizandoCredito** | Inicia em **Validando**. Se `[autorizado]`, move para **Ok**. Se `[não autorizado]`, o processo vai para o estado final **Rejeitado**. |

* **Finalização:** O *join* ocorre após **Aceitando lance** (região `Leiloando`) e **Ok** (região `AutorizandoCredito`), levando ao estado final **Comprado**.

***

### 3. Sistema de Atendimento de Chamadas (Ex.: Secretária Eletrônica)

Este modelo descreve o comportamento de um sistema de atendimento de chamadas telefônicas. 
* **Estados de Chamada:**
    * **Desligada:** Estado inicial de repouso.
    * **Tocando a campainha:** Entra neste estado por `chamada detectada`. Permanece nele (`campainha [n toques < 5]`) ou, se o número de toques atingir 5, o sistema pode **Avisando**.
    * **Conversando:** Entra neste estado se o `chamado atende`.
* **Ações de Secretária Eletrônica:** Se o sistema transiciona para **Gravando** ou **Avisando**, significa que a secretária eletrônica está ativa.
    * **Gravando:** Ação `do / gravar a mensagem de quem chamou`. Sai quando o `aviso termina`.
    * **Avisando:** Ação `do / apresentar aviso`.
* **Desligamento:** O evento `chamador desliga` retorna o sistema para o estado **Desligada** a partir de qualquer estado (exceto `Conversando` se o `chamado atende`).

---

## 🧩 Outros Componentes do Projeto

Os seguintes arquivos indicam que o projeto também inclui outros módulos ou avaliações, provavelmente usando o mesmo framework de modelagem e pertencentes a um ambiente de trabalho unificado (`EntityStore`):

* **Avaliações e Trabalhos:**
    * `Somativa01.asta`, `Somativa02.asta`
    * `Trabalho2.asta`
    * `ExMSC.asta`
* **Laboratórios Adicionais:**
    * `LAB01.asta`, `LAB03.asta`, `LAB04.asta`
* **Documentação/Modelos Auxiliares:**
    * `Biblioteca.asta`
    * `DiagramaAtv.asta`
