# Biomedical_NER_models

Official repository for biomedical and clinical models generated by the Barcelona Supercomputing Center within the framework of the [PlanTL](https://plantl.mineco.gob.es/Paginas/index.aspx)

## Models:

The models generated are available as docker images that can be accessed and executed through a API. The models have been trained with [PharmaCoNER Tagger](https://github.com/TeMU-BSC/PharmaCoNER-Tagger), a Neural Named Entity Recognition program targeting domain adaptation, particularly in the case of Spanish medical texts.

| **Nombre de model** | **Version** | **Entidades** | **Link**                                         |
| ------------------- | ----------- | ------------- | ------------------------------------------------ |
| symptoms_base       | base        | sintoma       | https://hub.docker.com/r/bsctemu/symptoms_base   |
| symptoms            | best        | sintoma       | https://hub.docker.com/r/bsctemu/symptoms        |
| species_base        | base        | species       | https://hub.docker.com/r/bsctemu/species_base    |
| species             | best        | species       | https://hub.docker.com/r/bsctemu/species         |
| precedures_base     | base        | procedimiento | https://hub.docker.com/r/bsctemu/precedures_base |
| precedures          | best        | procedimiento | https://hub.docker.com/r/bsctemu/precedures      |
| medication_base     | base        | farmaco       | https://hub.docker.com/r/bsctemu/medication_base |
| medication          | best        | farmaco       | https://hub.docker.com/r/bsctemu/medication      |
| disease_base        | base        | enfermedad    | https://hub.docker.com/r/bsctemu/disease_base    |
| disease             | best        | enfermedad    | https://hub.docker.com/r/bsctemu/disease         |

## Usage example

1. Create Docker image
   docker pull bsctemu/symptoms_base
   docker build -t <name_of_image> .

2. Run image

   docker run -p 8003:5000 -t <name_of_image>

## Transformer-based biomedical language models

If you want to access biomedical language models tuned for biomedical tasks, you can access the repository [lm-biomedica-clinical-en](https://github.com/PlanTL-GOB-ES/lm-biomedical-clinical-es)

## Disclaimer

The models published in this repository are intended for a generalist purpose and are available to third parties. These models may have bias and/or any other undesirable distortions.

When third parties, deploy or provide systems and/or services to other parties using any of these models (or using systems based on these models) or become users of the models, they should note that it is their responsibility to mitigate the risks arising from their use and, in any event, to comply with applicable regulations, including regulations regarding the use of artificial intelligence.

In no event shall the owner of the models (SEDIA – State Secretariat for digitalization and artificial intelligence) nor the creator (BSC – Barcelona Supercomputing Center) be liable for any results arising from the use made by third parties of these models.

Los modelos publicados en este repositorio tienen una finalidad generalista y están a disposición de terceros. Estos modelos pueden tener sesgos y/u otro tipo de distorsiones indeseables.

Cuando terceros desplieguen o proporcionen sistemas y/o servicios a otras partes usando alguno de estos modelos (o utilizando sistemas basados en estos modelos) o se conviertan en usuarios de los modelos, deben tener en cuenta que es su responsabilidad mitigar los riesgos derivados de su uso y, en todo caso, cumplir con la normativa aplicable, incluyendo la normativa en materia de uso de inteligencia artificial.

En ningún caso el propietario de los modelos (SEDIA – Secretaría de Estado de Digitalización e Inteligencia Artificial) ni el creador (BSC – Barcelona Supercomputing Center) serán responsables de los resultados derivados del uso que hagan terceros de estos modelos.
