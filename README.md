# 🤖 PYTHON SEARCH APP - COLETOR DE E-MAILS E CONTATOS

Aplicação Python para coleta de e-mails e telefones de empresas usando Google/DuckDuckGo e Selenium com **Clean Architecture**.

## 📋 O que a Aplicação Faz

| Funcionalidade | Descrição |
|----------------|----------|
| **🔍 Escolha do motor** | Google Chrome ou DuckDuckGo (usuário escolhe) |
| **🎯 Busca inteligente** | Termos configuráveis por localização e segmento |
| **📧 Extração completa** | E-mails, telefones formatados e dados da empresa |
| **✅ Validação rigorosa** | Filtra e-mails/telefones inválidos automaticamente |
| **🚫 Controle de duplicatas** | Evita revisitar sites e e-mails já coletados |
| **📊 Planilha Excel** | Formato SITE \| EMAIL \| TELEFONE com `;` no final |
| **⚙️ Modo lote/completo** | Processamento configurável pelo usuário |
| **⏰ Horário inteligente** | Funciona apenas entre 8h-22h (configurável) |
| **🔄 Reinício opcional** | Continuar anterior ou começar do zero |

## 🏗️ Arquitetura - Clean Architecture

```
📁 PythonSearchApp/
├── 🔵 src/domain/                    # CAMADA DE DOMÍNIO
│   ├── models/                       # Entidades e modelos
│   │   ├── company_model.py          # Modelo de empresa
│   │   ├── search_term_model.py      # Modelo de termo de busca
│   │   ├── collection_result_model.py # Resultado da coleta
│   │   ├── collection_stats_model.py  # Estatísticas da coleta
│   │   ├── term_result_model.py      # Resultado por termo
│   │   ├── performance_metric_model.py # Métricas de performance
│   │   └── retry_config_model.py     # Configuração de retry
│   ├── factories/                    # Fábricas de domínio
│   │   └── search_term_factory.py    # Fábrica de termos
│   ├── protocols/                    # Interfaces e contratos
│   │   └── scraper_protocol.py       # Interface para scrapers
│   └── services/                     # Serviços de domínio
│       └── email_domain_service.py   # Regras de negócio e validações
├── 🟢 src/application/               # CAMADA DE APLICAÇÃO
│   └── services/                     # Serviços de aplicação
│       ├── email_application_service.py  # Orquestração principal
│       └── user_config_service.py    # Configuração do usuário
├── 🟡 src/infrastructure/            # CAMADA DE INFRAESTRUTURA
│   ├── config/                       # Gerenciamento de configuração
│   │   └── config_manager.py         # ConfigManager YAML/JSON
│   ├── drivers/                      # Gerenciamento de WebDriver
│   │   └── web_driver.py             # WebDriverManager com anti-detecção
│   ├── logging/                      # Sistema de logging
│   │   └── structured_logger.py      # Logger estruturado contextual
│   ├── metrics/                      # Métricas e performance
│   │   └── performance_tracker.py    # Rastreamento de performance
│   ├── network/                      # Rede e retry
│   │   └── retry_manager.py          # Gerenciador de retry com backoff
│   ├── repositories/                 # Persistência
│   │   └── data_repository.py        # JSON e Excel
│   ├── scrapers/                     # Web scraping
│   │   ├── duckduckgo_scraper.py     # Scraper DuckDuckGo
│   │   └── google_scraper.py         # Scraper Google
│   └── storage/                      # Gerenciamento de arquivos
│       └── data_storage.py           # Limpeza de dados
├── 📜 src/resources/                 # Recursos e configurações
│   └── application.yaml              # Configuração principal YAML
├── 📌 src/__version__.py               # Controle de versão dinâmico
├── ⚙️ config/
│   └── settings.py                   # Configurações legadas
├── 💾 data/                          # Dados de runtime (ignorado no Git)
│   ├── visited.json                  # Domínios visitados
│   └── emails.json                   # E-mails coletados
├── 📊 output/                        # Arquivos de saída (ignorado no Git)
│   └── empresas.xlsx                 # Planilha Excel
├── 🧪 tests/                         # Testes unitários (99% coverage)
│   ├── unit/                         # Testes por camada
│   ├── reports/                      # Relatórios de coverage
│   └── run_tests.bat                # Script de execução de testes
├── 📋 pyproject.toml                 # Gerenciamento de dependências
└── 🚀 main.py                        # Ponto de entrada
```

## 🚀 Como Executar

### Pré-requisitos
- Python 3.13.7+ (baixa automaticamente)
- Google Chrome instalado
- ChromeDriver (baixa automaticamente)

### Instalação e Execução

**Windows:**
```cmd
iniciar_coletor.bat
```
[![Executar no Windows](https://img.shields.io/badge/▶️-Executar%20no%20Windows-blue?style=for-the-badge)](iniciar_coletor.bat)

**Linux/macOS:**
```bash
./iniciar_coletor.sh
```
[![Executar no Linux/macOS](https://img.shields.io/badge/▶️-Executar%20no%20Linux/macOS-green?style=for-the-badge)](iniciar_coletor.sh)

### Fluxo Interativo
A aplicação perguntará:
1. **🔍 Motor de busca**: `1-DuckDuckGo` ou `2-Google Chrome`
2. **🔄 Reiniciar**: `s-do zero` ou `n-continuar anterior`
3. **📊 Modo**: `l-lote` ou `c-completo`

### Configurações
- **Modo teste**: Edite `IS_TEST_MODE = True` em `config/settings.py`
- **Horário**: Funciona entre 8h-22h (configurável)
- **ChromeDriver**: Download automático da versão compatível

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Descrição | Versão |
|------------|-----------|--------|
| **Python** | Linguagem de programação principal | 3.13.7+ |
| **Selenium** | Automação de navegadores web | ≥4.0.0 |
| **OpenPyXL** | Manipulação de arquivos Excel (.xlsx) | ≥3.0.0 |
| **TLDExtract** | Extração e processamento de domínios | ≥3.0.0 |
| **Requests** | Cliente HTTP para download de drivers | ≥2.25.0 |
| **PyYAML** | Parser e gerador de arquivos YAML | ≥6.0 |
| **Pytest** | Framework de testes unitários | ≥7.0.0 |
| **Pytest-Cov** | Plugin de coverage para pytest | ≥4.0.0 |
| **Coverage** | Medição de cobertura de código | ≥7.0.0 |
| **Google Chrome** | Navegador para automação web | Última versão |
| **ChromeDriver** | Driver para controle do Chrome | Auto-download |
| **Clean Architecture** | Padrão arquitetural | - |
| **SOLID Principles** | Princípios de design de software | - |
| **Type Hints** | Tipagem estática para Python | Built-in |
| **Dataclasses** | Classes de dados estruturadas | Built-in |



## ⚙️ Configurações

Edite `config/settings.py` para personalizar:
- **Horários**: `START_HOUR = 8`, `END_HOUR = 22`
- **Limites**: `MAX_EMAILS_PER_SITE = 5`
- **Modo**: `IS_TEST_MODE = True/False`
- **Blacklist**: Sites a serem ignorados
- **Termos**: Bases de busca e localizações

## 📊 Saída

A aplicação gera:
- **output/empresas.xlsx**: Planilha com `SITE | EMAIL | TELEFONE`
- **data/visited.json**: Controle de domínios já visitados
- **data/emails.json**: Controle de e-mails já coletados
- **Logs detalhados**: Progresso em tempo real

### Formato dos Dados
- **E-mails**: `email1@domain.com;email2@domain.com;`
- **Telefones**: `(11) 99999-8888;(11) 3333-4444;`
- **Validação**: Filtra e-mails/telefones inválidos automaticamente

## 🎯 Especificações Técnicas

### Modo Produção
- **Termos de busca**: 6 bases x (1 capital + 5 zonas + 30 bairros + 20 cidades) = 336 termos
- **Processamento**: Completo ou em lotes configuráveis

### Modo Teste
- **Termos de busca**: 2 termos apenas
- **Execução rápida**: Para desenvolvimento e validação

### Validações
- **E-mails**: Formato, domínios suspeitos, caracteres inválidos
- **Telefones**: DDD válido, formato brasileiro, números repetitivos
- **Máximo por site**: 5 e-mails e 3 telefones

### Controles
- **Horário**: Funciona apenas entre 8h-22h (configurável)
- **Deduplicação**: Por domínio e por e-mail
- **Simulação humana**: Scroll aleatório, pausas variáveis





## 📝 Logs

- `[INFO]`: Informações gerais e progresso
- `[OK]`: Operações bem-sucedidas
- `[ERRO]`: Falhas na execução
- `[VISITA]`: Acessando novo site
- `[PULAR]`: Site já visitado
- `[PAUSA]`: Fora do horário de funcionamento





## 📄 Licença

**Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)**

- ✅ **Compartilhamento livre**: Copie e redistribua em qualquer formato
- ✅ **Adaptação permitida**: Modifique, transforme e crie derivações
- ✅ **Atribuição obrigatória**: Dê crédito ao autor original
- ❌ **Uso comercial proibido**: Não pode ser usado para fins comerciais
- 🛡️ **Proteção contra patentes**: Publicado como arte anterior

Veja o arquivo [LICENSE](LICENSE) para detalhes completos.