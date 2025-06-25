# Simulador de Elevador Inteligente (Projeto C213)

Este projeto implementa um simulador de elevador inteligente, utilizando Python para a lógica de controle e simulação, Mosquitto como broker MQTT para comunicação, e Node-RED para a interface gráfica de usuário (Dashboard). O elevador simula o movimento, o cálculo de erro em relação a um andar alvo, e envia seu estado em tempo real para o Dashboard, que por sua vez permite o envio de comandos para o elevador.

## Funcionalidades

* **Simulação de Movimento:** Lógica de elevador em Python que simula física básica (posição, velocidade, potência do motor).
* **Controle de Andar Alvo:** Capacidade de definir um andar para o elevador se mover.
* **Indicação de Direção:** O dashboard visualiza se o elevador está subindo (seta azul) ou descendo (seta vermelha).
* **Comunicação MQTT:** Toda a troca de informações entre a simulação Python e o Dashboard Node-RED é feita via MQTT, permitindo comunicação assíncrona e escalável.
* **Dashboard Interativo:** Interface gráfica no Node-RED para visualizar o andar atual, posição, velocidade, erro, e interagir com o elevador através de botões de andar e de emergência.

## Tecnologias Utilizadas

* **Python:** Linguagem de programação para a lógica de simulação e controle do elevador.
    * `paho-mqtt`: Biblioteca Python para comunicação MQTT.
    * `math`: Para cálculos matemáticos.
    * `time`: Para controle do tempo na simulação.
* **Mosquitto MQTT Broker:** Servidor leve de mensagens MQTT.
* **Node-RED:** Ferramenta de programação visual para o Dashboard (interface web).
    * `node-red-dashboard`: Paleta essencial para criar a interface.

## Estrutura do Projeto

* `FuzzyEnzo.ipynb`: O principal arquivo Python (Jupyter Notebook) que contém a lógica da simulação do elevador e a comunicação MQTT.
* **(Opcional) seu_flow_node_red.json**: (Você pode exportar o seu flow do Node-RED para um arquivo .json e incluí-lo aqui para facilitar a importação).
* `.gitignore`: Arquivo para ignorar arquivos e diretórios que não devem ser versionados pelo Git.

## Como Configurar e Rodar

Siga os passos abaixo para configurar e rodar o simulador em sua máquina.

### Pré-requisitos

1.  **Python 3.x:** Baixe e instale do [python.org](https://www.python.org/downloads/).
2.  **pip:** Gerenciador de pacotes do Python (geralmente vem com a instalação do Python).
3.  **Mosquitto MQTT Broker:**
    * **Windows:** Baixe o instalador em [mosquitto.org/download/](https://mosquitto.org/download/). Instale-o e garanta que ele esteja rodando como um serviço ou inicie-o manualmente via prompt de comando (`mosquitto -v`).
    * **Linux/macOS:** Use seu gerenciador de pacotes (ex: `sudo apt-get install mosquitto` ou `brew install mosquitto`).
4.  **Node-RED:**
    * Instale o Node-RED globalmente via npm: `npm install -g --unsafe-perm node-red`
    * Instale a paleta Dashboard no Node-RED: Vá para a interface do Node-RED (geralmente `http://localhost:1880`), clique no menu (três linhas no canto superior direito) -> `Manage palette` -> `Install` e procure por `node-red-dashboard`.

### Passos de Configuração

1.  **Clone o Repositório:**
    ```bash
    git clone [URL_DO_SEU_REPOSITORIO]
    cd Projeto2-C213
    ```
2.  **Instale as Dependências do Python:**
    Navegue até a pasta onde está seu `FuzzyEnzo.ipynb` (ou o script Python) no terminal e instale as bibliotecas necessárias:
    ```bash
    pip install paho-mqtt jupyter
    ```
    (Se você estiver usando o Jupyter Notebook, `jupyter` é necessário. Caso contrário, apenas `paho-mqtt`.)

### Como Rodar o Projeto

1.  **Inicie o Mosquitto MQTT Broker:**
    Certifique-se de que o Mosquitto esteja rodando. Se você o instalou como um serviço, ele deve iniciar automaticamente. Caso contrário, abra um prompt de comando e execute:
    ```bash
    mosquitto -v
    ```
    Mantenha este prompt de comando aberto.

2.  **Inicie o Node-RED:**
    Abra um **novo** prompt de comando e execute:
    ```bash
    node-red
    ```
    Após iniciar, acesse a interface do Node-RED no seu navegador (geralmente `http://localhost:1880`).
    **Importe o Flow:** Se você exportou seu flow do Node-RED para um arquivo `.json`, importe-o agora: Menu (três linhas) -> `Import` -> `Clipboard` ou `Select file`.
    Clique em `Deploy` no Node-RED.
    Acesse o Dashboard do elevador, geralmente em `http://localhost:1880/ui`.

3.  **Inicie a Simulação Python:**
    Abra um **novo** prompt de comando (ou o Jupyter Notebook se preferir) e navegue até o diretório do seu arquivo `FuzzyEnzo.ipynb`.
    * **Via Jupyter Notebook:**
        ```bash
        jupyter notebook
        ```
        Seu navegador abrirá o Jupyter. Abra `FuzzyEnzo.ipynb` e execute todas as células em ordem.
    * **Se você exportou a lógica para um script `.py`:**
        ```bash
        python FuzzyEnzo.py
        ```
    Mantenha este prompt/Jupyter aberto enquanto deseja que a simulação esteja ativa.

## Interagindo com o Dashboard

* **Botões de Andar:** Clique nos botões numerados (1 a 8, 'T' para Térreo) para enviar o elevador para o andar desejado.
* **Visualização:** Observe a posição da cabine, o andar atual no display, o erro de posicionamento e a seta de direção (azul para subir, vermelha para descer, oculta com erro < 20cm).


## Solução de Problemas

* **"Cliente MQTT não está conectado!"**: Verifique se o Mosquitto broker está rodando e se não há firewalls bloqueando a porta 1883.
* **Elevador não se move ou não responde a comandos**:
    * Certifique-se de que a simulação Python (`FuzzyEnzo.ipynb` ou `.py`) está rodando.
    * Verifique os logs no prompt de comando do Python para ver se há erros ou avisos.
    * Confira se os tópicos MQTT estão corretos e se o Node-RED está enviando mensagens para `elevador/comando`.


---
