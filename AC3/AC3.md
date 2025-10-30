# Avaliação Continuada 3


### 1. Como o olho humano percebe as cores e a função dos cones

O **sistema visual humano** é composto por estruturas como **córnea**, **cristalino**, **retina** e **nervo óptico**, responsáveis pela captação e transmissão da luz.  
A **retina** contém dois tipos de fotorreceptores:

- **Bastonetes** → atuam na visão **noturna (escotópica)**, distinguindo luz e sombra.  
- **Cones** → atuam na visão **diurna (fotópica)**, responsáveis pela **percepção das cores**.

Segundo a **Teoria Tricromática de Maxwell**, existem **três tipos de cones**, sensíveis a diferentes faixas do espectro visível:

- **Cones L** → sensíveis ao **vermelho (R)** (~700 nm)  
- **Cones M** → sensíveis ao **verde (G)** (~546 nm)  
- **Cones S** → sensíveis ao **azul (B)** (~435 nm)

O **cérebro combina** os sinais desses três tipos de cones para gerar a percepção de milhares de tonalidades. Assim, toda cor percebida é uma **combinação ponderada das intensidades R, G e B**.

---

### 2. Diferença entre os modelos RGB e CMYK (e exemplos)

| Aspecto | **RGB** | **CMYK** |
|----------|----------|-----------|
| Tipo de mistura | Aditiva (adição de luz) | Subtrativa (absorção de pigmentos) |
| Cores primárias | Vermelho (R), Verde (G), Azul (B) | Ciano (C), Magenta (M), Amarelo (Y), Preto (K) |
| Origem | Luz emitida (monitores, TVs) | Luz refletida (impressão, pigmentos) |
| Resultado da soma máxima | Branco (R+G+B) | Preto (C+M+Y) |
| Exemplo de uso | Telas de computador, smartphones | Impressoras, revistas, fotografias impressas |

O **modelo RGB** é o sistema **aditivo**, utilizado em **dispositivos emissores de luz**, enquanto o **CMYK** é **subtrativo**, utilizado em **sistemas reflexivos**, como impressão.

---

### 3. Conceito de cor aditiva e subtrativa

- **Cor Aditiva (luz):**
  - Ocorre pela **adição de luz** de diferentes cores primárias (R, G, B).  
  - A ausência de luz resulta em **preto**, e a soma máxima em **branco**.  
  - Aplicação: monitores, TVs, projetores.  
  - Exemplo: um pixel de tela que combina luz vermelha e verde forma **amarelo**.

- **Cor Subtrativa (pigmento):**
  - Baseia-se na **absorção de determinadas frequências de luz**.  
  - Mistura das primárias C, M, Y gera tons escuros até o preto.  
  - Aplicação: impressão, pintura e fotografia analógica.  
  - Exemplo: ao misturar tinta amarela e ciano, obtemos **verde**.

Essas duas formas são complementares — **o CMY é o inverso do RGB**.

---

## Aplicação Prática

O **sensoriamento remoto por satélite** consiste em captar, via satélite ou outro veículo orbital, a radiação refletida ou emitida pela superfície terrestre ou pela atmosfera, em diferentes comprimentos de onda.  
Esses dados permitem **inferir propriedades do solo, vegetação, água e atmosfera**, entre outros elementos.

---

## 1. Aplicações Principais

- **Monitoramento agrícola:** análise da saúde da vegetação, produtividade, irrigação e uso do solo.  
- **Mapeamento de uso e cobertura da terra:** identificação de expansão urbana, desmatamento e áreas agrícolas.  
- **Monitoramento ambiental e de desastres naturais:** detecção de secas, inundações, erosão e qualidade da água.  
- **Meteorologia e clima:** estudo de nuvens, umidade, vapor d’água e tempestades.  
- **Oceanografia:** análise da temperatura da superfície do mar, correntes e concentração de clorofila.

---

## 2. Espaços de Cores em Imagens de Satélite

Imagens multiespectrais de satélite registram informações em várias bandas espectrais (vermelho, verde, azul, infravermelho, etc.).  
Ao mapear três dessas bandas nos canais **R (Red)**, **G (Green)** e **B (Blue)**, formamos diferentes **espaços de cores**.

A seguir, dois dos mais comuns:

---

### 2.1 Espaço de Cor Natural (True Color)

**Descrição:**  
- Usa as bandas visíveis (vermelho, verde e azul) mapeadas diretamente para R, G e B.  
- O resultado é uma imagem semelhante à visão humana.

**Mapeamento típico:**  
- R = Banda Vermelha  
- G = Banda Verde  
- B = Banda Azul

**Vantagens:**  
- Representação realista e intuitiva.  
- Facilita a interpretação visual da paisagem.

**Limitações:**  
- Fenômenos fora do espectro visível (como umidade do solo ou vigor da vegetação) não são destacados.

**Exemplo (True Color):**  
![Imagem True Color](https://earthobservatory.nasa.gov/blogs/elegantfigures/wp-content/uploads/sites/4/2013/10/00_mtjefferson_oli_2013225_crop.jpg)

Na imagem acima, a vegetação aparece em verde, a água em azul escuro e o solo em tons de marrom ou cinza.

---

### 2.2 Espaço de Cor Falsa (False Color Composite)

**Descrição:**  
- Utiliza bandas fora do visível (como o infravermelho próximo — NIR) e as associa aos canais RGB.  
- Permite destacar propriedades invisíveis ao olho humano.

**Mapeamento típico (Landsat):**  
- R = Banda Infravermelha Próxima (NIR)  
- G = Banda Vermelha  
- B = Banda Verde

**Vantagens:**  
- Realça a vegetação saudável (em tons de vermelho intenso).  
- Facilita a distinção entre solo, áreas urbanas e corpos d’água.  
- Excelente para estudos de uso do solo, agricultura e meio ambiente.

**Exemplo (False Color):**  
![Imagem False Color](https://gsp.humboldt.edu/olm/Courses/GSP_216/images/false-color.jpg)

Aqui, a vegetação saudável aparece em vermelho, áreas urbanas em tons acinzentados e corpos d’água em azul escuro.

---

## 3. Conclusão

O uso de diferentes **espaços de cores** em imagens de satélite permite visualizar e interpretar informações distintas da superfície terrestre.  
Enquanto o **True Color** é útil para visualização natural, o **False Color** destaca aspectos invisíveis ao olho humano, sendo fundamental para **monitoramento ambiental, análise agrícola e detecção de mudanças**.

---

### Referências

- [NASA Earth Observatory – How to Interpret a False-Color Satellite Image](https://science.nasa.gov/earth/earth-observatory/how-to-interpret-a-false-color-satellite-image/)
- [Applied Sciences – NASA Remote Sensing for Agriculture](https://appliedsciences.nasa.gov/)
- [NOAA Satellite and Information Service](https://www.nesdis.noaa.gov/)
- [ESA Earth Observation Portal](https://www.esa.int/Applications/Observing_the_Earth)

---

