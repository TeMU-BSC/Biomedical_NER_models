# Biomedical_NER_models

Official repository for biomedical and clinical models generated by the Barcelona Supercomputing Center within the framework of the [PlanTL](https://plantl.mineco.gob.es/Paginas/index.aspx)

## Models

The models generated are available as docker images that can be accessed and executed through a API. The models have been trained with [PharmaCoNER Tagger](https://github.com/TeMU-BSC/PharmaCoNER-Tagger), a Neural Named Entity Recognition program targeting domain adaptation, particularly in the case of Spanish medical texts. The generation of the Docker images with an internal API has been done with the [neuro_ner_docker](https://github.com/darrylestrada97/neuro_ner_docker) repository.

| **Model name** | **Version** | **Label**     | **Model trained with clinical data** | **Dockerhub alias**      | **Link**                                          |
|---------------------|-------------|---------------|--------------------------------------|--------------------------|---------------------------------------------------|
| symptoms_base       | biomedical  | SINTOMA       | ❌                                    | `bsctemu/symptoms_base`    | https://hub.docker.com/r/bsctemu/symptoms_base    |
| symptoms            | clinical    | SINTOMA       | ✅                                    | `bsctemu/symptoms`         | https://hub.docker.com/r/bsctemu/symptoms         |
| species_base        | biomedical  | SPECIE        | ❌                                    | `bsctemu/species_base`     | https://hub.docker.com/r/bsctemu/species_base     |
| species             | clinical    | SPECIE        | ✅                                    | `bsctemu/species`          | https://hub.docker.com/r/bsctemu/species          |
| precedures_base     | biomedical  | PROCEDIMIENTO | ❌                                    | `bsctemu/precedures_base`  | https://hub.docker.com/r/bsctemu/precedures_base  |
| precedures          | clinical    | PROCEDIMIENTO | ✅                                    | `bsctemu/precedures`       | https://hub.docker.com/r/bsctemu/precedures       |
| medications_base    | biomedical  | FARMACO       | ❌                                    | `bsctemu/medications_base` | https://hub.docker.com/r/bsctemu/medications_base |
| medications         | clinical    | FARMACO       | ✅                                    | `bsctemu/medications`      | https://hub.docker.com/r/bsctemu/medications      |
| diseases_base       | biomedical  | ENFERMEDAD    | ❌                                    | `bsctemu/diseases_base`    | https://hub.docker.com/r/bsctemu/diseases_base    |
| diseases            | clinical    | ENFERMEDAD    | ✅                                    | `bsctemu/diseases`         | https://hub.docker.com/r/bsctemu/diseases         |


## Usage example
<details>
<summary><b>1. Pull image from Docker hub</b></summary>

```
   docker pull <name_of_image>
```
   
For example, you could download the species model:
```
   docker pull bsctemu/species
```
</details>
   
<details>
<summary><b>2. Run image</b></summary>
The port number should be a free port in your system, in this case we are using 8003 as an example.
```
   docker run -d -p 8003:5000 -t --name <internal_name_of_container> <name_of_image>
```
For example, run the previously pulled image in port 8003:
```
   docker run -d  -p 8003:5000 -t --name species  bsctemu/species
```
</details>

<details>
<summary><b>3. Make API requests</b></summary>
You can make requests to the generated API through Curl from terminal or another interface of your system.
```
   curl --location 'http://0.0.0.0:8003/api/submit' \
   --header 'Content-Type: application/json' \
   --data '{
   "inputText": "Anamnesis Varón de 17 años con antecedentes personales de trastorno de déficit de atención e hiperactividad en la infancia y obesidad en seguimiento por Servicio de Endocrinología. Estudiante de un módulo de mecánica. Antecedentes familiares: hermana con parálisis cerebral infantil ependimoma variante de células claras grado II según la Organización Mundial de la Salud (OMS). Evolución » Se realiza resección completa del tumor sin presencia de complicaciones postquirúrgicas. En RM de control no se observa presencia de focos tumorales residuales. » Su mujer era una ama de casa que por las tardes tambien enseñaba ingles a menores. Se completa estudio de extensión mediante las siguientes pruebas complementarias: » RM columna vertebral: sin presencia de lesiones tumorales. » Punción lumbar: hematíes: 0, leucocitos: 20 con 65 % de linfocitos, glucosa de 52 mg/dl, Proteínas de 48 mg/dl.» Se comenta el caso en comité multidisciplinar, decidiéndose la no realización de tratamiento radioterápico complementario. Durante su seguimiento, el paciente no ha presentado nuevas recidivas tumorales. Como secuela permanente presenta amaurosis en ojo izquierdo."
   }'
```
</details>

<details>
<summary><b>4. Obtain results</b></summary>
The results appear within a dictionary type data structure, within the key "brat". The "brat" value is a list of extracted entities containing the text and the start and end positions of the span.

```
    #in the terminal you should see something like this.
    {
  "data": {
    "brat": [
      {
        "class": "SPECIES",
        "end": 15,
        "entity": "Varón",
        "id": "T1",
        "start": 10
      },
      {
        "class": "SPECIES",
        "end": 54,
        "entity": "personales",
        "id": "T2",
        "start": 44
      },
      {
        "class": "SPECIES",
        "end": 122,
        "entity": "infancia",
        "id": "T3",
        "start": 114
      },
      {
        "class": "SPECIES",
        "end": 191,
        "entity": "Estudiante",
        "id": "T4",
        "start": 181
      },
      {
        "class": "SPECIES",
        "end": 241,
        "entity": "familiares",
        "id": "T5",
        "start": 231
      },
      {
        "class": "SPECIES",
        "end": 250,
        "entity": "hermana",
        "id": "T6",
        "start": 243
      },
      {
        "class": "SPECIES",
        "end": 562,
        "entity": "mujer",
        "id": "T7",
        "start": 557
      },
      {
        "class": "SPECIES",
        "end": 582,
        "entity": "ama",
        "id": "T8",
        "start": 571
      },
      {
        "class": "SPECIES",
        "end": 1053,
        "entity": "paciente",
        "id": "T9",
        "start": 1045
      }
    ],
    "original_text": "Anamnesis Varón de 17 años con antecedentes personales de trastorno de déficit de atención e hiperactividad en la infancia y obesidad en seguimiento por Servicio de Endocrinología. Estudiante de un módulo de mecánica. Antecedentes familiares: hermana con parálisis cerebral infantil ependimoma variante de células claras grado II según la Organización Mundial de la Salud (OMS). Evolución » Se realiza resección completa del tumor sin presencia de complicaciones postquirúrgicas. En RM de control no se observa presencia de focos tumorales residuales. » Su mujer era una ama de casa que por las tardes tambien enseñaba ingles a menores. Se completa estudio de extensión mediante las siguientes pruebas complementarias: » RM columna vertebral: sin presencia de lesiones tumorales. » Punción lumbar: hematíes: 0, leucocitos: 20 con 65 % de linfocitos, glucosa de 52 mg/dl, Proteínas de 48 mg/dl.» Se comenta el caso en comité multidisciplinar, decidiéndose la no realización de tratamiento radioterápico complementario. Durante su seguimiento, el paciente no ha presentado nuevas recidivas tumorales. Como secuela permanente presenta amaurosis en ojo izquierdo.",
    "processing_time": "21.79176902770996"
  },
  "message": "Data retrieved successfully.",
  "success": true
}
```
</details>
  
<details>
<summary><b>5. Stop the Docker container</b></summary>
Once you have finished the requests you can stop the container as follows.
   
```
    docker stop <internal_name_of_container>    
```
In the case of the example, we could stop the container with the following terminal line
```
   docker stop species
```
</details>
 
## Transformer-based biomedical language models

If you want to access biomedical language models tuned for biomedical tasks, you can access the repository [lm-biomedica-clinical-en](https://github.com/PlanTL-GOB-ES/lm-biomedical-clinical-es)

## Disclaimer

The models published in this repository are intended for a generalist purpose and are available to third parties. These models may have bias and/or any other undesirable distortions.

When third parties, deploy or provide systems and/or services to other parties using any of these models (or using systems based on these models) or become users of the models, they should note that it is their responsibility to mitigate the risks arising from their use and, in any event, to comply with applicable regulations, including regulations regarding the use of artificial intelligence.

In no event shall the owner of the models (SEDIA – State Secretariat for digitalization and artificial intelligence) nor the creator (BSC – Barcelona Supercomputing Center) be liable for any results arising from the use made by third parties of these models.

Los modelos publicados en este repositorio tienen una finalidad generalista y están a disposición de terceros. Estos modelos pueden tener sesgos y/u otro tipo de distorsiones indeseables.

Cuando terceros desplieguen o proporcionen sistemas y/o servicios a otras partes usando alguno de estos modelos (o utilizando sistemas basados en estos modelos) o se conviertan en usuarios de los modelos, deben tener en cuenta que es su responsabilidad mitigar los riesgos derivados de su uso y, en todo caso, cumplir con la normativa aplicable, incluyendo la normativa en materia de uso de inteligencia artificial.

En ningún caso el propietario de los modelos (SEDIA – Secretaría de Estado de Digitalización e Inteligencia Artificial) ni el creador (BSC – Barcelona Supercomputing Center) serán responsables de los resultados derivados del uso que hagan terceros de estos modelos.
