# 🐾 PetCare

Aplicação web para **agendamento e acompanhamento de consultas veterinárias**, integrando tutores, clínicas e médicos veterinários em um único sistema.

Projeto Integrador do curso de **Engenharia de Software** da **UniEVANGÉLICA** (Anápolis/GO).

---

## 📌 Sobre o projeto

Hoje, grande parte do atendimento veterinário ainda depende de ligações telefônicas, conversas soltas em aplicativos de mensagem e cadernetas de vacina em papel. Isso gera atrasos, esquecimentos, faltas sem aviso e dificuldade para encontrar atendimento em emergências.

O **PetCare** busca resolver esse cenário com uma aplicação que permite ao tutor:

- descobrir clínicas e serviços veterinários;
- agendar e acompanhar consultas de forma prática;
- manter o histórico de atendimentos organizado;
- receber lembretes (vacinas, retornos e check-ups, no escopo planejado).

> ⚠️ **Estado atual:** o repositório contém um **MVP de front-end em React.js**. Ainda não há back-end nem banco de dados; os dados ficam salvos no navegador (`localStorage`).

---

## ✨ Funcionalidades

- Introdução (onboarding) em 3 etapas, com opção de pular
- Telas de login, cadastro, confirmação e recuperação de senha
- Listagem e busca de clínicas pelo nome
- Seleção de serviços por clínica (Consulta, Retorno, Exame, Procedimento clínico)
- Agendamento com clínica, serviço, pet, data e hora
- Agenda com calendário mensal, filtro por dia e remoção de agendamentos
- Clínicas favoritas (adicionar/remover)
- Conversas demonstrativas separadas por clínica
- Perfil com edição de nome
- Notificações locais derivadas dos agendamentos

### Regras de negócio e validações

- Agendamentos exigem nome do pet, serviço, data e hora; a data/hora deve ser **futura**.
- Não é permitido **duplicar horário** na mesma clínica, na mesma data e hora.
- Cadastro exige nome e senhas coincidentes (mínimo de 6 caracteres); a senha **não é armazenada**.
- Limites: mensagens com até 1.000 caracteres, nomes de pets com até 80 e nomes de usuário com até 100.
- O React escapa o conteúdo dinâmico por padrão, evitando injeção de HTML.

### Limitações conhecidas (MVP)

- O login não confere credenciais em nenhum serviço.
- A aba de pets no perfil ainda não tem cadastro implementado.
- As notificações não disparam alertas automáticos.
- Os dados somem se o usuário limpar os dados do site.

---

## 🛠️ Tecnologias

| Camada | Tecnologia |
|---|---|
| Interface | **React.js** (componentes e hooks) |
| Build e servidor de desenvolvimento | **Vite** |
| Rotas | React Router |
| Estilo e responsividade | CSS3 (Flexbox e Grid) |
| Persistência (MVP) | `localStorage` (chave `petcare-demo-v1`) |
| Design e prototipagem | Figma |
| Ambiente de execução | Node.js |
| Versionamento | Git e GitHub |

### Stack planejada para as próximas fases

Node.js + Express (API REST) e PostgreSQL (banco de dados relacional).

---

## 📁 Estrutura do repositório

```
PI_Petcare/
├── public/                # arquivos estáticos
├── src/
│   ├── assets/            # imagens: logo, avatar, onboarding, ícones
│   ├── components/        # componentes reutilizáveis (cards, menu, calendário)
│   ├── pages/             # telas (Login, Home, Clínicas, Agenda, Perfil...)
│   ├── hooks/             # hooks customizados (ex.: useLocalStorage)
│   ├── data/              # clínicas e serviços de demonstração
│   ├── services/          # acesso a dados (hoje localStorage; futuramente API)
│   ├── styles/            # estilos globais
│   ├── App.jsx            # rotas e estrutura principal
│   └── main.jsx           # ponto de entrada
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

> A pasta `services/` isola o acesso aos dados. Quando o back-end existir, só ela precisará mudar.

---

## ▶️ Como executar

**Pré-requisito:** Node.js 18 ou superior.

```bash
# 1. Clonar o repositório
git clone https://github.com/luidi09/PI_Petcare.git
cd PI_Petcare

# 2. Instalar as dependências
npm install

# 3. Iniciar o servidor de desenvolvimento
npm run dev
```

Acesse o endereço exibido no terminal (geralmente `http://localhost:5173`).

### Outros comandos

| Comando | O que faz |
|---|---|
| `npm run dev` | Inicia o servidor de desenvolvimento com recarregamento automático |
| `npm run build` | Gera a versão de produção na pasta `dist/` |
| `npm run preview` | Serve localmente a versão gerada pelo build |

> 💡 No **GitHub Codespaces**, abra a aba **Portas** e clique no ícone de globo ao lado da porta 5173.

---

## 🧭 Rotas da aplicação

| Grupo | Rotas |
|---|---|
| Entrada e autenticação | `/`, `/onboarding/:etapa`, `/start`, `/login`, `/register`, `/confirm`, `/forgot`, `/recovery` |
| Navegação principal | `/home`, `/clinics`, `/clinic/:id`, `/booking/:id`, `/schedule` |
| Conversas | `/chats`, `/chat/:id` |
| Conta e menu | `/profile`, `/edit-profile`, `/menu`, `/favorites`, `/notifications`, `/settings`, `/payments`, `/addresses`, `/help`, `/logout` |

---

## 🗃️ Modelo de dados local

Salvo em `localStorage` sob a chave `petcare-demo-v1`:

```json
{
  "profile": { "name": "..." },
  "appointments": [{ "id": "", "clinic": "", "service": "", "pet": "", "date": "", "time": "" }],
  "messages": { "<idDaClinica>": [{ "sender": "", "text": "" }] },
  "favorites": ["<idDaClinica>"]
}
```

---

## 🏗️ Arquitetura

O sistema foi projetado em **camadas**:

1. **Apresentação:** interface em React (componentes e páginas).
2. **Aplicação:** regras de funcionamento e validações (hooks e serviços).
3. **Dados:** armazenamento e manipulação das informações.

```
Usuário → Interface (React) → Lógica da Aplicação (Backend) → Banco de Dados
```

Na versão atual, as camadas de apresentação e aplicação estão no front-end, e a persistência é feita no navegador. A SPA (Single Page Application) permite navegar entre telas sem recarregar a página.

---

## ♿ Acessibilidade

Viewport responsiva, texto alternativo em imagens relevantes, rótulos nos formulários, navegação principal com `aria-label`, `aria-current` na aba ativa, feedback por *toast* com `aria-live` e atalho para o conteúdo.

---

## 🗺️ Roadmap

- [x] Documentação de especificação
- [x] Protótipo no Figma
- [x] Definição da arquitetura e das tecnologias
- [x] MVP de front-end em React com fluxos de navegação
- [ ] Back-end com API REST (Node.js + Express)
- [ ] Banco de dados PostgreSQL
- [ ] Autenticação real e perfis de acesso (tutor, clínica, veterinário)
- [ ] Cadastro e gerenciamento de pets
- [ ] Histórico de atendimentos e prontuário digital
- [ ] Notificações automáticas de vacinas e check-ups
- [ ] Canal de atendimento de emergência
- [ ] Testes e segurança da informação

---

## 👥 Equipe

| Matrícula | Nome |
|---|---|
| 2320132 | Augusto Cesar Nunes Oliveira |
| 2420166 | Emanuel Antônio Lima Rocha |
| 2420476 | Luis Antônio Alves dos Santos |
| 2420045 | Victor Moreira Veloso |

**Orientadores:** Jeferson Silva Araujo (principal) e Wosney Ramos De Souza (secundário).

---

## 📄 Documentação

A especificação completa do projeto (requisitos, regras de negócio, pesquisa com usuários, arquitetura e demais seções) está no **Documento de Especificação de Projeto Integrador**.
