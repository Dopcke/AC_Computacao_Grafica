# Documentação AP2 – Cena Ponte e Abdução 🛸
Link do Drive do Blender e Video - https://drive.google.com/drive/folders/1P3aeJbHZ88_e-igGd_YXWgaLJl0CrCT-?usp=sharing

## 1. Conceito da Animação (O que acontece)

A ideia foi pegar a cena da AP1 (ponte e lago) e dar um final inesperado.

A animação segue este conceito:
* A *Galinha* atravessa a ponte.
* Chegando ao final, um *OVNI* (Objeto Voador Não Identificado) surge no céu noturno.
* O OVNI ativa um *raio trator*.
* A Galinha é puxada para cima, completando a travessia por abdução.
* A *câmera* faz um tour suave seguindo a ação.

---

## 2. Materiais e Texturas (Como a cena parece)

Para deixar a cena realista (usando PBR/Principled BSDF), utilizei os seguintes materiais:


### 🪵 Materiais Aplicados
| Objeto | Material/Textura | Técnica-Chave |
| :--- | :--- | :--- |
| *Ponte* | Madeira PBR | Usei *Texturas UV* com mapas de *Normal* e *Roughness* para fazer a madeira parecer áspera e antiga. |
| *Terreno* | Grama | Material simples com rugosidade alta, para parecer fosco e natural. |
| *Água do Lago* | Água PBR | Usei o nó *Principled BSDF* com *Transmission* alta (1.0) e *Roughness* baixa (quase espelho). |
| *Movimento da Água* | Shader de Ondas | *Animei* a posição de uma Noise Texture ligada ao *Normal Map* da água para criar ondulações que se movem, sem precisar de simulação pesada (Animação por Keyframes). |

---

## 3. Desafios e Soluções (O que deu errado e como consertei)

### 1. Dificuldade de Visualização (Problema com o PC)
* *O Desafio:* Meu computador é *muito fraco* e não conseguia mostrar as luzes e texturas em tempo real no viewport.
* *A Solução:* Tive que fazer muitos *renders de teste* em baixa qualidade para conferir as cores e o brilho dos materiais, garantindo que o resultado final ficasse correto.

### 2. Movimento Irregular da Câmera
* *O Desafio:* Animar a câmera à mão com keyframes resultou em movimentos "tremidos".
* *A Solução:* Usei uma *Curva (Path)* e apliquei a Constraint *"Follow Path"* na câmera. Isso forçou a câmera a seguir o caminho de forma suave.

### 3. Ajuste de Textura na Ponte
* *O Desafio:* A textura de madeira estava esticada em algumas partes da ponte.
* *A Solução:* Fiz o *UV Unwrapping* da ponte novamente e apliquei o *Scale* (Ctrl+A), corrigindo a distorção.

