# 🐾 PetCare

Protótipo web para **agendamento e acompanhamento de consultas veterinárias**, integrando tutores, clínicas e médicos veterinários em um único sistema.

Projeto Integrador do curso de **Engenharia de Software** da **UniEVANGÉLICA** (Anápolis/GO).

---

## 📌 Sobre o projeto

Hoje, grande parte do atendimento veterinário ainda depende de ligações telefônicas, conversas soltas em aplicativos de mensagem e cadernetas de vacina em papel. Isso gera atrasos, esquecimentos, faltas sem aviso e dificuldade para encontrar atendimento em emergências.

O **PetCare** busca resolver esse cenário com uma aplicação que permite ao tutor:

- descobrir clínicas e serviços veterinários;
- agendar e acompanhar consultas de forma prática;
- manter o histórico de atendimentos organizado;
- receber lembretes (vacinas, retornos e check-ups, no escopo planejado).

> ⚠️ **Estado atual:** o repositório contém um **MVP demonstrativo de front-end**. Não há back-end nem banco de dados implementados ainda; os dados ficam salvos no navegador (`localStorage`).

---

## ✨ Funcionalidades implementadas

- Introdução (onboarding) em 3 etapas, com opção de pular
- Telas de login, cadastro, confirmação e recuperação de senha
- Listagem e busca de clínicas pelo nome (5 clínicas fictícias)
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
- Todo conteúdo dinâmico é escapado antes de ser inserido no HTML.

### Limitações conhecidas (protótipo)

- O login não confere credenciais em nenhum serviço.
- A aba de pets no perfil ainda não tem cadastro implementado.
- As notificações não disparam alertas automáticos.
- Os dados somem se o usuário limpar os dados do site.

---

## 🛠️ Tecnologias

| Camada | Tecnologia |
|---|---|
| Estrutura | HTML5 |
| Estilo e responsividade | CSS3 |
| Lógica, rotas e estado | JavaScript nativo (SPA simples com rotas por `#`) |
| Persistência | `localStorage` (chave `petcare-demo-v1`) |
| Design e prototipagem | Figma |
| Versionamento | Git e GitHub |

### Stack planejada para as próximas fases

React.js + Vite (front-end), Node.js + Express (API REST) e PostgreSQL (banco de dados).

---

## 📁 Estrutura do repositório

```
PI_Petcare/
├── PetCare/
│   ├── assets/        # imagens: logo, avatar, onboarding, ícones de serviços
│   ├── css/
│   │   └── styles.css # estilos e responsividade
│   ├── js/
│   │   └── bundle.js  # lógica, rotas e telas
│   └── index.html     # ponto de entrada
└── README.md
```

---

## ▶️ Como executar

O projeto é um site estático e **não precisa de `npm install`**. Basta servir a pasta `PetCare` por um servidor HTTP.

**Opção 1: `serve` (Node.js)**
```bash
cd PetCare
npx serve
```
Acesse o endereço exibido no terminal (geralmente `http://localhost:3000`).

**Opção 2: Python**
```bash
cd PetCare
python3 -m http.server 8080
```
Acesse `http://localhost:8080`.

**Opção 3: extensão Live Server (VS Code)**
Clique com o botão direito em `PetCare/index.html` e escolha **Open with Live Server**.

> 💡 No **GitHub Codespaces**, abra a aba **Portas** e clique no ícone de globo ao lado da porta do servidor.

---

## 🧭 Rotas da aplicação

As rotas usam fragmento de URL (`#/rota`):

| Grupo | Rotas |
|---|---|
| Entrada e autenticação | `#/`, `#/onboarding/1` a `/3`, `#/start`, `#/login`, `#/register`, `#/confirm`, `#/forgot`, `#/recovery` |
| Navegação principal | `#/home`, `#/clinics`, `#/clinic/:id`, `#/booking/:id`, `#/schedule` |
| Conversas | `#/chats`, `#/chat/:id` |
| Conta e menu | `#/profile`, `#/edit-profile`, `#/menu`, `#/favorites`, `#/notifications`, `#/settings`, `#/payments`, `#/addresses`, `#/help`, `#/logout` |

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

1. **Apresentação:** interface e telas (HTML/CSS/JS).
2. **Aplicação:** regras de funcionamento e validações.
3. **Dados:** armazenamento e manipulação das informações.

```
Usuário → Interface (Frontend) → Lógica da Aplicação (Backend) → Banco de Dados
```

Na versão atual, as camadas de apresentação e aplicação estão no próprio front-end, e a persistência é feita no navegador.

---

## ♿ Acessibilidade

Viewport responsiva, texto alternativo em imagens relevantes, rótulos nos formulários, navegação principal com `aria-label`, `aria-current` na aba ativa, feedback por *toast* com `aria-live` e atalho para o conteúdo.

---

## 🗺️ Roadmap

- [x] Documentação de especificação
- [x] Protótipo no Figma
- [x] Definição da arquitetura e das tecnologias
- [x] MVP de front-end com fluxos de navegação
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
