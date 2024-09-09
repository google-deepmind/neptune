# Neptune

Neptune is a dataset consisting of challenging question-answer-decoy (QAD) sets
for long videos (up to 15 minutes). The goal of this dataset is to test
video-language models for a broad range of long video reasoning abilities, which
are provided as "question type" labels for each question, for example "video
summarization", "temporal ordering", "state changes" and "creator intent"
amongst others.

Neptune allows for two modes of evaluation: multiple-choice and
open-ended question answering. For the latter, we provide our own open-ended
metric based on Gemma, called Gemma Equivalence Metric (GEM).

Neptune was created using a semi-automatic pipeline, which involves careful
prompting of large LLMs and VLMs, including Gemini. See more details in the paper link provided below.

Neptune has more than 3,200 questions for over 2,400 videos.

## Downloading the Data

We provide links to json files that contain the YouTube IDs and annotations for each split below.

The json files contains the following fields:

- key: Unique identifier for each question
- video_id: YouTube URL
- question: Free-form question
- answer: Free-form answer
- answer_choice_{i}: Decoys for MCQ evaluation, i in range(0,4)
- answer_id: ID of the correct answer in the decoys
- question type: Question type

[Neptune-Full Split]()

[Neptune-Full MMH]()

[Neptune-Full MMA]()

## Evaluation and Metrics

Multiple choice evaluation involves selecting the answer from 5 options (including 4 decoys) and using accuracy as the metric.

For open-ended evaluation, we create a new language model based metric, called
the Gemma Equivalence Metric (GEM). We do this by fine tuning a Gemma
checkpoint on the
[BEM answer equivalence dataset](https://github.com/google-research-datasets/answer-equivalence-dataset)
and prompt it to determine if a produced answer is equivalent to the ground truth.
We will be releasing the model for the metric soon.

## Citing this work

```latex
@article{neptune24,
      title={Neptune: The Long Orbit to Benchmarking Long Video Understanding},
      author={Arsha Nagrani and Mingda Zhang and Ramin Mehran and Rachel Hornung and Nitesh Bharadwaj Gundavarapu and Nilpa Jha and Austin Myers and Xingyi Zhou and Boqing Gong and Cordelia Schmid and Mikhail Sirotenko and Yukun Zhu and Tobias Weyand},
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
