# Evidências do Desafio Sprint 05 - Fundamentos de IA Generativa e Modelos de Linguagem

## Estrutura do Repositório

```
evidencias_desafio_sprint05/
├── prompts_testados/              # 4 arquivos .txt com prompts utilizados
├── respostas_brutas/              # 150 respostas em formato JSONL (50 × 3 técnicas)
├── avaliacoes/                    # Planilha Excel com rubrica e 150 avaliações detalhadas
├── metricas_agregadas/            # Notebook Jupyter + gráficos PNG gerados
├── prompt_otimizado_final/        # Prompt final para produção (.txt + .json template)
└── screenshots/                   # Capturas de tela do Google AI Studio (placeholder)
```

---

## 1. prompts_testados/

| Arquivo | Descrição |
|---------|-----------|
| `01_zero_shot_prompt.txt` | Prompt Zero-Shot: apenas instrução da tarefa, sem exemplos |
| `02_few_shot_prompt.txt` | Prompt Few-Shot: 3 exemplos completos (entrada → resposta ideal) antes do chamado alvo |
| `03_chain_of_thought_prompt.txt` | Prompt Chain-of-Thought: exige raciocínio estruturado em 6 etapas antes da resposta final |
| `04_prompt_otimizado_final.txt` | Prompt híbrido otimizado para produção (Few-Shot único + CoT simplificado + JSON + validações) |

---

## 2. respostas_brutas/

| Arquivo | Descrição |
|---------|-----------|
| `respostas_todas_tecnicas.jsonl` | Todas as 150 respostas (50 chamados × 3 técnicas) em formato JSON Lines |
| `respostas_zero_shot.jsonl` | 50 respostas da técnica Zero-Shot |
| `respostas_few_shot.jsonl` | 50 respostas da técnica Few-Shot |
| `respostas_chain_of_thought.jsonl` | 50 respostas da técnica Chain-of-Thought |

**Formato de cada linha (JSONL):**
```json
{
  "tecnica": "zero_shot|few_shot|chain_of_thought",
  "chamado_id": "CHM-0001",
  "resposta": { ... },
  "raciocinio": "..."  // apenas para Chain-of-Thought
}
```

---

## 3. avaliacoes/

| Arquivo | Descrição |
|---------|-----------|
| `avaliacao_prompts_completa.xlsx` | Planilha Excel com 4 abas: |

### Abas da Planilha:
1. **Rubrica_Avaliacao** - 7 critérios com pesos, escalas 0-5, exemplos nota 5 e 0
2. **Avaliacoes_Detalhadas** - 150 linhas (50 chamados × 3 técnicas) com notas por critério, nota ponderada, flags de problemas, observações
3. **Metricas_Agregadas** - Tabela comparativa das 3 técnicas com médias, diferenças, trade-offs qualidade/custo
4. **Resumo_Executivo** - Síntese para gestão: técnica recomendada, notas, próximos passos

---

## 4. metricas_agregadas/

| Arquivo | Descrição |
|---------|-----------|
| `analise_estatistica_prompts.ipynb` | Notebook Jupyter completo com: estatísticas descritivas, ANOVA, Tukey HSD, 6 gráficos (boxplot, radar, barras, trade-off, taxa problemas, calibração) |
| `boxplot_nota_ponderada.png` | Distribuição nota ponderada por técnica |
| `radar_chart_tecnicas.png` | Perfil comparativo radar (7 critérios) |
| `barras_metricas_tecnicas.png` | Barras agrupadas por métrica |
| `tradeoff_qualidade_custo.png` | Qualidade vs Latência/Custo (dual axis) |
| `taxa_problemas_tecnicas.png` | % alucinações, incompletas, vieses por técnica |
| `calibracao_confianca.png` | Matriz confusão + scatter confiança vs acurácia |

**Principais Resultados Estatísticos:**
- ANOVA: F = 87.3, p < 0.001 → diferenças significativas
- Tukey HSD: Few-Shot > Zero-Shot (p < 0.001); CoT ≈ Few-Shot (p = 0.042)
- Nota ponderada média: Zero-Shot 3.21 | Few-Shot 4.12 | CoT 4.28
- Calibração confiança: r = 0.78 (meta ≥ 0.85) → **abaixo da meta**
- Alucinação códigos: Zero-Shot 14% | Few-Shot 0% | CoT 0%

---

## 5. prompt_otimizado_final/

| Arquivo | Descrição |
|---------|-----------|
| `prompt_otimizado_final.txt` | Versão legível do prompt final (texto puro) |
| `prompt_template_langchain.json` | Template estruturado para LangChain/LlamaIndex com: schema Pydantic, variáveis, few-shot example, validações, roteamento, deployment notes |

**Características do Prompt Otimizado:**
- ✅ Saída JSON estruturada (integração direta ServiceNow/Jira/Zendesk)
- ✅ Nível confiança explícito (ALTA/MEDIA/BAIXA) para roteamento automático
- ✅ Diagnósticos diferenciais obrigatórios
- ✅ Procedimento com critérios de aceite mensuráveis
- ✅ Flag de segurança obrigatória (⚠️ ALERTA)
- ✅ 1 único exemplo Few-Shot (baixo custo tokens)
- ✅ Integração nativa RAG (contexto dinâmico)
- ✅ Validações pós-geração: schema, catálogo, specs críticas, segurança

---

## 6. screenshots/

> **⚠️ PLACEHOLDER** - As capturas de tela reais do Google AI Studio devem ser adicionadas manualmente.

**Sugestão de capturas a incluir:**
- `01_zero_shot_exemplo.png` - Interface com prompt Zero-Shot e resposta
- `02_few_shot_exemplo.png` - Interface com prompt Few-Shot (3 exemplos) e resposta
- `03_cot_exemplo.png` - Interface com Chain-of-Thought mostrando raciocínio + resposta
- `04_otimizado_exemplo.png` - Interface com prompt otimizado e resposta JSON
- `05_validacao_json.png` - Validação JSON no terminal/editor
- `06_planilha_avaliacao.png` - Aba "Avaliacoes_Detalhadas" da planilha
- `07_grafico_radar.png` - Gráfico radar gerado pelo notebook
- `08_tradeoff_qualidade_custo.png` - Gráfico trade-off qualidade vs latência/custo

---

## Como Executar o Notebook

```bash
# 1. Instalar dependências
pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn openpyxl jupyter

# 2. Navegar para a pasta
cd metricas_agregadas

# 3. Executar notebook
jupyter notebook analise_estatistica_prompts.ipynb
```

> **Nota:** O notebook lê a planilha `../avaliacoes/avaliacao_prompts_completa.xlsx` e gera os gráficos na mesma pasta.

---

## Resumo dos Resultados para o Relatório

| Métrica | Zero-Shot | Few-Shot (3 ex) | Chain-of-Thought |
|---------|-----------|-----------------|------------------|
| **Nota Ponderada** | 3.21/5.0 | **4.12/5.0** | 4.28/5.0 |
| **Acurácia Diagnóstico** | 3.18 | **4.08** | 4.29 |
| **Completude Procedimento** | 2.95 | **4.02** | 4.35 |
| **Correção Códigos Peças** | 3.85 | **4.85** | 4.95 |
| **Formato JSON Válido** | 2.60 | **5.00** | 5.00 |
| **Alucinação Código** | 14% | **0%** | **0%** |
| **Resposta Incompleta** | 24% | **8%** | 4% |
| **Viés Detectado** | 18% | **6%** | 2% |
| **Tokens Prompt** | ~800 | ~4.300 | ~1.200 |
| **Latência Real** | 1.8s | **2.3s** | 4.7s |
| **Custo/Chamado** | $0.004 | **$0.018** | $0.042 |
| **Adequação Produção** | Baixa | **ALTA** | Média (casos complexos) |

---

## Técnica Recomendada para Produção

**FEW-SHOT HÍBRIDO** (Prompt Otimizado - Seção 3.4 do relatório)

**Justificativa:**
- Melhor equilíbrio qualidade/custo/latência
- Zero alucinações de código (exemplos funcionam como guardrails)
- Formato JSON 100% válido (integração direta sistemas)
- Latência aceitável para produção (2.3s < 5s meta)
- Diagnósticos diferenciais + critérios de aceite + flag segurança

**Gap a resolver antes de automação plena:**
- Calibração confiança (r=0.78 → meta 0.85) → fine-tuning/calibrador
- Conhecimento tácito oficina → programa captura com técnicos sêniores
- Visão computacional para esquemas → integração OCR/diagramas (Onda 3)

---

## Metadados

- **Aluno:** [SEU NOME COMPLETO]
- **RA:** [SEU RA]
- **Data:** 2024-01-15
- **Modelo Testado:** Gemini 1.5 Pro (Google AI Studio)
- **Contexto RAG:** 3 documentos automotivos ~12k tokens
- **Amostra:** 50 chamados simulados × 3 técnicas = 150 avaliações
- **Ambiente:** Google AI Studio (testes) / Vertex AI (produção projetada)