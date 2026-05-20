# Plano de Implementação — Fase 7: A Consolidação de um Sistema
> **FarmTech Solutions** | FIAP — IA para Devs  
> Implementação linear por agente IA com supervisão humana

---

## 1. Visão Geral e Contexto das Fases Anteriores

### O que foi entregue (fonte: `.context/`)

| Fase | Tema | Entregável existente | Stack | Status |
|------|------|---------------------|-------|--------|
| 1 | Base de Dados Inicial | `farmTech_app.py` (CRUD Café/Cana), `analise_estatistica3.R`, `meteo.R`, CSVs | Python, R | ✅ |
| 2 | Banco de Dados Estruturado | Sistema BRIX para Cana (`main.py`, `analytics.py`, `database_oracle.py`, `file_manager.py`, `utils.py`) | Python + Oracle | ✅ |
| 3 | IoT e Automação Inteligente | `HugoSilva_RM566891_fase3_cap2.ipynb`, `produtos_agricolas.csv` (sensores ESP32 simulados) | Python/Jupyter, Wokwi | ✅ |
| 4 | Dashboard Interativo | `streamlit_app.py`, `train_model.py`, `ingest_db.py`, `recommend.py` + modelo `.joblib` | Streamlit, Scikit-learn, SQLite | ✅ |
| 5 | Cloud Computing & Segurança | `HugoRodrigues_rm566891_pbl_fase4.ipynb` (crop_yield ML + clusterização), análise custos AWS | Python/Jupyter, AWS | ✅ |
| 6 | Visão Computacional | `HugoRodrigues_rm566891_pbl_fase6.ipynb` (YOLOv5 customizado + CNN), imagens Shih Tzu / Nissan Kicks | PyTorch, TensorFlow/Keras, YOLO | ✅ |

### O que a Fase 7 exige adicionalmente
1. **Dashboard unificado** (extensão da Fase 4) que integre serviços das Fases 1, 2, 3 e 6 via botões/abas.
2. **Serviço de alertas AWS** (SNS + e-mail/SMS) monitorando dados dos sensores (Fase 1 ou 3) ou da visão computacional (Fase 6).
3. **Projeto em pasta única** no VS Code com todos os programas organizados.
4. **README completo** com prints, links do YouTube e documentação de todas as fases.
5. **Vídeo de até 10 min** no YouTube (não listado).

---

## 2. Arquitetura do Sistema Consolidado

```
farmtech_fase7/
├── README.md                        # Documentação principal
├── requirements.txt                 # Todas as dependências Python
├── .env.example                     # Template de variáveis de ambiente
├── run_dashboard.sh                 # Script para iniciar o dashboard
│
├── fase1/                           # Base de Dados & Insumos
│   ├── __init__.py
│   ├── crop_manager.py              # Port do farmTech_app.py como módulo
│   ├── weather_api.py               # Consulta OpenWeatherMap (port do meteo.R)
│   └── statistics.py                # Análise estatística (port do analise_estatistica3.R)
│
├── fase2/                           # Banco de Dados BRIX / Oracle
│   ├── __init__.py
│   ├── database.py                  # Abstração DB (Oracle primário, SQLite fallback)
│   ├── brix_analytics.py            # Port do analytics.py
│   └── file_manager.py              # Port do file_manager.py
│
├── fase3/                           # IoT & Automação
│   ├── __init__.py
│   ├── iot_simulator.py             # Gerador de leituras de sensores (N, P, K, pH, umidade)
│   ├── irrigation_logic.py          # Lógica de decisão de irrigação
│   └── sensor_data_store.py         # Persistência das leituras (SQLite)
│
├── fase4/                           # Dashboard ML (núcleo central)
│   ├── __init__.py
│   ├── dashboard.py                 # App Streamlit unificado (PONTO DE ENTRADA)
│   ├── ml_pipeline.py               # Port/melhoria do train_model.py
│   ├── recommendations.py           # Port do recommend.py
│   └── ingest.py                    # Port do ingest_db.py
│
├── fase5/                           # AWS Cloud & Alertas
│   ├── __init__.py
│   ├── aws_alerts.py                # Cliente SNS (boto3) — disparo de alertas
│   ├── alert_rules.py               # Regras de alertas (thresholds configuráveis)
│   └── aws_cost_analysis.md         # Documentação da análise de custos (Fase 5)
│
├── fase6/                           # Visão Computacional
│   ├── __init__.py
│   ├── vision_detector.py           # Wrapper YOLO para inferência
│   ├── sample_images/               # Imagens estáticas para demo
│   └── results/                     # Outputs de inferência (gerados em runtime)
│
└── data/                            # Dados compartilhados
    ├── areas_export.csv             # Fase 1
    ├── manejos_export.csv           # Fase 1
    ├── produtos_agricolas.csv       # Fase 3
    ├── crop_yield.csv               # Fase 5
    └── farmtech.db                  # SQLite (Fase 4, banco de desenvolvimento)
```

---

## 3. Fluxo de Dados entre Fases

```
Fase 1 (Insumos/Clima)
    ↓ dados de área, manejo, clima
Fase 2 (Banco Oracle/SQLite)
    ↓ registros persistidos, análise BRIX
Fase 3 (IoT Simulado)
    ↓ leituras de sensores N/P/K/pH/umidade → decisão de irrigação
         ↓
    Fase 5 (AWS SNS Alertas) ←──── Fase 6 (YOLO: detecção de pragas/doenças)
         ↓ e-mail / SMS para funcionários
Fase 4 (Dashboard Streamlit — HUB CENTRAL)
    ← integra outputs de todas as fases via módulos Python
```

---

## 4. Plano de Implementação Linear

> Cada etapa tem: objetivo, ações concretas, arquivos a criar/modificar, critério de aceite e checkpoint de revisão humana.

---

### ETAPA 0 — Preparação do Ambiente
**Objetivo:** Criar estrutura de pastas, arquivo de dependências e configuração.

**Ações:**
1. Criar pasta raiz `farmtech_fase7/` no workspace.
2. Criar subpastas `fase1/`, `fase2/`, `fase3/`, `fase4/`, `fase5/`, `fase6/`, `data/`.
3. Criar `__init__.py` vazio em cada subpasta.
4. Criar `requirements.txt` com todas as dependências (ver abaixo).
5. Criar `.env.example` com variáveis necessárias.
6. Criar `run_dashboard.sh` como atalho para `streamlit run fase4/dashboard.py`.
7. Copiar arquivos de dados para `data/` (CSVs das fases anteriores).

**`requirements.txt` consolidado:**
```
streamlit>=1.32.0
pandas>=2.0.0
numpy>=1.26.0
scikit-learn>=1.4.0
joblib>=1.3.0
matplotlib>=3.8.0
altair>=5.0.0
torch>=2.0.0
torchvision>=0.15.0
Pillow>=10.0.0
boto3>=1.34.0
python-dotenv>=1.0.0
requests>=2.31.0
oracledb>=2.0.0
plotly>=5.18.0
ultralytics>=8.0.0
```

**`.env.example`:**
```
# OpenWeatherMap API
OPENWEATHER_API_KEY=your_openweather_api_key_here
OPENWEATHER_CITY=Ribeirao_Preto,BR

# Oracle Database (Fase 2)
ORACLE_USER=your_oracle_username_here
ORACLE_PASSWORD=your_oracle_password_here
ORACLE_DSN=oracle.fiap.com.br

# AWS (Fase 5)
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
AWS_DEFAULT_REGION=sa-east-1
SNS_TOPIC_ARN=arn:aws:sns:sa-east-1:ACCOUNT_ID:FarmTechAlertas

# Alertas
ALERT_EMAIL=fazenda@exemplo.com
SENSOR_HUMIDITY_MIN=40.0
SENSOR_PH_MIN=5.5
SENSOR_PH_MAX=7.5
```

**Critério de aceite:** Estrutura de pastas criada, `pip install -r requirements.txt` executa sem erros críticos, variáveis de ambiente documentadas.

> 🔍 **CHECKPOINT HUMANO 0:** Revisar estrutura de pastas e dependências. Confirmar versões compatíveis com ambiente local (Python 3.10+, acesso à AWS e Oracle opcionais).

---

### ETAPA 1 — Módulo Fase 1: Insumos e Clima
**Objetivo:** Transformar o `farmTech_app.py` e os scripts R em funções Python reutilizáveis pelo dashboard.

**Arquivo: `fase1/crop_manager.py`**

Port do `farmTech_app.py` como módulo (sem `input()` interativo). Expõe:
- `calculate_area(cultura: str, largura: float, comprimento: float) -> dict`  
  Retorna `{"cultura", "area_m2", "largura", "comprimento"}`
- `calculate_manejo(cultura: str, produto: str, qtd_por_m2: float, area: float) -> dict`  
  Retorna `{"cultura", "produto", "qtd_por_m2", "total_ml"}`
- `load_areas_from_csv(path: str) -> list[dict]`  
  Lê `areas_export.csv`
- `load_manejos_from_csv(path: str) -> list[dict]`  
  Lê `manejos_export.csv`
- `export_to_csv(areas: list, manejos: list, path: str) -> None`

**Arquivo: `fase1/weather_api.py`**

Port da funcionalidade do `meteo.R` para Python:
- `get_current_weather(city: str, api_key: str) -> dict`  
  Chama `https://api.openweathermap.org/data/2.5/weather`  
  Retorna `{"temperatura", "umidade", "descricao", "vento_kmh", "chuva_mm"}`
- `get_forecast(city: str, api_key: str, days: int = 5) -> list[dict]`  
  Usa endpoint `/forecast`
- `should_irrigate_weather(forecast: list) -> bool`  
  Retorna `True` se previsão de chuva > 5mm nas próximas 24h

**Arquivo: `fase1/statistics.py`**

Port das análises do `analise_estatistica3.R`:
- `basic_stats(data: list[float]) -> dict`  
  Retorna `{"media", "mediana", "desvio_padrao", "minimo", "maximo"}`
- `plot_weather_stats(df: pd.DataFrame) -> matplotlib.figure.Figure`

**Critério de aceite:** Funções importáveis sem erros. `calculate_area("Café", 100, 50)` retorna dict correto. `get_current_weather()` retorna dados da API (ou mock se sem chave).

> 🔍 **CHECKPOINT HUMANO 1:** Testar `crop_manager.py` e `weather_api.py` isoladamente. Verificar se a chave OpenWeatherMap está configurada no `.env`.

---

### ETAPA 2 — Módulo Fase 2: Banco de Dados e Análise BRIX
**Objetivo:** Abstrair a camada de banco (Oracle ou SQLite) e expor a análise BRIX como funções reutilizáveis.

**Arquivo: `fase2/database.py`**

Abstração que tenta Oracle primeiro, cai para SQLite:
- `get_connection() -> Connection`  
  Tenta `oracledb.connect()` com credenciais do `.env`; se falhar, usa `sqlite3.connect("data/farmtech.db")`
- `create_tables() -> None`  
  Cria tabelas BRIX se não existirem
- `insert_brix_record(record: dict) -> None`
- `fetch_all_brix_records() -> list[dict]`
- `delete_brix_record(id: int) -> None`

**Arquivo: `fase2/brix_analytics.py`**

Port do `analytics.py` da Fase 2:
- `calculate_brix(base: float, meio: float, ponta: float) -> dict`  
  Retorna `{"brix_medio", "indice_maturacao", "pronto_para_colheita": bool}`
- `predict_harvest_date(records: list[dict]) -> dict`  
  Usa regressão linear (NumPy) sobre histórico de BRIX  
  Retorna `{"dias_para_colheita", "data_estimada", "confianca"}`
- `plot_brix_evolution(records: list[dict]) -> matplotlib.figure.Figure`

**Arquivo: `fase2/file_manager.py`**

Port do `file_manager.py` da Fase 2:
- `save_json(data: list, filepath: str) -> None`
- `load_json(filepath: str) -> list`
- `save_txt(data: list, filepath: str) -> None`

**Critério de aceite:** `get_connection()` retorna conexão SQLite sem Oracle local. `calculate_brix(18, 19, 20)` retorna dicionário com `pronto_para_colheita: True`. Dados persistidos no SQLite são recuperáveis.

> 🔍 **CHECKPOINT HUMANO 2:** Validar conexão SQLite. Se Oracle disponível, testar conexão Oracle. Verificar persistência de dados entre execuções.

---

### ETAPA 3 — Módulo Fase 3: IoT e Irrigação Inteligente
**Objetivo:** Simular leituras dos sensores ESP32 (N, P, K, pH, umidade) e implementar a lógica de irrigação, gerando dados para o dashboard.

**Arquivo: `fase3/iot_simulator.py`**

Simula as leituras dos sensores do Wokwi:
- `SensorReading` dataclass:  
  `timestamp, nitrogenio: bool, fosforo: bool, potassio: bool, ph: float, umidade: float, temperatura: float`
- `simulate_reading(culture: str = "Cana") -> SensorReading`  
  Gera valores aleatórios realistas (pH: 5.0-8.0, umidade: 20-80%, temperatura: 20-35°C)
- `simulate_time_series(n: int = 100, interval_minutes: int = 15) -> list[SensorReading]`  
  Gera série temporal de `n` leituras retroativas
- `readings_to_dataframe(readings: list[SensorReading]) -> pd.DataFrame`

**Arquivo: `fase3/irrigation_logic.py`**

Lógica de decisão de irrigação (documentada conforme Fase 2 IoT):
```python
# Critérios para Cana-de-Açúcar:
# - Irrigar se umidade < 45%
# - Não irrigar se umidade > 70%
# - Verificar NPK: se falta N, P ou K → alerta de fertilização
# - pH ideal: 5.5 a 7.0
```
- `should_irrigate(reading: SensorReading, culture: str = "Cana") -> dict`  
  Retorna `{"irrigar": bool, "razao": str, "urgencia": str}` (urgencia: "normal"/"alta"/"critica")
- `get_irrigation_recommendation(reading: SensorReading) -> str`  
  Texto descritivo para exibição no dashboard
- `classify_alert_level(reading: SensorReading) -> str`  
  Retorna: `"ok"` / `"atencao"` / `"critico"`

**Arquivo: `fase3/sensor_data_store.py`**

Persistência das leituras:
- `store_reading(reading: SensorReading, db_path: str) -> None`
- `get_recent_readings(n: int = 50, db_path: str) -> list[dict]`
- `get_readings_dataframe(db_path: str) -> pd.DataFrame`

**Critério de aceite:** `simulate_time_series(50)` gera 50 leituras com timestamps decrescentes. `should_irrigate()` retorna `{"irrigar": True}` para umidade=30%. Dados persistidos no SQLite e recuperáveis.

> 🔍 **CHECKPOINT HUMANO 3:** Verificar lógica de irrigação com valores-limite (ex.: umidade=44.9 → irrigar, umidade=45.1 → não irrigar). Revisar thresholds da cana-de-açúcar.

---

### ETAPA 4 — Módulo Fase 5: Alertas AWS SNS
**Objetivo:** Implementar o serviço de mensageria AWS que dispara alertas por e-mail/SMS baseado nas leituras das Fases 1, 3 e 6.

**Arquivo: `fase5/alert_rules.py`**

Regras de alerta configuráveis:
```python
ALERT_RULES = {
    "umidade_critica": {
        "threshold": 30.0,
        "operator": "<",
        "field": "umidade",
        "message": "🚨 ALERTA CRÍTICO: Umidade do solo em {value:.1f}% — IRRIGAÇÃO IMEDIATA necessária. Ligue a bomba da setores {sectors}.",
        "action": "Ativar bomba de irrigação imediatamente. Irrigar por 45 minutos."
    },
    "ph_baixo": {
        "threshold": 5.5,
        "operator": "<",
        "field": "ph",
        "message": "⚠️ pH do solo em {value:.1f} — Abaixo do ideal para cana-de-açúcar (5.5-7.0). Aplicar calcário.",
        "action": "Aplicar 2 ton/ha de calcário dolomítico. Reavaliar em 7 dias."
    },
    "ph_alto": {
        "threshold": 7.5,
        "operator": ">",
        "field": "ph",
        "message": "⚠️ pH do solo em {value:.1f} — Acima do ideal. Solo alcalino.",
        "action": "Aplicar enxofre elementar. Consultar agrônomo."
    },
    "praga_detectada": {
        "message": "🐛 VISÃO COMPUTACIONAL: Possível praga/doença detectada ({label}, confiança {confidence:.0%}). Enviar inspetor ao campo.",
        "action": "Acionar equipe de campo para inspeção visual no setor indicado. Considerar aplicação preventiva de defensivo."
    }
}
```

**Arquivo: `fase5/aws_alerts.py`**

Cliente AWS SNS com fallback para log:
- `class AlertService`:
  - `__init__(self, topic_arn: str, region: str)` — configura `boto3.client("sns")`
  - `send_alert(self, rule_key: str, context: dict) -> dict`  
    Formata mensagem da regra, publica no SNS  
    Retorna `{"status": "sent"/"simulated", "message_id": str, "timestamp": str}`
  - `check_and_alert_sensor(self, reading: SensorReading) -> list[dict]`  
    Avalia todas as regras contra uma leitura, dispara alertas relevantes
  - `check_and_alert_vision(self, detection: dict) -> dict`  
    Dispara alerta quando YOLO detecta ameaça
  - `get_alert_history(self, n: int = 20) -> list[dict]`  
    Retorna log local dos últimos n alertas

**Lógica de fallback:** Se `boto3` não conseguir conectar à AWS (sem credenciais ou sem rede), logar alerta em `data/alert_log.json` e exibir no dashboard com badge "Simulado".

**Critério de aceite:** `send_alert()` retorna `{"status": "sent"}` com credenciais AWS configuradas, ou `{"status": "simulated"}` sem elas. `check_and_alert_sensor()` dispara alerta correto para leitura com umidade=25%.

> 🔍 **CHECKPOINT HUMANO 4:** Configurar tópico SNS na AWS (sa-east-1), adicionar e-mail como subscriber e confirmar assinatura. Testar envio manual de mensagem de teste. Verificar ARN do tópico no `.env`.

---

### ETAPA 5 — Módulo Fase 6: Visão Computacional
**Objetivo:** Integrar o modelo YOLO treinado na Fase 6 como módulo Python chamável pelo dashboard.

**Arquivo: `fase6/vision_detector.py`**

Wrapper do modelo YOLO:
- `class VisionDetector`:
  - `__init__(self, model_path: str = None)`  
    Tenta carregar modelo customizado da Fase 6; se não disponível, usa YOLOv8 nano pré-treinado como fallback
  - `detect(self, image_source) -> dict`  
    Aceita: caminho de arquivo, URL, `PIL.Image`, `np.ndarray`  
    Retorna: `{"detections": list[{"label", "confidence", "bbox"}], "annotated_image": PIL.Image, "has_threat": bool}`
  - `detect_threats(self, image_source) -> dict`  
    Versão focada em ameaças agrícolas; retorna `{"threat_detected": bool, "threat_type": str, "confidence": float}`
  - `get_demo_result(self) -> dict`  
    Retorna resultado pré-processado para demo sem modelo carregado

**Imagens de demo:** Copiar 3-5 imagens representativas do Fase 6 para `fase6/sample_images/`.

**Critério de aceite:** `VisionDetector().detect("fase6/sample_images/test.jpg")` retorna dict com `detections` (mesmo que lista vazia). `has_threat` é `bool`. Dashboard exibe imagem anotada.

> ✅ **CHECKPOINT HUMANO 5 — CONCLUÍDO:** Pesos YOLO confirmados localmente em `.context/fase6/entrega/yolov5_runs/train/farmtech_exp_30_epocas/weights/best.pt` e `farmtech_exp_60_epocas/weights/best.pt`. Modelo CNN em `cnn_models/cnn_farmtech.keras`. Usar **best.pt de 60 épocas** como modelo principal (melhor performance per conclusão do notebook). Fallback YOLOv8n dispensado.

---

### ETAPA 6 — Dashboard Unificado (Fase 4 aprimorada)
**Objetivo:** Criar o dashboard Streamlit central que integra todos os módulos, com abas por fase e painel de alertas.

**Arquivo: `fase4/dashboard.py`** *(substitui/aprimora o `streamlit_app.py` da Fase 4)*

**Estrutura do dashboard:**

```
┌─────────────────────────────────────────────────────┐
│  🌾 FarmTech Solutions — Painel de Gestão Agrícola  │
│  Sidebar: Status Geral · Alertas Ativos · Config    │
├──────┬──────┬──────┬──────┬──────┬──────────────────┤
│Fase 1│Fase 2│Fase 3│Fase 4│Fase 5│     Fase 6       │
│Insu- │BRIX  │IoT   │ML &  │Alerta│Visão             │
│mos & │& DB  │Senso-│Predi-│AWS   │Computa-          │
│Clima │      │res   │ções  │SNS   │cional            │
└──────┴──────┴──────┴──────┴──────┴──────────────────┘
```

**Aba Fase 1 — Insumos & Clima:**
- Formulário: seleção de cultura, largura, comprimento → botão "Calcular Área"
- Resultado: área calculada + recomendação de insumos
- Widget: Clima atual (cidade configurável) com dados da OpenWeatherMap
- Seção: "Dados Históricos" — tabela editável com `areas_export.csv`
- Gráfico: distribuição de áreas por cultura

**Aba Fase 2 — Análise BRIX:**
- Formulário: inserir leituras BRIX (base, meio, ponta) → botão "Calcular BRIX"
- Métricas: BRIX médio, Índice de Maturação, status (pronto / não pronto para colheita)
- Gráfico: evolução histórica do BRIX (linha temporal)
- Previsão: data estimada de colheita (regressão linear)
- Tabela: registros do banco de dados com ações (editar/excluir)

**Aba Fase 3 — IoT & Sensores:**
- Botão "Gerar Nova Leitura Simulada" → exibe leitura atual com gauges
- Gauges em tempo real: umidade (%), pH, temperatura (°C), N/P/K (on/off)
- Status de irrigação: 💧 IRRIGAR / ✅ OK — com justificativa
- Gráfico: série temporal das últimas 50 leituras (umidade e pH)
- Botão "Iniciar Simulação Contínua (30s)" → atualização automática

**Aba Fase 4 — ML & Predições:**
- Seção: Análise exploratória dos dados (baseada no `crop_yield.csv` e `produtos_agricolas.csv`)
- Mapa de correlação (Pearson)
- Scatter interativo: variável X vs Rendimento (selecionável)
- Previsão: slider com parâmetros → modelo prediz rendimento esperado (ton/ha)
- Tabela: métricas do modelo (MAE, MSE, RMSE, R²)
- Recomendações: texto gerado por `recommendations.py` baseado na predição

**Aba Fase 5 — Alertas AWS:**
- Painel: Histórico dos últimos 20 alertas (tabela com timestamp, tipo, status)
- Badge: "SNS Conectado" (verde) ou "Modo Simulação" (amarelo)
- Botão "Testar Alerta de Umidade" → dispara alerta de teste
- Botão "Testar Alerta de pH" → dispara alerta de teste
- Formulário: threshold customizável para alertas
- Exibição: último e-mail enviado (formato preview)

**Aba Fase 6 — Visão Computacional:**
- Upload de imagem ou seleção de imagem de demo
- Botão "Detectar Ameaças" → executa inferência YOLO
- Exibição: imagem anotada com bounding boxes e labels
- Tabela: detecções com label, confiança, coordenadas
- Status: "Ameaça detectada" (vermelho) ou "Plantação saudável" (verde)
- Botão "Enviar Alerta AWS se Ameaça" → integra Fase 5

**Sidebar:**
- Resumo de status de cada fase (ícones ✅/⚠️/❌)
- Último alerta disparado
- Link para README e repositório GitHub

**Critério de aceite:** `streamlit run fase4/dashboard.py` abre sem erros. Todas as 6 abas carregam. Formulários de cálculo retornam resultados corretos. Importações de módulos das fases 1-6 funcionam.

> 🔍 **CHECKPOINT HUMANO 6 (PRINCIPAL):** Executar dashboard completo. Testar fluxo end-to-end:
> 1. Calcular área na Aba Fase 1
> 2. Inserir leitura BRIX na Aba Fase 2 e verificar persistência
> 3. Gerar leitura IoT na Aba Fase 3 e confirmar lógica de irrigação
> 4. Verificar predição ML na Aba Fase 4
> 5. Enviar alerta de teste na Aba Fase 5
> 6. Fazer upload de imagem e detectar na Aba Fase 6

---

### ETAPA 7 — Pipeline ML Aprimorado (Fase 4)
**Objetivo:** Aprimorar o `train_model.py` com o dataset da Fase 5 (`crop_yield.csv`) e expor modelos para o dashboard.

**Arquivo: `fase4/ml_pipeline.py`**

- `load_and_preprocess(csv_path: str) -> tuple[pd.DataFrame, pd.Series]`  
  Carrega `crop_yield.csv`, trata missing values, normaliza
- `train_models(X: pd.DataFrame, y: pd.Series) -> dict`  
  Treina 5 modelos: Linear Regression, Ridge, Random Forest, Gradient Boosting, SVR  
  Salva melhor modelo em `data/best_model.joblib`  
  Retorna dict com métricas de cada modelo
- `load_model(path: str) -> object`  
  Carrega modelo salvo
- `predict(model, features: dict) -> float`  
  Faz predição single-point
- `get_feature_importance(model) -> pd.DataFrame`  
  Para modelos baseados em árvore

**Arquivo: `fase4/recommendations.py`** *(aprimora o existente)*

- `generate_recommendation(prediction: float, features: dict) -> str`  
  Regras baseadas na predição de rendimento:
  - < 1.5 ton/ha: "Rendimento muito baixo — revisar fertilização e irrigação urgentemente"
  - 1.5-2.5 ton/ha: "Rendimento abaixo da média — aumentar irrigação se umidade < 50%"
  - 2.5-3.5 ton/ha: "Rendimento esperado — manter manejo atual"
  - \> 3.5 ton/ha: "Excelente rendimento previsto — monitorar pragas"

**Critério de aceite:** `train_models()` executa e salva arquivo `.joblib`. `predict()` retorna float. Métricas R² > 0.5 para pelo menos um modelo.

> 🔍 **CHECKPOINT HUMANO 7:** Revisar métricas dos modelos treinados. Se R² < 0.4 para todos, investigar qualidade dos dados. Confirmar que modelo salvo é carregado corretamente no dashboard.

---

### ETAPA 8 — Script de Entrada e Integração Final
**Objetivo:** Criar script de execução principal que permite iniciar serviços por terminal.

**Arquivo: `run_all.py`**

```python
"""
FarmTech Solutions — Fase 7
Uso:
  python run_all.py dashboard    # Inicia o Streamlit dashboard
  python run_all.py fase1        # Executa CLI da Fase 1 (modo interativo)
  python run_all.py fase2        # Executa CLI da Fase 2 (BRIX)
  python run_all.py fase3        # Roda simulação IoT por 60s
  python run_all.py treinar      # Re-treina modelos ML
  python run_all.py alerta-test  # Dispara alerta de teste na AWS
  python run_all.py detectar <caminho_imagem>  # Inferência YOLO
"""
import sys
import subprocess
...
```

**`run_dashboard.sh`:**
```bash
#!/bin/bash
cd "$(dirname "$0")"
source .venv/bin/activate 2>/dev/null || true
streamlit run fase4/dashboard.py --server.port 8501
```

**Critério de aceite:** `python run_all.py dashboard` inicia dashboard sem erros. `python run_all.py fase1` executa modo CLI. `python run_all.py alerta-test` dispara ou simula alerta.

---

### ETAPA 9 — README Completo
**Objetivo:** Criar documentação final cobrindo todas as fases com screenshots, explicações e links.

**Arquivo: `README.md`** — estrutura:

```markdown
# FarmTech Solutions — Sistema Integrado de Gestão Agrícola

## 🎯 Sobre o Projeto
## 👨‍🎓 Integrantes
## 🏗️ Arquitetura do Sistema
### Diagrama de Componentes
### Fluxo de Dados

## 📁 Estrutura do Projeto (VS Code)

## 🚀 Como Executar
### Pré-requisitos
### Instalação
### Iniciando o Dashboard
### Executando por Terminal

## 📋 Documentação por Fase

### Fase 1 — Base de Dados & Insumos
### Fase 2 — Banco de Dados BRIX & Oracle
### Fase 3 — IoT & Automação Inteligente
### Fase 4 — Dashboard ML (Streamlit)
### Fase 5 — Cloud AWS & Alertas SNS
  #### Arquitetura AWS
  #### Screenshots da Calculadora
  #### Serviço de Alertas SNS
### Fase 6 — Visão Computacional (YOLO)

## ☁️ Serviço de Alertas AWS (Fase 7)
### Configuração do SNS
### Regras de Alerta
### Screenshots

## 🎥 Vídeo Demonstrativo
[Link YouTube]

## 🔧 Variáveis de Ambiente

## 📊 Resultados dos Modelos ML
```

**Critério de aceite:** README cobre todas as fases com pelo menos 1 screenshot cada. Link do YouTube presente e funcional. Instruções de execução testadas e corretas.

> 🔍 **CHECKPOINT HUMANO 8:** Revisar README completo. Verificar que todos os links funcionam. Gravar vídeo de até 10 minutos e adicionar link.

---

### ETAPA 10 — Testes e Validação Final
**Objetivo:** Verificar que todo o sistema funciona end-to-end antes do commit final.

**Checklist de validação:**

- [ ] `pip install -r requirements.txt` sem erros
- [ ] `python run_all.py dashboard` → dashboard abre em `localhost:8501`
- [ ] Aba Fase 1: calcular área Café 100x50m → retorna 5000m²
- [ ] Aba Fase 1: clima carrega da API (ou exibe mock)
- [ ] Aba Fase 2: inserir BRIX 18/19/20 → status "pronto para colheita"
- [ ] Aba Fase 2: dados persistem após recarregar
- [ ] Aba Fase 3: gerar leitura com umidade=25% → status "IRRIGAR"
- [ ] Aba Fase 3: gráfico de série temporal exibe
- [ ] Aba Fase 4: predição ML retorna valor numérico
- [ ] Aba Fase 4: recomendação de texto gerada
- [ ] Aba Fase 5: alerta de teste dispara (SNS ou simulação)
- [ ] Aba Fase 5: histórico de alertas exibe
- [ ] Aba Fase 6: upload de imagem + detecção retorna resultado
- [ ] Sidebar: status de todas as fases exibido
- [ ] `python run_all.py fase1` executa modo CLI
- [ ] `python run_all.py alerta-test` executa sem erro

> 🔍 **CHECKPOINT HUMANO 9 (FINAL):** Executar checklist completo. Fazer commit no GitHub. Gravar vídeo demonstrativo.

---

## 5. Diagrama de Dependências entre Etapas

```
ETAPA 0 (Setup)
    │
    ├──► ETAPA 1 (Fase 1 módulos)
    ├──► ETAPA 2 (Fase 2 módulos)
    ├──► ETAPA 3 (Fase 3 módulos)
    ├──► ETAPA 4 (Fase 5 alertas)
    └──► ETAPA 5 (Fase 6 visão)
              │
              └──► ETAPA 6 (Dashboard — depende de todas)
                        │
                        ├──► ETAPA 7 (ML Pipeline — depende de ETAPA 6)
                        ├──► ETAPA 8 (run_all.py — depende de ETAPA 6)
                        ├──► ETAPA 9 (README — depende de tudo)
                        └──► ETAPA 10 (Testes — depende de tudo)
```

As etapas 1-5 podem ser implementadas em paralelo. A etapa 6 (Dashboard) requer todas as anteriores.

---

## 6. Decisões de Design

| Decisão | Escolha | Justificativa |
|---------|---------|---------------|
| DB principal | SQLite (fallback Oracle) | Oracle requer instalação; SQLite zero-config para desenvolvimento |
| YOLO | Ultralytics YOLOv8 + fallback pré-treinado | Modelo Fase 6 pode não estar disponível localmente |
| AWS SNS | boto3 com fallback para log local | Permite demo sem credenciais AWS |
| Dashboard | Streamlit com `st.tabs()` | Nativo Streamlit, sem dependências extras de roteamento |
| Dados IoT | Simulados (não Wokwi) | Wokwi não integra diretamente com Python; simulação é equivalente |
| ML Dataset | `crop_yield.csv` (Fase 5) como principal | Tem variável-alvo numérica clara para regressão |
| Gestão de dependências | Estratégia de baseline único + lock de versões + validação incremental | Elimina o risco de conflitos entre bibliotecas ao consolidar as fases em um único ambiente |

### Política Estratégica de Dependências (Fase 7)

Para assegurar a eliminação do risco de conflitos, a implementação seguirá obrigatoriamente:
1. Definição de baseline único de versões no `requirements.txt` consolidado.
2. Criação de ambiente limpo dedicado (`.venv`) para toda a Fase 7.
3. Instalação por blocos (core, ML, visão computacional, banco), com validação ao fim de cada bloco.
4. Congelamento final de versões efetivamente validadas (`pip freeze`) antes da entrega.
5. Proibição de upgrades ad hoc após início da validação final.

---

## 7. Riscos e Mitigações

| Risco | Probabilidade | Mitigação |
|-------|--------------|-----------|
| Credenciais AWS ausentes | Média | AlertService em modo simulação (log local) |
| `torch` incompatível com CPU-only Mac | Baixa | CPU inference configurado por padrão |

---

## 8. Critérios de Avaliação × Etapas do Plano

| Critério FIAP | Peso | Etapas que cobrem |
|---------------|------|-------------------|
| Repositório GitHub (estrutura, sem commits tardios) | 3.0 | Etapas 0, 9, 10 |
| VS Code — Códigos Python funcionais e organizados por fase | 3.0 | Etapas 1-8 |
| README — Documentação clara + link YouTube | 2.0 | Etapa 9 |
| Vídeo — Até 10 min, YouTube não listado, no README | 2.0 | Checkpoint 8/9 |

**Penalizações por fase não entregue (−0.5 cada):** Todas as Fases 1-6 estão cobiertas nas etapas acima. Nenhuma penalização esperada.

---

## 9. Ordem de Execução Recomendada para o Agente IA

```
1.  Etapa 0  → criar estrutura + requirements.txt + .env.example
2.  Etapa 1  → fase1/crop_manager.py + weather_api.py + statistics.py
3.  Etapa 2  → fase2/database.py + brix_analytics.py + file_manager.py
4.  Etapa 3  → fase3/iot_simulator.py + irrigation_logic.py + sensor_data_store.py
5.  Etapa 4  → fase5/alert_rules.py + aws_alerts.py
6.  Etapa 5  → fase6/vision_detector.py
7.  Etapa 7  → fase4/ml_pipeline.py + recommendations.py
8.  Etapa 6  → fase4/dashboard.py (integração de tudo)
9.  Etapa 8  → run_all.py + run_dashboard.sh
10. Etapa 9  → README.md
11. Etapa 10 → validação final (checklist manual)
```

---

## 10. Estimativa de Complexidade por Arquivo

| Arquivo | Linhas estimadas | Complexidade |
|---------|-----------------|-------------|
| `fase1/crop_manager.py` | ~80 | Baixa |
| `fase1/weather_api.py` | ~100 | Média |
| `fase1/statistics.py` | ~60 | Baixa |
| `fase2/database.py` | ~120 | Média |
| `fase2/brix_analytics.py` | ~100 | Média |
| `fase3/iot_simulator.py` | ~120 | Média |
| `fase3/irrigation_logic.py` | ~80 | Média |
| `fase4/ml_pipeline.py` | ~150 | Alta |
| `fase4/dashboard.py` | ~500 | Alta |
| `fase5/aws_alerts.py` | ~150 | Média |
| `fase6/vision_detector.py` | ~130 | Alta |
| `run_all.py` | ~80 | Baixa |
| `README.md` | ~300 | Baixa |
| **Total estimado** | **~1.970 linhas** | |

---

*Plano gerado em 03/05/2026 — FarmTech Solutions Fase 7*
