# FLEET: Otimização Inteligente de Pátios de Motocicletas - Prova de Conceito com Visão Computacional

## 📖 Descrição

Este repositório contém a Prova de Conceito (POC) desenvolvida para o projeto FLEET, que visa criar um sistema inteligente para otimização e controle de pátios de motocicletas. Esta POC foca na aplicação de técnicas de Visão Computacional para:
1.  Detectar motocicletas em imagens de pátios.
2.  Analisar a distribuição espacial das motocicletas detectadas.
3.  Sugerir potenciais zonas de estacionamento através de algoritmos de clusterização.

Este trabalho é parte da disciplina de DISRUPTIVE ARCHITECTURES: IOT, IOB & GENERATIVE IA do curso de Análise e Desenvolvimento de Sistemas da FIAP.

## 📂 Conteúdo do Repositório

* **/datasets/yolo_motorcycle_detector/**: Contém o arquivo `data.yaml` que descreve a estrutura do dataset de motocicletas utilizado para treinar o modelo YOLO.
    * **Nota:** As imagens e arquivos de anotação do dataset são armazenados no Google Drive devido ao tamanho e não estão versionados completamente neste repositório apesar 6 imagens e anotações de referência. Para acesso total ao conteúdo do dataset acesse: https://drive.google.com/drive/folders/12NsZ9NkLxkPyr8loIFLZ2ITJUFmwes8f?usp=sharing
* **/notebooks/**: Contém os Jupyter Notebooks desenvolvidos em Google Colab para:
    * `01_YOLO_Training_Motorcycle_Detector.ipynb`: Treinamento e fine-tuning do modelo YOLOv8n para detecção de motocicletas. Inclui análise de métricas de treinamento e validação. Link: https://colab.research.google.com/drive/1FweJfX52vQ8ZmeuugqhhrLn7oBnjDX8G?usp=sharing
    * `02_Main_Inference_Pipeline.ipynb`: Script principal para carregar o modelo treinado (`best.pt`), realizar detecções em imagens, aplicar clusterização e visualizar os resultados (incluindo sugestão de zonas). Link: https://colab.research.google.com/drive/1XjLhmshpXSGpRcrjVRkAIWYjTzhf-2ed?usp=sharing
* **/trained_models/yolo_detector/**: Pesos do modelo treinado (`best.pt` da run `yolov8n_motorbike_detector_run1`) são armazenados após o treinamento.
* **/test_media/images/**: Contém imagens de exemplo para rodar a inferência e a análise de clusterização.
* `README.md`: Este arquivo.

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python
* **Ambiente Principal:** Google Colaboratory (Colab)
* **Detecção de Objetos:** Ultralytics YOLOv8 (especificamente `YOLOv8n`)
* **Machine Learning / Data Science:**
    * Scikit-learn (para K-Means clustering)
    * Pandas (para manipulação de dados)
    * NumPy (para operações numéricas)
* **Visualização:** Matplotlib, Seaborn, OpenCV (para manipulação e exibição de imagens)
* **Controle de Versão:** Git e GitHub
* **Armazenamento de Dados (Datasets/Modelos Pesados):** Google Drive

## 📊 Resultados Parciais Obtidos (Detector YOLOv8n - `best.pt`)

Após o treinamento do modelo `YOLOv8n` por 30 épocas no dataset, o modelo `best.pt` apresentou os seguintes resultados no **conjunto de teste**:

* **mAP@0.50-0.95 (Teste):** 0.5388
* **mAP@0.50 (Teste):** 0.8789
* **Precision (P) (Teste):** 0.8904
* **Recall (R) (Teste):** 0.8116

Estes resultados indicam uma boa capacidade do modelo em detectar motocicletas com alta precisão e um recall robusto, validando a viabilidade técnica da abordagem de detecção para este POC. A análise das curvas de treinamento (perda, precisão, recall, mAP) e gráficos diagnósticos (Curva PR, Matriz de Confusão) podem ser encontradas no notebook `01_YOLO_Training_Motorcycle_Detector.ipynb`.

## 🚀 Instruções de Uso/Execução

Este projeto foi desenvolvido para ser executado em ambiente Google Colaboratory.

### Pré-requisitos

* Conta Google para acesso ao Google Colab e Google Drive.
* Dataset (disponível em [https://drive.google.com/drive/folders/12NsZ9NkLxkPyr8loIFLZ2ITJUFmwes8f?usp=sharing]).

### Configuração do Ambiente no Google Drive

1.  Crie uma pasta principal no seu Google Drive, por exemplo: `fleet_cv_project`.
2.  Clone este repositório GitHub para sua máquina local e, em seguida, faça upload da estrutura de pastas e arquivos (exceto os datasets pesados) para dentro da pasta `fleet_cv_project` no seu Google Drive. Alternativamente, crie as pastas manualmente no Drive e faça upload dos arquivos.
3.  **Estrutura de Pastas Esperada no Google Drive (dentro de `fleet_cv_project`):**
    ```
    fleet_cv_project/
    ├── datasets/
    │   └── yolo_motorcycle_detector/  # Coloque o dataset "Motorbike - v7" aqui
    │       ├── train/
    │       │   ├── images/
    │       │   └── labels/
    │       ├── valid/
    │       │   ├── images/
    │       │   └── labels/
    │       ├── test/
    │       │   ├── images/
    │       │   └── labels/
    │       └── data.yaml
    │
    ├── notebooks/                 # Contém os .ipynb
    ├── trained_models/            # Onde os modelos treinados serão salvos
    │   └── yolo_detector/
    ├── test_media/
    │   └── images/                # Coloque aqui a imagens para teste
    └── ... (outros arquivos do repo)
    ```
4.  Certifique-se que o arquivo `data.yaml` dentro de `datasets/yolo_motorcycle_detector/` aponta corretamente para as pastas `train`, `valid`, e `test` (ex: `train: train/images`, `val: valid/images`).

### Executando os Notebooks

1.  Abra o Google Colab e navegue até a pasta `notebooks` no seu Google Drive.
2.  **`01_YOLO_Training_Motorcycle_Detector.ipynb`:**
    * Este notebook treina o modelo YOLOv8n.
    * **Primeira Célula:** Monte seu Google Drive.
    * **Segunda Célula:** Instale `ultralytics`.
    * **Células de Configuração de Caminhos:** **Verifique e ajuste** a variável `PROJECT_FOLDER_NAME` (para `fleet_cv_project` ou o nome que você usou) para que os caminhos para o dataset e para salvar os modelos estejam corretos.
    * Execute as células sequencialmente para treinar o modelo. Os resultados e o `best.pt` serão salvos na pasta `trained_models/yolo_detector/NOME_DO_EXPERIMENTO/`.
    * As células subsequentes neste notebook realizam a análise das métricas de treinamento e validação (incluindo os gráficos que geramos).
3.  **`03_Main_Inference_Pipeline.ipynb` (ou as células correspondentes no notebook de treino):**
    * Este notebook (ou seção) carrega o `best.pt` treinado anteriormente.
    * **Célula de Configurações Iniciais:** Verifique e ajuste os caminhos para `path_to_best_pt` (apontando para o `best.pt` gerado pelo treino) e `test_media_images_path`. Defina `IMAGE_TO_ANALYZE` e `NUM_CLUSTERS`.
    * Execute as células sequencialmente para:
        1.  Ver a imagem com as detecções YOLO.
        2.  Ver o gráfico de dispersão dos centros das motos clusterizados.
        3.  Ver a imagem original com os centroides dos clusters (sugestão de zonas) sobrepostos.

## Próximos Passos

* Aprimorar o modelo YOLO com mais dados, especialmente para cenários de alta oclusão, motos pequenas e vistas de cima.
* Desenvolver o classificador secundário didático.
* Integrar este componente de CV com a solução FLEET baseada em BLE.
* Expandir a análise de zonas para incluir formas e capacidades.