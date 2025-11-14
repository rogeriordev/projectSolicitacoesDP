# 📋 Sistema de Gestão de Solicitações de RH

Sistema web completo para gerenciamento de solicitações de Recursos Humanos, desenvolvido com CodeIgniter 4, permitindo o controle eficiente de diversos tipos de requisições corporativas.

## 📸 Preview

![Menu de Solicitações](docs/menu-solicitacoes.png)

## 🎯 Sobre o Projeto

O **Sistema de Gestão de Solicitações de RH** é uma aplicação web robusta desenvolvida para automatizar e centralizar o processo de requisições e solicitações relacionadas ao departamento de Recursos Humanos de empresas. O sistema oferece um fluxo completo desde a criação da solicitação até sua aprovação/reprovação, com controle de permissões baseado em perfis e hierarquias organizacionais.

## ✨ Funcionalidades Principais

### 📝 Tipos de Solicitações

O sistema suporta os seguintes tipos de solicitações:

1. **Dispensa** - Solicitação de desligamento de colaboradores
   - Tipo de aviso (com ou sem aviso prévio)
   - Futura indicação
   - Motivo e justificativa detalhados

2. **Advertência** - Registro de advertências a colaboradores
   - Verificação se já foi advertido anteriormente
   - Forma de advertência (verbal, escrita)
   - Motivo e justificativa

3. **Férias** - Gestão de períodos de férias
   - Férias fracionadas (até 4 períodos)
   - Abono pecuniário
   - Controle de datas múltiplas

4. **Consulta de Fichas e Exames** - Requisição de informações cadastrais
   - Dados pessoais completos
   - Documentação
   - Histórico profissional
   - Informações de saúde e restrições

5. **Divulgação de Vaga** - Publicação de vagas disponíveis
   - Detalhes da posição
   - Requisitos
   - Informações do setor

6. **Carta de Comparecimento** - Emissão de documentos de comparecimento
   - Datas e horários
   - Finalidade
   - Dados do colaborador

7. **Mudança de Função** - Alteração de cargo/função do colaborador
   - Função atual vs. função proposta
   - Salário atual vs. salário proposto
   - Data de admissão e data de alteração
   - Tipo de alteração
   - Observações do departamento

### 👥 Perfis de Usuário

O sistema implementa três níveis de acesso:

#### 1. **Administrador**
- Acesso total ao sistema
- Gerenciamento de usuários
- Visualização de todas as solicitações
- Acesso a dashboard com estatísticas completas
- Configurações gerais do sistema

#### 2. **Operador (RH/Departamento Pessoal)**
- Visualização de solicitações específicas por tipo
- Aprovação/reprovação de solicitações
- Acesso a solicitações deferidas ou em andamento
- Comentários e feedback nas solicitações
- Controle de status

#### 3. **Solicitante**
Subdividido em três categorias:

- **Administrativo**: Visualiza apenas suas próprias solicitações
- **Gestão (Setores Comuns)**: Visualiza suas solicitações + solicitações de seu setor
- **Gestão (Departamento Técnico)**: Visualiza suas solicitações + solicitações de seu setor + consultas de fichas de fazendas

### 📊 Dashboard e Estatísticas

- **Gráficos Interativos**: Visualização de dados por tipo de solicitação, status e unidade
- **Indicadores**: 
  - Total de solicitações
  - Solicitações deferidas
  - Solicitações indeferidas
  - Solicitações em aberto
- **Filtros Avançados**: Por data, status, tipo, unidade e colaborador
- **Exportação de Dados**: Relatórios em formatos diversos

### 🔐 Sistema de Autenticação

- Login seguro com criptografia
- Recuperação de senha via e-mail
- Código de verificação
- Primeiro acesso com definição de senha
- Alteração de senha pelo usuário
- Sessões seguras

### 🔄 Fluxo de Aprovação

```
Solicitante → Cria Solicitação → Em Aberto
                    ↓
           Gestor/RH Analisa
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
    Deferido              Indeferido
        ↓                       ↓
  Em Andamento            Arquivado
        ↓
   Finalizado
```

### 📝 Recursos Adicionais

- **Soft Delete**: Solicitações podem ser recuperadas após exclusão
- **Histórico de Modificações**: Rastreamento de alterações
- **Comentários**: Sistema de comunicação entre solicitante e aprovador
- **Upload de Arquivos**: Anexação de documentos às solicitações
- **Notificações**: Alertas sobre mudanças de status
- **Busca Avançada**: Filtros múltiplos para localização rápida

## 🛠️ Tecnologias Utilizadas

### Backend
- **PHP 8.x**
- **CodeIgniter 4** - Framework MVC
- **MySQL/MariaDB** - Banco de dados relacional

### Frontend
- **HTML5 / CSS3**
- **JavaScript (ES6+)**
- **Bootstrap 5** - Framework CSS responsivo
- **Chart.js** - Gráficos e visualizações
- **jQuery** - Manipulação DOM e AJAX

### Arquitetura
- **MVC (Model-View-Controller)**
- **RESTful principles**
- **Responsive Design**
- **Session Management**
- **Database Abstraction Layer**

## 📋 Pré-requisitos

- PHP >= 8.0
- Composer
- MySQL >= 5.7 ou MariaDB >= 10.3
- Apache/Nginx
- Extensões PHP:
  - intl
  - mbstring
  - json
  - mysqlnd
  - xml

## 📊 Estrutura do Banco de Dados

### Tabelas Principais

#### `solicitacoes`
```sql
- id (PK)
- tipo_solic
- status_solic (Em Aberto, Deferido, Indeferido, Em Andamento, Finalizado)
- data_solic
- solicitante
- unidade
- empresa
- setor
- gestor_und
- colaborador
- funcao_cargo
- motivo_justif
- comentario_dp
- situacao_dp
- id_user (FK)
- created_at
- updated_at
- deleted_at
```

#### `usuarios`
```sql
- id (PK)
- nome
- email
- password
- profile (Admin, Operador, Solicitante)
- cargo (Administrativo, Gestão)
- empresa
- setor
- unidade
- active
- created_at
- updated_at
- deleted_at
```

## 📁 Estrutura de Arquivos

```
/
├── app/
│   ├── Controllers/
│   │   ├── BaseController.php
│   │   ├── Main.php          # Controller principal e autenticação
│   │   ├── User.php          # Gerenciamento de solicitações
│   │   └── Admin.php         # Administração do sistema
│   ├── Models/
│   │   ├── SolicitacoesModel.php
│   │   └── UsuariosModel.php
│   ├── Views/
│   │   ├── solicitations_geral.php
│   │   ├── solicitation_advertencia_insert_frm.php
│   │   ├── solicitation_dispensa_edit_frm.php
│   │   ├── solicitation_divulgacao_insert_frm.php
│   │   └── etc.php
│   └── Helpers/
│       └── app_helper.php
├── public/
│   ├── assets/
│   ├── css/
│   └── js/
└── writable/
    └── uploads/
```

## 🔒 Segurança

- ✅ Proteção contra SQL Injection (prepared statements)
- ✅ Proteção CSRF (Cross-Site Request Forgery)
- ✅ Hash de senhas com bcrypt
- ✅ Validação de dados no backend
- ✅ Sanitização de inputs
- ✅ Controle de sessões seguro
- ✅ Proteção XSS (Cross-Site Scripting)
- ✅ Controle de acesso baseado em roles

## 📱 Responsividade

O sistema é totalmente responsivo e funciona perfeitamente em:
- 💻 Desktops
- 📱 Tablets
- 📱 Smartphones

## 📝 Roadmap

- [ ] Implementar notificações por e-mail automáticas
- [ ] Adicionar sistema de workflow customizável
- [ ] Integração com sistemas de ponto eletrônico
- [ ] App mobile nativo (iOS/Android)
- [ ] API REST completa para integrações
- [ ] Relatórios avançados em PDF
- [ ] Dashboard analítico com BI
- [ ] Integração com Active Directory/LDAP
- [ ] Sistema de aprovação em múltiplos níveis
- [ ] Assinatura digital de documentos

---

**Desenvolvido com ❤️ para facilitar a gestão de RH**
