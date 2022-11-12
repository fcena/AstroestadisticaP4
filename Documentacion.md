# **Trabajo Práctico #4 de Astroestadística: Inferencias Bayesianas con Cadenas de Markov**
#### Autor: Federico Ariel Cena, OAC-UNC
## Introducción
El presente trabajo busca experimentar de forma práctica con la noción de inferencia bayesiana a través de métodos conocidos como las cadenas de Markov Monte-Carlo (MCMC por sus siglas en inglés). El objetivo es buscar los parámetros óptimos para ajustar una *función de Schechter* a la función luminosidad proveniente de un conjunto de galaxias. Esto lo realizaremos mediante dos algoritmos conocidos: Metropolis-Hastings para MCMC y un algoritmo de *"Gradiente Descendiente"*. 

La inferencia bayesiana en estadística se puede pensar como una aplicación del mismo teorema de Bayes. Si poseemos un conjunto de datos $d$ que puede ser explicado por un modelo $m(\theta_{i})$ con parámetros $\theta_{i}$, queremos buscar los parámetros del modelo que mejor ajusten a mis datos $d$. Desde un punto de vista bayesiano, lo que estoy buscando es *maximizar* la función de probabilidad posterior de los parámetros dados mis datos. Esta función de probabilidad posterior es proporcional a la función de *Likelihood* $p(d|\phi,m)$ que me describe la probabilidad de que mis datos provengan del modelo con los parámetros propuestos multiplicado por el *prior* que son los supuestos que yo tengo respecto a los parámetros.

La función de likelihood tiene la siguiente forma si asumimos errores gaussianos: 

$$Likelihood = \prod_{n}P(x_{n}|\theta_{i}) = \prod_{i=0}^{n-1}\frac{1}{\sqrt(2\pi)\sigma_{i}} e^{-\left(\frac{(x_{i}-m(x_{i}))^{2}}{\sigma_{i}}\right)} $$

No obstante, en general, se trabaja con la función de likelihood logarítmica debido a su facilidad para ser computada: 

$$logLikelihood = \sum_{i} log\left(\frac{1}{\sqrt(2\pi\sigma_{i})}\right) + \sum_{i} - \frac{(x_{i} - m(x_{i}))^{2}}{\sigma_{i}} $$

El término que sólo involucra a los errores $\sigma_{i}$ se puede considerar constante, por ende la función que buscaremos minimizar será: 

$$ logLikelihood = ∑ \frac{(y_{i}-m(\theta_{i},x_{i}))^2}{\sigma_{i}} $$

La función prior puede tomar diversas formas dependiendo de las suposiciones que se quieran hacer acerca de los datos, en nuestro caso nos limitaremos a lo más simple. 

Los ejercicios son los siguientes: 
* **Ejercicio 1**: Leer y graficar los datos pertenecientes a la función de luminosidad de galaxias obtenida por Blanton et al.
(2001). Los datos correspondientes a la función de luminosidad se pueden descargar del aula virtual.
* **Ejercicio 2**: Se desea ajustar el modelo $m$ al conjunto de datos $d$, mediante un análisis Bayesiano. Para el caso de los
datos del Ej. 1, se utilizará como modelo la función de Schechter. Para ello se deberán escribir la función de prior, likelihood y probabilidad posterior. Explicitar las hipótesis involucradas y simplificaciones.
* **Ejercicio 3**: Visualizar las propiedades de convergencia de las cadenas así como mixing e identificar las condiciones iniciales que puedan llegar a producir un mal mixing. 
* **Ejercicio 4**: Para una buena elección de parámetros, corra y compare varias cadenas.
* **Ejercicio 5**: Implimente un algoritmo de gradiente descendiente para encontrar el mínimo de la función de likelihood. 
* **Ejercicio 6**: Compare los resultados obtenidos entre ambos modelos. 



## Conclusiones

* Si bien hay diferencias notables entre los parámetros ajustados por MCMC y gradiente descendiente, ambos ajustan curvas de Schechter representativas de los datos dentro de los errores estipulados. 
* La diferencia notable entre la cantidad de cadenas necesarias para converger entre MCMC y gradiente descendiente podría deberse a una mala optimización del código propuesto para implementar Metropolis-Hastings. 
