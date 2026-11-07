# 🖼️ SISTEMA DE RECOMENDAÇÃO VISUAL DE PRODUTOS
### 🤖 Image Similarity | Deep Learning | Transfer Learning | Computer Vision

**Projeto acadêmico | Sistema de Recomendação baseado em Similaridade Visual**

---

## 🎯 Objetivo do Projeto

Desenvolver um sistema de recomendação de produtos para e-commerce utilizando **similaridade visual entre imagens**, aplicando técnicas de Deep Learning e Transfer Learning.

Diferentemente dos sistemas tradicionais de recomendação, que utilizam atributos textuais como marca, preço, descrição ou categoria, esta solução utiliza características extraídas diretamente das imagens dos produtos.

O objetivo é identificar produtos visualmente semelhantes considerando características como:

- 🎨 Cores.
- 📐 Formatos e proporções.
- 🧵 Texturas.
- ✨ Estilos e características visuais.
- 🔍 Padrões e elementos presentes nas imagens.

A proposta é demonstrar como técnicas de Computer Vision podem ser utilizadas para desenvolver mecanismos de busca e recomendação visual em plataformas de comércio eletrônico.

---

## 🧠 1. Extração de Características Visuais – ResNet50

📌 **Objetivo:** transformar imagens de produtos em representações numéricas que permitam comparar suas características visuais.

Foi utilizado o modelo pré-treinado **ResNet50**, originalmente treinado com a base ImageNet, aplicando Transfer Learning para aproveitar o conhecimento adquirido durante seu treinamento.

### ⚙️ Configuração do modelo

- 🧠 Arquitetura: ResNet50.
- 📚 Pesos pré-treinados: ImageNet.
- ✂️ Camada de classificação original removida.
- 📊 Extração de características por meio de embeddings.
- 🔢 Representação vetorial: 2048 dimensões por imagem.

Cada imagem é transformada em um vetor numérico que representa suas características visuais.

Esses vetores permitem comparar imagens por proximidade no espaço de características, sem depender exclusivamente de informações textuais dos produtos.

---

## 📊 2. Geração e Normalização dos Embeddings

📌 **Objetivo:** preparar as representações vetoriais para comparação matemática.

Após a extração das características pela ResNet50, foi aplicada a normalização L2.

### 🔢 Normalização L2

A normalização L2 ajusta a magnitude dos vetores para que tenham norma unitária.

Isso permite realizar comparações por distância cosseno de maneira consistente, reduzindo a influência da magnitude original dos vetores.

### 📁 Armazenamento dos dados

Para evitar o processamento repetitivo das imagens, foram criados arquivos para armazenar os resultados:

- `embeddings_relogios.npy` – matriz com os embeddings extraídos das imagens.
- `paths_relogios.npy` – caminhos correspondentes aos arquivos de imagem.

Essa estratégia permite reutilizar os vetores já calculados, reduzindo o tempo de processamento em consultas futuras.

---

## 🔍 3. Busca por Similaridade – k-Nearest Neighbors (k-NN)

📌 **Objetivo:** encontrar produtos visualmente semelhantes a partir de uma imagem de consulta (*query image*).

Foi utilizado o algoritmo k-Nearest Neighbors (k-NN), configurado com distância cosseno.

### ⚙️ Funcionamento

1. 🖼️ O usuário seleciona uma imagem de produto.
2. 🧠 A imagem passa pelo modelo ResNet50.
3. 🔢 O sistema extrai seu embedding de 2048 dimensões.
4. 📐 O vetor é normalizado utilizando L2.
5. 🔍 O algoritmo k-NN compara o vetor de consulta com os embeddings armazenados.
6. 🏆 O sistema identifica os produtos mais próximos visualmente.
7. 📊 Os resultados são apresentados graficamente.

A busca é realizada com base na proximidade entre os vetores, permitindo encontrar imagens com características visuais semelhantes.

---

## 📏 4. Métrica de Similaridade – Distância Cosseno

A distância cosseno foi utilizada para avaliar a proximidade entre os embeddings.

Ela compara a orientação dos vetores no espaço multidimensional, sendo útil para avaliar similaridade entre representações de imagens.

**Interpretação geral:**

- 📉 Distância menor: vetores mais semelhantes.
- 📈 Distância maior: vetores menos semelhantes.

A métrica permite estabelecer um ranking de produtos candidatos a recomendação visual.

---

## 🖥️ 5. Visualização dos Resultados

📌 **Objetivo:** apresentar os produtos recomendados de forma visual e intuitiva.

Foi utilizado o Matplotlib para exibir:

- 🖼️ Imagem original selecionada pelo usuário.
- 🏆 Produtos visualmente mais semelhantes.
- 🔢 Ranking dos resultados encontrados.
- 📊 Comparação visual entre a consulta e as recomendações.

Essa apresentação permite avaliar visualmente se o sistema está identificando produtos com características semelhantes às esperadas.

---

## 🔄 6. Fluxo de Funcionamento do Sistema

A arquitetura do projeto pode ser resumida no seguinte fluxo:

**Imagens dos produtos → Pré-processamento → ResNet50 → Embeddings → Normalização L2 → k-NN → Distância Cosseno → Produtos recomendados**

O processo é dividido em duas etapas principais:

### 📦 Etapa 01 – Construção do banco de embeddings

- Carregamento das imagens.
- Pré-processamento.
- Extração das características visuais.
- Normalização dos vetores.
- Armazenamento dos embeddings e caminhos das imagens.

### 🔎 Etapa 02 – Consulta e recomendação

- Seleção da imagem de consulta.
- Extração do embedding da consulta.
- Comparação com o banco de embeddings.
- Identificação dos vizinhos mais próximos.
- Exibição dos produtos recomendados.

Essa separação permite que a etapa de extração seja executada apenas quando necessário, tornando as consultas posteriores mais eficientes.

---

## 🛠️ 7. Tecnologias e Bibliotecas Utilizadas

| Tecnologia | Aplicação |
|---|---|
| 🐍 Python | Linguagem de programação |
| 🧠 TensorFlow / Keras | Utilização do modelo ResNet50 |
| 📷 PIL | Carregamento e manipulação de imagens |
| 🔢 NumPy | Armazenamento e manipulação de embeddings |
| 📊 Matplotlib | Visualização dos resultados |
| 🔍 Scikit-learn | Algoritmo k-NN e distância cosseno |
| 🤖 Deep Learning | Extração de características visuais |
| 🔄 Transfer Learning | Aproveitamento de modelo pré-treinado |

---

## 💡 8. Aplicações Práticas

Sistemas de recomendação por similaridade visual podem ser utilizados em diferentes cenários:

- 🛍️ E-commerce: recomendação de produtos visualmente semelhantes.
- ⌚ Moda e acessórios: identificação de relógios, roupas e acessórios com estilos parecidos.
- 🏠 Decoração: busca de móveis e objetos com características visuais semelhantes.
- 🚗 Autopeças: apoio à identificação visual de componentes.
- 📦 Catálogos digitais: pesquisa de produtos por imagem.
- 🔎 Busca visual: localização de itens semelhantes sem depender de palavras-chave.

---

## 🧠 9. Competências Demonstradas

| Área | Conhecimentos aplicados |
|---|---|
| 🐍 Python | Programação e manipulação de dados |
| 🧠 Deep Learning | Utilização de redes neurais pré-treinadas |
| 🔄 Transfer Learning | Reaproveitamento de modelos existentes |
| 👁️ Computer Vision | Processamento e representação de imagens |
| 🔢 Embeddings | Extração de características vetoriais |
| 📐 Álgebra Linear | Normalização e comparação de vetores |
| 🔍 Machine Learning | Busca por proximidade com k-NN |
| 📊 Visualização | Apresentação dos resultados com Matplotlib |

---

## 🚀 10. Possíveis Melhorias e Evoluções

O projeto pode ser expandido com funcionalidades adicionais:

- 🌐 Desenvolvimento de uma interface web para consultas por imagem.
- 📂 Ampliação do banco de imagens e categorias de produtos.
- ⚡ Otimização da busca para grandes volumes de embeddings.
- 🧠 Comparação entre arquiteturas como ResNet50, MobileNetV2 e EfficientNet.
- 📏 Avaliação de métricas de qualidade das recomendações, como Precision@K e Recall@K.
- 🏷️ Combinação de similaridade visual com filtros de categoria, marca e preço.
- 📈 Desenvolvimento de uma API para integração com plataformas de e-commerce.

---

## ⚠️ Observação sobre o projeto

Este projeto tem finalidade acadêmica e demonstrativa. A similaridade visual é determinada pelas representações aprendidas pelo modelo ResNet50, não significando necessariamente equivalência funcional, compatibilidade técnica ou identidade entre os produtos recomendados.

Os resultados dependem da qualidade das imagens, da diversidade do banco de dados e das características visuais aprendidas pelo modelo.

---

## 🏁 Conclusão

O projeto demonstra a aplicação prática de Deep Learning e Transfer Learning na construção de um sistema de recomendação baseado em imagens.

A utilização da ResNet50 permite transformar imagens em representações vetoriais, enquanto a normalização L2 e o algoritmo k-NN com distância cosseno possibilitam realizar buscas por proximidade visual.

A solução apresenta uma alternativa aos sistemas tradicionais baseados exclusivamente em atributos textuais, explorando o potencial da visão computacional para melhorar a experiência de busca e descoberta de produtos em ambientes digitais.

**Projeto acadêmico | Python | Deep Learning | Computer Vision | Image Similarity | Recommendation Systems**
