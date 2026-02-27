<h1 align="center">
🚗 IPD - Illegal Parking Detection System
</h1>

<p align="center">
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
<img src="https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi" alt="FastAPI" />
<img src="https://img.shields.io/badge/YOLOv11-FF1493?style=for-the-badge&logo=ultralytics&logoColor=white" alt="YOLOv11" />
<img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white" alt="Next.js" />
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
</p>

Sistema Full-Cycle e Autônomo de Fiscalização Urbana utilizando Visão Computacional e Inteligência Artificial.

<p align="center">
<img src="https://via.placeholder.com/800x400.png?text=Coloque+aqui+um+GIF+do+sistema+rodando" alt="Demonstração do Sistema" width="100%">
</p>

## 📋 Sobre o Projeto
O IPD (Illegal Parking Detection) é uma solução tecnológica end-to-end desenvolvida para mitigar os impactos da fiscalização ineficiente de trânsito em centros urbanos. O sistema analisa imagens de vias públicas, detecta veículos e classifica automaticamente infrações de estacionamento com base em regras geométricas de intersecção e posicionamento relacional.

Projeto desenvolvido como Trabalho de Conclusão de Curso (TCC) em Ciência da Computação (UNIP), focando na união entre Engenharia de Software robusta e o estado da arte em Deep Learning.

## ✨ Principais Funcionalidades
Detecção e Segmentação (SOTA): Utiliza o modelo YOLOv11-seg para mapear com precisão de pixel veículos, calçadas, faixas de pedestre e sinalizações.

Validação Lógica Proprietária: Algoritmos matemáticos em Python (NumPy/OpenCV) para traduzir o Código de Trânsito Brasileiro (CTB) em regras determinísticas (ex: cálculo de área de contato via IoU).

ALPR e Metadados: Integração com APIs externas para reconhecimento de placas e extração de metadados geográficos/temporais das imagens.

Notificação e Alertas: Envio automatizado de e-mails detalhando a infração registrada.

Dashboard e Histórico: Interface web interativa com controle de acesso, histórico de validações e geolocalização em mapa.

## 📸 Galeria do Sistema
<details>
<summary><b>Clique para ver as telas da aplicação</b></summary>

1. Dashboard Principal & Métricas
<img src="https://via.placeholder.com/800x400.png?text=Cole+aqui+a+print+da+Tela+Inicial+(5.4.1" alt="Dashboard" width="100%">

2. Processamento e Validação da IA
<img src="https://via.placeholder.com/800x400.png?text=Cole+aqui+a+print+da+Infração+Processada+(5.7.3" alt="Validação IA" width="100%">

3. Histórico e Modal de Detalhes
<img src="https://via.placeholder.com/800x400.png?text=Cole+aqui+a+print+do+Modal+da+Infração+(5.6" alt="Detalhes" width="100%">

4. Geolocalização (Mapa)
<img src="https://via.placeholder.com/800x400.png?text=Cole+aqui+a+print+do+Mapa+(5.8.1" alt="Geolocalização" width="100%">

</details>

## 🛠️ Arquitetura e Tecnologias
O projeto é um Monorepo dividido em duas camadas principais:

### 🖥️ Backend (IA & API REST)
- Framework: Python 3.13+ com FastAPI
- Visão Computacional: YOLOv11 (Ultralytics), OpenCV, NumPy
- Banco de Dados: MySQL (com SQLAlchemy ORM)
- Segurança: Autenticação via JWT (Python-JOSE) e Hash de senhas (Passlib)

### 🎨 Frontend (Interface de Usuário)
- Framework: Next.js 15.2 (App Router)
- Biblioteca UI: React com TypeScript
- Estilização: Tailwind CSS

## 🔐 Variáveis de Ambiente (.env)
Para que o sistema funcione corretamente (comunicação com banco, criptografia e APIs externas), é necessário configurar as variáveis de ambiente no Backend.

Na pasta backend, crie um arquivo chamado .env (você pode copiar a estrutura do arquivo .env.example já fornecido) e preencha com as suas credenciais:

  ```bash
  --- BANCO DE DADOS (MySQL) ---
  MYSQL_USER=root 
  MYSQL_PASSWORD=sua_senha_aqui 
  MYSQL_HOST=localhost 
  MYSQL_PORT=3306 
  MYSQL_DB=ipd 
  
  --- SEGURANÇA (Autenticação) ---
  JWT_SECRET=sua_chave_secreta_aqui_gerada_aleatoriamente
  
  --- IA GENERATIVA (Opcional/Metadados) ---
  GEMINI_KEY=sua_chave_da_api_do_google
  GEMINI_URL=https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent
  
  --- ALPR (Reconhecimento de Placas) ---
  PLATEREQ_URL=url_da_api_plate_recognizer
  PLATEREQ_NAME=seu_usuario
  PLATEREQ_PASSWORD=seu_token_ou_senha
  
  --- NOTIFICAÇÕES (E-mail SMTP) ---
  EMAIL=seu_email_de_envio@gmail.com
  SENHA_APP=sua_senha_de_aplicativo_do_gmail
  ```

---

## 🚀 Como Rodar o Projeto

Você pode rodar o sistema completo através do Docker (Recomendado) ou manualmente configurando os serviços.

### Opção 1: Via Docker Compose (Modo Automatizado)
*Pré-requisito: Ter o Docker e o Docker Compose instalados.*

1. Clone o repositório:
   ```bash
   git clone https://github.com/Ryuko46/Tcc-IllegalParkingDetection-FullStack.git
   cd Tcc-IllegalParkingDetection-FullStack
   ```
2. Configure os arquivos .env conforme a seção acima.

3. Suba todos os serviços com um único comando:

  ```bash
  docker-compose up --build
  ```
O Frontend estará em http://localhost:3000 e a API em http://localhost:8000.
  
### Opção 2: Rodando Manualmente (Modo Desenvolvimento)
*Pré-requisitos: Node.js (v22+), Python (3.13+) e MySQL Server instalados localmente.*

1. Configurar o Banco de Dados:

Crie um banco de dados vazio no seu MySQL chamado ipd.

Importe o arquivo /backend/database/ipd.sql para popular as tabelas iniciais.

2. Rodar o Backend (Terminal 1):

  ```bash
  cd backend
  pip install -r requirements.txt
  uvicorn app.main:app --reload
  ```
3. Rodar o Frontend (Terminal 2):

  ```bash
  cd frontend
  npm install
  npm run dev
  Acesse http://localhost:3000 no seu navegador.
  ```

### 📚 Documentação da API (Swagger)
Com o Backend rodando, você pode testar todas as rotas e requisições HTTP do sistema diretamente pela interface interativa gerada pelo FastAPI.

👉 Acesse: http://127.0.0.1:8000/docs

### 👥 Autores & Direitos Acadêmicos
Este sistema foi idealizado e desenvolvido como Trabalho de Conclusão de Curso (TCC) do bacharelado em Ciências da Computação pela Universidade Paulista (UNIP).

Desenvolvimento de Software, Modelagem e Documentação: João Victor Crisci, Hitalo Chaves, Bruno Pimentel, Guilherme Abbenante.

Orientação: Prof. Alvaro

Projeto desenvolvido para fins acadêmicos e de pesquisa em Mobilidade Urbana.
