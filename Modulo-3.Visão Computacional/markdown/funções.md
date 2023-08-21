## Funções

```python
import cv2
```

1. **cv2.imread** = carrega a imagem.
   
   * `filemane` : caminho do arquivo
   
   * `flags` : Opcional. Parâmetro que define como a imagem deve ser lida. Pode ser uma combinação de várias constantes pré-definidas.
     
     - `cv2.IMREAD_COLOR` (ou 1): Carrega a imagem colorida (padrão).
     
     - `cv2.IMREAD_GRAYSCALE` (ou 0): Carrega a imagem em escala de cinza.
     
     - `cv2.IMREAD_UNCHANGED` (ou -1): Carrega a imagem com todos os canais, incluindo.
     
     - `cv2.IMREAD_ANYCOLOR`: Carrega a imagem, independentemente do número de canais.
     
     - `cv2.IMREAD_ANYDEPTH`: Carrega a imagem, independentemente da profundidade de bits.
     
     - `cv2.IMREAD_IGNORE_ORIENTATION`: Ignora a orientação de rotação da imagem se ela estiver armazenada nas tags de orientação do EXIF.
   
   &nbsp;

2. **cv2.cvtColor** = 
   
   * **src**: Obrigatório. A imagem de entrada que você deseja converter.
   
   * **code**: Obrigatório. O código de conversão que define a transformação de cores a ser aplicada. O código é uma constante que define a conversão desejada. Algumas constantes comuns incluem:
     
     - `cv2.COLOR_BGR2GRAY`: Converte de BGR para escala de cinza.
     
     - `cv2.COLOR_BGR2RGB`: Converte de BGR para RGB.
     
     - `cv2.COLOR_BGR2HSV`: Converte de BGR para HSV (Hue, Saturation, Value).
     
     - `cv2.COLOR_BGR2LAB`: Converte de BGR para CIELAB.
     
     - `cv2.COLOR_BGR2XYZ`: Converte de BGR para CIE 1931 XYZ.

```python
import cv2
import matplotlib.pyplot as plt

imagem = cv2.imread('imagens/img-gato/edgar-nKC772R_qog-unsplash.jpg')
imagem = cv2.cvtColor(imagem,cv2.COLOR_BGR2RGB)


plt.imshow(imagem)
plt.show()
```

3. **cv2.spit** = Essa função é usada para separar uma imagem em seus canais individuais.

```python
b, g, r = cv2.split(imagem)

plt.figure(figsize=(15,5))
plt.subplot(1,3,1)
plt.imshow(b)

plt.subplot(1,3,2)
plt.imshow(g)

plt.subplot(1,3,3)
plt.imshow(r)
plt.show()
```

&nbsp;

4. **cv2.resize**
   
   * **src**: Obrigatório. A imagem de entrada que você deseja redimensionar.
   
   * **dsize**: Obrigatório. O tamanho desejado para a imagem de saída. Pode ser uma tupla `(width, height)` especificando a largura e a altura.
   
   * **fx**: Opcional. Fator de escala horizontal. Se `fx` for especificado, o parâmetro `dsize` será ignorado.
   
   * **fy**: Opcional. Fator de escala vertical. Se `fy` for especificado, o parâmetro `dsize` será ignorado.
   
   * **interpolation**: Opcional. Método de interpolação a ser usado durante o redimensionamento. Alguns dos métodos mais comuns sã
     
     - `cv2.INTER_LINEAR`: Interpolação bilinear (padrão), boa para a maioria dos casos.
     
     - `cv2.INTER_NEAREST`: Interpolação por vizinho mais próximo.
     
     - `cv2.INTER_CUBIC`: Interpolação cúbica.
     
     - `cv2.INTER_LANCZOS4`: Interpolação Lanczos.

&nbsp;

5. **cv2.blur** = é usada para aplicar um filtro de média (também conhecido como desfoque médio) a uma imagem.
   
   * `src`: Obrigatório. A imagem de entrada na qual você deseja aplicar o desfoque.
   
   * `ksize`: Obrigatório. O tamanho do kernel do filtro. Deve ser um número ímpar positivo. Quanto maior o valor, maior será o desfoque.

```python
imagemR = cv2.resize(src=imagem,dsize=(50,300))
plt.imshow(imagemR)
plt.show()
```

&nbsp;

6. **cv2.GaussianBlur** = é usada para aplicar um desfoque gaussiano a uma imagem. O desfoque gaussiano é um método de suavização que reduz o ruído na imagem e cria um efeito de desfoque suave. Ele é especialmente útil para remover ruídos de alta frequência.
   
   * `src`: Obrigatório. A imagem de entrada na qual você deseja aplicar o desfoque gaussiano.
   
   * `ksize`: Obrigatório. O tamanho do kernel do filtro gaussiano. Deve ser um número ímpar positivo. Quanto maior o valor, maior será o desfoque.
   
   * `sigmaX`: Opcional. O desvio padrão no eixo X. Se não especificado, o OpenCV calculará automaticamente com base no tamanho do kernel.
   
   * `sigmaY`: Opcional. O desvio padrão no eixo Y. Se não especificado, será usado o valor de `sigmaX`.

```python
gaussinb = cv2.GaussianBlur(imagemZero,(101,101),sigmaX=6)
plt.imshow(gaussinb,cmap='gray')
```

&nbsp;

7. **cv2.convertScaleAbs** = realce 
   
   * `src`: Obrigatório. A imagem de entrada que você deseja converter.
   
   * `alpha`: Opcional. O fator de escala para multiplicar os valores dos pixels na imagem.
   
   * `beta`: Opcional. O valor a ser adicionado aos valores dos pixels após a multiplicação por `alpha`.

```python
scale = cv2.convertScaleAbs(imagemZero,alpha=1.5,beta=100)
plt.imshow(scale,cmap='gray')
plt.show()
```

&nbsp;

8. **cv2.calcHist** = usada para calcular o histograma de uma imagem. O histograma é uma representação estatística da distribuição de intensidades dos pixels em uma imagem, ou seja, mostra quantos pixels têm valores de intensidade em cada intervalo. Isso é útil para análise de imagem, processamento de imagem e várias tarefas de visão computacional.
   
   * **images**: Uma lista de imagens de entrada para as quais você deseja calcular o histograma. Normalmente, é uma única imagem.
   
   * **channels**: A lista de índices de canais para os quais você deseja calcular o histograma. Por exemplo, para uma imagem colorida BGR, use `[0]` para o canal azul, `[1]` para o canal verde e `[2]` para o canal vermelho.
   
   * **mask**: Uma máscara opcional que define quais pixels serão incluídos no cálculo do histograma. Pixels correspondentes à máscara em branco serão ignorados.
   
   * **histSize**: O número de intervalos (bins) no histograma. Geralmente, é uma lista contendo o número de intervalos para cada canal.
   
   * **ranges**: O intervalo de valores para cada intervalo. Normalmente, é `[0, 256]` para um intervalo de intensidade de pixel de 0 a 255.

```python
imagemZero = cv2.imread('imagens/img-passaro/pexels-roshan-kamath-1661179.jpg',cv2.IMREAD_GRAYSCALE)

hist = cv2.calcHist(imagemZero,[0],None, [256], [0, 256])

histimage = cv2.equalizeHist(imagemZero)

histhistimage = cv2.calcHist(histimage,[0],None, [256], [0, 256])


plt.figure(figsize=(10,8))
plt.subplot(2,2,1)
plt.imshow(imagemZero,cmap='gray')

plt.subplot(2,2,3)
plt.plot(hist)


plt.subplot(2,2,2)
plt.imshow(histimage,cmap='gray')

plt.subplot(2,2,4)
plt.plot(histhistimage)


plt.show()

```

&nbsp;



### 

### Imagens e suas propriedades

1. **imagem.shape** 
   
   * height
   * width
   * channels

2. **max**

3. **min**

4. **mean**

5. **std**

6. **transpose**

7. **dtype**

```python
print(f'\
valor maximo :{imagem.max()}           \n\
valor minimo :{imagem.min()}            \n\
media        :{imagem.mean()}            \n\
transpose    :{imagem.transpose()[1,1]}   \n\
')
```
