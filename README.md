  # Programa-Delfin-2023
 # Descripción y caracterización para el procesamiento de imágenes ruidosas 
## Capítulo 1: Estado del arte
### ***1.1 (Algo va aquí)***
### ***1.2 ¿Qué es ruido impulsivo "Sal y pimienta" en imágenes?***
El ruido impulsivo o sal y pimienta (salt-and-pepper) se trata de una clase de contaminación que es causada por defectos en los pixeles de los sensores de las cámaras, una locación en memoria del hardware defectuosa o directamente ruido en un canal de transmisión [1].

Estos defectos provocan una imagen corrupta con una serie de pixeles con ruido que solo pueden tomar valores máximos o mínimos de color y esto se conoce coloquialmente como sal y pimienta, donde la sal hace ilusión a todos los pixeles que entran en el valor máximo o blanco y la pimienta son aquellos que alcanzan el valor mínimo o negro.

Por otro lado, el procesamiento de la imagen que realiza después de la captura de esta, requiere de un proceso de detección y eliminación del ruido. En este punto entran los filtros de remoción, siendo el más usual el filtro mediano de tipo no linear que es muy utilizado por su alta eficiencia y buena eliminación de ruido pero con la consideración que con una corrupción mayor de 50% algunos detalles de la imagen original quedaran manchadas.

La ecuación matemática que modela el comportamiento del ruido impulsivo en una imagen es la siguiente:


$$
  P_{sp} ( z )  = \Biggl\{ \hspace{3mm} 
  \begin{align*}
  P_p \hspace{1mm} , \hspace{3mm} z=p \\
  P_s \hspace{1mm} , \hspace{3mm} z=s
    \end{align*}
$$


De la anterior ecuación indicamos que "***z***" es el porcentaje de pixeles que tendrán ruido y para este sea homogéneo  "***z***" se dividira en dos, siendo la mitad corrupción blanca y otra mitad negra.


### ***1.3 ¿Qué es el ruido guassiano en imágenes?***

El ruido gaussiano que se adicionan a una imagen es el que ensucia la señal, de tal manera que se obtienen pixeles al azar por toda la imagen que se guían en su tonalidad en base a una distribución uniforme de color.

Su importancia radica en que debido a que está presente de manera inherente en el ambiente, más por el hecho que los factores que lo generan son muchos y muy diversos, un ejemplo es el ruido blanco que percibe las cuando la señal de la estación de televisión es débil, ahora bien, especificando en las imágenes, a la hora de su obtención o capturo, el ruido gaussiano se genera en ocasiones con baja iluminación donde es más fácil percibir fotones de ruido originados de distintos lugares, pero cabe recalcar que no solo en estas ocasiones este ruido se modela por medio de la distribución normal o de Gauss, si no que también hay casos con la distribución de Poison.

En la mayoría de la literatura cuando se trata de agregar este tipo de ruido a una imagen se guían por la distribución normal estándar donde el valor μ es igual a 0 y solo se hace variar le desviación estándar o en su defecto la varianza, aunque estas dos últimas depende directamente la una de la otra, por ende, mover una hace que la otra también se mueva.

Como último, la ecuación que modela el ruido gaussiano es la misma de la distribución del mismo nombre, pero en este caso, como ya se mencionó, mu o la media (***μ***) lo evaluamos en 0 y variamos la deviación estándar (***σ***).

$$
    P_G = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2}  
$$

### ***1.4 ¿Qué es el filtro de Fourier?***
#### ***1.4.1 ¿Qué son las Series de Fourier?***

Antes de hablar completamente de que es el filtro de Fourier, debemos abordar primero la idea de que es una serie trigonométrica, que se define como una sumatoria infinita de la forma (3), la cual como su nombre lo indica, se trata de una suma de senos y cosenos que están definidos en un periodo de $2\pi$ y donde si alguno de los coeficientes an y bn es diferente de cero, entonces el grado del polinomio es $N$ [7].

$$
\begin{equation}
\frac{a_0}{2} + \sum_{k=1}^{\infty}(a_k\cos{kx} + b_k \sin{kx})
\end{equation}
$$


De ahí nace la función de Fourier

Para ello se sabe que la función de Fourier es:

$$
\begin{equation}
\displaystyle{f(x) = \frac{a_0}{2} + \sum \limits_{n = 1}^\infty \left[ a_n { \cos(n x)} + b_n {\sin(nx)}\right]}
\end{equation}
$$

$f(x)$ es una función periódica para $x\in \left[−\pi, \pi\right]$ de la cual se desea encontrar una representación. $a_{0}$ es una constante,

$$

a_0 = \displaystyle{\frac{1}{L} \int \limits_{-L}^{L} f(x) dx },
$$

$a_{n}$ y $b_{n}$ se definen como:

$$
a_n = \displaystyle{\frac{1}{L} \int \limits_{-L}^{L} f(x) {\cos(\frac{n\pi x}{L}) }dx },
$$

$$
b_n = \displaystyle{\frac{1}{L} \int \limits_{-L}^{L} f(x) {\sin(\frac{n\pi x}{L}) }dx }.

$$

Esta misma nace de su versión compleja la cual es la serie compleja de Fourier, que es una herramienta matemática muy importante para tratar problemas de funciones periódicas al descomponer una función $f(t)$ como una combinación lineal de funciones armónicas y presenta sus coeficientes como una función discreta que depende de las frecuencias armónicas de la serie, pero no todas las funciones son periódicas por lo que es necesario desarrollar un procedimiento [8].


$$
\begin{equation}
f(t) = \sum_{n=-\infty}^{\infty} \frac{1}{T} \int_{-T/2}^{T/2} f(τ)e^{-ω_n τ} dτ e^{ω_n τ}
\end{equation}
$$

#### ***1.4.2 ¿Qué es la tranformada de Fourier?***

Las Transformada de Fourier se define como una función matemática que al igual que transformada de Laplace, permite como primera línea, el transformar un problema complicado en otro más fácil de resolver y luego obtener la solución al problema original por medio de la función inversa de la transformada de Fourier, resolviendo el problema, y la transformada se expresa de la siguientes maneras:

$\bullet$Continua:

$$
X(F) =  \displaystyle\int_{-\infty}^{\infty} x(t)  e^{-j2\pi Ft} dt 
$$
<br>

$\bullet$Discreta:
$$
X_{k} = \displaystyle\sum_{n=0}^{N-1} x_{n} \cdot e^{-\frac{j2\pi kn}{N}}
$$

<br>
Dónde: 
<br>

$\bullet$ Frecuencia $F=\frac{k}{N}$ <br>
$\bullet$ Timpo $n=t$


La transformada tiene muchas aplicaciones como en el análisis de señales en el dominio de la frecuencia de un sistema lineal y las ecuaciones diferenciales lineales no son la excepción dado que la respuesta también puede estudiarse en el dominio de la frecuencia, donde es posible identificar la relación de la señal de entrada con la señal de salida mediante un producto de funciones. [8]
 
#### ***1.4.3 ¿Qué es la tranformada de Fourier?***

Ahora bien, siendo más específicos en la aplicación de la transformada de Fourier, tenemos al filtrado de señales, donde como su nombre lo indica se aplica la transformada de Fourier para obtener las frecuencias más importantes de la señal descartando así ruido en general que se encuentra fuera del espectro de la señal, y tomando la idea de que al final una imagen se puede traducir o pasar a una señal de varios canales, nos lleva a la conclusión que una imagen puede ser filtrado por Fourier para sacar el ruido que pueda tener esta imagen.


Esta misma conclusión lleva a la existencia del filtro de Fourier, que obtiene los datos más representativos de la imagen y los aísla de tal manera que definiendo un círculo de corte que solo contenga lo más importante de la imagen, podemos eliminar hasta determinado punto el ruido en una imagen, pero ahí depende mucho del tipo de imagen en referencia a su contraste y detalle, así mismo su nivel de ruido, lo cual llevara a tener que variar el radio de corte para obtener mejores imágenes filtradas.






## Biografía
  [1] Chan, R. H., Ho, C. -., & Nikolova, M. (2005). Salt-and-pepper noise removal by median-type noise detectors and detail-preserving regularization. IEEE Transactions on Image Processing, 14(10), 1479-1485. doi:10.1109/TIP.2005.852196


  [2] Toh, K. K. V., & Isa, N. A. M. (2010). Noise adaptive fuzzy switching median filter for salt-and-pepper noise reduction. IEEE Signal Processing Letters, 17(3), 281-284. doi:10.1109/LSP.2009.2038769


  [3]. Villa, M. M. (2017). Fundamentos de la reducción de ruido en imágenes.


  [4].Boncelet Charles,
4.5 - Image Noise Models,
Editor(s): AL BOVIK,
In Communications, Networking and Multimedia,
Handbook of Image and Video Processing (Second Edition),
Academic Press,
2005,
Pages 397-409,
ISBN 9780121197926,
https://doi.org/10.1016/B978-012119792-6/50087-5.
(https://www.sciencedirect.com/science/article/pii/B9780121197926500875)


  [5]. Ortiz Rangel, Estela, Mejía-Lavalle, Manuel, & Sossa, Humberto. (2017). Filtrado de ruido Gaussiano mediante redes neuronales pulso-acopladas. Computación y Sistemas, 21(2), 381-395. https://doi.org/10.13053/cys-21-2-2742


  [6]. González, G. (1997). Series de Fourier, transformadas de Fourier y aplicaciones. Divulgaciones matemáticas, 5(1/2), 43-60.

  [7].Duoandikoetxea, J. (2003). Lecciones sobre las series y transformadas de Fourier. Recuperado de http://www. ugr. es/acanada/docencia/matematicas/analisisdefourier/Duoandikoetxeafourier. pdf.

  [8].Vázquez Lorenzana. Transformada de Fourier. dcb.ingenieria.unam.mx. https://dcb.ingenieria.unam.mx/wp-content/themes/tempera-child/CoordinacionesAcademicas/CA/MA/MaterialDigital/materialT3.pdf. Published noviembre de 2022. Accedido julio 6, 2023.


