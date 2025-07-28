# Seguimiento-1
Seguimiento 1 - Bioinformática 2025-2 \
Preguntas \
**1.a. Describa los campos que se encontrara en los archivos con formato GFF3. ¿Que información esta contenida? Ejemplos.** \
Los archivos GFF3 son archivos de texto plano tabulado con 9 columnas: \

**_Columna 1_**: "sequid" -> El ID del punto de referencia utilizado para establecer el sistema de coordenadas de la entidad actual. No pueden contener espacios en blanco (a no ser de que sean literales) ni comenzar con un ">".  
Los IDs de cada caracteristica debe de ser unicos, y es un atributo obligatorio para aquellas caracteristicas que tienen hijos (jerarquia). Si son caracteristicas discontinuas (unica caracteristica que aparece/existe en varias ubiaciones genomicas) el mismo ID puede aparecer en diferentes lineas; teniendo esto en cuenta, todas las lineas que comparte un ID deben de representar colectivamente una unica caracteristica.  
Conjunto de caracteres permitidos: [a-zA-Z0-9.:^*$@!+_?-|]  
**_Columna 2_**:
