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

4. **cv2.resize**
   
   * **src**: Obrigatório. A imagem de entrada que você deseja redimensionar.
   *  **dsize**: Obrigatório. O tamanho desejado para a imagem de saída. Pode ser uma tupla `(width, height)` especificando a largura e a altura.
   * **fx**: Opcional. Fator de escala horizontal. Se `fx` for especificado, o parâmetro `dsize` será ignorado.
   * **fy**: Opcional. Fator de escala vertical. Se `fy` for especificado, o parâmetro `dsize` será ignorado.
   * **interpolation**: Opcional. Método de interpolação a ser usado durante o redimensionamento. Alguns dos métodos mais comuns sã
     - o:`cv2.INTER_LINEAR`: Interpolação bilinear (padrão), boa para a maioria dos casos.
     
     - `cv2.INTER_NEAREST`: Interpolação por vizinho mais próximo.
     
     - `cv2.INTER_CUBIC`: Interpolação cúbica.
     
     - `cv2.INTER_LANCZOS4`: Interpolação Lanczos.

&nbsp;

5. **cv2.blur** = é usada para aplicar um filtro de média (também conhecido como desfoque médio) a uma imagem.
   
   * `src`: Obrigatório. A imagem de entrada na qual você deseja aplicar o desfoque.
   
   * `ksize`: Obrigatório. O tamanho do kernel do filtro. Deve ser um número ímpar positivo. Quanto maior o valor, maior será o desfoque.

&nbsp;

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
