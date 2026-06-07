# CLAUDE.md — Projeto "Meu Resumo" (Breno Jahar)

Leia este arquivo inteiro antes de agir. Ele contém o estado completo do projeto.

---

## 🔗 Links importantes

- **Site ao vivo:** https://brennojahar.github.io/meu-resumo
- **Repositório:** https://github.com/Brennojahar/meu-resumo
- **Arquivo principal:** `index.html` — único arquivo, autossuficiente (HTML/CSS/JS inline)

---

## 📱 O que é

Painel nutricional e de treino **mobile-first em HTML estático** para o Breno Jahar.
Publicado no **GitHub Pages** (branch `master`, raiz `/`).

---

## 🎨 Identidade visual atual

Baseada no projeto Behance "Smart Home App" (nom.ai / pocolo.com.ua):

| Token | Valor | Uso |
|---|---|---|
| `--bg` | `#F7F7F7` | Fundo geral (Gray Whisper) |
| `--card` | `#FFFFFF` | Cards |
| `--card-edge` | `#EBEBEB` | Bordas |
| `--olive` | `#CBD77E` | Accent principal (Gentle Olive) |
| `--olive-deep` | `#a8b85e` | Texto/ícone de destaque |
| `--olive-light` | `#edf5d0` | Background suave olive |
| `--hazel` | `#E6CA9A` | Accent quente (Winter Hazel) |
| `--hazel-deep` | `#c4995a` | Números de déficit |
| `--hazel-light` | `#faf3e8` | Background suave hazel |
| `--ink` | `#282828` | Texto primário (Lunar Shadow) |
| `--muted` | `#888888` | Texto secundário |
| `--muted2` | `#BBBBBB` | Texto terciário |

**Estilo:** Tema claro, cards brancos com sombra suave (`0 2px 16px rgba(0,0,0,.06)`), bordas arredondadas (24px), sem texturas/glows neon. Clean e respira.

**Fontes:** Anton (números grandes) + Manrope (texto) — via Google Fonts.

---

## 🏗️ Estrutura da página

### Sempre visível (sem accordion):
1. **Hero** — nome "Breno Jahar", chips de dados (36 anos, 175cm, 83kg)
2. **Média estimada** — 3 cards lado a lado: Consumo (2.100), Gasto médio (2.700), Déficit médio (600) kcal/dia

### Accordion (colapsado por padrão, seta para abrir):
3. **Calorias por refeição** — 5 refeições com barras de progresso
4. **Gasto energético · ao vivo** — gasto do dia + agenda semanal com toggles
5. **Seu déficit hoje** — déficit dinâmico calculado pelo treino marcado
6. **Proteína do dia** — gauge com 120g vs ideal 135–180g
7. **Insights principais** — 4 bullets de análise
8. **Protocolo esteira · ao vivo** — 7 fases com timer ao vivo

### Rodapé:
- Renova Be · Nutrição / CRN 43226 / disclaimer

---

## ⚙️ Lógica JS principal

### Modelo calórico:
```
BASE = 2300 kcal  (metabolismo + rotina sem treino)
CONSUMO = 2100 kcal/dia
Gasto do dia = BASE + kcal do treino marcado hoje
Déficit = Gasto do dia − CONSUMO
~7.700 kcal = 1 kg de gordura
```

### Treinos cadastrados (WORKOUTS):
| Chave | Nome | Detalhe | kcal |
|---|---|---|---|
| `boxe` | Boxe | aula · 1h30 | 850 |
| `musc` | Musculação + esteira | + 25min esteira | 600 |
| `crossfit` | CrossFit | aula · 1h | 750 |
| `bike` | Bike na rua | 10 km | 300 |
| `esteira` | Esteira protocolo | 30 min · intervalado | 380 |

### Agenda semanal (WEEK):
| Dia | Treino |
|---|---|
| Domingo | bike |
| Segunda | boxe |
| Terça | musc |
| Quarta | crossfit |
| Quinta | musc |
| Sexta | musc |
| Sábado | boxe |

Marcações salvas em `localStorage` com chave `breno-treinos-v1`, expiram por semana.

### Protocolo esteira (TM_PHASES) — 30 min:
| Fase | Min | Inc | Vel |
|---|---|---|---|
| Aquecimento | 0–4 | 4 | 4,5 |
| Subida progressiva | 4–9 | 8 | 5,0 |
| Power walk forte | 9–13 | 6 | 6,0 |
| Montanha | 13–18 | 12 | 4,5 |
| Recuperação ativa | 18–22 | 7 | 5,2 |
| Pico final | 22–27 | 13 | 4,7 |
| Desaceleração | 27–30 | 4 | 4,0 |

Timer com ▶ Pausar / Continuar, cronômetro em tempo real, destaca fase ativa.

### Accordion:
Função `accToggle(header)` — usa `grid-template-rows: 0fr → 1fr` para animação suave. Ao abrir dispara fills das barras e count-ups.

---

## 👤 Dados do usuário

- Homem, 36 anos, 175 cm, 83 kg
- Consumo estimado: ~2.100 kcal/dia
- BMR (Mifflin-St Jeor): ~1.750 kcal
- Nutricionista: Renova Be · CRN 43226
- Queimas por treino (estimativas p/ 83 kg):
  - Boxe 1h30 = 850 kcal
  - Musculação + esteira = 600 kcal
  - CrossFit 1h = 750 kcal
  - Bike 10km = 300 kcal
  - Esteira protocolo 30min = 380 kcal

---

## 🚀 Como fazer deploy de alterações

```bash
# O projeto está em C:\Users\ADM\Desktop\meu-resumo\
cd C:\Users\ADM\Desktop\meu-resumo
git add index.html
git commit -m "descrição da alteração"
git push
# Aguardar ~1 min para o GitHub Pages atualizar
```

O GitHub CLI (`gh`) está instalado em `C:\Program Files\GitHub CLI\`.
Conta autenticada: **Brennojahar**

---

## ⏸️ Em pausa (não mexer)

- Integração Apple Watch — existem arquivos Swift (MeuResumoApp.swift, HealthManager.swift, DashboardView.swift) em outro local. Projeto pausado.
- Ponte Apple Watch → Supabase → página (gasto calórico medido ao vivo)

---

## 📋 TAREFA PENDENTE

O usuário quer **animações no estilo do site Aramco**:
https://sponsorships.aramco.com/cba/shoot-for-the-future/

Ele enviou um vídeo (MP4) mostrando as animações do site mas o Claude não conseguiu ler o vídeo.
**Próximo passo:** pedir prints/screenshots do vídeo ou descrição das animações para implementar.

Características típicas desse estilo de site (confirmar com o usuário):
- Elementos entram com fade + slide-up ao scrollar
- Texto com efeito de revelar (clip ou opacity stagger por palavra/letra)
- Paralaxe sutil em elementos de fundo
- Transições de seção com timing elaborado
- Números animam ao entrar na viewport
- Hover states suaves nos cards

---

## 🔒 Segurança

- Credenciais/tokens ficam locais, nunca em chat
- Valores calóricos são estimativas educativas, não prescrição médica
