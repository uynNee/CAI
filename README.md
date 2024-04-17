# CAI(Color Artificial Intelligence)

---

## [ About CAI Project ]

`CAI` applies a deep learning model to user-uploaded photos to diagnose their personal color type and recommends personal color palettes and fashion items based on this diagnosis. The subjective diagnosis process of personal color type, traditionally judged by human eyes, is replaced with preprocessing steps such as white balance adjustment on the user-uploaded photos to obtain color matching results, which are then used to diagnose the user's personal color type.

`Personal Color` refers to the unique color of an individual's skin. By analyzing individual characteristics, this system matches individuals to one of the types in the personal color type classification system, diagnosing suitable makeup, hair, clothing, and other color images to create a harmonious appearance.

#### `< CAI Total Process >`
<img src="jay/img/total-process.jpg" width=100%>

---

## [ Deep Learning_Personal Color Type Classifier ]

### Dataset Creator

#### `< Face Detection >`
<img src="jay/img/face-detection.jpg" width=100%>

#### `< Skin Color Extraction >`
<img src="jay/img/skin-color-extraction.jpg" width=100%>

#### `< Color System Converter & Type Classifier >`
<img src="jay/img/color-system-converter.jpg" width=100%>

- `Face Detection`
    Face recognition, image resizing (input image about 200,000 / output image about 150,000)
    Facial images are preprocessed and face recognition is performed using the `Haar Cascade` method to obtain uniform-sized facial images.
- `Skin Color Extraction`
    Facial skin color extraction from facial images obtained by Face Detection.
    Two filters are used for color accuracy, and colors are extracted using the K-means method.
- `Color System Converter`
    Replaces the extracted color list with average colors for color system conversion required for algorithm application.
    (BGR → RGB → HSV)
- `Type Classifier`
    Applies personal color type classification algorithm to create datasets using color matching results (facial colors).

### Deep Learning

#### `< CNN/AlexNet >`
<img src="jay/img/cnn-alexnet.jpg" width=100%>

`AlexNet`: Chosen for its suitability for 'color learning' as it separates color and non-color parts.
Result model: `CAI.h5`

---

## [ Color Palette Extraction ]

### Bright Palette & Harmony Palette

#### `< Personal color Analysis >`
<img src="jay/img/Data-Analysis.jpg" width=100%>

Primary color matching areas and diagnosed colors are selected based on color theory and personal color-related papers.
A survey is conducted to test the rationality of personal color theory, matching areas, and diagnosed colors.
Naver Data Lab is used for comprehensive analysis and accuracy enhancement.
Based on analysis results, matching areas and diagnosed colors, which are criteria for personal color type classification, are modified.
[* Personal color theory analysis report](https://github.com/slmteruto/CAI/blob/master/jay/Analysis/Report/Color_theory_analysis.ipynb)
[* Personal color statistical analysis report](https://github.com/slmteruto/CAI/blob/master/cys/CAI_elementaryItem_analysis.ipynb)

### Main Purchase Palette

#### `< Data acquisition & Main color Extraction >`
<img src="jay/img/color-clustering.jpg" width=100%>

- `Clothes Color Extraction`
    Masks are created using the `Topwear.h5` model for product images (fashion item separation).
    Fashion item exclusion is applied to the original image by combining the mask with it.
    Colors are extracted using the K-means method, and color data per product is loaded into the database.
- `Main Color Extraction`
    User's purchased items are queried in real-time, and color lists of purchased items are obtained.
    Items close to grayscale are excluded from the list using a gray tone filter.
    To reduce clustering errors, the Color Generator expands the scale of purchased item colors.
    Hierarchical Clustering is used to extract the main purchase color palette from the expanded color data.

---

## [ Website ]

#### `< Web structure >`
<img src="jay/img/cai-webpage.jpg" width=100%>

- `Personal color type Prediction`
    Predicts personal color type by applying **CAI.h5** to photos uploaded by users via the web.
- `Matched Personal color palette`
    Provides personalized palettes corresponding to user's type results and skin colors extracted through **Skin Color Extraction**.
- `Fashion item Recommendation`
    Recommends products corresponding to the extracted three palettes in real-time from the database, providing personalized services for each user.
    ※ Palette 1: **Bright Palette** / Palette 2: **Harmony Palette** / Palette 3: **Main Purchase Palette**
[* Clustering accuracy evaluation report](https://github.com/slmteruto/CAI/blob/master/jay/Analysis/Report/Clustering_Evaluation.ipynb)

---
