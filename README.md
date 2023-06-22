  # Programa-Delfin-2023
 # Descripción y caracterización para el procesamiento de imágenes ruidosas 
## Capítulo 1: Estado del arte
### 1.1 (Algo va aquí)
### 1.2 ¿Qué es ruido impulsivo "Sal y pimienta" en imágenes?
El ruido impulsivo o sal y pimienta (salt-and-pepper) se trata de una clase de contaminación que es causada por defectos en los pixeles de los sensores de las cámaras, una locación en memoria del hardware defectuosa o directamente ruido en un canal de transmisión [1].

Estos defectos provocan una imagen corrupta con una serie de pixeles con ruido que solo pueden tomar valores máximos o mínimos de color y esto se conoce coloquialmente como sal y pimienta, donde la sal hace ilusión a todos los pixeles que entran en el valor máximo o blanco y la pimienta son aquellos que alcanzan el valor mínimo o negro.

Por otro lado, el procesamiento de la imagen que realiza después de la captura de esta, requiere de un proceso de detección y eliminación del ruido. En este punto entran los filtros de remoción, siendo el más usual el filtro mediano de tipo no linear que es muy utilizado por su alta eficiencia y buena eliminación de ruido pero con la consideración que con una corrupción mayor de 50% algunos detalles de la imagen original quedaran manchadas.

La ecuación matemática que modela el comportamiento del ruido impulsivo en una imagen es la siguiente:


$$

\begin{equation}
  P_{sp} ( z )  = \Biggl\{ \hspace{3mm}
\begin{align*} 
  P_p \hspace{1mm} , \hspace{3mm} z=p \\ 
  P_s \hspace{1mm} , \hspace{3mm} z=s
\end{align*}
\end{equation}

$$



De la anterior ecuación indicamos que "***z***" es el porcentaje de pixeles que tendrán ruido y para este sea homogéneo  "***z***" se dividira en dos, siendo la mitad corrupción blanca y otra mitad negra.



## Biografía
  [1] Chan, R. H., Ho, C. -., & Nikolova, M. (2005). Salt-and-pepper noise removal by median-type noise detectors and detail-preserving regularization. IEEE Transactions on Image Processing, 14(10), 1479-1485. doi:10.1109/TIP.2005.852196


  [2] Toh, K. K. V., & Isa, N. A. M. (2010). Noise adaptive fuzzy switching median filter for salt-and-pepper noise reduction. IEEE Signal Processing Letters, 17(3), 281-284. doi:10.1109/LSP.2009.2038769


  [3]


  [1].


  [1].


