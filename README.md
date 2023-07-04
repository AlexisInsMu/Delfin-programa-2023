  # Programa-Delfin-2023
 # Descripción y caracterización para el procesamiento de imágenes ruidosas 
## Capítulo 1: Estado del arte
### ***1.1 (Algo va aquí)***
### ***1.2 ¿Qué es ruido impulsivo "Sal y pimienta" en imágenes?***
El ruido impulsivo o sal y pimienta (salt-and-pepper) se trata de una clase de contaminación que es causada por defectos en los pixeles de los sensores de las cámaras, una locación en memoria del hardware defectuosa o directamente ruido en un canal de transmisión [1].

Estos defectos provocan una imagen corrupta con una serie de pixeles con ruido que solo pueden tomar valores máximos o mínimos de color y esto se conoce coloquialmente como sal y pimienta, donde la sal hace ilusión a todos los pixeles que entran en el valor máximo o blanco y la pimienta son aquellos que alcanzan el valor mínimo o negro.

Por otro lado, el procesamiento de la imagen que realiza después de la captura de esta, requiere de un proceso de detección y eliminación del ruido. En este punto entran los filtros de remoción, siendo el más usual el filtro mediano de tipo no linear que es muy utilizado por su alta eficiencia y buena eliminación de ruido pero con la consideración que con una corrupción mayor de 50% algunos detalles de la imagen original quedaran manchadas.

La ecuación matemática que modela el comportamiento del ruido impulsivo en una imagen es la siguiente:


\begin{equation}

P_{sp} ( z )  = \Biggl\{ 
$\hspace{3mm}$

    \begin{align*}

  P_p $\hspace{1mm}$ , $\hspace{3mm}$ z=p \\ 
  P_s $\hspace{1mm}$ , $\hspace{3mm}$ z=s
    \end{align*}
    
\end{equation}




De la anterior ecuación indicamos que "***z***" es el porcentaje de pixeles que tendrán ruido y para este sea homogéneo  "***z***" se dividira en dos, siendo la mitad corrupción blanca y otra mitad negra.


### ***1.3 ¿Qué es el ruido guassiano en imágenes?***

El ruido gaussiano que se adicionan a una imagen es el que ensucia la señal, de tal manera que se obtienen pixeles al azar por toda la imagen que se guían en su tonalidad en base a una distribución uniforme de color.

Su importancia radica en que debido a que está presente de manera inherente en el ambiente, más por el hecho que los factores que lo generan son muchos y muy diversos, un ejemplo es el ruido blanco que percibe las cuando la señal de la estación de televisión es débil, ahora bien, especificando en las imágenes, a la hora de su obtención o capturo, el ruido gaussiano se genera en ocasiones con baja iluminación donde es más fácil percibir fotones de ruido originados de distintos lugares, pero cabe recalcar que no solo en estas ocasiones este ruido se modela por medio de la distribución normal o de Gauss, si no que también hay casos con la distribución de Poison.

En la mayoría de la literatura cuando se trata de agregar este tipo de ruido a una imagen se guían por la distribución normal estándar donde el valor μ es igual a 0 y solo se hace variar le desviación estándar o en su defecto la varianza, aunque estas dos últimas depende directamente la una de la otra, por ende, mover una hace que la otra también se mueva.

Como último, la ecuación que modela el ruido gaussiano es la misma de la distribución del mismo nombre, pero en este caso, como ya se mencionó, mu o la media (***μ***) lo evaluamos en 0 y variamos la deviación estándar (***σ***).


  \begin{equation}
    P_G = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^2}  
  \end{equation}


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


