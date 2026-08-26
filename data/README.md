---
title: Travel Assistant Test Data
description: Synthetic input files for the AI-Powered Travel Assistant lab
author: Lab Facilitator
ms.date: 2026-08-26
ms.topic: reference
keywords:
  - test data
  - Azure AI
  - travel assistant
estimated_reading_time: 3
---

## Data policy

Every file in this directory was generated specifically for this lab. The files contain
fictional information and may be used, modified, and redistributed with the lab under
the repository license. No real passport data, voice recording, photograph, or external
media is included.

Do not replace these fixtures with real identity documents or other sensitive personal
data. Keep API keys, service endpoints, and other secrets outside this directory.

## File inventory

### `travel-request.txt`

A UTF-8 text request for a five-day family trip to Singapore in December. Expected
language analysis results include English as the detected language and concepts related
to Singapore, a $2,000 budget, theme parks, aquariums, and shopping.

### `family-preferences.wav`

A generated PCM WAV recording that says:

```text
We are travelling with a 6-year-old child and would prefer family-friendly
attractions.
```

Speech recognition should return equivalent wording. Minor punctuation or spelling
differences are acceptable.

### `sample-passport.pdf`

A generated one-page PDF representing a fictional training document. It contains:

```text
Name: Alex Morgan
Nationality: Indian
Passport Number: X123456
```

Document processing should extract the three fields. Applications should mask the
passport number in logs and user-visible output, for example `X*****6`, and must not
send it to Azure OpenAI.

### `singapore-attraction.jpg`

A generated illustration of a Singapore theme park entrance labeled Universal Studios
Singapore. Vision results may mention an entrance arch, globe, palm trees, blue sky,
theme park, or Singapore. The image is synthetic and is not an official photograph or
brand asset.

## Expected workflow

1. Load the text request and analyze its language, key phrases, and entities.
2. Transcribe the WAV recording and retain the family preference.
3. Analyze the JPEG while treating uncertain results as unverified context.
4. Extract fictional fields from the PDF and remove unnecessary sensitive data.
5. Combine only trip-relevant results to generate a personalized itinerary.