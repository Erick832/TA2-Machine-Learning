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

### **2. Descripción del formato STL**

### **3. Identificar y describir en el inform las conversiones de tipos que considera necesarias para el proyecto del trabajo parcial y final**

### **4. Implementar funciones para transformar entre los formatos que usted considere pertinente para el proyecto**
```
import numpy as np
def read_file(name_file):
    with open(name_file, "r") as file:
        my_list = [line.rstrip() for line in file]

    my_list.remove('OFF')
    new_list = []

    for e in my_list:
        temp_list = []
        for sub_e in e.split(" "):
            temp_list.append(float(sub_e))
        new_list.append(temp_list)

    div = int(new_list[0][0])
    new_list.pop(0)

    vertex_list = np.array(new_list[:div])
    faces_list = np.array(new_list[div:])

    return vertex_list, faces_list
```

```
def get_normal_list(vertex_list, faces_list):
    surface_normal = []
    faces_transformed = []
    for face in faces_list:
        s_a = int(face[1])
        s_b = int(face[2])
        s_c = int(face[3])

        A = vertex_list[s_a]
        B = vertex_list[s_b]
        C = vertex_list[s_c]

        AB = B-A
        AC = C-A

        surface_normal.append(np.cross(AB, AC))
        faces_transformed.append([[s_a+1, s_b+1, s_c+1], len(surface_normal)])

    return surface_normal, faces_transformed
```
    
```
def create_obj_file(name_file):
    vertex_list, faces_list = read_file(name_file)
    surface_normal, faces_transformed = get_normal_list(vertex_list, faces_list)

    file_obj = open('./'+name_file[:-4]+'.obj', 'x', encoding='utf8')
    file_obj.write('g '+name_file[:-4]+'\n')

    for v in vertex_list:
        file_obj.write('v ' + str(v)[1:-1]+'\n')

    file_obj.write('\n')
    for normal in surface_normal:
        file_obj.write('vn ' + str(normal)[1:-1]+'\n')

    file_obj.write('\n')
    for face in faces_transformed:
        v1 = str(face[0][0])
        v2 = str(face[0][1])
        v3 = str(face[0][2])
        vn = str(face[1])
        word = "f "+v1 + "//"+vn+" "+v2+"//"+vn+" "+v3+"//"+vn+"\n"
        file_obj.write(word)

    file_obj.close()
```
