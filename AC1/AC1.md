
## 1) Síntese de Imagens (Computação Gráfica)

**O que é (em poucas palavras):**  
Gerar imagens **a partir de modelos ou fórmulas**. Em vez de “editar” uma foto, aqui nós **criamos** a cena: formas, cores, iluminação, câmera.

**Exemplo simples:**  
Gerar e renderizar uma **superfície 3D** definida por uma função matemática.

**Como executar**
```bash
python -m venv .venv && source .venv/bin/activate   # Linux/macOS
# No Windows: .venv\Scripts\activate
pip install matplotlib numpy
python cg_superficie3d.py
```

**Código (independente) – inspirado na gallery oficial do Matplotlib**  
Crie um arquivo `cg_superficie3d.py` com:
```python
# cg_superficie3d.py
# Inspirado na Matplotlib Gallery: 3D surface (licença compatível da doc oficial)
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import cm

# cria uma grade 2D
x = np.linspace(-6, 6, 200)
y = np.linspace(-6, 6, 200)
X, Y = np.meshgrid(x, y)

# superfície: Z é função de X e Y (síntese, não edição)
R = np.sqrt(X**2 + Y**2) + 1e-6
Z = np.sin(R) / R

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
surf = ax.plot_surface(X, Y, Z, cmap=cm.viridis, linewidth=0, antialiased=True)
ax.set_title("Síntese: superfície 3D criada por função matemática")
fig.colorbar(surf, shrink=0.6, aspect=10)
plt.show()
```

**Por que isso é CG?**  
Porque **criamos** a imagem a partir de uma **descrição matemática** (modelo), controlando câmera e aparência.

---

## 2) Processamento de Imagens

**O que é:**  
Aplicar **operações** para **melhorar ou transformar** uma imagem que **já existe** (filtros, detecção de bordas, equalização de histograma, etc.). Não reconhece “o que é” a imagem, apenas **processa** os pixels.

**Exemplo simples:**  
Gerar uma imagem sintética com formas (retângulos/círculos) e aplicar **detecção de bordas de Canny**.

**Como executar**
```bash
python -m venv .venv && source .venv/bin/activate
pip install opencv-python matplotlib numpy
python pi_canny_sintetico.py
```

**Código (independente) – baseado no uso comum do OpenCV Canny**  
Crie `pi_canny_sintetico.py`:
```python
# pi_canny_sintetico.py
# Baseado em exemplos públicos do OpenCV (Canny)
import cv2
import numpy as np
import matplotlib.pyplot as plt

# cria imagem sintética em tons de cinza
img = np.zeros((300, 400), dtype=np.uint8)
cv2.rectangle(img, (50, 50), (180, 200), 180, -1)     # retângulo cinza
cv2.circle(img, (280, 150), 60, 255, -1)              # círculo branco
cv2.line(img, (20, 260), (380, 260), 200, 5)          # linha

# aplica Canny (bordas)
edges = cv2.Canny(img, 100, 200)

# mostra lado a lado
plt.figure(figsize=(8,3))
plt.subplot(1,2,1); plt.imshow(img, cmap="gray"); plt.title("Imagem sintética"); plt.axis("off")
plt.subplot(1,2,2); plt.imshow(edges, cmap="gray"); plt.title("Bordas (Canny)"); plt.axis("off")
plt.tight_layout(); plt.show()
```

**Por que isso é Processamento?**  
Porque partimos de uma **imagem** (mesmo que criada na hora) e aplicamos um **filtro** (Canny) para **transformar/realçar** informações de borda.

---

## 3) Visão Computacional

**O que é:**  
Fazer o computador **entender** o conteúdo da imagem/vídeo (reconhecer, classificar, detectar). Aqui a saída é **semântica** (rótulos, classes), não apenas pixels transformados.

**Exemplo simples:**  
Usar o dataset **Digits** do scikit‑learn (imagens 8×8 de dígitos) e treinar um classificador **SVM** simples. 

**Como executar**
```bash
python -m venv .venv && source .venv/bin/activate
pip install scikit-learn numpy
python vc_digits_svm.py
```

**Código (independente) – inspirado na doc oficial do scikit‑learn**  
Crie `vc_digits_svm.py`:
```python
# vc_digits_svm.py
# Inspirado em exemplos da documentação do scikit-learn (licença BSD-3)
from sklearn import datasets, svm, metrics
from sklearn.model_selection import train_test_split

# carrega imagens de dígitos (8x8 pixels)
digits = datasets.load_digits()
X = digits.images.reshape((len(digits.images), -1))  # achata para vetores
y = digits.target

# separa treino/teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=0)

# classificador simples (SVM)
clf = svm.SVC(gamma=0.001)
clf.fit(X_train, y_train)

# avalia
pred = clf.predict(X_test)
acc = metrics.accuracy_score(y_test, pred)
print(f"Acurácia no teste: {acc:.4f}")
```

**Por que isso é Visão?**  
Porque o sistema **aprende a reconhecer** o **conteúdo** da imagem (qual dígito é), produzindo uma **classe** como resposta.

---

## 4) Visualização Computacional

**O que é:**  
Transformar **dados** em **gráficos** que facilitam enxergar padrões. A ideia é ajudar pessoas a entenderem informações complexas.

**Exemplo simples:**  
Aplicar **PCA** para reduzir o dataset **Iris** (4 dimensões) para 2D e **plotar** os pontos.

**Como executar**
```bash
python -m venv .venv && source .venv/bin/activate
pip install scikit-learn matplotlib
python vis_pca_iris.py
```

**Código (independente) – inspirado em exemplo oficial do scikit‑learn**  
Crie `vis_pca_iris.py`:
```python
# vis_pca_iris.py
# Inspirado no exemplo plot_pca_iris da doc do scikit-learn (licença BSD-3)
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.decomposition import PCA

iris = load_iris()
X, y = iris.data, iris.target

# reduz de 4D para 2D
X2 = PCA(n_components=2).fit_transform(X)

plt.scatter(X2[:, 0], X2[:, 1], c=y)
plt.title("Iris em 2D com PCA (Visualização)")
plt.xlabel("PC1"); plt.ylabel("PC2")
plt.show()
```

**Por que isso é Visualização?**  
Porque pegamos **dados numéricos** e os **mapeamos** em um gráfico que permite **ver** agrupamentos e diferenças.

---

## Fechando
- **CG (Síntese):** cria pixels a partir de modelos.  
- **Processamento:** transforma pixels já existentes.  
- **Visão:** interpreta o conteúdo e devolve significado (classe/objeto).  
- **Visualização:** converte dados em gráficos para humanos entenderem.
