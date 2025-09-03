## 1) Síntese de Imagens (Computação Gráfica)

### Explicação
A Computação Gráfica é a arte e a ciência de gerar imagens a partir de modelos matemáticos e computacionais. Em essência, ela constrói representações visuais de objetos e cenas que podem ou não ter uma correspondência com o mundo real. O objetivo é criar imagens sintéticas, realistas ou estilizadas, para uma variedade de aplicações.

### Exemplo
Cria uma figura simples mostrando um círculo colorido gerado com código Python:

```python
import numpy as np
import matplotlib.pyplot as plt

# criando uma grade de pontos
x = np.linspace(-1, 1, 400)
y = np.linspace(-1, 1, 400)
X, Y = np.meshgrid(x, y)

# equação de círculo: x² + y² <= 1
circle = X**2 + Y**2 <= 1

plt.imshow(circle, cmap="viridis")
plt.title("Síntese de Imagem: Círculo gerado por equação")
plt.axis("off")
plt.show()
```

---

## 2) Processamento de Imagens

### Explicação
Diferentemente da Computação Gráfica, o Processamento de Imagens não cria imagens do zero, mas sim manipula imagens existentes para aprimorá-las ou extrair informações. O objetivo é melhorar a qualidade da imagem, remover ruídos, realçar características ou prepará-la para outra aplicação.

### Exemplo
Cria uma imagem artificial em preto e branco e depois aplicar um "inversor de cores":

```python
import numpy as np
import matplotlib.pyplot as plt

# cria uma imagem simples em escala de cinza
img = np.zeros((100, 100), dtype=np.uint8)
img[25:75, 25:75] = 200  # quadrado cinza no meio

# processamento: inverter as cores
img_invertida = 255 - img

plt.subplot(1,2,1)
plt.imshow(img, cmap="gray")
plt.title("Original")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(img_invertida, cmap="gray")
plt.title("Invertida")
plt.axis("off")

plt.show()
```

---

## 3) Visão Computacional

### Explicação
A Visão Computacional vai um passo além do processamento de imagens. Seu objetivo é dotar as máquinas da capacidade de "entender" e interpretar o conteúdo de imagens e vídeos, de forma semelhante à visão humana. Em vez de apenas manipular pixels, ela busca extrair informações semânticas do mundo visual.

### Exemplo
Conta quantos pontos pretos existem em uma imagem binária.

```python
import numpy as np

# cria uma imagem binária com 0 (preto) e 1 (branco)
img = np.array([
    [0,1,0,1,0],
    [1,0,0,1,1],
    [0,0,1,0,0],
    [1,1,0,0,1],
    [0,0,0,1,0]
])

# visão computacional: "entender" algo -> aqui vou contar os pixels pretos
num_pretos = np.sum(img == 0)

print("Número de pixels pretos na imagem:", num_pretos)
```

---

## 4) Visualização Computacional

### Explicação
A Visualização Computacional foca na representação de dados de forma visual e interativa para facilitar a compreensão e a análise. Ela transforma dados abstratos, muitas vezes complexos e multidimensionais, em representações gráficas que permitem aos humanos identificar padrões, tendências e anomalias.

### Exemplo
Pega alguns dados de exemplo (altura e peso de pessoas fictícias) e mostra num gráfico de dispersão.

```python
import matplotlib.pyplot as plt

# dados fictícios
altura = [1.60, 1.65, 1.70, 1.75, 1.80, 1.85]
peso   = [55, 60, 65, 72, 80, 90]

plt.scatter(altura, peso, c="blue", marker="o")
plt.xlabel("Altura (m)")
plt.ylabel("Peso (kg)")
plt.title("Visualização de dados: Altura x Peso")
plt.show()
```

---

## Conclusão
| Área | Entrada Principal | Objetivo Principal | Saída Principal | Exemplo Chave |
| :--- | :--- | :--- | :--- | :--- |
| **Síntese de Imagens (C. Gráfica)** | Descrições Matemáticas/Abstratas | Criar imagens a partir do zero | Imagem Sintética | Renderização 3D |
| **Processamento de Imagens** | Imagem Digital | Melhorar ou modificar uma imagem | Imagem Modificada | Aplicação de Filtros |
| **Visão Computacional** | Imagem ou Vídeo | Interpretar e entender o conteúdo visual | Descrição do Conteúdo | Detecção de Objetos |
| **Visualização Computacional**| Conjuntos de Dados | Representar dados para análise humana | Representação Gráfica | Gráficos e Mapas |
