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

8. **cv2.calcHist** = usada para calcular o histograma de uma imagem. O histograma é uma representação estatística da distribuição de intensidades dos pixels em uma imagem, ou seja, mostra quantos pixels têm valores de intensidade em cada intervalo.
   
   * `images`: Uma lista de imagens de entrada para as quais você deseja calcular o histograma. Normalmente, é uma única imagem.
   
   * `channels`: A lista de índices de canais para os quais você deseja calcular o histograma. Por exemplo, para uma imagem colorida BGR, use `[0]` para o canal azul, `[1]` para o canal verde e `[2]` para o canal vermelho.
   
   * `mask`: Uma máscara opcional que define quais pixels serão incluídos no cálculo do histograma. Pixels correspondentes à máscara em branco serão ignorados.
   
   * `histSize`: O número de intervalos (bins) no histograma. Geralmente, é uma lista contendo o número de intervalos para cada canal.
   
   * `ranges`: O intervalo de valores para cada intervalo. Normalmente, é `[0, 256]` para um intervalo de intensidade de pixel de 0 a 255.

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

9. **cv2.Sobel** = é uma técnica de processamento de imagens usada para calcular gradientes de intensidade em uma imagem. Ele é frequentemente usado para detecção de bordas e realce de características nas imagens.
   
   * `src`: Obrigatório. A imagem de entrada na qual você deseja calcular as derivadas de Sobel.
   
   * `ddepth`: Opcional. A profundidade da imagem de saída. Deve ser um valor inteiro, como `-1` (usado para manter a mesma profundidade da imagem de entrada) ou `cv2.CV_64F` (para usar uma imagem de ponto flutuante).
   
   * `dx`: Ordem da derivada em relação ao eixo x (horizontal).  Pode ser `0`, `1` ou `2`.
   
   * `dy`: Ordem da derivada em relação ao eixo y (vertical).    Pode ser `0`, `1` ou `2`.
   
   * `ksize`: Opcional. O tamanho do kernel usado para o cálculo do gradiente. Deve ser um número ímpar, como `1`, `3`, `5`, etc.
   
   * `scale`: Opcional. Um fator de escala aplicado ao resultado da derivada. Pode ser útil para evitar a ampliação de valores após o cálculo.
   
   * `delta`: Opcional. Um valor adicionado ao resultado após a aplicação do fator de escala.

10. **cv2.Canny** = é usada para aplicar o operador Canny para detecção de bordas em uma imagem. Ela ajuda a identificar as bordas dos objetos presentes na imagem, destacando as mudanças abruptas de intensidade.
    
    * `image`: Obrigatório. A imagem de entrada na qual você deseja detectar as bordas.
    
    * `threshold1`: Obrigatório. O primeiro limiar para a histerese. Pixels com gradientes maiores que este valor serão considerados bordas fortes.
    
    * `threshold2`: Obrigatório. O segundo limiar para a histerese. Pixels com gradientes entre `threshold1` e `threshold2` serão considerados bordas fracas, a menos que estejam conectados a pixels de borda fortes.
    
    * `apertureSize`: Opcional. O tamanho da abertura para calcular os gradientes. Deve ser um valor ímpar, geralmente `3`, `5` ou `7`.
    
    * `L2gradient`: Opcional. Um booleano que indica se deve ser usada a norma L2 para calcular os gradientes. Se for `True`, a norma L2 será usada, o que pode fornecer resultados mais precisos. Caso contrário, será usada a norma L1.

```python
path   = cv2.imread('imagens/img-numbers/pexels-magda-ehlers-1339865.jpg',cv2.IMREAD_GRAYSCALE)
sobelx = cv2.Sobel(path,cv2.CV_64F,1,0,ksize=5)
sobelY = cv2.Sobel(path,cv2.CV_64F,0,1,ksize=5)

imageGray = np.sqrt(sobelx**2 + sobelY**2)

plt.imshow(imageGray,cmap='gray')
plt.show()

# Carregar uma imagem em escala de cinza
image = cv2.imread('imagem.jpg', cv2.IMREAD_GRAYSCALE)

# Aplicar o operador Canny para detecção de bordas
threshold1 = 100
threshold2 = 200
edges = cv2.Canny(image, threshold1, threshold2)

# Exibir as bordas detectadas
cv2.imshow('Bordas Detectadas', edges)
```

&nbsp;

11. **cv2.createCLAHE** = é um método de processamento de imagens que melhora o contraste local em regiões da imagem, evitando a amplificação de ruído.
    
    * `clipLimit`: Obrigatório. O limite de recorte que controla a amplificação do contraste. Valores maiores resultam em mais amplificação, mas podem introduzir artefatos. Geralmente, um valor entre 2 e 4 é usado.
    
    * `tileGridSize`: Obrigatório. O tamanho dos blocos nos quais a imagem é dividida. Deve ser uma tupla de dois valores `(width, height)`.
    
    * `Preprocess`: Opcional. Define se algum pré-processamento será aplicado à imagem antes de realizar a equalização. Pode ser `0` para nenhuma alteração ou `cv2.CV_CLAHE_NORMALIZE` para normalização

```python

```

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
