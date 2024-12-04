# Egocentric-Vision
This project leverages the **Ego4D NLQ benchmark** to process egocentric video data using **VSLNet**, predicting start/end timestamps for queries. It extends this with a **videoQA model** for generating textual answers, enabling deeper interaction with egocentric video and natural language tasks.

## Overview of NLQ Annotation Files in EGO4D

The NLQ (Natural Language Queries) dataset in the EGO4D benchmark contains approximately 19,000 annotated queries derived from around 227 hours of videos. These annotations are structured hierarchically and provide detailed metadata for fine-grained video understanding tasks. Below is a summary of the dataset structure and key components.

### Hierarchical Structure

1. **Video**:
   - A top-level entity representing a complete video.
   - Videos are divided into shorter segments called **clips**.

2. **Clip**:
   - A shorter, continuous segment of a video, defined by start and end times (`clip_start_sec`, `clip_end_sec`) and frames (`clip_start_frame`, `clip_end_frame`).
   - Each clip is associated with one or more **annotations**.

3. **Annotation**:
   - Represents a grouping of **language queries** related to a specific clip.
   - Provides a unique identifier (`annotation_uid`) and timestamps for queries.

4. **Language Query**:
   - A natural language question or task associated with a specific segment of the video.
   - Includes attributes like:
     - `query`: The text of the query (e.g., *"What did I put in the bowl?"*).
     - `template`: The query's general structure, one of 13 pre-defined templates from three categories (*Objects*, *Place*, *People*).
     - `clip_start_sec` and `clip_end_sec`: Timestamps relative to the clip.
     - `video_start_sec` and `video_end_sec`: Timestamps relative to the entire video.

### Key Attributes

- **`template`**:
  - Queries are structured using 13 templates across three categories:
    1. **Objects**: E.g., *"What X did I Y?"*, *"Where is object X before/after event Y?"*
    2. **Place**: E.g., *"Where did I put X?"*
    3. **Peope**: E.g., *"Who did I interact with whren I did activity X?"*

- **Timestamps**:
  - Each query is annotated with start and end times in two contexts:
    - **Clip-level**: `clip_start_sec`, `clip_end_sec`
    - **Video-level**: `video_start_sec`, `video_end_sec`

- **Raw Tags**:
  - Include metadata for query generation, often repeating information from the `template` and `query`.

### Notes
- Annotations ensure fine-grained alignment of language tasks to video segments.
- The `test_unannotated` file contains only the queries without additional temporal or structural metadata for benchmarking.

### Example JSON Snippet

#### Annotated (Training) File:
```json
{
  "version": "1",
  "date": "220216",
  "description": "NLQ Annotations (train)",
  "videos": [
    {
      "video_uid": "d250521e-5197-44aa-8baa-2f42b24444d2",
      "clips": [
        {
          "clip_uid": "fae92e70-88aa-4b77-b41a-5879b74c804c",
          "video_start_sec": 0.0210286,
          "video_end_sec": 480.0210286,
          "annotations": [
            {
              "language_queries": [
                {
                  "clip_start_sec": 0.0,
                  "clip_end_sec": 43.6657,
                  "query": "How many frying pans can I see on the shelf?",
                  "template": "Objects: How many X’s? (quantity question)"
                }
              ],
              "annotation_uid": "f3083484-a6c0-45cb-a40c-b1c2cb470443"
            }
          ]
        }
      ]
    }
  ]
}
```

#### Unannotated (Test) File:
```json
{
  "version": "1",
  "date": "220216",
  "description": "NLQ Annotations (test unannotated)",
  "videos": [
    {
      "video_uid": "c9c44dea-c37b-461d-aa14-20e934126df5",
      "clips": [
        {
          "clip_uid": "a603669a-57f9-4db4-8a81-0a6720946d45",
          "annotations": [
            {
              "language_queries": [
                { "query": "What did I put in the sack?" },
                { "query": "Who did I talk to in the shop?" }
              ],
              "annotation_uid": "f7e9c1c6-1381-4df2-9121-f0b1f437282d"
            }
          ]
        }
      ]
    }
  ]
}
```


