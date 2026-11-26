# Transfer Learning e Fine-Tuning com EfficientNetB1 — sintomas em folhas de café (BRACOL)

Trabalho da disciplina **Inteligência Computacional / Machine Learning** (CESUPA) — Profa. Polyana Santos Fonseca Nascimento.

Classificação de 5 sintomas em folhas de café arábica (saudável, bicho-mineiro, ferrugem, mancha de phoma e cercosporiose) com **EfficientNetB1** pré-treinada no ImageNet: base congelada como referência e duas estratégias de fine-tuning (A e B), com análise de erros e Grad-CAM.

## Notebooks

| Arquivo | Conteúdo |
|---|---|
| `defesa_efficientnetb1_bracol.ipynb` | Notebook principal: arquitetura, análise e divisão dos dados (teste reservado), base congelada, análise visual preliminar e estratégias A e B |
| `piloto_escolha_dataset.ipynb` | Piloto que comparou BRACOL, PBC e DeepWeeds para justificar a escolha do dataset |
| `guia_arguicao.md` | Guia de estudo para a arguição e checklist do que falta depois da defesa |
| `imagem_externa/` | Imagem da internet usada na Seção 13 (CC BY 2.5), com créditos |

## Como executar

Abra o notebook no Google Colab, escolha **GPU T4** (*Ambiente de execução → Alterar o tipo de ambiente de execução*) e use *Executar tudo*. As imagens são baixadas automaticamente, e a divisão dos dados, os pesos e as figuras são salvos no Google Drive.

## Dataset

- **BRACOL**: Krohling, Esgario & Ventura (2019), Mendeley Data, DOI [10.17632/yy2k5y8mxg.1](https://doi.org/10.17632/yy2k5y8mxg.1).
- A versão *symptom* vem do repositório dos autores, [esgario/lara2018](https://github.com/esgario/lara2018), porque o arquivo publicado no DOI está truncado (a auditoria está no notebook).
- Artigo: Esgario, Krohling & Ventura (2020), *Computers and Electronics in Agriculture* 169:105162.

## Arquitetura

Tan, M.; Le, Q. V. *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks*. ICML 2019 (arXiv:1905.11946).
