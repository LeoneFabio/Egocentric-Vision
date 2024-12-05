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
  "manifest": "s3://ego4d-consortium-sharing/public/v1/full_scale/manifest.csv",
  "videos": [
    {
      "video_uid":"d250521e-5197-44aa-8baa-2f42b24444d2",
      "clips":[
         {
           "clip_uid":"fae92e70-88aa-4b77-b41a-5879b74c804c",
           "video_start_sec":0.0210286,
           "video_end_sec":480.0210286,
           "video_start_frame":1,
           "video_end_frame":14401,
           "clip_start_sec":0,
           "clip_end_sec":480.0,
           "clip_start_frame":0,
           "clip_end_frame":14400,
           "source_clip_uid":"51e04dae-3ad0-48c1-b94b-c3ba0edaa99e",
           "annotations":[
             {
               "language_queries":[
                 {
                   "clip_start_sec":0.0,
                   "clip_end_sec":43.6657,
                   "video_start_sec":0.0210286,
                   "video_end_sec":43.6867286,
                   "video_start_frame":1,
                   "video_end_frame":1311,
                   "template":"Objects: How many X’s? (quantity question)",
                   "query":"How many frying pans can i see on the shelf?",
                   "slot_x":"frying pans",
                   "verb_x":"[verb_not_applicable]",
                   "slot_y":"i See on the shelf",
                   "verb_y":"see",
                   "raw_tags":[
                     "Objects: How many X’s? (quantity question)",
                     "How many frying pans can i see on the shelf?",
                     "frying pans",
                     "[verb_not_applicable]",
                     "i See on the shelf",
                     "see"
                   ]
                 }
               ],
               "annotation_uid": "f3083484-a6c0-45cb-a40c-b1c2cb470443"
             }
           ]
         }
       ],
      "split": "train"
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
  "manifest": "s3://ego4d-consortium-sharing/public/v1/full_scale/manifest.csv",
  "videos": [
    {
      "video_uid": "c9c44dea-c37b-461d-aa14-20e934126df5",
      "clips": [
        {
          "clip_uid": "a603669a-57f9-4db4-8a81-0a6720946d45",
          "video_start_sec": 1489.0943619333332,
          "video_end_sec": 1969.1310359242186,
          "video_start_frame": 66429,
          "video_end_frame": 66429,
          "clip_start_sec": 0,
          "clip_end_sec": 480.03667399088545,
          "clip_start_frame": 0,
          "clip_end_frame": 14401,
          "source_clip_uid": "4ee7dc88-3d7f-4607-a110-9419fb0eb93d",
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
      ],
      "split": "test"
    }
  ]
}
```


