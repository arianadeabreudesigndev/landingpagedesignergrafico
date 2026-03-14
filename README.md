# Landing Page Designer

> **short_description:** Site profissional para designer gráfico com agenda dinâmica, serviços, promoções e formulário de contato;
>
> **full_description:** Landing page desenvolvida para apresentar serviços de design gráfico, com seções de herói, agenda interativa (círculos de progresso alimentados por Supabase), promoção sazonal, cards de serviços com ícones autorais e formulário de contato otimizado para conversão. Design responsivo, animações suaves e código modular com Next.js, TypeScript e Tailwind CSS;
>
> **technologies:** React, Next.js, TypeScript, Tailwind CSS;

---

## 🚀 Características

- **Design autoral:** Ilustrações e ícones SVG exclusivos
- **Agenda interativa em tempo real:** Círculos de progresso com dados dinâmicos (vagas, análise, fila, finalizados) armazenados no **Supabase**
- **Atualização automática:** Cada novo formulário incrementa o contador "em análise"
- **Promoção destacada:** Forma geométrica personalizada e call-to-action para landing pages
- **Cards de serviços:** Ícones, título e modal com detalhes completos
- **Formulário integrado:** Envio para e-mail (Resend)
- **Animações suaves:** Framer Motion com efeitos de entrada e hover
- **Código limpo e modular:** Fácil manutenção e escalabilidade

---

## Sobre o Projeto

Site institucional de uma designer gráfica, desenvolvido para atrair clientes e facilitar o contato. O projeto prioriza experiência do usuário, conversão e performance, com um visual moderno e identidade visual própria. A **agenda é totalmente dinâmica**: os números são armazenados no Supabase e atualizados automaticamente quando um novo orçamento é solicitado.

---

## Tecnologias Utilizadas

- **Next.js 15** + React 19 + TypeScript
- **Tailwind CSS** para estilização rápida e responsiva
- **Framer Motion** para animações
- **React Hook Form** + **Zod** para validação de formulários
- **Resend API** para envio de e-mails
- **Supabase** como banco de dados e backend para a agenda dinâmica
- **Deploy na Vercel**

---

## Estrutura do Projeto

```text
src/
├── app/                         # Rotas e API (App Router)
│   ├── api/
│   │   └── send-email/          # Endpoint para envio do formulário (atualiza Supabase)
│   └── page.tsx                 # Página principal
│
├── components/                  # Componentes reutilizáveis
│   ├── ui/                      # Botão, Container, Section
│   ├── layout/                  # Navbar, Footer, MobileMenu
│   ├── sections/                # Hero, Agenda, Promo, Services, Contact
│   ├── services/                # ServiceCard, ServiceModal
│   └── agenda/                  # CircularProgress, AgendaStats
│
├── lib/                         # Funções utilitárias, validações e cliente Supabase
├── types/                       # Definições TypeScript
└── public/
    └── images/                  # Ícones e ilustrações SVG

```
---

## Funcionalidades Principais
Hero: Título em destaque (rosa #FAC2C2) com ilustração autoral e CTA animado

Agenda dinâmica: Círculos de progresso com números formatados (01, 02...) e link direto para o formulário

Promoção: Oferta de 26% off em landing pages com forma geométrica irregular no fundo

Serviços: Cards com ícones, título e descrição; modal com itens inclusos

Contato: Formulário validado que envia e-mail e incrementa automaticamente o contador "em análise" no Supabase

Footer: Etapas do processo (Briefing, Criação, Entrega) e informações sobre contrato de segurança

---

## Como Executar Localmente

### Pré-requisitos
- Node.js 18+
- npm ou yarn
- Conta no Resend (para e-mails)
- Conta no Supabase (para a agenda)

## Passos
1. Clone o repositório

git clone https://github.com/arianadeabreudesigndev/LandingPageDesignerGr-fico.git
cd LandingPageDesignerGr-fico

2. Instale as dependências

npm install

3. Configure as variáveis de ambiente
Crie um arquivo .env.local na raiz e preencha:

# Resend (e-mails)
RESEND_API_KEY=seu_token_resend

# Supabase (agenda dinâmica)
NEXT_PUBLIC_SUPABASE_URL=sua_url_do_projeto
NEXT_PUBLIC_SUPABASE_ANON_KEY=sua_chave_anon

4. Configure o banco de dados no Supabase

- Crie uma tabela agenda com os campos: id, vagas, em_analise, fila, finalizados, mes, created_at

- Insira um registro para o mês atual (ex: 2026-02)

- Crie a função SQL increment_em_analise conforme detalhado na documentação do projeto (ou veja o código ao final deste README)

5. Inicie o servidor de desenvolvimento

npm run dev

6. Acesse http://localhost:3000

---

## Scripts Disponíveis
npm run dev – Modo desenvolvimento

npm run build – Build de produção

npm run start – Servidor de produção

npm run lint – Verificação de lint

---

## Deploy na Vercel
O projeto está otimizado para deploy na Vercel. Conecte seu repositório e defina as mesmas variáveis de ambiente (RESEND_API_KEY, NEXT_PUBLIC_SUPABASE_URL, NEXT_PUBLIC_SUPABASE_ANON_KEY) no painel da Vercel.

---

## SQL para o Supabase
Execute este código no SQL Editor do seu projeto Supabase para criar a tabela e a função de incremento:

```text
-- Criação da tabela agenda
CREATE TABLE agenda (
  id SERIAL PRIMARY KEY,
  vagas INTEGER NOT NULL,
  em_analise INTEGER NOT NULL,
  fila INTEGER NOT NULL,
  finalizados INTEGER NOT NULL,
  mes TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);



-- Registro inicial para fevereiro de 2026 (ajuste o mês conforme necessário)
INSERT INTO agenda (vagas, em_analise, fila, finalizados, mes)
VALUES (5, 0, 0, 0, '2026-02');

-- Função para incrementar o contador 'em_analise'
CREATE OR REPLACE FUNCTION increment_em_analise(target_month TEXT)
RETURNS void AS $$
BEGIN
  UPDATE agenda SET em_analise = em_analise + 1 WHERE mes = target_month;
END;
$$ LANGUAGE plpgsql;

```

---

## Licença
Copyright © 2026 Ariana de Abreu. Todos os direitos reservados.
Este projeto é público para visualização como parte do portfólio profissional. Não é permitido uso comercial sem autorização.

## Contato
LinkedIn: linkedin.com/in/arianadeabreudev

Portfólio: portfolioariandeabreudesigndev.netlify.app

E-mail: arianadeabreudesigndev@gmail.com

⭐ Se este projeto foi útil para você, considere dar uma estrela!
