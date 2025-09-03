# Atividade – Computação Visual (versão expandida)

## Objetivo
Demonstrar as diferenças e principais características das áreas relacionadas à **Computação Visual**:  
- **Síntese de Imagens (Computação Gráfica)**  
- **Processamento de Imagens**  
- **Visão Computacional (Artificial)**  
- **Visualização Computacional**

Para cada área, incluí:
1) **Explicação conceitual ampliada**;  
2) **Aplicação real com repositório público** (link e instruções de execução);  
3) **Trecho executável** (adaptado do repositório citado) com comentários;  
4) **Aspectos específicos da área** destacados no código.

> **Importante**: Os trechos abaixo foram **adaptados** de repositórios públicos e documentações oficiais, com os devidos créditos.
Links originais estão em cada seção.

---

## Diferenças – visão geral rápida

| Área                         | Pergunta que responde                                   | Entrada típica                 | Saída típica                               | Núcleo técnico dominante                    | Exemplos comuns                                                |
|-----------------------------|----------------------------------------------------------|-------------------------------|--------------------------------------------|---------------------------------------------|----------------------------------------------------------------|
| **Computação Gráfica**      | *Como **gerar** uma imagem/modelo?*                     | Parâmetros geom./físicos      | Imagem/Animação sintetizada                | Modelagem, renderização, shaders, rasterização ou ray tracing  | Jogos, filmes, CAD, simulações                                 |
| **Processamento de Imagens**| *Como **melhorar/transformar** esta imagem?*            | Imagem existente              | Imagem transformada/realçada               | Filtros, convolução, morfologia, FFT                          | Remoção de ruído, equalização, detecção de bordas              |
| **Visão Computacional**     | *O que **significa** o conteúdo desta imagem/vídeo?*     | Imagem/vídeo                  | Rótulos, caixas, máscaras, medições        | ML/DL (CNNs), detecção, segmentação, rastreamento             | Reconhecimento facial, OCR, carros autônomos                   |
| **Visualização Computacional** | *Como **compreender** dados complexos via gráficos?* | Dados multidimensionais       | Gráficos 2D/3D/Interativos                 | Redução de dimensionalidade, mapeamento visual                 | Dashboards, gráficos científicos, mapas 3D                     |

---

## 1) Síntese de Imagens (Computação Gráfica)

**Conceito ampliado.** Gera imagens a partir de **modelos** (geometria, materiais, luzes, câmera) e **métodos de renderização** (rasterização, ray tracing, path tracing). A ênfase está na **formação de imagem** realista/estilizada, física de luz, texturização, sombreamento e animação.

**Repositório/Referência pública:**  
- *Matplotlib Gallery – 3D Surface (colormap)* – exemplo oficial de superfície 3D. (código e explicações)  
  Fonte: https://matplotlib.org/stable/gallery/mplot3d/surface3d.html

### Como executar rapidamente (ambiente local)
```bash
python -m venv .venv && source .venv/bin/activate  # (Linux/macOS)
# No Windows: .venv\Scripts\activate
pip install matplotlib numpy
python superficie3d_demo.py
```

Crie um arquivo `superficie3d_demo.py` com o trecho adaptado abaixo.

### Trecho executável (adaptado da documentação oficial do Matplotlib)
```python
# arquivo: superficie3d_demo.py
# Adaptado da gallery "3D surface (colormap)" do Matplotlib (licença Matplotlib)
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import cm
from matplotlib.ticker import LinearLocator

# grade 2D
x = np.linspace(-6, 6, 200)
y = np.linspace(-6, 6, 200)
X, Y = np.meshgrid(x, y)

# superfície: função radial suave (síntese geométrica)
R = np.sqrt(X**2 + Y**2)
Z = np.sin(R) / (R + 1e-6)

fig, ax = plt.subplots(subplot_kw={"projection": "3d"})
surf = ax.plot_surface(X, Y, Z, cmap=cm.coolwarm, antialiased=False)

ax.zaxis.set_major_locator(LinearLocator(8))
ax.set_title("Síntese: superfície 3D gerada de função matemática")
fig.colorbar(surf, shrink=0.6, aspect=10)
plt.show()
```

**Aspectos de CG no código:** modelagem **analítica** da superfície (função Z=f(x,y)), colormap simulando material/iluminação, câmera implícita e projeção 3D → 2D.


---

## 2) Processamento de Imagens

**Conceito ampliado.** Opera **sobre imagens existentes** para **realçar**, **filtrar**, **transformar** e **segmentar**. Não “entende” semanticamente; o foco é **processo sinal-imagem** (convolução, gradientes, morfologia, espaço de cores, frequências).

**Repositório público (exemplo Canny):**  
- *Ankush251992/OpenCV-Edge-Detection* – script com detecção de bordas Canny e variações.  
  Fonte: https://github.com/Ankush251992/OpenCV-Edge-Detection

### Como executar rapidamente
```bash
python -m venv .venv && source .venv/bin/activate
pip install opencv-python matplotlib
python canny_demo.py --img caminho/para/imagem.jpg --low 100 --high 200
```

Crie `canny_demo.py` com o trecho abaixo (adaptado do padrão de uso do OpenCV Canny).

### Trecho executável (adaptado de repositórios de Canny com OpenCV)
```python
# arquivo: canny_demo.py
# Adaptado de exemplos de Canny em OpenCV (ver repo citado)
import argparse
import cv2
import matplotlib.pyplot as plt

ap = argparse.ArgumentParser()
ap.add_argument("--img", required=True, help="caminho da imagem de entrada")
ap.add_argument("--low", type=int, default=100, help="limiar baixo")
ap.add_argument("--high", type=int, default=200, help="limiar alto")
args = ap.parse_args()

img = cv2.imread(args.img, cv2.IMREAD_GRAYSCALE)
edges = cv2.Canny(img, args.low, args.high)

plt.figure(figsize=(10,4))
plt.subplot(1,2,1); plt.imshow(img, cmap="gray"); plt.title("Original"); plt.axis("off")
plt.subplot(1,2,2); plt.imshow(edges, cmap="gray"); plt.title(f"Canny ({args.low}, {args.high})"); plt.axis("off")
plt.tight_layout(); plt.show()
```

**Aspectos de PI no código:** pipeline clássico **suavização → gradiente → supressão não-máxima → histerese** (Canny). Ajuste de thresholds altera sensibilidade a bordas.


---

## 3) Visão Computacional (Artificial)

**Conceito ampliado.** Procura **interpretar** o conteúdo: classificar objetos, localizar, segmentar e tomar decisões. Usa tanto **métodos clássicos** (Hough, SIFT/ORB) quanto **aprendizado profundo** (CNNs, Transformers). A saída é **semântica** (rótulos, caixas, máscaras).

**Repositório/Exemplo oficial (MNIST CNN – Keras):**  
- *Keras Examples – Simple MNIST convnet* (exemplo oficial com ~99% de acurácia em MNIST).  
  Fonte: https://keras.io/examples/vision/mnist_convnet/

### Como executar rapidamente
```bash
python -m venv .venv && source .venv/bin/activate
pip install --upgrade pip
pip install keras tensorflow numpy matplotlib
python mnist_cnn.py
```

Crie `mnist_cnn.py` com o trecho adaptado abaixo.

### Trecho executável (adaptado de Keras Examples)
```python
# arquivo: mnist_cnn.py
# Adaptado do exemplo "Simple MNIST convnet" (Keras Examples, licença Apache 2.0)
import numpy as np
from tensorflow import keras
from keras import layers

# carregar dados MNIST
(x_train, y_train), (x_test, y_test) = keras.datasets.mnist.load_data()
x_train = x_train.astype("float32") / 255.0
x_test  = x_test.astype("float32") / 255.0
x_train = np.expand_dims(x_train, -1); x_test = np.expand_dims(x_test, -1)

# modelo CNN mínimo
model = keras.Sequential([
    layers.Conv2D(32, 3, activation="relu", input_shape=(28, 28, 1)),
    layers.MaxPooling2D(),
    layers.Conv2D(64, 3, activation="relu"),
    layers.Flatten(),
    layers.Dense(64, activation="relu"),
    layers.Dense(10, activation="softmax"),
])
model.compile(optimizer="adam", loss="sparse_categorical_crossentropy", metrics=["accuracy"])
model.summary()

# treino curto
model.fit(x_train, y_train, epochs=2, batch_size=128, validation_split=0.1)
test_loss, test_acc = model.evaluate(x_test, y_test, verbose=0)
print(f"Acurácia em teste: {test_acc:.4f}")
```

**Aspectos de VC no código:** **aprendizado supervisionado** com **CNN** para reconhecer dígitos; saída **semântica** (classe 0–9). Difere de processamento (que só transforma pixel) e de CG (que gera pixels).


---

## 4) Visualização Computacional

**Conceito ampliado.** Converte **dados** (muitas dimensões) em **gráficos** para revelar padrões/estruturas. Técnicas incluem **PCA/TSNE/UMAP**, mapas de calor, superfícies, gráficos interativos. O foco é **insight humano** por meio de boa codificação visual (posição, cor, forma, tamanho).

**Repositório/Exemplo oficial (Scikit‑learn – PCA Iris):**  
- *scikit‑learn auto_examples/decomposition/plot_pca_iris* – exemplo clássico de PCA no dataset Iris.  
  Fonte: https://scikit-learn.org/stable/auto_examples/decomposition/plot_pca_iris.html

### Como executar rapidamente
```bash
python -m venv .venv && source .venv/bin/activate
pip install scikit-learn matplotlib
python pca_iris.py
```

Crie `pca_iris.py` com o trecho adaptado abaixo.

### Trecho executável (adaptado de scikit‑learn examples)
```python
# arquivo: pca_iris.py
# Adaptado do exemplo "plot_pca_iris" (scikit-learn, licença BSD-3)
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.decomposition import PCA

iris = load_iris()
X, y = iris.data, iris.target
pca = PCA(n_components=2).fit(X)
X2 = pca.transform(X)

plt.figure()
scatter = plt.scatter(X2[:, 0], X2[:, 1], c=y)
plt.legend(*scatter.legend_elements(), title="Classes (Iris)")
plt.xlabel("PC1"); plt.ylabel("PC2"); plt.title("Visualização: PCA em Iris (2D)")
plt.show()
```

**Aspectos de Visualização no código:** **redução de dimensionalidade** para 2D, **mapeamento de cores** por classe e **ênfase em leitura** (rótulos, legenda) para gerar insight.

---

## Conclusão (o que diferencia na prática)

- **CG**: começa com **modelos** → gera **pixels** (síntese).  
- **Processamento**: começa com **pixels reais** → gera **pixels transformados** (melhoria).  
- **Visão**: começa com **pixels reais** → gera **significado** (classes, caixas, máscaras).  
- **Visualização**: começa com **dados** → gera **gráficos** (insights humanos).

Essas áreas **se complementam**: por exemplo, CG pode gerar dados sintéticos para treinar modelos de Visão; Processamento pode preparar imagens antes da Visão; Visualização ajuda humanos a entender tanto dados de Processamento quanto resultados de Visão.

---

## Créditos e referências
- Matplotlib Gallery – 3D Surface (colormap) — documentação oficial.  
- Ankush251992/OpenCV‑Edge‑Detection — repositório OpenCV Canny.  
- Keras Examples — Simple MNIST convnet (Keras).  
- scikit‑learn — plot_pca_iris (exemplo oficial).

