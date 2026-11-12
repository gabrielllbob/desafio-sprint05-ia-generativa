# Placeholder para Capturas de Tela (Screenshots)

Esta pasta deve conter as capturas de tela reais das interações no **Google AI Studio** demonstrando a execução dos prompts e as respostas obtidas.

## Capturas Sugeridas (renomeie seus arquivos para estes nomes):

| Arquivo | Descrição |
|---------|-----------|
| `01_zero_shot_exemplo.png` | Tela do Google AI Studio com prompt Zero-Shot (01_zero_shot_prompt.txt) e resposta gerada |
| `02_few_shot_exemplo.png` | Tela com prompt Few-Shot (02_few_shot_prompt.txt) mostrando os 3 exemplos + resposta |
| `03_cot_exemplo.png` | Tela com Chain-of-Thought (03_chain_of_thought_prompt.txt) mostrando raciocínio explícito + resposta final |
| `04_otimizado_exemplo.png` | Tela com prompt otimizado (04_prompt_otimizado_final.txt) e resposta JSON estruturada |
| `05_validacao_json.png` | Validação do JSON de saída (VS Code, terminal `python -m json.tool`, ou editor online) |
| `06_planilha_avaliacao.png` | Planilha Excel aba "Avaliacoes_Detalhadas" mostrando as 150 linhas |
| `07_grafico_radar.png` | Gráfico radar gerado pelo notebook (radar_chart_tecnicas.png) |
| `08_tradeoff_qualidade_custo.png` | Gráfico trade-off qualidade vs latência/custo (tradeoff_qualidade_custo.png) |
| `09_boxplot_nota.png` | Boxplot da nota ponderada (boxplot_nota_ponderada.png) |
| `10_taxa_problemas.png` | Gráfico de taxa de problemas (taxa_problemas_tecnicas.png) |
| `11_calibracao_confianca.png` | Calibração de confiança (calibracao_confianca.png) |
| `12_respostas_jsonl.png` | Visualização do arquivo JSONL (ex: VS Code ou `head -5 respostas_todas_tecnicas.jsonl`) |

## Como Capturar no Google AI Studio:

1. Abra https://aistudio.google.com/
2. Cole o prompt na área "System instructions" + "User prompt"
3. Clique em "Run"
4. Capture a tela (Win+Shift+S no Windows, Cmd+Shift+4 no Mac)
5. Salve na pasta `screenshots/` com os nomes acima

## Dicas:
- Capture **antes e depois** de rodar (prompt + resposta completa)
- Para Chain-of-Thought, capture o raciocínio longo (pode precisar scroll)
- Para Few-Shot, mostre que os 3 exemplos estão no prompt
- Para o prompt otimizado, mostre a saída JSON formatada

---
*Arquivo placeholder - substitua pelos prints reais antes de subir no GitHub*