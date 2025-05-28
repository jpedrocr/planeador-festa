# Guia de Desenvolvimento Detalhado: Aplicação "Planeador de Festas Gastronómicas Colaborativo"

**1. Título do Projeto:**
Planeador de Festas Gastronómicas Colaborativo (Nome provisório, a definir)

**2. Visão Geral e Objetivos do Projeto:**

* **Descrição da Aplicação:** Uma aplicação web multiutilizador que permite aos utilizadores descobrir, selecionar, personalizar e organizar listas de pratos, petiscos e bebidas para festas e ocasiões especiais. A aplicação incluirá uma base de dados de sugestões (com receitas detalhadas e informações sobre onde comprar ingredientes ou pratos prontos), funcionalidades de partilha de eventos, atribuição de tarefas de compra/preparação, e interação com IA para sugestões personalizadas.
* **Público-Alvo:** Indivíduos que organizam eventos sociais (festas de aniversário, jantares com amigos, encontros familiares), que procuram inspiração para menus, facilidade no planeamento e na colaboração com outros participantes.
* **Problemas que Resolve / Valor que Oferece:**
    * Simplifica o planeamento de menus para eventos.
    * Facilita a colaboração e distribuição de tarefas entre participantes.
    * Oferece inspiração através de uma vasta lista de pratos e receitas.
    * Ajuda a encontrar fornecedores ou locais para comprar ingredientes/pratos.
    * Permite a personalização de acordo com as preferências e necessidades de cada evento.
* **Objetivos:**
    * **Curto Prazo (MVP):** Lançar uma versão funcional para um pequeno grupo de utilizadores (amigos), com registo, criação de eventos, seleção de pratos de uma lista base, personalização básica do evento e atribuição simples de tarefas.
    * **Médio Prazo:** Expandir a base de dados de pratos/receitas (com contribuições da comunidade e moderação), introduzir funcionalidades de IA para sugestões, melhorar as opções de partilha e permissões, e lançar a nível nacional.
    * **Longo Prazo:** Adicionar funcionalidades avançadas (avaliações, integrações), considerar modelos de monetização (funcionalidades premium), e ajustar para mercados internacionais.

**3. Arquitetura Geral da Aplicação:**

* **Estrutura:** Aplicação web com múltiplas páginas para melhor organização da complexidade crescente (ex: Página Inicial, Explorar Pratos/Receitas, Meus Eventos, Criar Novo Evento, Perfil do Utilizador, Administração de Conteúdo).
* **Frontend:** HTML, Tailwind CSS, JavaScript. A escolha de um framework JS (ex: Vue.js, React, Svelte) pode ser considerada se a complexidade da interface o justificar, priorizando tecnologias que facilitem o desenvolvimento e manutenção assistidos por IA.
* **Backend (BaaS):** **Firebase** será utilizado para:
    * Autenticação de utilizadores (Google, GitHub).
    * Base de Dados (Firestore) para armazenar: perfis de utilizador, lista base de pratos/categorias/receitas, dados de eventos criados pelos utilizadores (seleções, atribuições, convidados), sugestões da comunidade, informações de fornecedores.
    * Storage (Firebase Storage) para imagens e vídeos associados a receitas e pratos.
* **Fluxo de Dados:** O frontend comunicará com o Firebase para autenticação, leitura e escrita de dados. As atualizações de dados devem refletir-se em tempo real para os utilizadores que colaboram no mesmo evento, sempre que possível.

**4. Funcionalidades Detalhadas (Priorizadas - MVP e Fases Futuras):**

* **4.1. Gestão de Utilizadores:**
    * **MVP:**
        * Registo e Login utilizando fornecedores OAuth (Google, GitHub), minimizando a necessidade de armazenar dados pessoais sensíveis.
        * Perfil de Utilizador básico: Nome de exibição (do fornecedor OAuth), e-mail (para notificações/partilha).
    * **Fase Seguinte:**
        * No Perfil: Histórico de eventos criados, possibilidade de guardar pratos favoritos, e definir preferências alimentares gerais (ex: vegetariano, sem glúten) que podem ser usadas pela IA para sugestões.

* **4.2. Gestão de Conteúdo de Pratos/Petiscos/Receitas:**
    * **MVP:**
        * Uma lista base pré-preenchida de pratos e petiscos, organizada por categorias (as que já desenvolvemos podem ser o ponto de partida).
        * Interface de administração simples (inicialmente pode ser gestão manual no Firebase Console) para adicionar/editar/remover itens da lista base.
    * **Fase Seguinte:**
        * **Receitas Detalhadas:** Para cada prato na lista base, associar uma estrutura de receita detalhada:
            * Nome do prato, descrição, foto/vídeo principal.
            * Lista de ingredientes com quantidades.
            * Passos de preparação numerados e claros.
            * Tempo estimado de preparação e confeção.
            * Nível de dificuldade (ex: Fácil, Médio, Difícil).
            * Links para vídeos de demonstração (opcional).
            * Dicas adicionais.
        * **Informação sobre Fornecedores/Ingredientes:** Para cada prato ou ingrediente chave, permitir associar (inicialmente de forma manual pelo administrador):
            * Links diretos para compra online.
            * Nomes e moradas de lojas/restaurantes recomendados.
            * Contactos.
    * **Fase Avançada:**
        * **Sugestões da Comunidade:** Sistema para utilizadores sugerirem novos pratos, receitas ou fornecedores para a lista base, sujeitos a moderação por um administrador.
        * **Avaliações (Fornecedores/Receitas):** Permitir que utilizadores avaliem receitas e fornecedores (futuro).

* **4.3. Criação e Gestão de Eventos:**
    * **MVP:**
        * Funcionalidade para o utilizador criar um "Novo Evento" (ex: "Aniversário da Filipa").
        * Campos para o evento: Nome do evento, data, ocasião (ex: aniversário, jantar informal), número estimado de convidados.
        * Interface para o utilizador selecionar pratos e petiscos para o seu evento a partir da lista base de sugestões. A lista de pratos do evento será uma cópia personalizável.
        * Possibilidade de adicionar notas ou quantidades desejadas para cada prato selecionado no evento.
    * **Fase Seguinte:**
        * **Personalização Avançada da Lista do Evento:** Permitir que o utilizador adicione pratos que não existem na lista base (apenas para o seu evento) e crie/remova categorias dentro do seu evento específico.
        * Modelos de Eventos: Criar modelos pré-definidos para tipos comuns de festas (ex: "Festa de Crianças", "Jantar de Verão").

* **4.4. Funcionalidades de Partilha e Colaboração em Eventos:**
    * **MVP:**
        * Gerar um link único para cada evento, que pode ser partilhado para visualização da lista de pratos do evento.
        * Dentro de um evento, permitir ao criador atribuir itens da lista de compras a nomes de pessoas (entrada de texto livre para o nome da pessoa responsável). A lista de compras final será organizada por estes nomes.
    * **Fase Seguinte:**
        * Convidar outros utilizadores registados na plataforma para colaborar num evento através do seu e-mail.
        * **Níveis de Permissão para Colaboradores (definidos pelo criador do evento):**
            * Apenas Visualizar.
            * Marcar itens como "Eu levo/compro este".
            * Sugerir pratos adicionais para o evento (que o criador pode aprovar).
            * Editar a lista de pratos do evento (adicionar/remover itens).
        * **Interação com Convidados (mesmo não registados):**
            * Possibilidade de os convidados (via link) votarem nos pratos que gostam/não gostam para ajudar na seleção final (útil para restaurantes/take-away).
            * Confirmar presença (RSVP).
        * **Envio de Listas:** Funcionalidade para enviar a lista de compras atribuída a cada pessoa por e-mail (se o e-mail estiver registado).

* **4.5. Interação com Inteligência Artificial (IA):**
    * **Fase Seguinte/Avançada (após a base de dados de pratos/receitas estar mais robusta):**
        * **Sugestão de Menus:** IA sugere um conjunto de pratos da lista base com base em critérios definidos pelo utilizador para o evento (ex: tipo de ocasião, número de convidados, preferências alimentares do anfitrião, orçamento estimado, pratos favoritos do utilizador).
        * **Geração de Novas Sugestões:** Se o utilizador não encontrar o que procura, a IA pode tentar gerar novas ideias de pratos ou adaptações, com base nos seus conhecimentos gerais sobre culinária e nos ingredientes disponíveis.
        * **Assistência na Criação de Receitas:** IA pode ajudar a estruturar uma receita, sugerir variações, ou até gerar uma base de receita para um prato que o utilizador queira adicionar.
        * **Otimização de Listas de Compras:** IA pode ajudar a agrupar ingredientes de diferentes pratos para otimizar as compras.

**5. Design da Interface e Experiência do Utilizador (UI/UX):**

* **Princípios Gerais:** Interface limpa, intuitiva, moderna, amigável e totalmente responsiva (desktop, tablet, mobile).
* **Estrutura de Navegação (Múltiplas Páginas):**
    * Página Inicial (Dashboard com eventos recentes, atalhos).
    * Explorar Pratos/Receitas (com filtros por categoria, ingredientes, dificuldade, etc.).
    * Página de Detalhe de um Prato/Receita.
    * Meus Eventos (lista de eventos criados ou em que colabora).
    * Página de um Evento Específico (com a lista de pratos, gestão de convidados/colaboradores, atribuição de tarefas).
    * Criar/Editar Evento (formulário).
    * Perfil do Utilizador (configurações, preferências).
    * Administração (para gestão da lista base de pratos/receitas e moderação de conteúdo da comunidade - acesso restrito).
* **Layouts de Página Chave:** Priorizar a facilidade de leitura e interação. Usar cartões para pratos, listas claras, formulários bem estruturados.
* **Paleta de Cores:** Manter a base de "Neutros Quentes com Acentos Azuis Suaves", garantindo bom contraste e legibilidade.

**6. Tecnologias a Utilizar:**

* **Frontend:** HTML5, Tailwind CSS, JavaScript. Avaliar a necessidade de um framework JS leve (como Svelte ou Vue.js na sua versão mais simples) se a gestão de estado e componentes se tornar muito complexa com Vanilla JS para múltiplas páginas interligadas.
* **Backend (BaaS):** **Firebase** (Authentication, Firestore, Firebase Storage).
* **Inteligência Artificial:** Interação com APIs de modelos de linguagem (como Gemini ou Claude) para as funcionalidades de sugestão e geração de conteúdo, a serem implementadas em fases posteriores.
* **Outras:** Ferramentas de build e deployment (ex: Vite para o frontend, se aplicável; Firebase Hosting para o frontend).

**7. Considerações de Desenvolvimento e Manutenção com IA:**

* O código (frontend e backend, especialmente as Cloud Functions do Firebase, se usadas) deve ser bem estruturado, modular e comentado (internamente) para facilitar a análise e assistência por modelos de IA.
* A estrutura da base de dados no Firestore deve ser desenhada de forma lógica e bem documentada, para que a IA possa mais facilmente compreender as relações entre os dados e ajudar a construir queries ou a sugerir otimizações.
* Utilizar APIs bem definidas entre o frontend e o backend (mesmo que o backend seja Firebase, a forma como os dados são estruturados e acedidos conta).

**8. Plano de Implementação Faseado (MVP e Iterações Futuras):**

* **Fase 1 (MVP):**
    * Registo/Login de utilizadores (Google/GitHub via Firebase Auth).
    * Lista base de pratos/petiscos (a que já temos, inserida no Firestore) com categorias. Visualização destes pratos.
    * Criação de um "Evento" pelo utilizador (nome, data).
    * Possibilidade de o utilizador selecionar pratos da lista base para o seu evento.
    * Visualização da lista de pratos do evento.
    * Funcionalidade simples de "quem leva o quê" (atribuição por nome de texto livre dentro do evento).
    * Exportação/Importação básica dos dados da aplicação (lista de pratos, pessoas, seleções, atribuições).
* **Fase 2:**
    * Implementação de receitas detalhadas para os pratos da lista base.
    * Melhorar o perfil do utilizador (favoritos, preferências).
    * Partilha de eventos por link (visualização) e convite a outros utilizadores registados.
    * Níveis de permissão básicos para colaboradores do evento.
    * Envio de lista de compras por e-mail.
* **Fase 3:**
    * Sistema de sugestões da comunidade para pratos/receitas (com moderação).
    * Informação sobre fornecedores/locais de compra.
    * Primeiras funcionalidades de IA para sugestão de menus.
    * Funcionalidades de votação e RSVP em eventos.
* **Fases Seguintes:** Monetização (funcionalidades premium, como sugeriste), internacionalização, integrações com calendários, IA mais avançada para planeamento completo.

**9. Critérios de Sucesso:**

* **MVP:** Utilizadores conseguem registar-se, criar um evento, selecionar pratos e organizar minimamente quem trata do quê. A funcionalidade de exportar/importar permite guardar e restaurar o trabalho.
* **Médio Prazo:** Aumento do número de utilizadores, feedback positivo sobre a utilidade da plataforma, crescimento da base de dados de receitas e pratos, utilização das funcionalidades colaborativas.
* **Longo Prazo:** Tornar-se uma referência para planeamento de eventos gastronómicos, com uma comunidade ativa e, potencialmente, um modelo de negócio sustentável.

---
