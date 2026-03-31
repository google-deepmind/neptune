# MINERVA Dataset Collection

## Tl;dr
This page covers the Minerva Dataset Collection which is a set of video QA
datasets.
This collection currently includes the [Minerva-cultural](#minerva-cultural) dataset,
[Minerva-Ego](#minerva-ego), the [MINERVA](#minerva) dataset and the original [Neptune](#neptune) dataset.

## Minerva-cultural

Minerva-cultural is a challenging benchmark for multicultural and
multilingual long video reasoning. It consists of ~2,200 high-quality,
entirely human-generated question-answer pairs from 540
culturally-rich videos across 18 global locales. Unlike prior work
that relies on automatic translations, Minerva-cultural provides
complex questions, answers, and multi-step reasoning steps, all
crafted in native languages by locally-situated experts.

Minerva-cultural is designed to test whether Video-LLMs can achieve
a deeply situated understanding of visual cultural context. Videos
span six key cultural domains: **Sports**, **Cuisine**,
**Festivals**, **Tourism**, **Rituals**, and **Education**, with
durations ranging from 1 minute to over 1 hour. Each question
requires at least two reasoning skills (e.g., Temporal Ordering,
Spatial Perception, Cause and Effect, Counting, Object Recognition)
along with a mandatory Visual Cultural Understanding skill.

A key feature of Minerva-cultural is the inclusion of detailed,
human-authored multi-step reasoning traces in the native language,
providing ground-truth for reasoning evaluation. We leverage these
traces to construct evidence-based graphs and propose a novel
iterative strategy for fine-grained error analysis. Our evaluations
reveal that SoTA Video-LLMs struggle significantly—the best model
(Gemini-2.5-Pro) achieves 45.07% accuracy compared to a human
baseline of 95.22%.

More details are provided in our
[arXiv](https://arxiv.org/abs/2601.10649) paper.

<div style="text-align:center">
    <figure>
        <img src ="curve_teaser.png" width="900", alt="Examples of Minerva-cultural questions and videos from multiple locales.">
        <figcaption>
        <b>Examples from Minerva-cultural. Each question is crafted in
        the native language by locally-situated experts, accompanied by
        multi-step reasoning traces. Minerva-cultural spans 18 locales
        and 6 cultural domains.</b>
        </figcaption>
        <br>
    </figure>
</div>

### Locales

Minerva-cultural covers 18 diverse locales and languages:

| Locale | Language |
|---|---|
| ar-EG | Arabic (Egypt) |
| bn-BD | Bengali (Bangladesh) |
| de-DE | German (Germany) |
| en-GB | English (United Kingdom) |
| es-MX | Spanish (Mexico) |
| fr-FR | French (France) |
| hi-IN | Hindi (India) |
| id-ID | Indonesian (Indonesia) |
| it-IT | Italian (Italy) |
| ja-JP | Japanese (Japan) |
| kn-IN | Kannada (India) |
| ko-KR | Korean (South Korea) |
| mr-IN | Marathi (India) |
| pt-BR | Portuguese (Brazil) |
| ru-RU | Russian (Russia) |
| ta-IN | Tamil (India) |
| te-IN | Telugu (India) |
| zh-TW | Chinese (Taiwan) |

### Downloading the Data

We provide a JSON file that contains the YouTube IDs and annotations.

The JSON file contains the following fields:

- **key**: Unique identifier for each question
- **video_id**: YouTube URL
- **locale**: Locale code (e.g., `ja-JP`, `hi-IN`)
- **question**: Question in the native language
- **answer**: Answer in the native language
- **reasoning_steps**: Detailed multi-step reasoning trace in the
  native language
- **external_links**: External reference links used during annotation
- **skills**: Comma-separated list of reasoning skills required to
  answer the question
- **category**: Cultural domain (e.g., Sports, Cuisine, Festivals)
- **subcategory**: Fine-grained, locale-specific cultural sub-category

[Minerva-cultural JSON](https://storage.mtls.cloud.google.com/neptunedata/curve.json)

### Evaluation and Metrics

Minerva-cultural uses open-ended question answering. Given the
open-ended nature of the questions, standard string matching is
inadequate. We employ an LLM Judge (Gemini-2.5-Flash) to score each
response on a three-point scale (0, 1, 2) based on its semantic
alignment with the ground truth. The same metric is used for both
model and human evaluations. The full evaluation prompt is provided
in the [paper](https://arxiv.org/abs/2601.10649).

### Citing this work
<!-- disableFinding(SNIPPET_INVALID_LANGUAGE) -->
```latex
@article{curve25,
  title={CURVE: A Benchmark for Cultural and Multilingual Long Video Reasoning},
  author={Singh, Darshan and Nagrani, Arsha and Manikantan, Kawshik and Singh, Harman and Tewari, Dinesh and Weyand, Tobias and Schmid, Cordelia and Angelova, Anelia and Dave, Shachi},
  journal={arXiv preprint arXiv:2601.10649},
  year={2025}
}
```

## Minerva-Ego
Minerva-Ego extends the MINERVA benchmark to egocentric video. It consists of
1,160 complex multiple choice questions over videos selected from the
[HD-EPIC](https://epic-kitchens.github.io/epic-fields/) dataset. As with
MINERVA, each question is accompanied by a dense, spatiotemporally grounded
reasoning trace that connects the steps required to solve the problem to
specific timestamps and objects within the video. All annotations in Minerva-Ego
have been hand-crafted by expert human raters.

<div style="text-align:center">
    <figure>
        <img src ="minerva_ego_examples.png" width="900", alt="Examples of Minerva-Ego questions and videos.">
        <figcaption>
        <b>Examples from Minerva-Ego. Each multiple choice question comes with
        a natural language reasoning trace, outlining the steps required to come
        to the answer, which are grounded in time (localization with timestamps)
        and space (associations with segmentation masks of objects).</b>
        </figcaption>
        <br>
    </figure>
</div>

### Downloading the Data
We provide a json file that contains the video IDs and annotations.

The json file contains the following fields:

- key: Unique identifier for each question
- video_id: Video identifier from HD-EPIC
- question: Free-form question
- answer: Free-form answer
- answer_choice_{i}: Decoys for MCQ evaluation, i in range(0,4)
- answer_id: ID of the correct answer in the decoys
- reasoning: Detailed reasoning trace
- question type: A comma-separated list of multiple skills needed to answer the
question

[Minerva-Ego json](minerva-ego_20260205.json)

### Citing this work
<!-- disableFinding(SNIPPET_INVALID_LANGUAGE) -->
```latex
@article{minerva_ego26,
  title={Minerva-Ego: Spatiotemporal Hints for Egocentric Video Understanding},
  author={Nagrani, Arsha and Uijlings, Jasper and Buch, Shyamal and Weyand, Tobias and Vijayanarasimhan, Sudheendra and Hu, Bo and Mehran, Ramin and Ross, David A and Schmid, Cordelia},
  year={2026}
}
```

## MINERVA
MINERVA consists of ~1.5K
challenging question-answer-decoy (QAD) sets for variable length videos. For
each question, we provide 5 answer choices, as well as detailed,
manually-annotated reasoning traces. Every question in MINERVA requires complex
reasoning using two or more skills
(for example numerical reasoning, temporal reasoning, spatial navigation).
Videos also span multiple domains (short films, sports, instructional videos
etc), with various video lengths (from 2 minutes to over 1.5 hours). The
hand-crafted, detailed reasoning trace accompanying each question outlines
the steps that are required to come to the correct answer.
These traces include timestamps where necessary to refer to relevant sections of
the video, and also describes key actions, objects, as well as outlines logical
reasoning steps. More details are provided in our
[arXiv](https://arxiv.org/abs/2505.00681) paper.

<div style="text-align:center">
    <figure>
        <img src ="minerva_examples.png" width="900", alt="Examples of Minerva questions and videos.">
        <figcaption>
        <b>Examples from MINERVA. MINERVA consists of challenging
        question-answer-decoy sets for videos. The answer to each question is
        also accompanied by a detailed reasoning trace, which outlines the steps
         required to come to the answer. Reasoning traces are detailed,
         including timestamps (highlighted in green) and key actions
         (highlighted in pink).</b>
        </figcaption>
        <br>
    </figure>
</div>

<div style="text-align:center">
    <figure>
        <img src ="combined_lengths.png" width="700", alt="Statistics of Minerva dataset, including video length and and reasoning trace lengths.">
        <figcaption>
        <b>MINERVA covers a variety of video lengths. Reasoning traces are long and detailed.</b>
        </figcaption>
    </figure>
</div>

### Downloading the Data
We provide a json file that contains the YouTube IDs and annotations.

The json file contains the following fields:

- key: Unique identifier for each question
- video_id: YouTube URL
- question: Free-form question
- answer: Free-form answer
- answer_choice_{i}: Decoys for MCQ evaluation, i in range(0,4)
- answer_id: ID of the correct answer in the decoys
- reasoning: Detailed reasoning trace
- question type: A comma-separated list of multiple skills needed to answer the
question
- split: Coarse video domain
- category: Fine-grained video domain

[MINERVA json](https://storage.mtls.cloud.google.com/neptunedata/minerva.json)

### Citing this work
<!-- disableFinding(SNIPPET_INVALID_LANGUAGE) -->
```latex
@article{minerva25,
  title={MINERVA: Evaluating Complex Video Reasoning},
  author={Nagrani, Arsha and Menon, Sachit and Iscen, Ahmet and Buch, Shyamal and Mehran, Ramin and Jha, Nilpa and Hauth, Anja and Zhu, Yukun and Vondrick, Carl and Sirotenko, Mikhail and Schmid, Cordelia and Weyand, Tobias},
  journal={arXiv preprint arXiv:2505.00681},
  year={2025}
}
```

## Neptune
Neptune is a dataset consisting of
challenging question-answer-decoy (QAD) sets
for variable length videos (up to 15 minutes). The goal of this dataset is to
test video-language models for a broad range of long video reasoning abilities,
which are provided as "question type" labels for each question, for example
"video summarization", "temporal ordering", "state changes" and "creator intent"
amongst others. More details are provided in our
[arXiv](https://www.arxiv.org/abs/2412.09582) paper.

<div style="text-align:center">
    <figure>
        <img src ="examples.png" width="1000" alt="Examples of Neptune questions and videos.">
        <figcaption>
        Neptune consists of challenging question-answer-decoy sets for videos
        to assess a number of long video reasoning abilities.
        </figcaption>
    </figure>
</div>

Neptune allows for two modes of evaluation: multiple-choice and
open-ended question answering. For the latter, we provide our own open-ended
metric based on Gemma, called Gemma Equivalence Metric (GEM).

Neptune was created using a semi-automatic pipeline, which involves careful
prompting of large LLMs and VLMs, including Gemini. See more details provided
in the [paper](https://www.arxiv.org/abs/2412.09582).

Neptune has more than 3,200 questions for over 2,400 videos.

<div style="text-align:center">
    <figure>
        <img src ="stats.png" width="1000" alt="Statistics of Neptune dataset, including video length and question types.">
        <figcaption>
        Greater than 12% of the videos are longer than 5 minutes and over 25%
        are longer than 3 minutes. Neptune covers a number of question types
        and video domains.
        </figcaption>
    </figure>
</div>

### Downloading the Data

We provide links to json files that contain the YouTube IDs and annotations for
each split below.
Please see the paper for details regarding each split.

The json files contains the following fields:

- key: Unique identifier for each question
- video_id: YouTube URL
- question: Free-form question
- answer: Free-form answer
- answer_choice_{i}: Decoys for MCQ evaluation, i in range(0,4)
- answer_id: ID of the correct answer in the decoys
- question type: Question type

[Neptune-Full](https://storage.mtls.cloud.google.com/neptunedata/neptune_full.json)

[Neptune-MMH](https://storage.mtls.cloud.google.com/neptunedata/neptune_mmh.json)

[Neptune-MMA](https://storage.mtls.cloud.google.com/neptunedata/neptune_mma.json)

### Evaluation and Metrics

Multiple choice evaluation involves selecting the answer from 5 options
(including 4 decoys) and using accuracy as the metric.

For open-ended evaluation, we create a new language model based metric, called
the Gemma Equivalence Metric (GEM). We do this by fine tuning a Gemma
checkpoint on the
[BEM answer equivalence dataset](https://github.com/google-research-datasets/answer-equivalence-dataset)
and prompt it to determine if a produced answer is equivalent to the ground
truth.

### Citing this work
<!-- disableFinding(SNIPPET_INVALID_LANGUAGE) -->
```latex
@article{neptune24,
      title={Neptune: The Long Orbit to Benchmarking Long Video Understanding},
      author={Nagrani, Arsha and Zhang, Mingda and Mehran, Ramin and Hornung, Rachel and Gundavarapu, Nitesh Bharadwaj and Jha, Nilpa and Myers, Austin and Zhou, Xingyi and Gong, Boqing and Schmid, Cordelia and Sirotenko, Mikhail and Zhu, Yukun and Weyand, Tobias},
      journal={arXiv preprint arXiv:2412.09582},
      year={2024},
}
```

## License and disclaimer
Copyright 2024 DeepMind Technologies Limited

All software is licensed under the Apache License, Version 2.0 (Apache 2.0);
you may not use this file except in compliance with the Apache 2.0 license.
You may obtain a copy of the Apache 2.0 license at:
https://www.apache.org/licenses/LICENSE-2.0

All other materials are licensed under the Creative Commons Attribution 4.0
International License (CC-BY). You may obtain a copy of the CC-BY license at:
https://creativecommons.org/licenses/by/4.0/legalcode

Unless required by applicable law or agreed to in writing, all software and
materials distributed here under the Apache 2.0 or CC-BY licenses are
distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied. See the licenses for the specific language governing
permissions and limitations under those licenses.

This is not an official Google product.
