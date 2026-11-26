# Guia de estudo para a arguição e checklist da entrega

Material de apoio da equipe (Vithor dos Santos, Murilo Pantoja e João Felipe). Fica fora do notebook de propósito: o notebook contém só o que a lauda pede.

## Perguntas prováveis na arguição

1. **Qual a principal inovação da EfficientNet?** O escalonamento composto (*compound scaling*): profundidade, largura e resolução crescem juntas, controladas por um único coeficiente φ (α = 1,2; β = 1,1; γ = 1,15), sobre uma rede-base (B0) encontrada por busca de arquitetura (NAS).
2. **Qual a diferença da B1 para a B0?** Profundidade ×1,1 por estágio (23 blocos MBConv em vez de 16), entrada de 240 px em vez de 224, 7,8 M parâmetros em vez de 5,3 M e +2 pontos no ImageNet (79,1% × 77,1%).
3. **O que é um bloco MBConv? E o SE?** Expansão 1×1 → convolução *depthwise* k×k → *Squeeze-and-Excitation* (atenção por canal) → projeção 1×1 linear, com conexão residual quando os formatos coincidem.
4. **Por que a convolução depthwise é barata?** Uma convolução comum 3×3 de 144 para 144 canais faz ~186 mil multiplicações por pixel; a depthwise (3·3·144) mais a 1×1 (144·144) fazem ~22 mil, cerca de 8 vezes menos.
5. **Por que não normalizaram as imagens?** A normalização ImageNet está dentro do modelo Keras, que espera pixels de 0 a 255.
6. **Por que dividir por folha?** Recortes da mesma folha em treino e teste inflariam o resultado (vazamento). A divisão oficial dos autores deixa 286 folhas em mais de um conjunto; a nossa, nenhuma.
7. **Por que F1 macro e não acurácia?** As classes são desbalanceadas (3,9:1): a acurácia esconderia um mau desempenho nas classes pequenas.
8. **Qual o erro mais grave?** Doença classificada como saudável (falso saudável): caiu de 7 casos (1,98%) na base congelada para 1 (0,28%) depois do fine-tuning.
9. **Por que a BatchNorm fica congelada no fine-tuning?** Com batch 32, as estatísticas seriam ruidosas e destruiriam o que foi pré-treinado; é a recomendação oficial do Keras para EfficientNet.
10. **Como escolheram o modelo sem olhar o teste?** Regra fixada antes (maior F1 macro de validação; empate < 0,01 → menor falso saudável → menor custo), registrada em `escolha_do_modelo.json` antes de liberar o teste. A e B empataram (0,950 × 0,952), e a A venceu pelo custo.
11. **Por que o GitHub e não o DOI?** O arquivo do DOI está truncado (auditoria na Seção 3.2), e a versão *symptom* só está no repositório dos autores.
12. **Houve overfitting?** Na base congelada, não. Na estratégia A, há sinal depois da época 6 (loss de validação subindo), contido pelo early stopping. A B foi mais estável.
13. **O ganho do fine-tuning valeu o custo?** Sim em relação à base congelada (F1 0,903 → 0,950; erros na validação 31 → 15). A B não compensa em relação à A: 76% mais tempo para uma diferença dentro do ruído.

## Checklist depois da defesa intermediária

- [ ] Incorporar as orientações da professora. Se for preciso retreinar, retreinar **antes** de liberar o teste.
- [ ] Na célula de configuração, `RUN_FINAL_TEST = True`; rodar a Seção 12 (avaliação única no teste).
- [ ] Escrever a discussão da Seção 12 e a linha "Resultado no teste" da Seção 14.
- [ ] Salvar o notebook **com as saídas** no GitHub (*Arquivo → Salvar uma cópia no GitHub*).
- [ ] Slides (até 12 min, sem foco em código; todos apresentam).
- [ ] Classroom: slides + `modelo_recomendado.keras` + `modelo_recomendado_info.json` (link da pasta do Drive `cnn_efficientnetb1_bracol/modelos`).
