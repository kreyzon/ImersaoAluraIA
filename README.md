# 🎉 Organizador de Festas com Agentes de IA 🎉

## Introdução 👋

Este projeto implementa um sistema de organização de festas utilizando agentes de inteligência artificial. O objetivo é simplificar o planejamento de eventos, desde a definição das necessidades do cliente até a apresentação de planos de orçamento detalhados. O sistema é composto por quatro agentes distintos, cada um com um papel específico no processo de organização.

## Instruções de Utilização 🚀

Para executar este código, você precisará seguir os seguintes passos:

1.  **Configurar a API Key do Google Gemini 🔑:**
    * Certifique-se de ter uma API Key válida para o Google Gemini.
    * Utilize o recurso `userdata.get('GOOGLE_API_KEY')` do Google Colab para armazenar e acessar sua chave de forma segura. O código assume que você já configurou essa chave no Colab.

2.  **Instalar a Framework de Agentes do Google 👇:**
    * Execute a seguinte célula no seu ambiente Python (preferencialmente no Google Colab) para instalar a biblioteca `google-adk`:
        ```python
        !pip install -q google-adk
        ```

3.  **Executar o Script ▶️:**
    * Execute todas as células do script `main.py` em ordem.
    * O script iniciará perguntando o tipo de evento que você deseja organizar:
        ```
        🚀 Iniciando o Sistema de Criação de MVP com 4 Agentes 🚀
        Olá, somos a Kreyzon Events, em que tipo de evento podemos ajudar?
        ```
    * Digite o tipo de evento desejado (por exemplo, "Casamento no Porto 💍", "Aniversário infantil em Lisboa 🎈", "Team building para 50 pessoas 🤝").
    * O sistema processará sua solicitação através dos diferentes agentes e exibirá os resultados de cada etapa.

4.  **Interagir com o Atendente 💬:**
    * Após a apresentação dos planos de evento, o sistema perguntará se você gostou de alguma opção ou tem alguma dúvida:
        ```
        Você gostou de alguma das opções ou tem alguma dúvida sobre o evento?
        ```
    * Você pode digitar suas perguntas ou comentários. O `agente_atendente` responderá e fará novas perguntas até que você digite `fim` para encerrar a conversa.

## Explicação dos Agentes 🤖

O sistema de organização de festas é composto por quatro agentes de IA, cada um especializado em uma etapa do processo:

1.  **`agente_cliente(tipo_evento)`: Stakeholder 🙋‍♀️/🙋‍♂️**
    * **Função:** Simula um cliente que deseja organizar um evento.
    * **Instruções:** Ao receber o tipo de evento desejado, este agente gera detalhes aleatórios sobre o evento, como uma data futura (em até um mês 🗓️), horário ⏰ e número de convidados 👥.
    * **Objetivo:** Criar uma demanda inicial com os requisitos básicos do evento.
    * **Exemplo de interação:** Se o tipo de evento for "Casamento no Porto 💍", o agente pode gerar uma saída como: "Problema principal: Casamento no Porto\n\nO evento será no dia 15 de junho de 2025, às 19h00, e terá aproximadamente 120 convidados."

2.  **`agente_aux_adm(tipo_evento, detalhes_evento)`: Auxiliar Administrativo 🕵️‍♀️/🕵️‍♂️**
    * **Função:** Atua como um auxiliar administrativo que recebe o pedido do cliente e pesquisa os elementos essenciais necessários para o evento.
    * **Instruções:** Utiliza a ferramenta de busca do Google (`google_search`) para identificar os itens cruciais para o tipo de evento especificado (por exemplo, local 🏢, catering 🍽️, decoração 💐 para um casamento). A saída é formatada como uma estrutura de dados Python seguindo um schema JSON predefinido.
    * **Objetivo:** Criar um plano inicial dos elementos essenciais necessários para o evento.
    * **Exemplo de saída (em formato de dicionário Python):**
        ```python
        {
            "Tipo de Evento": "Casamento no Porto",
            "Localização": "Porto, Portugal 🇵🇹",
            "Data": "15 de junho de 2025",
            "Horário": "19h00",
            "Número de Convidados": 120,
            "Elementos Essenciais": [
                {"Categoria": "Local/Espaço para Casamento", "Necessidades": ["salão grande", "open space", "mesas e cadeiras"]},
                {"Categoria": "Catering", "Necessidades": ["aperetivos 🥨", "bebidas alcoolicas 🍷", "bebidas não-alcoolicas 🍹", "bolo de casamento 🎂"]},
                {"Categoria": "Decoração", "Necessidades": ["flores 🌸"]},
                {"Categoria": "Entretenimento", "Necessidades": ["DJ 🎧"]}
            ]
        }
        ```

3.  **`agente_analista_budget(tipo_evento, categoria, elemento_essencial)`: Analista de Orçamentos 💰**
    * **Função:** Especializado em fornecer orçamentos para categorias específicas de elementos essenciais do evento (por exemplo, orçamento para locais 🏢, catering 🍽️, DJ 🎧).
    * **Instruções:** Utiliza a ferramenta de busca do Google (`google_search`) para encontrar pelo menos 5 opções de orçamento para a categoria e seleciona as 3 opções mais baratas. A saída é formatada como uma lista de dicionários Python seguindo um schema JSON predefinido.
    * **Objetivo:** Levantar opções de orçamento detalhadas para cada elemento essencial do evento.
    * **Exemplo de saída (para a categoria "Local/Espaço para Casamento"):**
        ```python
        [
            {"Opção": "Quinta dos Sonhos", "Preço": "2500€", "Características": ["Salão para 150 pessoas", "Jardim amplo 🌳", "Estacionamento 🅿️"]},
            {"Opção": "Espaço Vintage", "Preço": "2200€", "Características": ["Salão charmoso ✨", "Decoração inclusa", "Boa localização"]},
            {"Opção": "Celebrações Douro", "Preço": "2800€", "Características": ["Vista para o rio 🏞️", "Catering próprio", "Espaço ao ar livre"]}
        ]
        ```

4.  **`agente_organizador(tipo_evento, budgets)`: Organizador do Evento  Planner ✍️**
    * **Função:** Analisa os orçamentos recebidos dos diferentes analistas e monta 3 planos resumidos para apresentar ao cliente, destacando o valor principal de cada plano.
    * **Instruções:** Recebe o tipo de evento e uma lista de orçamentos (budgets) para os diversos elementos essenciais. Com base nessas informações, gera três propostas concisas para o cliente.
    * **Objetivo:** Sintetizar as informações de orçamento em planos de evento claros e resumidos.
    * **Exemplo de saída:** "Com base nos orçamentos levantados, apresento 3 planos para o seu casamento:\n\n**Plano 1 (Econômico 🟢):** Inclui o Espaço Vintage (2200€), um serviço de catering básico (1500€) e um DJ local (500€). Total estimado: 4200€.\n\n**Plano 2 (Intermediário 🟡):** Inclui a Quinta dos Sonhos (2500€), um serviço de catering com mais opções (2500€) e uma banda (1200€). Total estimado: 6200€.\n\n**Plano 3 (Premium 🔴):** Inclui o Celebrações Douro (2800€), um serviço de catering completo (3500€) e uma banda renomada (2000€). Total estimado: 8300€."

5.  **`agente_atendente(tipo_evento, evento, msg)`: Atendente de Eventos 🗣️**
    * **Função:** Interage com o cliente após a apresentação dos planos do evento, respondendo a dúvidas e buscando feedback até que o cliente esteja satisfeito.
    * **Instruções:** Recebe o tipo de evento, o plano do evento gerado e a mensagem do cliente. Fornece respostas e sempre faz uma nova pergunta para manter a interação até que o cliente confirme sua satisfação.
    * **Objetivo:** Garantir a comunicação com o cliente e refinar o plano do evento conforme necessário.
    * **Exemplo de interação:**
        * **Cliente:** "O plano econômico parece interessante, mas o catering é muito básico?"
        * **Atendente:** "Entendi 🤔. Para o plano econômico, podemos buscar opções de catering um pouco mais elaboradas dentro de uma faixa de preço similar. Isso te interessaria? Ou gostaria de ver mais detalhes sobre as opções de catering do plano intermediário?"

Este README fornece uma visão geral do projeto 💡, instruções para sua utilização ▶️ e uma explicação detalhada de cada um dos agentes de IA envolvidos no processo de organização de festas 🤖.
