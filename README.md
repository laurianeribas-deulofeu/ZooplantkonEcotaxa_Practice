<body>

<h1> Zooplankton Image Dataset for AI-Assisted Identification and Community Analysis</h1>
<p class="subtitle">Demo materials — <em>AI Applications in Marine Science</em></p>
<p class="author">L. Ribas-Deulofeu — Nord University, Norway</p>

<span class="badge">ZooImage; Ecotaxa</span>
<span class="badge green">Teaching</span>
<span class="badge gray">CC BY 4.0</span>

<hr>

<h2>Overview</h2>

<p>This repository contains demo materials for practising building an AI classifier for zooplankton taxa identification, community description, and biodiversity metrics calculation using real, split plankton net samples from a long-term monitoring programme in Saltfjord, Norway.<p>

<p>The dataset consists of 11 samples spanning nearly four decades (1983–2021), randomly selected from a 43-year time series. Each sample contains segmented zooplankton images (>180 µm) and associated morphological feature tables, ready for upload to EcoTaxa (.tsv) or direct use in ZooImage (.zim).<p>

<blockquote> These are demo materials for you to practise building your own classifier.</blockquote>

<hr>

<h2>The Data</h2>

<h3>Sampling design</h3>

<tr><th>Parameter</th><th>Value</th></tr>
<tr><td>Location</td><td>Saltfjord, Norway</td></tr>
<tr><td>Sampling seasons</td><td>February/March and October</td></tr>
<tr><td>Original time series length</td><td>43 years</td></tr>
<tr><td>Samples in this demo</td><td>11 (randomly selected)</td></tr>
<tr><td>Sample range</td><td>1983 – 2021</td></tr>
<tr><td>Size fraction</td><td> >500 µm</td></tr>

<h3>Imaging</h3>

<tr><th>Parameter</th><th>Value</th></tr>
<tr><td>Instrument</td><td>Epson Perfection V750 Pro flatbed scanner</td></tr>

<tr><td>Scan mode </td><td>Color</td></tr>
<tr><td>Resolution</td><td>3600 dpi</td></tr>
<tr><td>Segmentation software</td><td><a href="https://www.sciviews.org/zooimage/"> ZooImage</a></td></tr>


<h3>Files in this repository</h3>
<div class="file-tree">
├── README.md<br>
├── samples/<br>
├── BIO24_P150.stsa12_1983-2-7.4.zip     # One zip per sample (see structure below) [stsa12= Sampling station in Saltfjord; YYYY-M-D= Sampling date; other part of the sample name refers to internal label standards not relevant to use these samples]<br>
├── BIO24_P150.stsa12_1986-1-30.8.zip<br>
├── BIO24_P150.stsa12_1986-1-30.8.zip<br>
├── BIO24_P150.stsa12_1988-3-1.10.zip<br>
├── BIO24_P150.stsa12_1991-2-26.15.zip<br>
├── BIO24_P150.stsa12_1994-3-1.20.zip<br>
├── BIO24_P150.stsa12_2003-2-11.36.zip<br>
├── BIO24_P150.stsa12_2005-10-27.41.zip<br>
├── BIO24_P150.stsa12_2007-3-7.44.zip<br>
├── BIO24_P150.stsa12_2012-10-5.53.zip<br>
├── BIO24_P150.stsa12_2017-2-21.62.zip<br>
└── BIO24_P150.stsa12_2021-2-3.70.zip     # 11 samples total<br>
</div>

<hr>

<p>Each `.zip` archive contains:</p>

<div class="file-tree">
BIO24_P150.stsa12_YYYY-M-D.*/<br>
├── *.jpg                    # Segmented organism images (JPEG)<br>
├── SampleName.tsv           # Morphological features table (EcoTaxa format)<br>
└── SampleNAme.zim           # ZooImage metadata file<br>
</div>

<hr>

<h3>Feature table format</h3>

<p>The `.tsv` files follow the **EcoTaxa import format**: each row is one object (segmented organism), with the first two header rows specifying column names and data types. Columns include object-level morphological descriptors (area, perimeter, Feret diameter, grey-level statistics, etc.) computed by ZooImage from the scanned images.</p>

<p>The `.zim` files store ZooImage-specific metadata and are required for re-processing or re-classifying images directly in ZooImage.</p>

---

<h2>What these materials are for</h2>

<p>Working with these samples, students can practise:

- **AI-assisted identification** — upload `.tsv` files to EcoTaxa and apply a pre-trained classifier, or use ZooImage's built-in random forest classifier
- **Manual validation** — review and correct AI predictions image by image to build a ground-truth dataset
- **Community description** — compute taxon-level and sample-level summaries (abundance, relative composition)
- **Biodiversity metrics** — calculate Hill numbers (q = 0, 1, 2), total abundance, and biomass estimates
- **Temporal analysis** — compare community structure across seasons and decades using a real long-term dataset
</p>

<h2>Getting started</h2>

<h3> 1. Clone or download this repository</h3>
<pre><code>git clone https://github.com/laurianeribas-deulofeu/ZooplantkonEcotaxa_Practice</code></pre>
<p>Or click <strong>Code → Download ZIP</strong> and unzip locally.</p>



<h3> 2. Unzip sample archives</h3>

<p>Each sample is stored as a `.zip` in the `samples/` folder.</p>

<h3> 3. EcoTaxa workflow</h3>
<p>
<ul>
<li>1. Create a free account at<a href="https://ecotaxa.obs-vlfr.fr">ecotaxa.obs-vlfr.fr</a> </li>
<li>2. Create a new project and import your samples</li>
<li>3. Apply a pre-trained zooplankton classifier from the available list</li>
<li>4. Export prediction results for later classifier performance evaluation</li>
<li>5. Validate predictions and export results</li>
<li>6. Evaluate classifier results using code available at <a href="https://github.com/laurianeribas-deulofeu/Basic-AI-model-evaluation-Demo"> laurianeribas-deulofeu/Basic-AI-model-evaluation-Demo</a> </li>
<li>7. Re-train & re-evaluate. Always export prediction results before re-training, as predictions will be erased on validated pictures, preventing you to access these info later on and therefore preventing re-evaluation of your classifier</li>
</ul>
</p>
<hr>


<h3> 4. Biodiversity analysis in R</h3>
<p>
Once identifications are available, compute community metrics:

```r
install.packages(c("tidyverse", "vegan", "hillR", "iNEXT"))
```

Key metrics to calculate:
- **Abundance** — total individuals per sample, per taxon
- **Biomass** — estimated from body length–weight regressions or biovolume
- **Hill numbers** — species richness (*q* = 0), Shannon diversity (*q* = 1), Simpson diversity (*q* = 2)
</p>

<h2> Key concepts covered</h2>

| Concept | What it means in practice |
|---------|--------------------------|
| **Image segmentation** | Isolating individual organisms from the scanned image background |
| **Morphological features** | Quantitative shape, size, and grey-level descriptors used as classifier input |
| **AI-assisted identification** | Automated taxon prediction from features; always requires human validation |
| **Validation workflow** | Reviewing classifier predictions to build a reliable annotated dataset |
| **Hill numbers** | A unified framework for diversity that spans richness to dominance by varying *q* |
| **Class imbalance** | Common taxa dominate samples; rare taxa are harder to classify reliably |
| **Long-term monitoring** | Changes in community composition over time require standardised, comparable methods |

---

<h2> Learning objectives </h2>
<p>
By working with these materials, students will be able to:
<ul>
<li>1. Import zooplankton scan data into EcoTaxa or ZooImage and apply an AI classifier</li>
<li>2. Critically validate AI-predicted identifications using reference images</li>
<li>3. Construct a species-by-sample abundance matrix from validated annotations</li>
<li>4. Calculate Hill numbers, abundance, and biomass estimates in R</li>
<li>5. Interpret your results</li>
</ul>
<p>
<hr>

<h2>Citation</h2>
<p>
If you use these materials in your teaching or research, please cite:

<pre><code>Ribas-Deulofeu, L. (2026). Zooplankton Image Dataset for AI-Assisted Identification
and Community Analysis — Demo materials, Nord University, Norway.
GitHub: https://github.com/laurianeribas-deulofeu/ZooplantkonEcotaxa_Practice</code></pre>
</p>

<hr>

<h2>License</h2>
<p>These materials are shared for educational use under [CC BY 4.0] (https://creativecommons.org/licenses/by/4.0/) — you are free to use, adapt, and redistribute with attribution. </p>


</body>
</html>
