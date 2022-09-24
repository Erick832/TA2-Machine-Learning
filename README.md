# TA2-Machine-Learning

**Integrantes**

- Erick Wilson Aronés Garcilazo U201924440
- Ronaldo Cornejo

### **1. Descripción de los formatos utilizados para los modelos del artículo**

El formato OFF (Object File Format) es un formato de archivo basado en texto ASCII para describir objetos gómetricos 2D y 3D. Este formato describe las superficies geométricas de los objetos 3D mediante vértices y polígonos, mientras que los colores se definen mediante valores RGB.

Composicion de un archivo OFF estandar:

- Primera línea (opcional): Las letras OFF para marcar el tipo de archivo.
- Segunda línea: El número de vértices, el número de caras y el número de aristas, en orden (este último puede ignorarse escribiendo 0 en su lugar).
- Lista de vértices: Coordenadas X, Y y Z.
- Lista de caras: Número de vértices, seguido de los índices de los vértices que la componen, en orden (indexados desde cero).
  - Opcionalmente, los valores RGB para el color de la cara pueden seguir los elementos de las caras.
