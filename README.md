# 📊 Macro API - Dados Macroeconômicos para Visor Crypto

API gratuita de dados macroeconômicos, atualizada automaticamente via GitHub Actions e servida via GitHub Pages.

## 🎯 Solução Escalável

**Problema**: APIs de dados financeiros têm limites de requisições (rate limits)
**Solução**: GitHub Actions coleta os dados periodicamente e salva em JSON estático

✅ **Escala para infinitos usuários** - JSON servido via CDN do GitHub  
✅ **Sem custos** - GitHub Actions + GitHub Pages gratuitos  
✅ **Dados reais** - FRED, FMP, Yahoo Finance  
✅ **Atualização automática** - A cada 30 minutos  

## 📡 Endpoint

```
https://SEU_USUARIO.github.io/macro-api/data/macro-data.json
```

## 📋 Dados Disponíveis

### 1. Taxa de Juros (Fed Funds Rate)
Fonte: **FRED** (Federal Reserve Economic Data)
```json
{
  "fedRate": {
    "current": {
      "range": "4.25-4.50%",
      "midpoint": 4.5,
      "effective": 4.5
    },
    "lastDecision": {
      "type": "cut",
      "change": 25,
      "date": "2025-12-18"
    },
    "history": [...],
    "source": "FRED (Federal Reserve)"
  }
}
```

### 2. Probabilidades do Fed
Fonte: **Polymarket** ou estimativa via Treasury Futures
```json
{
  "probabilities": {
    "cut": 35,
    "hold": 55,
    "hike": 10,
    "source": "Polymarket"
  }
}
```

### 3. Calendário Econômico
Fonte: **Financial Modeling Prep (FMP)**
```json
{
  "calendar": {
    "events": [
      {
        "date": "2026-02-07",
        "day": 7,
        "month": "FEV",
        "time": "10:30",
        "title": "Non-Farm Payrolls",
        "country": "🇺🇸 EUA",
        "impact": "high",
        "previous": 256000,
        "estimate": 180000,
        "history": [...]
      }
    ],
    "source": "Financial Modeling Prep"
  }
}
```

### 4. Indicadores de Mercado
Fonte: **Yahoo Finance**
```json
{
  "marketIndicators": {
    "indicators": [
      {
        "name": "S&P 500",
        "desc": "Índice americano",
        "value": "6025.99",
        "change": 0.53
      },
      {
        "name": "VIX",
        "desc": "Índice de Volatilidade",
        "value": "16.85",
        "change": -3.21
      },
      {
        "name": "DXY",
        "desc": "Índice do Dólar",
        "value": "107.32",
        "change": 0.12
      },
      {
        "name": "Ouro",
        "desc": "XAU/USD",
        "value": "$2865.40",
        "change": 0.87
      },
      {
        "name": "Petróleo WTI",
        "desc": "Crude Oil",
        "value": "$72.53",
        "change": -1.24
      },
      {
        "name": "Treasury 10Y",
        "desc": "Yield 10 Anos",
        "value": "4.521%",
        "change": 0.05
      }
    ],
    "source": "Yahoo Finance"
  }
}
```

### 5. Próximas Reuniões FOMC
```json
{
  "nextMeetings": [
    {
      "date": "2026-03-18",
      "label": "17-18 Mar 2026",
      "time": "16:00",
      "daysUntil": 43
    }
  ]
}
```

## 🚀 Como Usar no Seu App

```javascript
const MACRO_API_URL = 'https://SEU_USUARIO.github.io/macro-api/data/macro-data.json';

async function loadMacroData() {
    const response = await fetch(MACRO_API_URL);
    const data = await response.json();
    
    // Taxa de juros
    console.log('Taxa atual:', data.fedRate.current.range);
    
    // Probabilidades
    console.log('Prob. corte:', data.probabilities.cut + '%');
    
    // Próxima reunião
    console.log('Próxima FOMC:', data.nextMeetings[0].label);
    
    // Indicadores
    data.marketIndicators.indicators.forEach(ind => {
        console.log(`${ind.name}: ${ind.value} (${ind.change}%)`);
    });
}
```

## ⚙️ Setup (Para seu próprio repositório)

### 1. Fork este repositório

### 2. Configurar Secrets (Opcional, melhora os dados)
No GitHub, vá em **Settings > Secrets and variables > Actions** e adicione:

| Secret | Descrição | Obrigatório |
|--------|-----------|-------------|
| `FRED_API_KEY` | [Criar aqui](https://fred.stlouisfed.org/docs/api/api_key.html) | Recomendado |
| `FMP_API_KEY` | [Criar aqui](https://financialmodelingprep.com/developer/docs/) | Opcional |

### 3. Ativar GitHub Pages
- Vá em **Settings > Pages**
- Source: **Deploy from a branch**
- Branch: **main**, Folder: **/ (root)**
- Salve e aguarde o deploy

### 4. Ativar GitHub Actions
- Vá em **Actions**
- Clique em "I understand my workflows, go ahead and enable them"
- Execute manualmente o workflow "Update Macro Data"

### 5. Seu endpoint estará disponível em:
```
https://SEU_USUARIO.github.io/macro-api/data/macro-data.json
```

## 📅 Frequência de Atualização

| Período | Frequência |
|---------|------------|
| Segunda a Sexta (9h-22h BRT) | A cada 30 minutos |
| Finais de Semana | A cada 2 horas |

## 🔧 Executar Localmente

```bash
# Instalar dependências
npm install

# Executar coleta de dados
npm run fetch

# Os dados serão salvos em data/macro-data.json
```

## 📝 Licença

MIT - Use livremente!

---

**Desenvolvido para o Visor Crypto** 🚀
