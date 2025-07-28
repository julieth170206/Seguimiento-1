# Seguimiento-1
Seguimiento 1 - Bioinformática 2025-2 \

### Preguntas:
**1.a. Describa los campos que se encontrara en los archivos con formato GFF3. ¿Que información esta contenida? Ejemplos.** \
Los archivos GFF3 son archivos de texto plano tabulado con 9 columnas:
\
_Caracteristica = feature_
\
\
**_Columna 1_**: "sequid" **->** El ID del punto de referencia utilizado para establecer el sistema de coordenadas de la entidad actual. No pueden contener espacios en blanco (a no ser de que sean literales) ni comenzar con un ">".  
Conjunto de caracteres permitidos: [a-zA-Z0-9.:^*$@!+_?-|]
\
**_Columna 2_**: "source" **->** Normalmente es el nombre de un programa (Genescan) o el nombre de una base de datos (Genebank) donde se genero esta caracteristica. Esta columna se utiliza para añadir un dato de la caracteristica, siendo una subclase de la columna "type" (para dar un poco de jerarquia a los datos).
\
**_Columna 3_**: "type" **->** Aca nos referimos al tipo de la caracteristica. Debe ser un item de la Sequence Ontology o un numero/codigo de acceso de la SO, la cual utiliza la sintaxis SO:000000.   
Debe ser sequence_feature (SO:0000110) o un elemento secundario (is_a).
\
**_Columna 4 y 5_**: "start" y "end" **->** Son las coordenadas del inico y fin de la caracteristica, y se dan en cordenadas enteras de base 1 positiva. _El inicio debe de ser menor o igual que el final. Si el inicio es igual al fin (sitios de inserción) el sitio implicito esta a la derecha de la base indicada en la direccion del punto de referencia._ Para las caracteristicas que pasan por el origen de un atributo circular se hace lo siguiente: _fin = posicion final + la posicion del punto de referencia (landmark)_.
\
**_Columna 6_**: "score" **->** A floating point number. La semantica de la puntuacion no esta bien definida, pero se recomienda utilizar E-values (estima la calidad del alineamiento de secuencias, un valor bajo indica que la similitud de las secuencias no es probablemente casual) para caracteristicas de similitude de secuencia, y el P-value (evaluar la significancia estadística de los resultados en modelos predictivos ab initio, un valor bajo indica que las caracteristicas identificadas no son producto del azar - prediccion significativa) para las caracteristicas de prediccion genetica ab initio.
\
**_Columna 7_**: "strand" **->** la cadena relativa al landmark. + para cadena positiva (secuencia identica), - para cadena negativa (secuencia complementaria), y . para características sin cadena; ? se utiliza para caracteristicas cuya cadena es relevante pero es desconocida.
\
**_Columna 8_**: "phase" **->**
\
**_Columna 9_**: "attributes" **->**
\
\
**3. Analisis del archivo**
**a.**
**b.**
