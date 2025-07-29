# Seguimiento-1
Seguimiento 1 - Bioinformática 2025-2 \

### Preguntas:
**1.a. Describa los campos que se encontrara en los archivos con formato GFF3. ¿Que información esta contenida? Ejemplos.** \
Los archivos GFF3 son archivos de texto plano tabulados con 9 columnas:
\
_Característica = feature_
\
\
**_Columna 1_**: "sequid" **->** El ID del punto de referencia utilizado para establecer el sistema de coordenadas de la entidad actual. No puede contener espacios en blanco (a menos que sean literales) ni comenzar con ">".
Conjunto de caracteres permitidos: [a-zA-Z0-9.:^*$@!+_?-|]
\
**_Columna 2_**: "source" **->** Normalmente es el nombre de un programa (por ejemplo, Genescan) o el nombre de una base de datos (por ejemplo, GenBank) donde se generó esta característica. Esta columna se utiliza para añadir información adicional a la característica, siendo una subcategoría de la columna "type" (para dar algo de jerarquía a los datos).
\
**_Columna 3_**: "type" **->** Aquí se especifica el tipo de característica. Debe ser un ítem de la Sequence Ontology o un número/código de acceso de la SO, que utiliza la sintaxis SO:000000.
Debe ser sequence_feature (SO:0000110) o un elemento subordinado (is_a).
\
**_Columna 4 y 5_**: "start" y "end" **->** Son las coordenadas de inicio y fin de la característica, y se expresan en coordenadas enteras basadas en 1 (no en 0). _El inicio debe ser menor o igual al final. Si el inicio es igual al fin (caso de sitios de inserción), el sitio implícito está a la derecha de la base indicada, en la dirección del punto de referencia._ Para características que atraviesan el origen de una secuencia circular, se usa: _fin = posición final + posición del punto de referencia (landmark)_.
\
**_Columna 6_**: "score" **->** Un número de punto flotante. La semántica de esta puntuación no está completamente definida, pero se recomienda usar:
* E-values: para características de similitud de secuencia (un valor bajo indica que la similitud no es probablemente casual).
* P-values: para características de predicción genética ab initio (un valor bajo indica una predicción significativa, no atribuible al azar).

\
**_Columna 7_**: "strand" **->** La cadena relativa al punto de referencia (landmark).  
(+) para la cadena positiva (idéntica a la referencia).  
(-) para la cadena negativa (complementaria).  
(.) para características sin cadena.  
(?) para características cuya cadena es relevante, pero desconocida.
\
**_Columna 8_**: "phase" **->** Obligatoria para todas las características CDS. La fase indica dónde comienza el siguiente codón en relación con el extremo 5' de la característica CDS actual (el extremo 5' es el inicio en la hebra + y el fin en la hebra -). La fase puede ser 0, 1 o 2:
* Fase de "0": codon inicia en el primer nucleotido del CDS.
* Fase de "1": codon inicia en el segundo nucleotido del CDS.
* Fase de "2":  codon inicia en el tercer nucleotido de la region.
Este concepto no debe confundirse con el "frame", que se refiere al valor de una base en relación con el inicio del ORF. En cambio, "phase" describe el inicio del siguiente codón respecto a la CDS dada.

**_Columna 9_**: "attributes" **->**  Lista de atributos con formato tag=value. Varios atributos se separan con ;, y los valores múltiples dentro de un mismo atributo se separan por ,. Los valores no deben estar entre comillas, salvo que los analizadores los incluyan como parte del valor. Algunas etiquetas comunes:
* ID: identificador del atributo. Obligatorio para características que tienen "hijas" o que abarcan varias líneas. En características discontinuas (una sola característica en varias ubicaciones genómicas), el mismo ID puede usarse en varias líneas; todas las líneas que comparten un ID representan colectivamente una única característica. Los ID deben ser únicos dentro del archivo GFF.
* Name: nombre que se muestra al usuario. No necesita ser único.
* Alias: nombre secundario de la característica (por ejemplo, locus o números de acceso). No necesita ser único.
* Parent: relaciona la característica con su "progenitor". Se usa para indicar una relación jerárquica parcial.
* Target: objetivo de una alineación nucleótido-nucleótido o proteína-nucleótido. Formato: "target_id start end [strand]", donde strand es opcional.
* Gap: información de la alineación entre la característica y su objetivo, si no son colineales (por ejemplo, si contienen huecos o gaps).
* Derives_from: indica una relación temporal entre dos características, como en genes policistrónicos.
* Note: es una nota/comentario de texto libre.
* Dbxref: una referencia cruzada a bases de datos externas.
* Ontology_term: una referencia cruzada a un término de ontología.
* Is_circular: para indicar si una característica es circular.

Ejemplo:  

        0  sequid | source | type | start | end  | score | strand | phase | attribute                                         
        1  ctg123 |   .    | exon |  5000 | 5500 |   .   |    +   |   .   | ID=exon00004;Parent=mRNA00001,mRNA00002,mRNA00003 

**3. Analisis del archivo**
/
**a. Descripción del organismo**
/
Junco hyemalis, también conocido como Junco de Ojos Negros, es una especie de ave pasiforme de la familia Emberizidae propia de América del Norte. Los Juncos de Ojo Oscuro se reproducen en bosques a lo largo de casi todo Norteamérica, y a elevaciones que van desde el nivel del mar hasta 3353 m de altura. Son mayormente consumidores de semillas, especialmente de pamplina, alforfón, bledos, alazán, y otras similares, las cuales representan alrededor de un 75% de su dieta a lo largo del año. (Junco De Ojo Oscuro | Celebrate Urban Birds, 2016)
/
**b. Investigue:**
* ¿Cuantos features contiene el archivo? 734551
* ¿Cuantas regiones de la secuencia (cromosomas) contiene el archivo? 4457
* ¿Cuántos genes están listados en el organismo? 17477, que se dividen de la siguiente manera:
  * 14551 gene (Una region(es) que incluye todos los elementos necesarios de la secuencia para codificar un transcrito funcional.)
  * 2861 ncRNA_gene (Non-coding RNA.)
  * 65 pseudogene (Una secuencia que se parece a un gen funcional, en otro locus dentro del genoma, que no es funcional como consecuencia de mutaciones que previenen su trasncripcion o traducción.)
* ¿Cuál es el top 10 de tipo de features (columna 3) más anotados en el genoma?
  * 294399 exon
  * 275104 CDS
  * 87769 biological_region
  * 23225 mRNA
  * 16191 five_prime_UTR
  * 14551 gene
  * 10875 three_prime_UTR
  * 4514 lnc_RNA
  * 4457 region
  * 2861 ncRNA_gene
 
## Referencias
Junco de Ojo Oscuro | Celebrate Urban Birds. (2016, August 31). Celebrate Urban Birds. https://celebrateurbanbirds.org/es/learn/birds/focal-species/junco-de-ojo-oscuro/#:~:text=de%20Ojo%20Oscuro-,Especies%20Regionales,%C2%BFC%C3%B3mo%20identificar%20el%20ave?  
Sacado de Bio explain  
Srl, B. G. (2021, July 29). lcnRNA: long non-coding RNA. Breda Genetics Srl. https://bredagenetics.com/lcnrna-long-non-coding-rna/
