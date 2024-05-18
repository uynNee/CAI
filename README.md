# CAI(Color Artificial Intelligence)

---

## [About CAI Project]

`CAI` applies a deep learning model to user-uploaded photos to diagnose personal color types and recommends personalized color palettes and fashion items based on them. The subjective diagnosis process of personal color types, which was previously judged by human eyes, is diagnosed based on the color matching results obtained through preprocessing such as white balance adjustment of the photos received from users.

`Personal Color` refers to the unique body color of an individual, and the system diagnoses suitable makeup, hair, clothing, and other color images by analyzing individual characteristics and diagnosing colors that harmonize with the individual by matching them to one type of the personal color type classification system.

#### `<CAI Total Process>`
<img src="jay/img/total-process.jpg" width=100%>

---

## [Deep Learning_Personal Color Type Classifier]

### Dataset Creator

#### `<Face Detection>`
<img src="jay/img/face-detection.jpg" width=100%>

#### `<Skin Color Extraction>`
<img src="jay/img/skin-color-extraction.jpg" width=100%>

#### `<Color System Converter & Type Classifier>`
<img src="jay/img/color-system-converter.jpg" width=100%>

- `Face Detection`
   Face recognition, image resizing (input image about 200,000 / output image about 150,000)
   Face recognition is performed using the Haar Cascade method after preprocessing the portrait image, and uniform-sized face images are obtained.
- `Skin Color Extraction`
   Extract facial skin color from the face images obtained through Face Detection.
   Two filters are used for color accuracy, and colors are extracted using the K-means method.
- `Color System Converter`
   Replace the extracted color list with average colors to convert the color system for algorithm application.
   (BGR → RGB → HSV)
- `Type Classifier`
   Apply the personal color type classification algorithm to generate datasets using the color matching result values (facial colors).

### Deep Learning

#### `<CNN/AlexNet>`
<img src="jay/img/cnn-alexnet.jpg" width=100%>

`AlexNet`: Selected because it is convenient for 'color learning' as it is divided into color and non-color parts for processing.
Result model: `CAI.h5`

---

## [Color Palette Extraction]

### Bright Palette & Harmony Palette

#### `<Personal color Analysis>`
<img src="jay/img/Data-Analysis.jpg" width=100%>

Based on color theory and papers related to personal colors, primary color matching areas & diagnosis colors are selected.
To verify the rationality of personal color theory and primary color matching areas & diagnosis colors, surveys are conducted.
Naver Data Lab is used for multidimensional analysis and accuracy extension.
Based on the analysis results, the primary color matching areas & diagnosis colors, which are the criteria for personal color type classification, are modified.
[*Personal color theory analysis report](https://github.com/uynNee/CAI/blob/master/jay/Analysis/Report/Color_theory_analysis.ipynb)
[*Personal color statistical analysis report](https://github.com/uynNee/CAI/blob/master/cys/CAI_elementaryItem_analysis.ipynb)

### Main purchase Palette

#### `<Data acquisition & Main color Extraction>`
<img src="jay/img/color-clustering.jpg" width=100%>

- `Clothes color Extraction`
   Masks are generated using the `Topwear.h5` (fashion item separation model) for product images.
   The original image is combined with the mask to delete the image area excluding the fashion item.
   Colors are extracted using the K-means method, and color data for each product is loaded into the database.
- `Main color Extraction`
   User's purchased items are queried in real-time to obtain a list of colors of purchased items.
   Items close to black and white are excluded from the list using a Gray tone Filter.
   To reduce clustering errors, the Color Generator expands the scale of purchased item colors.
   The expanded color data is used to extract the main purchase color palette using Hierarchical Clustering.

---

## [Website]

#### `<Web structure>`
<img src="jay/img/cai-webpage.jpg" width=100%>

- `Personal color type Prediction`
   Predicts the personal color type of the user through the web using **CAI.h5** and guides the user.
- `Matched Personal color palette`
   Provides personalized palettes corresponding to the user's type results and skin colors extracted by **Skin Color Extraction**.
- `Fashion item Recommendation`
   Recommends products corresponding to the extracted three palettes in real-time from the database, providing personalized services for each user.
   ※ Palette 1: **Bright Palette** / Palette 2: **Harmony Palette** / Palette 3: **Main purchase Palette**
[*Clustering accuracy evaluation report](https://github.com/uynNee/CAI/blob/master/jay/Analysis/Report/Clustering_Evaluation.ipynb)
