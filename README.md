# Handwritten Math Image Recognition *<span style="font-size: 16px; float: right; vertical-align: top; margin-right: 100px;">Marc Serrano Altena</span>*

Het doel van het project is om een afbeelding van geschreven wiskunde te analyseren en te converteren naar latex-code met behulp van Machine Learning. Dit zou ik dan vervolgens kunnen koppelen op mijn bestaande website: [Wiskundewijs](https://wiskundewijs.com/). Specifiek heb ik daar een vergelijking oplosser gemaakt om ingevoerde vergelijkingen op te lossen (bijvoorbeeld $x^2 = 1 \longrightarrow x = 1 \ \vee \ x = -1$).

Hier zou ik dan de functionaliteit kunnen toevoegen om afbeeldingen in te sturen om die op te lossen. Dit zou het makkelijker maken voor middelbare scholieren die moeite hebben met wiskunde om te werken met de bestaande oplosser.

De tekst in de afbeeldingen wordt herkend met Machine Learning, maar om dit te doen wordt er gebruik gemaakt van Data Processing om de afbeeldingen te verwerken. Door dit te doen wordt de kans groter dat de tekst correct voorspeld wordt door het model. Bijvoorbeeld eerst de pixels te normaliseren of het formaat van een afbeelding aan te passen zodat het overeenkomt met de training data. En tijdens het ontwikkelen van een goed model visualiseer ik de *validation loss* en *validation accuracy* van een model om (deels) te kunnen zien hoe het model presteert.

## Opties om de voorspelling te maken

Om de handgescreven afbeeldingen om te zetten naar latex code zijn er verschillende mogelijkheden. Een optie is om de afbeeldingen te splitsen in enkele componenten en een Convolutional Neural Network (CNN) te gebruiken om voorspelling mee te maken van de individuele componenten. Verder zou dan met behulp van een attention mechanisme de relatie tussen de symbolen kunnen worden vastgesteld. Dit is de optie die *Sunia team* had gekozen in deze paper: https://hal.science/hal-04264727/file/CROHME_2023_competition_report_paper.pdf 

Een andere optie is om gebruik te maken van een Vision Transformer (ViT). Deze zou goede resultaten geven in vergelijking met de state-of-the-art convolutional networks [[1]](https://arxiv.org/pdf/2010.11929).

Beide opties maken gebruik van een encoder-decoder structuur om de afbeeldingen te *encoden* en de output nadat het door het model verwerkt is te *decoden* als een sequence van latex-tokens.

## Repository Structuur
### Notebooks
In de "Own Notebooks" folder zitten verschillende notebooks waar verschillende modelen getraind worden:

- CROHME
- Double English
- EMNIST + English font
- EMNIST
- English font
- Math Symbols

En van deze notebooks zijn de bovenste twee de belangrijkste.

In de *Double English*, *EMNIST + English font*, *EMNIST* en *English font* notebooks worden verschillende modellen getraind om losse letters en cijfers correct te herkennen. Elke notebook gebruikt andere (combinaties van) datasets. Het model dat het beste heeft gepresteerd met eigen handgeschreven en getypte letters voorspellen is het *Double English* model:

<img src="models results\Result Double English model handwritten letters upper.png" alt="Handwritten Uppercase" width="50%" style="display:inline-block; margin-right:2%;" />
<img src="models results\Result Double English model typed letters upper.png" alt="Typed Uppercase" width="45.75%" style="display:inline-block;" />

<br><br>

De CROHME notebook is een encoder-decoder model met een ViT als encoder een Gated Recurrent Unit (GRU) als decoder. Het model had veel potentie, maar uiteindelijk is het niet binnen de tijd gelukt om er zinvolle voorspellingen uit te krijgen.

De *Math Symbols* notebook probeert de voorspellingen van losstaande letters en cijfers uit de *Double English* model uit te breiden. Zodat behalve letters en cijfers ook wiskundige tekens zoals $+$, $-$, $*$, $\sqrt{}$ en $\int$ zouden worden herkend. Maar ook hier zijn geen zinvolle voorspellingen uit gekomen.

In de "Working Example" folder zijn twee notebooks van het internet om een idee te krijgen van hoe een werkend model er uit zou kunnen zien. Volledige credit gaat naar [Dohyeong Kim](https://dohyeongkim.medium.com/image-to-latex-using-vision-transformer-13fc4ce253d7).

### Overige data

Apart van de notebooks zijn de de "Image characters" en "models performence" folder misschien nog interessant. In "Image characters" zitten de eigen afbeeldingen om een model mee te controlleren (Zoals bijvoorbeeld de afbeeldingen hierboven). De "models performence" folder bevat plots met de validation loss en validation accuracy van allerlei soorten modelen. 

## Bronnen
### Gegevensbronnen

- [EMNIST data](https://www.kaggle.com/datasets/crawford/emnist) $\longrightarrow 28 \times 28$ handgeschreven zwart-wit afbeeldingen van letters en cijfers.
- [English Font-Number Recognition data](https://www.kaggle.com/datasets/yaswanthgali/english-fontnumber-recognition) $\longrightarrow 128 \times 128$ afbeeldingen met verschillende lettertypes.
- [English Handwritten Characters data](https://www.kaggle.com/datasets/dhruvildave/english-handwritten-characters-dataset) $\longrightarrow 128 \times 128$ afbeeldingen met handgeschreven letters en cijfers.
- [Handwritten math symbols dataset](https://www.kaggle.com/datasets/xainano/handwrittenmathsymbols) $\longrightarrow 128 \times 128$ afbeeldingen met individuele symbolen.
- [CROHME dataset](https://zenodo.org/records/8428035) $\longrightarrow$ handgeschreven afbeeldingen met wiskundige formules en de bijbehorende latex code erbij

### Externe Componenten

- [matplotlib](https://matplotlib.org/stable/index.html) $\longrightarrow$ loss en accuracy weergave voor model evaluatie.
- [tensorflow](https://www.tensorflow.org/api_docs/python/tf/keras) $\longrightarrow$ keras om model te kunnen maken en voor datamanipulatie (data normalisatie of one-hot encoding bijvoorbeeld).
- [numpy](https://numpy.org/doc/) $\longrightarrow$ werken met arrays om sommige afbeeldingen van data om te kunnen zetten naar numpy arrays.
- [os](https://docs.python.org/3/library/os.html) $\longrightarrow$ om door folders te gaan en data te importeren.
- [sklearn](https://scikit-learn.org/stable/) $\longrightarrow$ voor train_test_split en accuracy_score.
- [idx2numpy](https://pypi.org/project/idx2numpy/) $\longrightarrow$ om EMNIST data te laden.